# ADR-007: Staged Hybrid Motion Orchestration

**Task:** KOS-SKILL-001  
**Status:** PROPOSED — REPOSITORY-ADOPTED; NORMATIVE CONTRACT APPROVAL PENDING UPSTREAM REVIEW
**Decision:** D — Sequential initial orchestration; concurrency deferred  
**Decision date:** 2026-11-27

## Context
A Skill may express a multi-step operation, while the current Motion interface available to the Skill design is a joint-level draft without an approved multi-joint coordination contract. Skill must not assume unsupported Motion features.

## Decision
Use a staged hybrid model.

### Initial contract
A Skill may define a multi-step operation, but it dispatches one Motion command at a time:
1. Validate the step and required capability.
2. Evaluate required preconditions.
3. Dispatch one Motion command.
4. Track admission and execution status using the approved Motion contract.
5. Await the command's terminal outcome before dispatching the next step.
6. Stop further dispatch after rejection, failure, cancellation or unresolved outcome.

Successful submission is not proof that physical execution completed.

### Partial execution
The execution report identifies completed steps; failed or cancelled step; steps not dispatched; active or unresolved operations; known physical effects; and recovery/operator-intervention requirements where known.

No automatic rollback is assumed. Compensation or recovery must be explicitly declared, independently authorized and safety-checked.

### Deferred capabilities
Concurrent dispatch, synchronized trajectories, multi-joint coordination and distributed execution are deferred until Motion publishes an approved, versioned contract supporting the required semantics and Skill defines corresponding orchestration, failure behavior and conformance tests.

## Consequences
The initial design is compatible with sequential command dispatch within a selected Skill run and can evolve without claiming unsupported coordinated behavior. This does not define ordering or scheduling among multiple CLEARED proposals returned in one Mind result; that remains OPEN under ADR-005, owned by the KOS-SKILL-001 task owner and targeted for V2-M5 / `PROPOSED-NEW-SKILL-004`. Until resolved, no cross-proposal order or concurrent dispatch is implied. The actual command/query/cancel mapping, correlation identifiers, idempotency and safe active-command handling must be derived from the approved Motion contract, not an unreviewed draft.
