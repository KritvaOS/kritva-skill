# KOS-SKILL-001: Skill manifest and execution contract

Status: IN_PROGRESS. Milestone: V2-M1-SKILL-001. Criteria (proposed): [ACCEPTANCE_CRITERIA.md](../../ACCEPTANCE_CRITERIA.md) section 3.

## Start

The owner (Dinesh) instructed in chat on 2026-11-03 to start the groundwork. That is the owner's chat instruction, not a separate approval record: the task criteria, the design note and any contract artifact remain proposed. This repository reports facts; the program repository decides baseline, weights, approvals and gates.

## Scope

The Skill manifest and execution contract: skill identity and version, declared capabilities, input and output schema, preconditions, lifecycle, resource and failure reporting. Not in scope: capability implementations, the control plane, the platform foundation.

## Why now

The joint Mind and Skill contract review is blocked until Skill has a manifest and execution contract to review against. kritva-mind holds a proposed Mind contract (0.1.0-draft, task KOS-MIND-001) with seven open questions for Skill.

## Work so far

- [Design note, proposed](../../docs/design/MIND_SKILL_INTERFACE.md): answers to Mind's seven questions. Not approved.

## Not done

- No manifest schema, no execution-contract schema, no tests; `make test-unit`, `make test-integration` and `make test-regression` are NOT_IMPLEMENTED.
- No Mind, Motion or Core contract version is pinned.
- No review. The architecture reviewer is the owner on an interim basis (program decision D-047), so nothing here is independent review.
