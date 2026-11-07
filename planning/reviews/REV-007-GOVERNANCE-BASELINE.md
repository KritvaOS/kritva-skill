# REV-007: kritva-skill governance baseline (V2-M0-SKILL-001)

Status: PREPARED, OWNER DECISION PENDING.
Reviewed commit: `c17192001f6c672819589857e8644ad21573d8d8` (local `main` HEAD on 2026-11-07; confirm it equals GitHub `main` when the owner reviews).
Program record: REV-007 in kritva-program `v2/planning/PENDING_REVIEWS.md`.
Related plan: kritva-program `v2/planning/M0_CLOSURE_PLAN.md` and `v2/planning/M0_TASK_DEFINITIONS.md`.

This record is evidence for the owner's review. It does not accept a task, award progress, or close V2-M0-SKILL-001. Closure needs the owner's decision below and an approved completion record for the milestone.

## 1. Proposed M0 task (planning only)

Title: Skill governance baseline accepted. Weight: 3. Registered as a `KOS-SKILL` task only after baseline v11 and owner approval; no placeholder row is added to `TASKS.md` before then.

| Criterion | Statement | Evidence at the reviewed commit | Result |
|---|---|---|---|
| AC-M0-1 | Governance files exist: `AGENTS.md`, `ACCEPTANCE_CRITERIA.md`, `SECURITY.md`, `.github/CODEOWNERS`, `.github/kritva-gate.json` | All present | PRESENT |
| AC-M0-2 | Required checks are defined and named the same in workflows and `.github/kritva-gate.json` | `kritva-gate.json` lists `secret-scan`, `commit-message-check`, `pr-acceptance-gate`; workflows of the same names exist. `readme-check` workflow also exists and is not required | MATCH (job names not compared line by line) |
| AC-M0-3 | The branch ruleset on `main` requires those checks, a pull request, and the approvals `REPO_CODE_OWNER` and `ARCHITECTURE_REVIEWER` | GitHub settings, not visible from the repository | OWNER TO ATTEST |
| AC-M0-4 | Commit policy is enforced by an automated check | `commit-message-check` workflow; checker tests in `tests/commit_message_check/` run by `make check` | PRESENT |
| AC-M0-5 | The program has a status source for Skill | None: there is no `status/` directory and Skill is not registered on a program workstream (PD-014) | NOT MET until PD-014 is decided |
| AC-M0-6 | Planning records are consistent and no unimplemented gate is reported as passing | `make lint`, `test-unit`, `test-integration`, `test-regression`, `test` and `acceptance` are NOT_IMPLEMENTED (exit 3), none reported as passing. There is no `unit-tests` workflow because there is no code | CONSISTENT |

## 2. Open items

- PD-014: choose how the program reads Skill state (a `status/status.json` in the Sense schema, or registration from `planning/TASKS.md` alone). Until decided this repository adds no status file.
- Task records: `planning/TASKS.md` shows KOS-SKILL-001 as IN_PROGRESS with proposed criteria. `docs/design/MIND_SKILL_INTERFACE.md` exists as design groundwork. Neither is an acceptance.

## 3. CI evidence

There is no `unit-tests` workflow. Record the passing runs of the required checks on the reviewed commit:

- secret-scan run id: ____
- commit-message-check run id: ____
- pr-acceptance-gate run id: ____
- commit: ____

## 4. Owner attestations

- [ ] Ruleset on `main` requires pull request, the three required checks, and both approval roles (AC-M0-3).
- [ ] CODEOWNERS entries are the intended approvers.

## 5. Decision

Decision: PENDING
Decided by: ____
Date: ____
Notes: ____
