---
name: Research proposal
about: Propose a requirement, research question, comparison, or experiment plan.
title: "Research: "
---

<!-- Do not put vulnerability details or secrets in a public issue. Use the repository security policy: https://github.com/a91602788-jpg/VLP-Protocol-Core/security/policy -->
<!-- Read CONTRIBUTING.md and docs/process/decision-process.md. This issue proposes work; it does not authorize protocol implementation or pass a gate. -->

## Problem and use case

Who needs the proposed behavior, under which network conditions, and what current limitation matters? Link related requirements or issues.

## Research question or falsifiable hypothesis

State what evidence would support the proposal and what evidence would cause it to be rejected.

## Existing approaches and primary sources

List relevant protocols, standards, papers, or implementations. Give exact sections and revisions, releases, or commits where available. Identify source limitations and additions needed in `docs/research/source-register.md`.

## Scope and alternatives

Identify the affected engineering cores: Protocol Core, Transport, Cryptography, Handshake, Camouflage, Data Plane, and Security. Explain alternatives, including whether an existing protocol or extension can satisfy the requirement. State what is outside the proposal.

## Assumptions and threat model

Describe trust boundaries, attacker capabilities, deployment assumptions, observable metadata, and failure conditions. Explain relevant effects on authentication, authorization, replay, downgrade, key lifecycle, and resource use.

## Proposed method and evaluation criteria

Define baselines, workloads, metrics, network conditions, resource budgets, and criteria for interpreting results. Explain how the method avoids misleading comparisons or data leakage. Mark any numeric targets as proposed until adopted through the decision process.

## Authorization and data handling

Identify whether the work requires executable code, infrastructure changes, external services, or data collection. State the required authorization and how private or third-party information will be excluded from public evidence.

## Evidence already available

Separate cited facts, observed results, assumptions, and open questions. List only experiments and checks actually performed; say explicitly if none have been run.

## Requested next step

Describe the bounded research action or decision requested. Identify any dependency on a gate record. Do not request implementation as an implicit consequence of accepting the research question.
