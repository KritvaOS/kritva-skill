# ADR-001: Role-Based Authorization

**Task:** KOS-SKILL-001  
**Status:** PROPOSED — REPOSITORY-ADOPTED; NORMATIVE CONTRACT APPROVAL PENDING UPSTREAM REVIEW
**Decision:** A — Role-based authorization  
**Decision date:** 2026-11-27

## Context
Mind proposes Skills for execution but does not authorize them. Skill must independently decide whether an authenticated principal may invoke a Skill and its declared capabilities. Authorization is distinct from manifest validation, release approval, precondition checks, Motion admission and robot safety enforcement.

## Decision
Use role-based access control (RBAC) with default-deny semantics. A trusted platform security boundary supplies the authenticated principal and role assignments. Skill enforces the role-to-permission mapping for the requested Skill, capability and applicable scope.

Initial permission concepts include:
- skill.execute — permission to initiate an eligible Skill execution.
- skill.cancel — permission to request cancellation of an execution.
- Capability-specific permissions where the governed capability definition requires them.

Permissions are scoped to the applicable robot, deployment or execution context. Exact identifiers and scope grammar are normative contract work, not assumed by this ADR.

## Required authorization sequence
1. Obtain a verifiable principal and trusted role assignments.
2. Resolve an approved Skill release.
3. Determine required Skill/capability permissions.
4. Check assigned roles against required permissions and scope.
5. Deny by default if identity, role, mapping or scope cannot be verified.
6. Proceed to independent parameter, precondition and safety checks only after authorization succeeds.

Mind-provided identity, role or permission claims are untrusted and never grant authority. Proposal priority, rationale, uncertainty and status do not alter authorization.

## Security invariants
- Missing or unverifiable authorization means no execution.
- Least privilege: roles grant only explicitly mapped permissions.
- Skills cannot grant themselves additional permissions.
- Authorization does not replace platform/robot safety or Motion checks.
- Reports retain authorization outcome and non-secret role/permission references.
- Emergency stop is independent of ordinary Skill RBAC and is not a Skill API operation.

## Consequences
A general-purpose policy engine is not required for the initial Skill contract. The platform must provide a trusted identity/role interface. Implementing an enterprise identity-management system is outside KOS-SKILL-001.

## Dependencies and open contract work
The Core/platform identity assertion and role-assignment interface is not pinned. Define principal, role, permission, scope and failure semantics only against an approved upstream trust contract. Until then ADR-001 is architecture direction, not an executable security boundary.
