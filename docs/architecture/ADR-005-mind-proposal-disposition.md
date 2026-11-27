# ADR-005: Mind Proposal Eligibility and Per-Proposal Disposition

**Task:** KOS-SKILL-001  
**Status:** PROPOSED — REPOSITORY-ADOPTED; NORMATIVE CONTRACT APPROVAL PENDING UPSTREAM REVIEW
**Decision:** C — Per-proposal disposition with strict initial eligibility  
**Decision date:** 2026-11-27

## Context
Mind produces proposals; it does not authorize execution. A Mind result may contain multiple proposals and may have a status indicating incomplete, failed or cancelled inference. Skill must independently decide each proposal's eligibility and preserve the distinction between Skill disposition and Motion admission.

## Decision
Evaluate each proposal independently, but initially accept proposals for evaluation only when the enclosing Mind result status is COMPLETED.

| Mind result status | Initial Skill behavior |
|---|---|
| COMPLETED | Each proposal is eligible for independent evaluation |
| PARTIAL | Advisory only; decline execution |
| FAILED | Decline all proposals |
| CANCELLED | Decline all proposals |

There is no deployment-specific override in the initial contract.

## Proposal disposition
RECEIVED -> CLEARED | DECLINED
- CLEARED means all mandatory Skill checks passed and the proposal may proceed to Skill orchestration.
- DECLINED means eligibility failed; no Motion command may be dispatched for that proposal.
- A disposition includes a reason code and provenance.
- CLEARED is not Motion's ACCEPTED and does not mean execution has started.

## Required independent checks
Skill verifies result shape and contract compatibility, proposal identity, approved Skill release, capability definitions, RBAC authorization, parameter schema, runtime preconditions and state freshness, and applicable safety requirements. Mind priority, rationale, uncertainty and own validation results never grant authority.

## Consequences
A completed result can contain proposals with different dispositions. Partial Mind results cannot trigger execution under the initial contract. Per-proposal disposition does not define Skill execution ordering or scheduling across multiple CLEARED proposals. In particular, if one Mind result contains several CLEARED proposals, the initial one-command-at-a-time Motion dispatch rule does not define which proposal is selected first, whether proposals are serialized across runs, or whether any may be deferred. This is an explicit OPEN item, not an implied priority rule. Owner: KOS-SKILL-001 task owner. Target: V2-M5, under proposed programme work item `PROPOSED-NEW-SKILL-004` (runtime against simulated capabilities). Until resolved by an approved contract, no cross-proposal ordering or concurrent dispatch is implied. The scheduling decision must not weaken authorization or precondition checks.

## Compatibility requirement
The existing Mind–Skill design note references an unaccepted Mind 0.1.0-draft. Before this ADR becomes a normative interface, the Mind contract owner must review the strict COMPLETED-only policy and proposal/result fields jointly with Skill.


## Open item: multiple CLEARED proposals

The disposition decision is per proposal only. It does not define scheduling/order among multiple CLEARED proposals from a single Mind result. Resolve under `PROPOSED-NEW-SKILL-004` at V2-M5; owner: KOS-SKILL-001 task owner. Until then, no cross-proposal ordering or concurrency is normative.
