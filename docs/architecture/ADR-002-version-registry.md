# ADR-002: Hybrid Skill Release Identity and Execution Approval

**Task:** KOS-SKILL-001  
**Status:** PROPOSED — REPOSITORY-ADOPTED; NORMATIVE CONTRACT APPROVAL PENDING UPSTREAM REVIEW
**Decision:** C — Hybrid repository release identity plus trusted platform approval registry  
**Decision date:** 2026-11-27

## Context
A repository release identifies published software, but publication or tagging alone must not authorize execution. Skill needs immutable identity, reproducible provenance and an explicit authority for approving a release for runtime use.

## Decision
Separate release establishment from execution approval:
1. The Skill repository/package release establishes immutable source and package identity.
2. A trusted platform registry independently approves that exact release identity for execution.
3. Skill resolves only exact immutable releases whose registry state is APPROVED.

Minimum release identity: skill_id, SemVer version, manifest_digest, package_digest, immutable source_revision and release_reference. The manifest and package are immutable after publication. Any content change requires a new release identity and approval.

## Registry states
- PENDING — awaiting approval.
- APPROVED — eligible for runtime resolution.
- SUSPENDED — temporarily ineligible for new execution.
- REVOKED — approval withdrawn.

Approval provenance records approver identity, timestamp, exact release identity and reason/evidence reference. Registry approval cannot modify package contents.

## Runtime resolution
1. Mind supplies skill_id and an allowed version constraint.
2. Skill queries the trusted registry for matching releases.
3. Only APPROVED releases are candidates.
4. Skill verifies manifest and package digests.
5. Skill selects one exact version and records it.
6. If no valid approved version matches, the proposal is declined without dispatch.

No wildcard, latest, mutable tag or implicit fallback resolution is permitted. Version-constraint grammar and deterministic tie-breaking must be specified in the normative contract.

## Revocation and running executions
Suspended or revoked releases are ineligible for new executions. Behavior for already-running executions must be specified with ADR-006 cancellation and fault semantics; this ADR does not assume forced termination or safe rollback.

## Consequences and scope
Repository maintainers establish release provenance but cannot implicitly approve execution. The registry service, governance authority, API, availability and revocation protocol are not implemented by this ADR. The public Skill contract may depend only on an approved public registry/platform interface, not private Control Plane implementation details.
