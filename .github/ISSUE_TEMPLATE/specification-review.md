---
name: Specification review
about: Review an authorized specification revision with evidence and explicit limits.
title: "Specification review: "
---

<!-- Do not disclose vulnerability details here. Use the repository security policy: https://github.com/a91602788-jpg/VLP-Protocol-Core/security/policy -->
<!-- Read CONTRIBUTING.md and docs/process/decision-process.md. If the Research Gate has not authorized this specification work, use the research proposal template instead. -->

## Reviewed material and authorization

Link the exact specification revision or commit, related requirements, and the Research Gate decision authorizing this scope. Identify which documents were reviewed together.

## Reviewer and scope

State your involvement in authoring the material, the review scope, and any relevant limitations. Do not describe a self-review as independent.

## Requirement coverage and consistency

Identify satisfied, ambiguous, missing, or conflicting requirements with exact document sections. Consider consistency between architecture, packet format, handshake, and failure behavior.

## Transport and Data Plane findings

Address applicable state transitions, delivery semantics, acknowledgment and retransmission rules, congestion and flow control, MTU, fragmentation bounds, migration, session closure, and resource limits.

## Security and Camouflage findings

Address applicable authentication and authorization, negotiation binding, key and nonce lifecycle, replay and downgrade behavior, malformed input, anti-amplification, pre-authentication costs, observable metadata, and the limits of camouflage claims. Keep sensitive findings out of this public issue.

## Evidence and verification

List sources with exact sections, reasoning, counterexamples, or authorized experiments that support the findings. Identify checks not performed. A proposed test is not a completed test.

## Findings and required changes

For each finding, identify the affected section, impact, evidence, and proposed resolution. Distinguish a confirmed defect from uncertainty or a request for clarification.

## Reviewer recommendation

Recommendation: `Not evaluated` / `PASS` / `CONDITIONAL PASS` / `FAIL`.

State the scope and rationale. For each condition, state what evidence would close it and who is proposed to own it; do not treat an unassigned condition as resolved. This recommendation is not the maintainer's gate decision or an implementation approval.

## Requested maintainer decision

Specify whether the request is to revise the material, continue review, record a specification decision, or return to research. Identify any separate approval still required.
