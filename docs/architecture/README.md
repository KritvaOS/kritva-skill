# KOS-SKILL-001 Architecture Consolidation Package

**Task:** KOS-SKILL-001 — Skill manifest and execution contract  
**Package status:** PROPOSED — REPOSITORY-ADOPTED; NORMATIVE CONTRACT APPROVAL PENDING UPSTREAM REVIEW  
**Prepared:** 2026-11-27

## Purpose
This package consolidates the eight architecture decisions made by the project owner. It is the proposed architecture baseline for repository review; it is not a released contract, implementation, acceptance record, milestone closure or programme-credit claim.

## Documents
- [ARCHITECTURE.md](ARCHITECTURE.md) — system context, responsibilities, trust boundaries and execution flow
- [DEPENDENCY_REGISTER.md](DEPENDENCY_REGISTER.md) — upstream contract dependencies, current evidence and closure conditions
- [ADR-001](ADR-001-authorization.md) — role-based authorization
- [ADR-002](ADR-002-version-registry.md) — hybrid release identity and execution approval
- [ADR-003](ADR-003-capability-vocabulary.md) — governed extensible capability vocabulary
- [ADR-004](ADR-004-preconditions.md) — hybrid precondition and runtime validation
- [ADR-005](ADR-005-mind-proposal-disposition.md) — per-proposal disposition and strict initial eligibility
- [ADR-006](ADR-006-execution-lifecycle.md) — execution lifecycle and RBAC-controlled cancellation
- [ADR-007](ADR-007-motion-orchestration.md) — staged hybrid Motion orchestration
- [ADR-008](ADR-008-execution-reporting.md) — append-only event history and consolidated report

## Decision status
All eight ADRs have the common status PROPOSED — REPOSITORY-ADOPTED; NORMATIVE CONTRACT APPROVAL PENDING UPSTREAM REVIEW. They were adopted into this repository as a proposed architecture baseline by pull request #25 and recorded in kritva-program as D-158. Repository adoption is not implementation approval, normative contract approval or programme acceptance; the status changes only after the relevant upstream contract owners complete compatibility review and a separate owner decision authorizes it. No independent review is implied.

## Scope boundary
This package defines architecture direction and contract requirements. It does not implement a registry, identity provider, authorization service, capability registry service, safety controller, Skill runtime, Motion adapter, event store or resource measurement system.

## Required review before adoption
1. Check consistency across all eight ADRs and the architecture overview.
2. Reconcile the existing Mind–Skill design note with the proposed decisions, keeping the Mind draft explicitly unapproved and compatibility unresolved.
3. Verify current upstream Core, Mind and Motion contract status and record immutable references only where a reviewed/approved contract exists.
4. Update repository navigation and changelog.
5. Review KOS-SKILL-001 acceptance criteria; any change must follow controlled criteria versioning.
6. Run repository checks and record results on the exact PR head.
7. Obtain approvals required by current programme repository-pipeline rules.

Until the relevant upstream contracts are approved and a separate owner decision changes their status, these documents are architecture decisions and design inputs only, not externally consumable API specifications.


## Programme alignment (snapshot v12)

KOS-SKILL-001 remains the only current Skill task in the repository task inventory. The following later work items are proposed in the kritva-program v12 planning snapshot and are not new IDs in this repository's `planning/TASKS.md`:

| Proposed programme work item | Milestone | Scope |
|---|---|---|
| `PROPOSED-NEW-SKILL-002` | M2 | Build and package |
| `PROPOSED-NEW-SKILL-003` | M3 | Control Plane registration through an approved public interface |
| `PROPOSED-NEW-SKILL-004` | M5 | Runtime against simulated capabilities; includes resolving the open multi-proposal scheduling contract |
| `PROPOSED-NEW-SKILL-005` | M8 | Production readiness |

Do not register these proposed work-item identifiers in `planning/TASKS.md`. Any task ID, scope, weight or milestone change requires an approved baseline amendment in kritva-program. The M1 target date of 2026-11-30 is withdrawn as a credible delivery target; KOS-SKILL-001 remains architecture documentation only, with normative schemas outstanding. A revised date must be approved and recorded by kritva-program. No M1 progress or completion is claimed.
