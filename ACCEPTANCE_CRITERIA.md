# Acceptance Criteria: kritva-skill

Standard: kritva-program `v2/planning/ACCEPTANCE_STANDARD.md` (proposed; approval pending PD-005, PD-006). Criteria below are for task KOS-SKILL-001 (Skill manifest and execution contract) and are proposed until the owner approves the task. Nothing here is accepted, weighted or credited.

## 1. Purpose and scope

Owns: the Skill manifest and execution contract: skill identity and version, declared capabilities, input and output schema, preconditions, lifecycle, resource and failure reporting.

Does not own: capability implementations (kritva-sense, -motion, -mind), the control plane (kritva-raas), and the platform foundation (kritva-core).

## 2. Normative dependencies

kritva-core (approved contract), kritva-mind and kritva-motion (versioned contracts). Exact versions or commit SHAs are recorded here when the contracts they refer to are approved; none are pinned yet.

## 3. Functional criteria (KOS-SKILL-001)

| ID | Criterion (testable) | Verified by |
|---|---|---|
| AC-001 | A skill manifest declares identity, version, capabilities used, and input and output schemas. | manifest validation tests |
| AC-002 | Preconditions are explicit and checked before execution; a failed precondition gives a defined error. | precondition tests |
| AC-003 | The skill lifecycle (loaded, running, completed, cancelled, failed) is specified and conformance-tested. | lifecycle tests |
| AC-004 | Resource use and failures are reported in defined fields. | failure-path tests |
| AC-005 | Skill orchestrates capabilities through declared interfaces only; capability repositories never depend on Skill. | dependency review |

## 4. Interface and API compatibility

The contract defines inputs, outputs, error handling, versioning and lifecycle, with time and units stated. Contracts are versioned independently of program phases. Depends on core, mind and motion contract versions; capability repositories must not depend on skill.

## 5. Test gates

| Gate | Command | Required result | State |
|---|---|---|---|
| Unit | `make test-unit` | all pass | NOT_IMPLEMENTED until KOS-SKILL-002 (Manifest validation and lifecycle conformance tests) |
| Integration | `make test-integration` | all pass, real dependency boundaries | NOT_IMPLEMENTED |
| Regression | `make test-regression` | all pass, suite unchanged by the change | NOT_IMPLEMENTED |
| Structure | `make check` | planning files present, commit checker self-test passes | implemented |

An unimplemented gate is reported as NOT_IMPLEMENTED and is never counted as a pass. No coverage threshold is set; one needs an approved decision.

## 6. Specialised gates

Determinism and error-path behaviour apply to every criterion above. No hardware-in-loop or physical validation applies: any such claim stays gated on program milestone V2-M6 (HOLD).

## 7. Evidence requirements

Immutable commit SHAs, CI run IDs for secret-scan, commit-message-check and the test gates, and the review record against the closing commit.

## 8. Definition of Done

As in the program standard section 1: stable task ID, merged through the approved PR, required checks green on the exact closing commit, reviews recorded, documentation and changelog updated, immutable evidence, no blocker converted into a pass.

## 9. Known limitations and exclusions

- No implementation exists; criteria are not yet testable by automated gates (gates listed NOT_IMPLEMENTED).
- The architecture and safety reviewer roles are held by the owner on an interim basis (program decision D-047, resolving PD-007); independent review is not yet in place.
- Licence: Apache-2.0, confirmed by the owner (program decision D-064, closing PD-013).

## 10. Change control

Accepted criteria are never edited. A change is a new criteria version with its own review; accepted evidence keeps the version it was produced under.
