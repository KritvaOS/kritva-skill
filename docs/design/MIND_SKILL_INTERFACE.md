# Design note: Mind proposal to Skill execution (PROPOSED)

Task: KOS-SKILL-001. Status: proposed, not approved, not reviewed by anyone but the owner, who holds the architecture review role on an interim basis (program decision D-047). It answers the seven questions in kritva-mind `ARCHITECTURE.md` section 12 and `contract/COMPATIBILITY.md`. Every statement below is a proposal. Nothing here is a released interface, and nothing in it is hardware or safety validation.

## 0. Basis and limits

- Read: kritva-mind `contract/*.schema.json`, `contract/README.md`, `contract/SEMANTICS.md`, `contract/COMPATIBILITY.md` (Skill section), `ARCHITECTURE.md` section 5 and the decisions table (section 8), at kritva-mind `main` commit `7569b80` (pull request 19; local checkout, 2026-11-03). The first version of this note was written against `db1600e`; Mind has since merged pull requests 16 to 19 and this version is re-read against `7569b80`.
- Not verified: nothing was executed; no validator exists on either side; no schema for the Skill interface exists yet. No Core contract was read. No kritva-motion checkout is available here and no Motion repository was read: what this note says about Motion's public command states is taken from kritva-mind `contract/COMPATIBILITY.md`, and is not checked against kritva-motion, nor against anything unapproved there. The Mind contract is an unaccepted `0.1.0-draft` and is **not pinned** here ([ACCEPTANCE_CRITERIA.md](../../ACCEPTANCE_CRITERIA.md) section 2).
- The Mind result carries `proposed_skills[]` (`skill_id`, `version_constraint`, `parameters`, `preconditions`, `rationale`, `priority`, `uncertainty`). It has no authorize or execute field. Skill therefore treats every field as an untrusted claim.

## (a) Skill identity and version reference

Proposal:

- **Identity.** `skill_id` is a lowercase dotted name, pattern `^[a-z][a-z0-9_]{0,31}(\.[a-z0-9_]{1,32}){0,3}$` (the same shape as the Sense `sensor_id`, so one naming rule is used across repositories). It is stable across versions and is never reused for a different skill. Mind's current draft uses the same pattern (`SkillId`); Skill would reject ids outside it.
- **Version.** Skill versions are SemVer `MAJOR.MINOR.PATCH`. The manifest declares exactly one version. A reference to a concrete skill is `skill_id` plus `version`.
- **Constraint grammar (closed).** Exact `1.2.3`; caret `^1.2.0` (same MAJOR, at least this version; for 0.x, same MINOR); range `>=1.2.0 <2.0.0`. No wildcards, no tags such as `latest`.
- **Can Mind propose a constraint without pinning an unapproved version?** Yes, because a constraint is a selector over versions Skill already holds, never a pin and never an approval. Skill resolves it only among manifest versions whose approval state is APPROVED. A constraint cannot make an unapproved or pre-release version eligible, even if it names that version exactly; such a proposal is rejected as `SKILL_VERSION_UNAVAILABLE`. When several versions match, Skill picks the highest and records which one. Mind should not need to know which versions exist. Mind's schema now states the same rule: a constraint selects among versions the consumer holds and is never a pin or an approval.
- **Open (not decided here):** where the approval state of a skill version is recorded and who sets it. That is a program decision, not a Skill invention.

## (b) What Skill needs to resolve a proposal

From the proposal: `skill_id`, `version_constraint` (optional; absent means any approved version), `parameters`.

From the enclosing result, for traceability and policy: `contract_version`, `result_id`, `request_id`, `context_ref`, `status`, `created_at`, and the proposal's position.

From its own manifest registry, per candidate version: identity and version, approval state, declared capabilities, input schema, output schema, precondition definitions, lifecycle and failure-reporting declarations, and the range of Mind contract versions it accepts.

**What Mind's current draft provides** (read at `7569b80`; Mind's own proposals, unaccepted):

| Need of Skill | Mind draft `0.1.0-draft` now |
|---|---|
| Handle on one proposal | `proposal_id`, required, unique within a result (a validator rule; JSON Schema cannot express it) |
| Skill name shape | `SkillId` pattern, the same as in (a) |
| Version selector | closed `VersionConstraint` grammar: exact, caret, range; semantics in Mind `SEMANTICS.md` section 3 (no pre-release, wildcards or tags) |
| Naming a manifest precondition | optional `precondition_id`; `expression` is descriptive and never evaluated |
| Ordering | `priority` ascending, 0 first; ties and absent values by ascending `proposal_id`; absent after present; array order not authoritative |
| PARTIAL results | proposals advisory; consumer must not execute them unless its own policy says so |
| Parameter validation by Mind | only against a schema supplied as runtime data, within Mind's validator subset; Mind depends on no Skill code or version |
| FAILED and CANCELLED results | attempt-only provenance when no inference ran; their proposals are not to be executed |
| Errors | closed `MIND_*` error codes |
| Replay evidence | digests on input, output and context snapshot; a context snapshot is required for COMPLETED and PARTIAL |

Skill must still adopt these on its side (unverified: no Skill schema exists to check them against).

## (c) Parameter schema and precondition format

- **Parameters.** The manifest holds the input schema as JSON Schema 2020-12 (the dialect Mind already uses). Skill validates `parameters` against the resolved version's schema with unknown properties rejected by default. Units and time follow the same rule as Mind: durations and quantities carry their unit in the field name; timestamps are RFC 3339.
- **Preconditions, Skill side.** The manifest declares each precondition with an `id`, a human `description`, and a machine-evaluable `check` taken from a closed vocabulary. **The vocabulary is not defined in this note**; defining it is the main open design work of KOS-SKILL-001. A precondition that cannot be machine-checked is not allowed to gate execution silently: it is declared as requiring explicit confirmation.
- **Preconditions, Mind side.** Mind's `{description, expression}` is treated as an informational claim about what Mind assumed. Skill does not evaluate `expression` (an untyped object) and never accepts it in place of its own check. Mind's current draft has an optional `precondition_id` that can name a manifest precondition, and states that `expression` is never evaluated; Skill proposes to match it against manifest precondition `id` values.

## (d) Who validates what

| Validation | Mind | Skill, before every execution |
|---|---|---|
| Result well-formed against the Mind schema | produces it | repeats, rejecting unknown fields |
| Contract version compatible | states `contract_version` | checks against the range it accepts |
| `skill_id` exists, version eligible and approved | no | yes |
| Parameters satisfy the input schema | only against a runtime-supplied schema, see below | yes, always |
| Preconditions met | may state assumptions | evaluates its own |
| Context and observations still fresh at execution time | evaluated at inference time | re-evaluated at execution time |
| Result status allows use | sets it | policy below |
| Authorization to execute | never | Skill only, by a policy this note does not define |
| Uncertainty, `rationale`, `priority` | produces them | advisory only; never grant authority; `priority` orders candidates and nothing more |

**Parameter validation by Mind.** This repository's [AGENTS.md](../../AGENTS.md) says capability repositories must not depend on Skill, and Mind is one. Mind's current draft is consistent with that: Mind may validate parameters only against a schema handed to it as runtime data, within its limited validator subset, and otherwise validates nothing against Skill. Skill's input schema must therefore stay within that subset if Mind is to use it (open: nobody has checked this). Either way Skill repeats the check against its own manifest. Skill orders candidates with Mind's rule (`priority` ascending, then `proposal_id`) and treats the order as a hint, not a decision.

**Result-status policy (proposed).** Proposals from a FAILED or CANCELLED result are rejected. Proposals from a PARTIAL result are advisory, as Mind also states; they are not executed unless Skill's own policy says so explicitly. The proposed default is to reject them, because `missing[]` states information Mind lacked. A COMPLETED result is eligible, not authorized.

## (e) Rejection, preconditions, cancellation, partial execution, failure

Two separate state machines, so a rejected proposal is never confused with a failed run.

**Proposal disposition:** RECEIVED, then REJECTED or ACCEPTED. A REJECTED proposal records one reason code (proposed names, not final): `SKILL_RESULT_MALFORMED`, `SKILL_CONTRACT_INCOMPATIBLE`, `SKILL_RESULT_STATUS`, `SKILL_UNRESOLVED`, `SKILL_VERSION_UNAVAILABLE`, `SKILL_PARAMETERS_INVALID`, `SKILL_PRECONDITION_UNMET`, `SKILL_INPUT_STALE`, `SKILL_NOT_AUTHORIZED`. Rejection never executes anything and is never silently retried. Skill does not edit Mind's parameters to make them pass.

**Run lifecycle** (criterion AC-003): loaded, running, completed, cancelled, failed. A run starts only from an ACCEPTED proposal.

**Separate from Motion (proposed).** Skill's run lifecycle and Motion's public command states (ACCEPTED, RUNNING, COMPLETED, CANCELLED, FAILED, as Mind's `COMPATIBILITY.md` lists them) are separate state machines until a mapping is designed. Motion's ACCEPTED means admission of a command, not the start of a run, and must not be equated with Skill's `loaded`; no pairing of the two sets of names is proposed here. Skill reason codes (`SKILL_*`) are a separate namespace from Motion's codes, as `MIND_*` is from both. Not verified: Motion's states were not read from kritva-motion, and nothing unapproved there was read or relied on.

- **Unmet precondition:** checked before `running`; the run does not start and the report gives a defined error naming the precondition `id` (AC-002).
- **Cancellation:** two different things. Cancelling a Mind request (`MIND_CANCELLED`) leads to rejection of its proposals, as above. Cancelling a Skill run is cooperative: the run ends `cancelled` and the report states how far it got. Who may cancel is not decided here.
- **Partial execution:** the report lists steps or effects that did happen and those that did not. Whether effects can be undone is a per-skill manifest declaration (for example `reversible`, `idempotent`) that does not yet exist; until it does, Skill must not claim rollback.
- **Failure:** state `failed` with a defined error (code, severity, message, detail), plus the partial-execution record above. Resource use is reported in defined fields (AC-004).

## (f) What Skill returns for traceability

An execution report, one per proposal considered (including rejected ones), proposed fields:

| Field | Purpose |
|---|---|
| `report_id`, `skill_contract_version` | identity and version of this report |
| `mind_result_id`, `mind_request_id`, `mind_context_ref`, `mind_contract_version`, `proposal_id` | link back to the proposal |
| `mind_result_digest` | digest of the result as received (`sha256:<hex>`, the Mind format) |
| `resolved_skill_id`, `resolved_version`, `manifest_digest` | which manifest actually ran |
| `parameters_digest` | digest of the parameters as validated |
| `disposition`, `reason_code` | accepted or rejected, and why |
| `precondition_results[]` | each manifest precondition `id` and outcome |
| `lifecycle_state`, `started_at`, `ended_at`, `duration_ms` | run facts, RFC 3339 and milliseconds |
| `resource_use`, `errors[]` | defined reporting fields |
| `output_ref` | reference and digest of the output |

Only facts are returned. The report never states that execution was "safe" or "validated".

## (g) Confirmation

Proposed, and consistent with Mind's schema: **Mind proposes; Skill independently resolves, validates and authorizes.** A Mind result confers no execution authority, and Skill does not trust `uncertainty`, `rationale`, `priority`, preconditions or any Mind-side validation as authorization. This is Skill's position as proposed by this note; it is not an approved decision.

## Still open on the Mind side (not edited from here)

Items 1 to 6 of the first version of this note were adopted in Mind's draft (see the table in (b)). What remains:

1. Whether Skill's input schemas and Mind's limited validator subset are compatible, if Mind is ever to validate against a Skill schema.
2. Mind's `COMPATIBILITY.md` Skill section still describes this note's earlier wording (gaps and two names for one rejection code); this version supersedes it.
3. Nothing in the Mind draft names Skill's `SKILL_*` reason codes or Skill's report; that is Skill-side design and is not a Mind change.

## Not decided, needs the owner

Approval state and registry of skill versions; the authorization policy; the precondition `check` vocabulary; who may cancel a run; whether PARTIAL results may ever be executed; the mapping between Skill's run lifecycle and Motion's public command states (not designed, Motion not read).
