# REV-007: kritva-skill governance baseline (V2-M0-SKILL-001)

Status: APPROVED by the owner (D-114, 2026-11-07); ruleset and CODEOWNERS verified against GitHub on 2026-11-07 (D-115).
Reviewed commit: `c17192001f6c672819589857e8644ad21573d8d8` (local `main` HEAD on 2026-11-07; confirm it equals GitHub `main` when the owner reviews).
Program record: REV-007 in kritva-program `v2/planning/PENDING_REVIEWS.md`.
Related plan: kritva-program `v2/planning/M0_CLOSURE_PLAN.md` and `v2/planning/M0_TASK_DEFINITIONS.md`.

This record is evidence for the owner's review. It does not accept a task, award progress, or close V2-M0-SKILL-001. Closure needs the owner's decision below and an approved completion record for the milestone.

## 1. Proposed M0 task (planning only)

Title: Skill governance baseline accepted. Weight: 3. Registered as a `KOS-SKILL` task only after baseline v11 and owner approval; no placeholder row is added to `TASKS.md` before then.

| Criterion | Statement | Evidence at the reviewed commit | Result |
|---|---|---|---|
| AC-M0-1 | Governance files exist: `AGENTS.md`, `ACCEPTANCE_CRITERIA.md`, `SECURITY.md`, `.github/CODEOWNERS`, `.github/kritva-gate.json` | All present | PRESENT |
| AC-M0-2 | Required checks are defined and named the same in workflows, `.github/kritva-gate.json` and the ruleset: `secret-scan`, `commit-message-check`, `pr-acceptance-gate`, `readme-check` | Workflow job names match. The ruleset requires `readme-check`; the gate file was aligned by PR #13 | MATCH (PR #13 merged) |
| AC-M0-3 | The branch ruleset on `main` requires a pull request and the required checks. The approval roles `REPO_CODE_OWNER` and `ARCHITECTURE_REVIEWER` are held by the owner on an interim basis (D-047) and are not enforced by the ruleset (D-115) | Checked 2026-11-07 through the GitHub rulesets API: ruleset `protect-main` is active on the default branch, blocks deletion and force-push, requires a pull request with 0 approving reviews and no code-owner review, and requires pr-acceptance-gate, commit-message-check, readme-check, secret-scan. Bypass actors are not visible without admin access | PARTIAL: pull request and checks verified; approvals not enforced |
| AC-M0-4 | Commit policy is enforced by an automated check | `commit-message-check` workflow; checker tests in `tests/commit_message_check/` run by `make check` | PRESENT |
| AC-M0-5 | The program has a status source for Skill | `status/status.json` (schema 2.0) registers the workstream (PD-014, D-116) and reports KOS-SKILL-M0-001 (baseline v11, D-117) | MET |
| AC-M0-6 | Planning records are consistent and no unimplemented gate is reported as passing | `make lint`, `test-unit`, `test-integration`, `test-regression`, `test` and `acceptance` are NOT_IMPLEMENTED (exit 3), none reported as passing. There is no `unit-tests` workflow because there is no code | CONSISTENT |

## 2. Open items

- PD-014 was decided in D-116: Skill publishes `status/status.json` (schema 2.0). Baseline v11 (D-117) adds KOS-SKILL-M0-001, which the status report now lists; KOS-SKILL-001 is not baselined and is not reported.
- Task records: `planning/TASKS.md` shows KOS-SKILL-001 as IN_PROGRESS with proposed criteria. `docs/design/MIND_SKILL_INTERFACE.md` exists as design groundwork. Neither is an acceptance.

## 3. CI evidence

Recorded 2026-11-07 from the GitHub check runs on the reviewed commit:

- secret-scan run id: 41598873743 (success, push run on `main`)
- readme-check run id: 41598873766 (success)
- commit: `c17192001f6c672819589857e8644ad21573d8d8`
- `commit-message-check` and `pr-acceptance-gate` run on pull requests, so they have no run on this commit. Skill has no `unit-tests` workflow.

## 4. Verification of ruleset and CODEOWNERS (2026-11-07)

- Ruleset: verified as stated in AC-M0-3. The approval requirement is not enforced; the owner merges under the interim reviewer roles of D-047.
- CODEOWNERS: verified. `*` and the protected files (`.github/`, `SECURITY.md`, `LICENSE`, `ACCEPTANCE_CRITERIA.md`) are owned by `@dineshannayya`. GitHub does not enforce code-owner review because the ruleset does not require it.
- Not verified: bypass actors (admin access needed).

## 5. Decision

Decision: APPROVED (owner, interim reviewer roles of D-047; recorded in D-114 on 2026-11-07; verification in D-115)
Decided by: Dinesh
Date: 2026-11-07
Notes: This is not independent review.
