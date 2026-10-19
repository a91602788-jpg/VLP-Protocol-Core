# Governance

## Current maintainer authority

The repository owner and current maintainer account is [a91602788-jpg](https://github.com/a91602788-jpg).

At this stage, that account holds maintainer review and acceptance authority for this repository. No committee, security team, foundation, legal entity, or additional maintainer is established by these documents. Contributors and external reviewers can provide evidence and recommendations; doing so does not grant merge, release, or gate-decision authority.

## How decisions are made

Technical proposals should be discussed in a focused issue or pull request, supported by requirements, alternatives, evidence, and unresolved questions. The maintainer records the accepted outcome and rationale, including the scope of the decision and any conditions.

Research and specification work follows the [decision process](docs/process/decision-process.md). In particular:

- Acceptance of repository documentation does not establish an approved protocol design.
- A Research Gate decision authorizes only the next stage and scope recorded in that decision.
- Specification review and implementation approval are separate decisions.
- Implementation, deployment, release, and security claims cannot be inferred from a merged proposal.

A performed Research Gate or Specification Review should identify the reviewed revision and use `PASS`, `CONDITIONAL PASS`, or `FAIL` only with evidence and a clear interpretation of the permitted next step. Ordinary documentation checks report their procedure and findings without a gate outcome. Conditions need a closure criterion and an owner before they can be treated as resolved. Work that has not been evaluated should be described as unevaluated.

## Reviews and independence

Anyone may raise a technical objection or submit a review within the contribution process. Reviews should identify the examined material, assumptions, findings, and limitations.

Where the maintainer is also the author, record that fact rather than describing the review as independent. External specialist review is valuable for transport and cryptographic design, but no such review is claimed or guaranteed by this governance document. A reviewer recommendation and the maintainer's acceptance decision should remain distinguishable.

## Disagreements and new evidence

An unresolved objection should remain visible in the issue, pull request, or decision record with the reasoning for accepting, deferring, or rejecting it. A decision can be revisited when new evidence changes a requirement, assumption, risk, or feasibility assessment.

Security-sensitive details follow [SECURITY.md](SECURITY.md). Public decision records can refer to the existence and scope of a private review without disclosing material that should remain private.

## Changes to project authority or policy

Adding maintainers or changing governance requires an explicit decision by the current repository owner and an update to this file. Repository access should reflect the authority actually granted. Issue participation, review comments, employment, branding, and authorship do not confer that authority by themselves.

The Apache License 2.0 choice included in the foundation pull request, its scope, and third-party review requirements are documented in [Licensing](docs/LICENSING.md). The license terms are in [LICENSE](LICENSE). This governance document does not grant intellectual property rights or introduce a CLA or DCO requirement.

Any later release or operational process must be documented and authorized for its actual scope. This foundation does not create a release schedule, deployment service, support commitment, or automated approval mechanism.
