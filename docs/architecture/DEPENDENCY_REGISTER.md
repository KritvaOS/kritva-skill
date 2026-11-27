# KOS-SKILL-001 Upstream Dependency Register

**Task:** KOS-SKILL-001  
**Status:** PROPOSED REGISTER — REPOSITORY ADOPTION PENDING  
**Prepared:** 2026-11-27

## 1. Purpose
This register distinguishes architecture dependencies from approved, usable contracts. A repository name, draft document, branch head or unreviewed tag is not sufficient evidence of a normative dependency. Exact versions and immutable references are recorded only after the upstream owner has approved and released the relevant contract.

## 2. Dependency inventory

| Dependency | Required interface | Evidence currently recorded in Skill | Status | Closure condition |
|---|---|---|---|---|
| kritva-core | Trusted principal identity, role assignments, security context propagation, robot/deployment scope | No Core contract version or immutable reference is pinned in Skill acceptance criteria | UNDEFINED | Core security contract reviewed, approved and released; Skill records exact version and compatibility range |
| kritva-mind | Result envelope, proposal schema, result status, provenance/digests, version constraints and proposal IDs | `kritva-mind` commit `7569b80`, contract `0.1.0-draft` | DRAFT | Mind contract approved/released; joint compatibility review; Skill records exact release and accepted range |
| kritva-motion | Command submission, identity assertion, command lifecycle, query, cancellation, idempotency, safe active-command handling and error codes | `kritva-motion` commit `d286114` (draft source reference) | DRAFT | Motion contract reviewed, approved and released; verify exact schemas/semantics; record version and adapter compatibility |
| Public platform integration boundary | Public API for registry/platform integration; no private implementation dependency | Existing README describes a planned peer dependency but no contract is established | UNDEFINED | Approved public interface contract exists; Skill consumes only that contract |
| Skill release approval registry | Exact release approval state and provenance | ADR-002 establishes architecture direction; no registry service or schema exists | UNDEFINED | Registry record/query contract, authority, trust, availability and revocation semantics specified |
| Capability vocabulary | Versioned capability IDs, semantics and permission mapping | ADR-003 establishes governed extensible model; catalogue/governance artifact not pinned | UNDEFINED | Initial approved vocabulary and change process published |
| Preconditions vocabulary/runtime | Machine-evaluable checks, state source, freshness and result semantics | ADR-004 establishes hybrid model; vocabulary/runtime interface not defined | ARCHITECTURE DECIDED / CONTRACT NOT DEFINED | Versioned vocabulary, freshness rules and trusted state interface approved |

## 3. Integration rules
1. Depend on released contracts, not upstream implementation internals.
2. Pin immutable version/tag and commit identity for every normative upstream dependency.
3. Record the exact compatibility range Skill accepts.
4. Do not silently consume breaking upstream changes.
5. Where an upstream contract is not approved, keep the dependent Skill contract explicitly draft and prevent claims of executable integration.
6. Public kritva-skill artifacts may depend only on approved public contracts. Do not depend on private Control Plane implementation details.
7. Keep repository ownership and programme status in their respective governance repositories.

## 4. Dependency closure evidence
For each dependency, record upstream repository and contract path; contract version and immutable release/tag; source commit SHA; approval/review evidence; compatibility decision and supported range; relevant Skill tests and CI evidence after implementation.

## 5. Runtime authority availability and freshness (OPEN)

Per-dispatch registry eligibility and principal identity/role checks are part of the proposed RUNNING behavior. Consequently, the registry and identity services are runtime availability dependencies, not merely onboarding-time dependencies. The following policy is UNDEFINED and must be resolved against approved upstream contracts before implementation is treated as normative:

- Maximum age/freshness of cached registry and identity assertions.
- Whether revocation notifications supplement or replace synchronous checks.
- Per-check timeout budget and behavior when a check times out.
- Safe behavior for an already-active Motion command when a registry/identity check fails or a service becomes unavailable.
- Recovery/revalidation conditions before dispatch can resume (if resumption is permitted at all).

Fail closed for new command dispatch when authority cannot be verified. Do not infer that abruptly terminating an active physical command is safe; follow the approved Motion/platform safety contract and record the outcome.

## 6. Current architecture blockers
- Identity/RBAC: Core/platform trust interface is not pinned. ADR-001 is an architecture decision, not a deployable identity contract.
- Mind proposal intake: Mind draft must be approved and jointly checked against Skill's strict COMPLETED-only initial eligibility policy; alignment with ADR-005 is not yet established.
- Motion adapter: Motion draft must be approved; sequential orchestration must be mapped to actual command/query/cancel semantics.
- Platform registry access: public registry interface and ownership are not defined.
- Capability and precondition governance: both vocabularies require normative definitions before manifests can be validated for execution.

## 7. Review rule
Updating a dependency to APPROVED requires evidence and an immutable reference; an owner discussion or draft synchronization alone is insufficient.
