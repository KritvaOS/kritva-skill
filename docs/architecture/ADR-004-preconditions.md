# ADR-004: Hybrid Preconditions and Runtime Validation

**Task:** KOS-SKILL-001  
**Status:** PROPOSED — AGREED IN ARCHITECTURE DISCUSSION; PENDING REPOSITORY ADOPTION THROUGH PR REVIEW
**Decision:** D — Hybrid validation  
**Decision date:** 2026-11-27

## Context
Mind may describe assumptions made during inference, but those claims may be stale or incomplete. Skill must evaluate execution requirements against trusted runtime state. Operational safety must remain independently enforced.

## Decision
Use three coordinated layers:
1. Governed vocabulary: versioned, machine-evaluable common precondition semantics.
2. Skill runtime: validates parameters and evaluates common plus Skill-specific preconditions against trusted runtime interfaces.
3. Platform/robot safety layer: independently enforces operational safety constraints.

Motion retains its own command-admission and runtime checks. Passing Skill preconditions does not imply Motion admission or establish physical safety.

## Result contract
Each evaluated precondition returns exactly one of SATISFIED, NOT_SATISFIED or UNKNOWN. Only SATISFIED permits progression. NOT_SATISFIED and UNKNOWN prevent execution. Results include precondition ID, outcome, evaluation timestamp, relevant state/evidence reference and reason code.

## Validation rules
- Mind descriptions and expressions are advisory; Skill does not treat them as authoritative checks.
- Skill evaluates its own declared checks using trusted runtime interfaces.
- Freshness requirements are explicit and appropriate to the check.
- Missing, stale, unavailable or unverifiable state yields UNKNOWN.
- Required checks are performed before execution and re-evaluated during execution when the contract specifies.
- No Skill, Mind proposal, role or capability declaration can override safety enforcement.

## Consequences and open work
The architecture separates reusable common checks, Skill-specific domain checks and independent safety enforcement. The normative precondition vocabulary, trusted state interfaces, freshness limits, re-evaluation triggers and evidence schema remain to be defined.
