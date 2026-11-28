# Status report: kritva-skill

`status.json` is this repository's task-level report for the program (schema 2.0, `status.schema.json`). It reports facts only; acceptance and credit live in KritvaOS/kritva-program.

`tasks` lists the baselined `KOS-SKILL` tasks. Today that is KOS-SKILL-M0-001 (baseline v11, D-117); KOS-SKILL-001 is not baselined and is not reported (D-116). Planning inventory stays in `planning/TASKS.md`. When another task is baselined, add it here with its execution state and evidence, and refresh `source.commit` and `updated_at` after reviewing the report against the planning records.

The program does not expire a report on age (D-165): a task keeps its credit until this repository changes inside that task's scope, or in shared material, after `source.commit` (scopes are in `v2/planning/task_scopes.json` in KritvaOS/kritva-program). A report older than 60 days only raises a warning.
