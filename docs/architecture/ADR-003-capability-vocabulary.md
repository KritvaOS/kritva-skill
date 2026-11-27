# ADR-003: Governed Extensible Capability Vocabulary

**Task:** KOS-SKILL-001  
**Status:** PROPOSED — AGREED IN ARCHITECTURE DISCUSSION; PENDING REPOSITORY ADOPTION THROUGH PR REVIEW
**Decision:** B — Governed extensible vocabulary  
**Decision date:** 2026-11-27

## Context
Skill manifests need consistent capability identifiers and semantics so compatibility, authorization and audit can be handled consistently. Free-form declarations make permissions and behavior difficult to compare; a permanently closed list impedes domain evolution.

## Decision
Use a versioned, governed, extensible capability vocabulary. Each capability definition must include:
- globally unique namespaced identifier;
- normative description and semantics;
- definition version and compatibility/change policy;
- input/output expectations where applicable;
- required authorization permission(s);
- applicable execution and safety constraints;
- owning domain and governance status.

Illustrative identifiers only (not approved catalogue entries): robot.motion.joint_position, robot.motion.joint_velocity, robot.sensing.observe, robot.manipulation.grasp.

## Governance rules
1. A manifest may declare only capabilities in the approved vocabulary.
2. Unknown, deprecated or unapproved capability definitions are not executable.
3. Changes preserve compatibility or introduce a new version under the vocabulary versioning policy.
4. A capability declaration does not grant caller permission; ADR-001 RBAC remains authoritative.
5. Capability semantics cannot bypass Core identity, independent safety enforcement, preconditions or Motion admission.
6. Domain repositories consume governed definitions; they do not silently redefine shared semantics.

## Consequences and open work
New capabilities can be added without changing the overall manifest shape. A normative vocabulary artifact, initial approved catalogue, owner/governance process and permission mapping format remain to be defined. The illustrative identifiers above must not be treated as approved capabilities.
