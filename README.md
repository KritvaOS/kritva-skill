# kritva-skill

Kritva Skill: part of Kritva OS V2, planned and tracked from [kritva-program](https://github.com/KritvaOS/kritva-program).

**Status:** planning and governance baseline only. There is no implementation yet; the first task (KOS-SKILL-001, Skill manifest and execution contract) is proposed and not yet approved.

## Scope

Owns: the Skill manifest and execution contract: skill identity and version, declared capabilities, input and output schema, preconditions, lifecycle, resource and failure reporting.

Does not own: capability implementations (kritva-sense, -motion, -mind), the control plane (kritva-raas), and the platform foundation (kritva-core).

Depends on: kritva-core (approved contract), kritva-mind and kritva-motion (versioned contracts).

## Layout

| Path | Purpose |
|---|---|
| [ACCEPTANCE_CRITERIA.md](ACCEPTANCE_CRITERIA.md) | Acceptance criteria and test gates |
| [planning/](planning/) | Tasks, milestones, review checklist, commit step, changelog |
| [AGENTS.md](AGENTS.md), [CONTRIBUTING.md](CONTRIBUTING.md), [SECURITY.md](SECURITY.md) | Rules for contributors, agents and vulnerability reporting |
| [Makefile](Makefile) | Standard check targets (unimplemented gates report NOT_IMPLEMENTED, never pass) |
| `.github/` | CODEOWNERS and the secret-scan and commit-message-check workflows |

Source folders are added only when the first real task needs them.

## Checks

```bash
make check   # planning files present, commit-checker self-test
make test    # reports NOT_IMPLEMENTED (exit 3) until tests exist
```

## Program alignment

Milestones: V2-M0-SKILL-001 (governance baseline), V2-M1-SKILL-001 (contract), V2-M2-SKILL-001 (validation). Dates are proposed in kritva-program `v2/planning/` and are not approved. Nothing in this repository adds baseline weight or credit.
