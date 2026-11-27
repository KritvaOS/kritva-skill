# KOS-SKILL-001: Skill manifest and execution contract

Status: IN_PROGRESS. Milestone: V2-M1-SKILL-001. The eight architecture decisions (ADR-001 to ADR-008) are adopted into this repository as a PROPOSED architecture baseline by pull request #25 and recorded in kritva-program as D-158; normative contract approval is pending upstream review. Criteria (proposed): [ACCEPTANCE_CRITERIA.md](../../ACCEPTANCE_CRITERIA.md) section 3.

## Start

The owner (Dinesh) instructed in chat on 2026-11-03 to start the groundwork. That is the owner's chat instruction, not a separate approval record: the task criteria, the design note and any contract artifact remain proposed. This repository reports facts; the program repository decides baseline, weights, approvals and gates.

## Scope

The Skill manifest and execution contract: skill identity and version, declared capabilities, input and output schema, preconditions, lifecycle, resource and failure reporting. Not in scope: capability implementations, the control plane, the platform foundation.

## Why now

The joint Mind and Skill contract review is blocked until Skill has a manifest and execution contract to review against. kritva-mind holds a proposed Mind contract (0.1.0-draft, task KOS-MIND-001) with seven open questions for Skill.

## Work so far

- [Design note, proposed](../../docs/design/MIND_SKILL_INTERFACE.md): answers to Mind's seven questions; reconciled with the proposed architecture decisions agreed in discussion, but remains a draft input.
- [Architecture consolidation package](../../docs/architecture/README.md): architecture overview, ADR-001 through ADR-008 and upstream dependency register; repository-adopted as PROPOSED (pull request #25, D-158), normative contract approval pending upstream review.

## Not done

- No manifest schema, no execution-contract schema, no tests; `make test-unit`, `make test-integration` and `make test-regression` are NOT_IMPLEMENTED.
- No Mind, Motion or Core contract version is pinned.
- The architecture package was merged by the owner (pull request #25) under the interim reviewer roles of program decision D-047, so owner review is not independent review. Review by the upstream contract owners is outstanding.

## Programme alignment and schedule

The kritva-program v12 planning snapshot lists proposed future Skill work items: `PROPOSED-NEW-SKILL-002` (M2 build/package), `PROPOSED-NEW-SKILL-003` (M3 Control Plane registration), `PROPOSED-NEW-SKILL-004` (M5 runtime against simulated capabilities), and `PROPOSED-NEW-SKILL-005` (M8 production readiness). These are not registered as task IDs in this repository's `planning/TASKS.md`; any addition or change requires a kritva-program baseline amendment.

The proposed M1 target date 2026-11-30 is withdrawn as a credible delivery target. This task is currently architecture documentation only; normative schemas remain outstanding. A revised target date must be approved and recorded by kritva-program. D-159 records the withdrawal and PD-022 tracks the reforecast; kritva-program `milestones.json` keeps showing 2026-11-30 until a replacement schedule is approved. No M1 progress or completion is claimed.
