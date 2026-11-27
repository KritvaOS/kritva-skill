# kritva-skill

> Planning and governance repository for the Skill manifest and execution contract of the Kritva OS V2 plan. There is no implementation yet: the repository holds acceptance criteria, planning records, pull-request checks and rules, and no source code. The visibility class of this repository is PUBLIC (D-063).

| Property | Value |
|---|---|
| Project | KritvaOS (Kritva OS V2) |
| Repository | `KritvaOS/kritva-skill` |
| Repository Type | Capability (contract only; planning baseline, no implementation) |
| Visibility Class | PUBLIC (owner decision D-063 in kritva-program; it is an exception to the D-039 recommendation of PRIVATE, and no release review is recorded) |
| GitHub Setting | PUBLIC, the same as the class (D-063 in kritva-program keeps this repository public and takes it out of the return-to-private plan); OWNER-ATTESTED: no independent check of the setting and no verification date is recorded here |
| Lifecycle Status | PLANNING (governance baseline only) |
| Repository Owner | Project owner (role; see section 15) |
| Security Owner | Security Owner role ([SECURITY.md](SECURITY.md)) |
| Architecture | proposed architecture decisions in discussion; proposed consolidation package pending repository adoption ([docs/architecture/](docs/architecture/)) |
| Milestones | [planning/MILESTONE.md](planning/MILESTONE.md) and [planning/MILESTONE_STATUS.md](planning/MILESTONE_STATUS.md) |
| Tasks | [planning/TASKS.md](planning/TASKS.md) |
| Acceptance Criteria | [ACCEPTANCE_CRITERIA.md](ACCEPTANCE_CRITERIA.md) |
| Status Reporting | [status/status.json](status/status.json) (schema 2.0) and the generated progress view [status/STATUS.md](status/STATUS.md) (see section 10) |
| License | [LICENSE](LICENSE) (Apache License 2.0; see section 17 for an open question) |

This README follows the Kritva README standard ([`common/readme/README_STANDARD.md`](https://github.com/KritvaOS/kritva-standard/blob/main/common/readme/README_STANDARD.md) in [kritva-standard](https://github.com/KritvaOS/kritva-standard)). It is a navigation map; the documents it links own the detail.

## 1. Purpose and Scope

Kritva Skill is the part of Kritva OS V2 that will own the Skill manifest and execution contract. Today this repository only plans that work.

**This repository owns** (as planned): the Skill manifest and execution contract: skill identity and version, declared capabilities, input and output schema, preconditions, lifecycle, resource and failure reporting.

**This repository does not own**: capability implementations (kritva-sense, -motion, -mind), the control plane (kritva-raas), and the platform foundation (kritva-core).

**Implementation state.** IMPLEMENTED: governance baseline and repository checks. ARCHITECTURE: eight proposed ADRs agreed in discussion and pending repository adoption have been consolidated under [docs/architecture/](docs/architecture/). NOT YET IMPLEMENTED: normative manifest/execution schemas, runtime, source code, contract tests, unit/integration/regression gates and release. KOS-SKILL-001 is IN_PROGRESS; its acceptance criteria remain proposed and no programme credit is implied. Source folders are added only when a real task needs them, so their absence is intended and is not a defect.

## 2. Position in the KritvaOS Ecosystem

Kritva Skill is one of the capability repositories planned for Kritva OS V2, next to the other capability repositories and above the platform foundation (kritva-core). It is planned and tracked from [kritva-program](https://github.com/KritvaOS/kritva-program). The roster, order and dependencies of repositories are owned by kritva-program (`v2/planning/repo-pipeline.json`), not by this README. Boundaries: capability implementations (kritva-sense, -motion, -mind), the control plane (kritva-raas), and the platform foundation (kritva-core).

## 3. Architecture

The proposed architecture package is under [docs/architecture/](docs/architecture/). It records eight ADRs agreed in discussion and pending repository adoption; they are not yet normative or externally consumable interfaces. KOS-SKILL-001 remains IN_PROGRESS; its acceptance criteria are still proposed. Normative schemas, upstream compatibility pins, implementation and conformance tests remain outstanding. Interfaces are contract-first and versioned independently of program phases ([AGENTS.md](AGENTS.md)). Manifest conformance is a software property and does not show that an executed Skill is safe on a robot.

## 4. Documents to Read First

Role first, then the status the document declares. A label is a role, not an approval; where a document does not declare a status in its header, none is shown here.

| # | Document | Label, status | What it answers |
|---|---|---|---|
| 1 | [AGENTS.md](AGENTS.md) | AUTHORITATIVE for the rules for agents and contributors in this repository; in force | Scope, boundaries, commits, tests, tags |
| 2 | [ACCEPTANCE_CRITERIA.md](ACCEPTANCE_CRITERIA.md) | AUTHORITATIVE for the acceptance criteria of KOS-SKILL-001; PROPOSED (not accepted, weighted or credited) | What the first task must satisfy |
| 3 | [docs/architecture/README.md](docs/architecture/README.md) | PROPOSED architecture consolidation package; owner decisions recorded, repository adoption pending | Architecture decisions and dependencies |
| 4 | [planning/TASKS.md](planning/TASKS.md) | AUTHORITATIVE for this repository's task inventory (proposed registry, PD-004) | Which tasks exist and their status |
| 5 | [planning/MILESTONE.md](planning/MILESTONE.md) | REFERENCE: generated from kritva-program; dates are proposed targets, not approved | Proposed milestones |
| 6 | [planning/MILESTONE_STATUS.md](planning/MILESTONE_STATUS.md) | REFERENCE: the repository's own record, as of the governance baseline commit | Milestone status and evidence |
| 7 | [planning/REVIEW_CHECKLIST.md](planning/REVIEW_CHECKLIST.md) | AUTHORITATIVE for the pull-request review list | What a reviewer checks |
| 8 | [planning/GIT_COMMIT_STEP.md](planning/GIT_COMMIT_STEP.md) | REFERENCE | How to branch, commit, check, merge and tag |
| 9 | [planning/CHANGELOG.md](planning/CHANGELOG.md) | REFERENCE | What changed |
| 10 | [CONTRIBUTING.md](CONTRIBUTING.md) | AUTHORITATIVE for contribution steps | How to contribute |
| 11 | [SECURITY.md](SECURITY.md) | AUTHORITATIVE for vulnerability reporting (route tested 18 October 2026, owner-attested) | How to report a vulnerability |

## 5. Repository Structure and File Responsibilities

Labels: INPUT is edited by hand and read by a tool or review; GENERATED is written by a tool and never edited; EVIDENCE supports a claim; AUTHORITATIVE owns a rule; REFERENCE governs nothing. A label is a role, not an approval.

| Path | Content | Label, status | Notes |
|---|---|---|---|
| [planning/](planning/) | Tasks, milestones, milestone status, review checklist, commit step, changelog | MIXED: planning records | Governs execution and acceptance |
| [ACCEPTANCE_CRITERIA.md](ACCEPTANCE_CRITERIA.md) | Criteria and test gates for KOS-SKILL-001 | AUTHORITATIVE; PROPOSED | Accepted criteria are never edited; a change is a new version |
| [scripts/](scripts/) | `docs_check.py` (link check), `pipeline/pr_gate.py` (PR gate), `security/` (commit checkers), `check_readme.py` (README check) | INPUT; IMPLEMENTED | `pipeline/` and `security/` are protected paths of the gate |
| [tests/](tests/) | `commit_message_check/` (commit checker tests) and `readme_check/` (README checker tests) | EVIDENCE; IMPLEMENTED | Tests of the checkers only; no test of the contract exists |
| [.github/](.github/) | CODEOWNERS, pull request template, `kritva-gate.json` and four workflows | AUTHORITATIVE | `kritva-gate.json` configures the PR gate |
| [Makefile](Makefile) | Check targets; unimplemented gates exit 3 | INPUT; IMPLEMENTED | See section 11 |
| [docs/architecture/](docs/architecture/) | Architecture overview, eight ADRs and upstream dependency register | PROPOSED; proposed in discussion, repository adoption pending | Architecture baseline candidate |
| [AGENTS.md](AGENTS.md), [CONTRIBUTING.md](CONTRIBUTING.md), [SECURITY.md](SECURITY.md), [LICENSE](LICENSE) | Rules, contribution steps, security policy, licence | AUTHORITATIVE | |
| `src/`, `include/`, `status/`, `examples/` | Source, interfaces, status report, examples | NOT YET IMPLEMENTED (absent) | Added only when a real task needs them |

## 6. Toolchain and Development Workflow

| Tool | Purpose | Version | Check |
|---|---|---|---|
| Python 3 | Check scripts, PR gate, tests (standard library only) | 3.12 in CI; the scripts use only the standard library | `python3 --version` |
| GNU make | Convenience wrapper | any | `make --version` |
| Git | Branching and the commit checker | any | `git --version` |

There is no build, compiler or package toolchain because there is no implementation. Work follows [planning/GIT_COMMIT_STEP.md](planning/GIT_COMMIT_STEP.md): branch from an up-to-date `main`, commit with the format in section 12, run the checks, open a pull request.

```bash
make check          # check: required planning files exist; commit-message checker tests pass
make docs-check     # check: every relative Markdown link points to an existing file
make check-readme   # check: structural check of this README only
```

## 7. Dependencies and Interfaces

| Dependency | Direction | Kind | Contract | State |
|---|---|---|---|---|
| kritva-core | upstream | planned contract use; no Git submodule, build or runtime link | trusted identity/role interface | UNDEFINED: no approved contract version or immutable reference is pinned |
| kritva-mind | upstream | planned contract use; no Git submodule, build or runtime link | versioned Mind result/proposal contract | DRAFT: `0.1.0-draft`, source commit `7569b80`; not approved or normative |
| kritva-motion | upstream | planned contract use; no Git submodule, build or runtime link | versioned Motion command/lifecycle contract | DRAFT: source commit `d286114`; not approved or normative |
| public platform integration boundary | peer interface | contract-only; no private implementation dependency | public platform integration API | UNDEFINED: no approved public interface contract is established |

The Mind and Motion references above pin the reviewed source snapshots for traceability only; both contracts remain DRAFT and are not approved runtime dependencies. Identity/Core, public platform integration, registry, capability vocabulary and precondition interfaces remain UNDEFINED. Per-dispatch identity and registry checks make those services runtime availability dependencies; freshness, cache and timeout policy remain open in [DEPENDENCY_REGISTER.md](docs/architecture/DEPENDENCY_REGISTER.md). Five kinds of relationship are kept apart: program ordering, Git submodule, source or build dependency, runtime integration, and governance or status reporting. A PLANNED dependency is not an integration that exists.

## 8. Milestones and Implementation Plan

Proposed milestones, from [planning/MILESTONE.md](planning/MILESTONE.md) (generated from kritva-program `v2/planning/milestones.json`; edit them there) and the status recorded in [planning/MILESTONE_STATUS.md](planning/MILESTONE_STATUS.md):

| ID | Program milestone | Status recorded here | Outcome (proposed) |
|---|---|---|---|
| V2-M0-SKILL-001 | V2-M0 FOUNDATION | IN_REVIEW (this change) | Repository governance baseline merged: acceptance criteria, CI checks, CODEOWNERS, AGENTS.md. |
| V2-M1-SKILL-001 | V2-M1 STUDIO | PROPOSED | Architecture baseline and normative manifest/execution-contract schemas (schemas are not yet produced). |
| PROPOSED-NEW-SKILL-002 | V2-M2 BUILD & ARTIFACT | PROPOSED programme work item | Build and package. |
| PROPOSED-NEW-SKILL-003 | V2-M3 CONTROL PLANE | PROPOSED programme work item | Control Plane registration through an approved public interface. |
| PROPOSED-NEW-SKILL-004 | V2-M5 EXECUTION | PROPOSED programme work item | Runtime against simulated capabilities; resolve multi-proposal scheduling. |
| PROPOSED-NEW-SKILL-005 | V2-M8 PRODUCTION | PROPOSED programme work item | Production readiness. |

The target dates are in [planning/MILESTONE.md](planning/MILESTONE.md); they are proposed targets, not approved dates and not delivery commitments (program decision PD-001). The M1 target of 2026-11-30 is withdrawn as a credible delivery target; the package is architecture documentation only and normative schemas remain outstanding. A revised date requires an approved kritva-program baseline amendment. No M1 progress or completion is claimed. The status table is "as of the governance baseline commit" and may lag the repository (it shows the governance baseline as IN_REVIEW although the baseline change has since been merged). A milestone closes only through an approved `COMPLETION_RECORD.md`; a tag or a merge does not close it, and no completion record exists.

## 9. Tasks and Acceptance Criteria

- **Where tasks live.** [planning/TASKS.md](planning/TASKS.md) lists the tasks (registry type `repo-tasks-md`, prefix `KOS-SKILL`); the proposed task registry is program decision PD-004. Tasks are planning inventory with no weight and no credit until a separately approved baseline amendment. The v12 snapshot's `PROPOSED-NEW-SKILL-002` through `PROPOSED-NEW-SKILL-005` are programme planning work items only; do not add them to `planning/TASKS.md`. Any ID, scope, weight or milestone change requires a kritva-program baseline amendment.
- **Acceptance.** [ACCEPTANCE_CRITERIA.md](ACCEPTANCE_CRITERIA.md) holds the criteria and test gates; they are proposed until the owner approves the task. Unimplemented gates are reported as NOT_IMPLEMENTED and are never counted as a pass. [planning/REVIEW_CHECKLIST.md](planning/REVIEW_CHECKLIST.md) is the review list.
- Work is not accepted because a commit or merged pull request exists, a check is green or a milestone says it is proposed. Interface and boundary changes, safety and security behaviour and dependency changes need human review ([AGENTS.md](AGENTS.md)).

## 10. Status Reporting and Program Integration

**Progress view.** [status/STATUS.md](status/STATUS.md) is a generated progress view: a bar of accepted weight, with execution, evidence, acceptance and release readiness kept apart. `scripts/progress_report.py` renders it from the pinned snapshot `status/program_snapshot.json`, which kritva-program writes (`tools/publish_repo_progress.py`, decision D-120). The `progress-check` workflow runs on pull requests and on pushes to main, runs `python3 scripts/progress_report.py --check` (read-only), and fails when the report and the snapshot differ. The view is a derived snapshot of the program and can lag it; it records no acceptance, and its figures are not repeated in this README (README standard, rule 4).

A `status/` directory holds `status/status.json` (schema 2.0), which reports facts only; this repository has no generator for it. The program tracks its tasks through the registry named in `.github/kritva-gate.json` (`planning/TASKS.md`, type `repo-tasks-md`). This repository reports facts only and earns no program credit; nothing in it adds baseline weight (kritva-program decides baseline, weights, approvals and gates).

| Dimension | Source record | Authority |
|---|---|---|
| Execution | the task status in [planning/TASKS.md](planning/TASKS.md); KOS-SKILL-001 is IN_PROGRESS | The task owner records it |
| Evidence | none recorded: no CI run, test result or review record is cited as task evidence | Evidence is recorded at acceptance, by the author, and checked by another reviewer |
| Acceptance | [ACCEPTANCE_CRITERIA.md](ACCEPTANCE_CRITERIA.md), the review record and the central approvals in kritva-program | The independent reviewer and the owner, never a status report |
| Release readiness | not defined: no release, tag or completion record exists | The owner, through the central gates |

## 11. Build, Test, Regression and Validation

CI runs four workflows. `make check` is a local command and is not the same as CI.

| Workflow | Trigger | What it runs |
|---|---|---|
| `commit-message-check` | pull requests | the commit checker's unit tests, and the checker on the pull request's commits (rejects AI-session trailers and links only) |
| `pr-acceptance-gate` | pull requests | `scripts/pipeline/pr_gate.py static` against `.github/kritva-gate.json`: report-only rules R01 commit format, R02 task exists and is open, R03 acceptance criteria changed, R04 protected paths, R05 completion record, R06 required workflows, R07 required approvals, R08 dependencies. REJECT fails the check; NEEDS_HUMAN and APPROVE pass it; it posts or updates a report comment and approves and merges nothing |
| `readme-check` | pull requests; push to `main` | the README checker's unit tests, then `python3 scripts/check_readme.py README.md` (structure, metadata and local links only; not a required check yet, D-067) |
| `secret-scan` | push to `main`; pull requests; manual dispatch | gitleaks over the git history |

| Command | Effect | Notes |
|---|---|---|
| `make check` | check | required planning files exist; the commit-message checker's unit tests run; it does not run `docs-check`, the PR gate or any contract test |
| `make docs-check` | check | every relative Markdown link points to an existing file (not an anchor check) |
| `make check-readme` | check | structural check of this README only (metadata, topics, relative links, placeholders); a PASS does not show the content is accurate; not part of `make check` or CI |
| `make preflight` | check | the CI checks run locally: `make check`, `make docs-check`, `make check-readme` and the README checker tests, `make progress-check`, the commit checks and the static PR gate over your branch commits, and no test target (the test targets are NOT_IMPLEMENTED and are left out, never counted as a pass); lists every failure; run `git fetch origin` first; it does not run `secret-scan` and does not replace CI |
| `make hooks-install`, `make preflight-hook-off` | modify | `hooks-install` makes `git push` run `make preflight` in this clone; `preflight-hook-off` turns that off (`git push --no-verify` skips it once) |
| `make lint`, `make test-unit`, `make test-integration`, `make test-regression`, `make test`, `make acceptance` | placeholder | print NOT_IMPLEMENTED and exit 3: they check nothing and are never a pass |
| `python3 scripts/security/check_commit_format.py --range origin/main..HEAD` | check | the commit format of the commits on a branch (the PR gate runs the same check as rule R01) |

There is nothing to build and no test of the contract, because there is no contract yet. A passing `make check` shows only that the listed files exist and that the commit checker's own tests pass. It does not show that a design is right, that a gate is closed or that anything is safe. `.github/kritva-gate.json` declares three required checks (`secret-scan`, `commit-message-check` and `pr-acceptance-gate`); that list is the gate's own declaration, not the branch ruleset. [AGENTS.md](AGENTS.md) and [CONTRIBUTING.md](CONTRIBUTING.md) now name the same three. The owner decided that `pr-acceptance-gate` is a required check in the `main` ruleset (PD-018, D-061); the owner states that it has been added to the `main` ruleset (D-069); that is OWNER-ATTESTED and not independently verified from this README.

## 12. Git Workflow and Review

Controlling statement ([AGENTS.md](AGENTS.md) section 3, the D-053 form): header `type(scope): summary` (types feat, fix, docs, refactor, test, build, ci, chore, perf, revert, security; at most 90 characters; an optional `[KOS-SKILL-NNN]` suffix must match the footer), exactly one `Task:` or `Tasks:` footer line, and `Tasks: None (reason)` only on a docs or chore commit that implements no task; merge by merge commit; pull requests use `.github/PULL_REQUEST_TEMPLATE.md`. [CONTRIBUTING.md](CONTRIBUTING.md) repeats the same rule. Enforcement: `commit-message-check` rejects only AI-session trailers and links; the format (rule R01) is checked by the `pr-acceptance-gate` report, whose `.github/kritva-gate.json` records the commit standard as adopted (the PR gate treats a missing footer as a failure). Work on a branch and open a pull request; do not push to `main`. Required checks and approvals are in section 11; the Code Owner reviews ([.github/CODEOWNERS](.github/CODEOWNERS)); with one owner the PR author cannot self-approve, so use the owner bypass or a second reviewer.

## 13. Safety and Security

No implementation and no safety case exist at this planning stage: the repository contains no software that runs and no hardware, and it makes no safety claim. The planned contract can still influence what other software does, so its safety implications need human review when it is designed. The planning records state that any hardware-in-loop or physical validation claim stays gated on program milestone V2-M6 (HOLD) and that no architecture or safety reviewer was assigned when the criteria were written (program decision PD-007, since resolved on an interim basis by D-047: both roles are assigned to the owner). Software acceptance, tests, simulation and mocks are never described as hardware or safety validation. Skill describes how capabilities are declared and executed; conformance of a manifest is a software property and does not show that an executed skill is safe on a robot.

**Reporting a vulnerability:** follow [SECURITY.md](SECURITY.md). It names GitHub private vulnerability reporting as the first route and gives a direct-contact fallback. The Security Owner reports having tested the reporting route on 18 October 2026 (D-068); that is ATTESTED, not independently verified, and nothing here promises a response time. Never put details of an unfixed vulnerability in a public issue, pull request or commit message.

- Never commit secrets, private keys, tokens, passwords or production data. The `secret-scan` workflow runs on pull requests and on pushes to `main`.
- If a secret is committed by mistake, tell the Security Owner at once; removing it in a later commit does not make it safe.

## 14. Release and Versioning

No release exists and no version is defined. The plan is annotated SemVer tags (`vMAJOR.MINOR.PATCH`) created only after the approved merge, with contracts versioned independently of program phases and a MAJOR version for a breaking contract change ([AGENTS.md](AGENTS.md) sections 2 and 6). A milestone closes only through an approved completion record. This README records no release state.

## 15. Ownership and Escalation

| Role | Responsibility |
|---|---|
| Repository owner (Dinesh; `.github/CODEOWNERS`) | Directs the work, decides, approves and merges |
| Security Owner | Handles vulnerability reports and committed secrets |
| Architecture reviewer and safety reviewer | Both roles are assigned to the owner on an interim basis (D-047); that is not independent review, and the independence requirement remains unmet; the CODEOWNERS comments say the same (D-065) |
| Implementers (people and agents) | Implement approved scope, record evidence and follow `AGENTS.md` |

## 16. Related Repositories and References

| Repository | Relationship |
|---|---|
| [kritva-program](https://github.com/KritvaOS/kritva-program) | Program plan, baseline, decisions, repository pipeline, README standard |
| [kritva-core](https://github.com/KritvaOS/kritva-core) | Platform foundation (planned dependency) |
| [kritva-mind](https://github.com/KritvaOS/kritva-mind) and [kritva-motion](https://github.com/KritvaOS/kritva-motion) | Mind and Motion contracts (planned dependencies) |

## 17. License

The [LICENSE](LICENSE) file is the Apache License 2.0. Copyright (c) 2026 Kritva Robotics Private Limited. The owner confirmed Apache-2.0 as the licence of this repository (program decision D-064, which closes PD-013), and [ACCEPTANCE_CRITERIA.md](ACCEPTANCE_CRITERIA.md) section 9 says the same.
