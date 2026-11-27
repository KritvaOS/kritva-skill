# ADR-008: Append-Only Execution Events and Consolidated Report

**Task:** KOS-SKILL-001  
**Status:** PROPOSED — AGREED IN ARCHITECTURE DISCUSSION; PENDING REPOSITORY ADOPTION THROUGH PR REVIEW
**Decision:** C — Append-only event history plus consolidated final report  
**Decision date:** 2026-11-27

## Context
A final status alone is insufficient to diagnose interrupted or partially executed operations. Skill needs traceable provenance across Mind, authorization, preconditions, Motion commands, lifecycle transitions and known physical effects.

## Decision
Maintain two complementary artifacts:
1. Append-only execution event history — records lifecycle transitions and significant execution events.
2. Consolidated execution report — structured summary derived from the available event history and evidence.

## Event requirements
Each event includes stable unique event_id, execution_id, monotonically increasing execution-local sequence number, timestamp, event type and relevant source/evidence references.

Events cover execution creation/loading; start-time authorization and release-eligibility re-checks; pre-start denial; precondition outcomes; start; per-dispatch identity/registry checks; registry SUSPENDED/REVOKED observations; role/permission revocation; Motion dispatch/admission/outcomes; cancellation request/acknowledgement; safety-stop observation or initiation; active-command safe handling; faults; recovery; and terminal state. A failed start-time re-check is recorded as a LOADED-to-FAILED transition with a reason code and termination_status=NOT_REQUESTED. Append-only means prior events are not silently overwritten; corrections are represented by additional attributable events.

## Consolidated report
The report includes Skill identity/version and digests; Mind result/proposal provenance; start-time and per-dispatch authorization outcomes; release eligibility; registry/role revocation events; precondition results; lifecycle and duration; Motion command outcomes; completed, failed, unresolved and undispatched steps; errors and recovery information; resource usage with measurement provenance; and output/evidence references. Every terminal report includes mandatory termination_status (CONFIRMED, UNRESOLVED or NOT_REQUESTED). For a safety stop, the report records whether Skill initiated the stop or observed a platform/independent safety-system stop.

## Required event categories

The event type vocabulary includes at least `EXECUTION_LOADED`, `AUTHORIZATION_CHECKED`, `RELEASE_ELIGIBILITY_CHECKED`, `START_BLOCKED`, `LIFECYCLE_TRANSITION`, `MOTION_DISPATCH_REQUESTED`, `MOTION_OUTCOME_OBSERVED`, `REGISTRY_STATE_CHANGED`, `PRINCIPAL_PERMISSION_REVOKED`, `DISPATCH_BLOCKED`, `CANCELLATION_REQUESTED`, `CANCELLATION_OUTCOME_OBSERVED`, `SAFETY_STOP_OBSERVED`, `SAFETY_STOP_INITIATED`, `ACTIVE_COMMAND_SAFE_HANDLING_SELECTED`, `ACTIVE_COMMAND_TERMINAL_OUTCOME`, `FAULT_RECORDED` and `EXECUTION_TERMINAL`. The event schema may refine names, but it must preserve these distinctions and identify the stop initiator as SKILL or PLATFORM_SAFETY.

## Resource accounting
The report supports measured usage, estimated usage, declared limits and unavailable/unmeasured values. Detailed resource measurement, collection and accounting infrastructure are deferred. The contract must not present an estimate as a measurement.

## Security and integrity
Events and reports must not contain credentials, secrets or unnecessary sensitive data. Missing event history is not evidence of success. Unresolved outcomes remain explicit. Event ordering, durability, integrity protection, retention and access-control guarantees must be specified in the normative reporting contract.

## Consequences and open work
The event history supports audit and diagnosis while the final report supports consumers and operators. Event storage implementation and detailed resource metering are outside this ADR; event schema, persistence semantics, integrity and retention policy remain contract-design work.
