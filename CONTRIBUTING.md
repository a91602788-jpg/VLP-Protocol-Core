# Contributing to VLP Protocol Core

Contributions currently focus on research, requirements, evidence, and preparation for specification review. The protocol architecture, wire format, and handshake are not established merely by creating this repository.

Start with the [decision process](docs/process/decision-process.md), [requirements](docs/requirements/README.md), [governance](GOVERNANCE.md), and [source register](docs/research/source-register.md).

## Research before specification and implementation

The project follows this order:

1. Research the problem, existing work, alternatives, threat assumptions, and measurable requirements.
2. Record a Research Gate decision with its evidence, scope, and unresolved conditions.
3. Prepare the architecture, packet wire format, and handshake specifications within the scope authorized by that decision.
4. Review the specifications together for consistency and security implications.
5. Obtain a separate, recorded implementation approval before implementing the protocol.

The [decision process](docs/process/decision-process.md) defines how these gates operate. Opening or merging a documentation pull request does not by itself pass a gate, establish a protocol version, or authorize implementation. Do not introduce protocol code, cryptographic code, production configuration, deployment automation, or a release through a research or documentation pull request.

An experiment that requires new executable code should first identify its scope and obtain the applicable authorization under the decision process. A proposed experiment is not a completed benchmark.

## Useful contributions at this stage

- A concrete use case, requirement, or failure scenario.
- A primary-source comparison that distinguishes a protocol from an application, transport, security layer, or carrier.
- A falsifiable hypothesis about functionality, performance, or observable traffic behavior.
- A threat model, counterexample, state-machine ambiguity, or composition concern.
- A reproducible experiment plan with baselines, metrics, resource limits, and evaluation criteria.
- A correction to evidence, terminology, citations, or document consistency.

Use the research proposal issue template for a new question. Use the specification review template only for a specification revision that has reached that stage through the decision process. Follow [SECURITY.md](SECURITY.md) for findings that need private reporting.

## Evidence and claims

Separate facts supported by a cited source, observations from an actual experiment, design proposals, assumptions, and open questions. Link to primary sources and identify the exact section and document revision, release, or commit where available. Add relevant sources to the [source register](docs/research/source-register.md), including limitations and the date reviewed.

When reporting an experiment, provide the commands or procedure actually used, the exact input and environment, the compared revisions and configuration, the measurements, and the limits of the result. Share only sanitized data that you are authorized to publish.

Do not claim that a test ran, an audit occurred, a gate passed, or an implementation achieved a property without corresponding evidence. Cryptographic primitive selection does not prove the security of a composed protocol. A traffic classifier result does not establish universal invisibility or resistance to every network policy.

Reserve `PASS`, `CONDITIONAL PASS`, or `FAIL` for a performed Research Gate or Specification Review with a stated revision, scope, evidence, and permitted next step. Describe ordinary documentation checks by what was checked and what was found. An unevaluated criterion stays unevaluated; it is not a conditional success. An external review recommendation is distinct from the maintainer's recorded gate decision.

## Scope and security review

Keep each contribution focused on a single research question or a related set of documentation changes. Explain effects on the affected engineering cores: Protocol Core, Transport, Cryptography, Handshake, Camouflage, Data Plane, and Security. Address authentication, authorization, key and nonce lifecycle, replay, downgrade, resource exhaustion, metadata, and failure behavior where the proposal touches them.

Identify competing requirements rather than hiding tradeoffs. For example, padding and scheduling proposals should account for additional traffic, delay, congestion control, MTU, memory, and power consumption. Changes to a carrier or recovery path need an explicit account of session state and security assumptions.

## Pull requests

1. Work on a separate branch and limit changes to the stated scope.
2. Link the research issue, requirement, or gate record that motivates the change.
3. Describe the problem, the proposed change, alternatives considered, and unresolved questions.
4. Review the diff for unrelated changes, secrets, inaccurate claims, broken local references, and third-party material.
5. Report the checks actually performed. For documentation-only work, a focused content and link review is sufficient unless a concrete concern requires more; do not invent a test suite or report unrun tests as passing.
6. Submit the pull request for maintainer review. Use a draft pull request when evidence, authorization, or licensing decisions are still unresolved.

Do not assume a reviewer request authorizes work outside the contribution's scope. Record material changes to the hypothesis or assumptions so that reviewers can follow the decision.

## Licensing and attribution

This foundation change includes Apache License 2.0 for original project material, with the license choice presented for maintainer review in the pull request. Read [LICENSE](LICENSE) for the license terms and [Licensing](docs/LICENSING.md) for the scope and third-party review requirements; this contribution guide does not replace the license text.

Identify the origin and terms of any third-party text, code, diagram, dataset, or other material you propose to include. A source being publicly accessible is not evidence that its contents can be copied or relicensed. Prefer original explanations with citations and preserve required attribution.

No contributor license agreement or Developer Certificate of Origin requirement is introduced by this foundation. Such a requirement would need a separate, explicit owner decision. If license terms for a contribution are unresolved, surface that question before it is merged.

## Review conduct

Discuss technical claims and evidence respectfully. Make objections concrete, distinguish a missing argument from an established defect, and allow a proposal to be rejected when its costs or assumptions do not satisfy the requirements. Automated or AI-assisted material is subject to the same evidence and review expectations as any other contribution.
