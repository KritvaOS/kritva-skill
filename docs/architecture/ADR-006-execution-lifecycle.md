# ADR-006: Skill Execution Lifecycle, Revocation and Cancellation

**Task:** KOS-SKILL-001  
**Status:** PROPOSED — REPOSITORY-ADOPTED; NORMATIVE CONTRACT APPROVAL PENDING UPSTREAM REVIEW  
**Decision:** RBAC-controlled cancellation; execution-start authorization re-check; revocation-aware dispatch; independent platform safety stop  
**Decision date:** 2026-11-27

## Context

Skill execution spans preparation, orchestration and physical operations that may not be reversible. A proposal disposition of CLEARED is a point-in-time eligibility result, not a durable authorization lease. Release approval, caller roles and permissions may change before execution starts or while a run is active. Cancellation or abrupt termination of a physical operation may itself create risk; Skill must follow the approved Motion/platform safety contract rather than assume that immediate termination is always safe.

## Decision and lifecycle

The Skill lifecycle is:

`LOADED -> RUNNING -> COMPLETED | CANCELLED | FAILED`

A pre-start authorization or release-eligibility failure adds the direct transition:

`LOADED -> FAILED`

- `LOADED`: Skill instance and execution context prepared; no Motion execution is implied.
- `RUNNING`: Skill execution has started and may dispatch Motion commands.
- `COMPLETED`: Skill operation completed successfully under its contract.
- `CANCELLED`: an authorized cancellation completed and all required termination outcomes are confirmed.
- `FAILED`: execution failed, a safety interruption occurred, start-time authorization failed, or the outcome of a required stop/termination remains unresolved.

Skill lifecycle states are distinct from proposal disposition and Motion command states. A failure before RUNNING does not imply that physical work was active.

## Mandatory termination status

Every terminal execution report includes `termination_status`, exactly one of:

- `CONFIRMED`: no outstanding operation remains, or every operation requiring termination is confirmed stopped or safely terminal.
- `UNRESOLVED`: at least one operation may remain active, or its final state cannot be verified.
- `NOT_REQUESTED`: no termination action was necessary or requested.

Rules:
- `CANCELLED` requires `CONFIRMED`.
- `COMPLETED` normally uses `NOT_REQUESTED`.
- A `FAILED` run may use any of the three values, according to the actual outcome.
- A failure before the LOADED-to-RUNNING transition caused by a failed start-time check uses `NOT_REQUESTED` and a specific failure reason code, because no Motion command has been dispatched.
- If a physical operation may still be active, the report must use `UNRESOLVED`; Skill must never imply that the robot stopped.
- An `UNRESOLVED` outcome includes a reason code and indicates operator intervention when required.

## Authorization re-check before RUNNING

CLEARED is a point-in-time proposal disposition and is not an indefinite execution authorization. Immediately before the LOADED-to-RUNNING transition, Skill re-checks:
1. The authenticated principal and trusted role/permission assertions.
2. `skill.execute` and all applicable capability-specific permissions, including execution/robot scope.
3. The exact immutable release's current registry eligibility; only `APPROVED` is eligible.
4. The manifest/package digests and execution scope selected during resolution.

If any check fails, is stale, or cannot be verified, Skill must not transition to RUNNING and must not dispatch a Motion command. It transitions directly from LOADED to FAILED, records a specific reason code (for example `AUTHORIZATION_REVOKED_BEFORE_START`, `RELEASE_SUSPENDED_BEFORE_START`, `RELEASE_REVOKED_BEFORE_START`, or `AUTHORITY_CHECK_UNAVAILABLE`), and sets `termination_status=NOT_REQUESTED`. The earlier proposal disposition remains CLEARED as a historical result of its earlier checks; the report records the later start denial separately.

## Registry and role revocation

Registry states `SUSPENDED` and `REVOKED` both prevent new executions. `SUSPENDED` is a non-eligible hold state; `REVOKED` permanently withdraws eligibility for that exact immutable release. Neither state, by itself, proves that an already-running physical operation has stopped.

- **Between CLEARED and RUNNING:** if the exact release becomes SUSPENDED/REVOKED, or the principal's required role/permission is revoked, block the start. Do not dispatch Motion. Record the observed state/revocation and fail from LOADED with `termination_status=NOT_REQUESTED` and a reason code.
- **During RUNNING:** re-check release eligibility and principal authorization before each subsequent Motion command dispatch. On SUSPENDED/REVOKED status or role/permission revocation, stop dispatching new commands. Handle any active command as the approved Motion/platform safety contract requires: request termination when that contract says it is appropriate, or allow the operation to reach a defined safe terminal state when that is the contractually safe behavior. Do not mandate abrupt termination. Record the revocation, active command, selected safety-contract handling and observed outcome. The Skill lifecycle becomes FAILED; set `termination_status` to CONFIRMED only when the required stopped/safe-terminal outcome is verified, otherwise UNRESOLVED.
- **Registry or identity service unavailable:** fail closed for any new dispatch. Stop further command dispatch and handle an already-active command under the approved Motion/platform safety contract, not by assuming abrupt cancellation is safe.

Because per-dispatch registry and identity checks make those services runtime availability dependencies, their freshness guarantees, cache policy, timeout budget, outage behavior and safe handling of in-flight commands remain open contract items. See DEPENDENCY_REGISTER.md.

## Cancellation authorization and behavior

Cancellation is controlled by ADR-001 RBAC:
- `skill.cancel` permission is required and scoped to the relevant execution/robot context.
- The initiating principal has no implicit cancellation privilege.
- The request is authenticated, authorized and auditable.

On an authorized cancellation request:
1. Stop dispatching new Motion commands.
2. Handle any active Motion command as the approved Motion/platform safety contract requires; this may mean requesting termination or allowing it to reach a safe terminal state.
3. Await and evaluate the contractually defined acknowledgements and terminal outcomes.
4. Record completed operations, active/unresolved operations and known physical effects.
5. Report CANCELLED only when all required outcomes are confirmed; otherwise report FAILED with the appropriate termination status and reason.

## Safety stop and emergency stop

Emergency stop is an independent robot/platform safety function. It is not an ordinary Skill API, does not depend on Skill RBAC and is not implemented by KOS-SKILL-001. On a trusted safety-stop signal, Skill stops new dispatch, records the signal source/time/evidence, and observes or handles active commands as the approved platform/Motion safety contract requires. It records the outcome as FAILED with reason `SAFETY_STOP` or `EMERGENCY_STOP`; `termination_status` is CONFIRMED only if the relevant stop/safe-terminal outcome is verified, otherwise UNRESOLVED. The report must record whether the stop was initiated by Skill or by the platform/independent safety system, so audit can distinguish a Skill-initiated stop from a Skill-observed stop. Skill lifecycle/report updates must never delay or inhibit the independent safety mechanism.

## Consequences and open work

Cancellation and revocation handling are asynchronous and safety-contract-dependent, not state assignments. Exact authorization freshness, registry/identity availability, timeout and acknowledgement policy, revocation notification, safe in-flight command handling, safety-signal interface, reason-code registry and report fields require approved upstream contracts. No rollback, instantaneous stop or guaranteed reversibility is implied.
