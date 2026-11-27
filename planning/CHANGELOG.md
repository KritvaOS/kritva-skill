# Changelog: kritva-skill

## Unreleased

- Marked the eight ADRs PROPOSED, REPOSITORY-ADOPTED after pull request #25, and recorded the program decisions D-158 and D-159 (PD-022 tracks the V2-M1 reforecast); corrected a literal line break in the task record. No approval, weight or credit change (Task: KOS-SKILL-001).

- Added the KOS-SKILL-001 architecture consolidation package: architecture overview, eight proposed ADRs agreed in discussion and pending repository adoption and upstream dependency register; repository adoption and normative contract work remain pending (Task: KOS-SKILL-001).

- Governance baseline: acceptance criteria, planning files, CI checks, CODEOWNERS, AGENTS.md, SECURITY.md (Task: KOS-SKILL-001 planning; program milestone V2-M0-SKILL-001).
- Started KOS-SKILL-001 on the owner's chat instruction (2026-11-03): task file and a proposed design note answering Mind's seven open questions. Nothing approved; no Mind contract version pinned (Task: KOS-SKILL-001).
- Synced the Mind to Skill design note with kritva-mind `main` 7569b80 (still a proposal; no Mind contract version pinned): replaced the stale gap list, used `SKILL_VERSION_UNAVAILABLE` throughout, stated that Skill's run lifecycle and Motion's public command states are separate (Task: KOS-SKILL-001).
- Added the kritva-motion facts (read at `d286114`) to the Mind to Skill design note, renamed Skill's proposal dispositions to CLEARED and DECLINED to avoid Motion's ACCEPTED and REJECTED, and proposed a deterministic `client_request_id` (Task: KOS-SKILL-001).

- Refined the proposed lifecycle with pre-start LOADED-to-FAILED handling, termination_status, revocation-aware dispatch, safety-contract handling for active commands, safety-stop initiator evidence, and runtime authority-service availability open items (Task: KOS-SKILL-001).
- Recorded the explicit multi-CLEARED-proposal scheduling open item and aligned proposed follow-on work items with kritva-program snapshot v12; no new task IDs were added to planning/TASKS.md (Task: KOS-SKILL-001).
