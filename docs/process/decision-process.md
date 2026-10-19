# Decision process

## Current position

**Research is open. The Research Gate has not been performed.** The repository organisation, requirements register, research notes and validation plan are preparatory work. They do not demonstrate protocol correctness, establish technical novelty, or authorise a VLP implementation.

The required sequence is:

**Research → Research Gate → VLP-0001 / VLP-0002 / VLP-0003 → Specification Review → Implementation Approval**

No stage may be skipped by describing implementation work as documentation, research, a prototype, a compatibility layer, or a benchmark helper. New implementation work requires the applicable explicit approval.

## Stages and admission rules

| Stage | Required work and evidence | Result of the stage | What it does not authorise |
| --- | --- | --- | --- |
| **Research** | Preserve all 220 requirements; define use cases and exclusions; examine primary sources and existing implementations; compare architecture and cryptographic candidates; develop a threat model; identify constraints, prior art and unknowns; design validation | An evidence package and unresolved-question register suitable for a Research Gate | Selecting technology by assumption, publishing formal packet or handshake specifications, or starting VLP runtime code |
| **Research Gate** | Review evidence, alternatives, feasibility, tradeoffs, requirement conflicts, security assumptions and the proposed specification scope | A recorded evidence-based admission decision, with conditions and responsible owners where applicable | An assertion that unbuilt code is secure, fast or interoperable; approval to implement |
| **VLP-0001 / VLP-0002 / VLP-0003** | After admission, prepare the architecture, packet wire format and handshake specifications as a consistent set; map requirements and deferred items; expose unresolved issues | A reviewable specification set with traceable decisions and references | Treating an unreviewed draft as a stable protocol or beginning implementation without its separate approval |
| **Specification Review** | Check state-machine and cross-document consistency, threat coverage, cryptographic composition, negotiation, parsing, resource limits, compatibility and testability; assess every requirement disposition | An evidence-based review decision and any required corrections | Substituting for implementation validation or public deployment approval |
| **Implementation Approval** | Present the concrete specification set, review record, residual risks, implementation scope, repository boundaries, dependency and licence decisions, and verification plan to the user | An explicit recorded approval for a bounded implementation scope, or a request for further work | Unbounded changes, production deployment, infrastructure purchases, or weakening accepted security requirements |

Repository and documentation publication can be authorised separately from implementation. Publishing research materials does not move the technical process past its current stage.

## Meaning of gate outcomes

The labels **PASS / CONDITIONAL PASS / FAIL** are reserved for a performed gate or review supported by evidence. Requirements and planned checks use lifecycle descriptions such as `research-open`, `planned`, or `not executed`; they must not receive a success label because text was written.

| Outcome | Meaning | Required handling |
| --- | --- | --- |
| **PASS** | The evidence meets the stated admission criteria for the next stage within its recorded scope | Record the evidence and scope. Proceed only to that next stage |
| **CONDITIONAL PASS** | A bounded next stage is justified, but explicit, limited conditions remain | State each condition, owner, closure evidence, permitted work and blocking point. Missing fundamental security or delivery semantics cannot be hidden in an unrestricted conditional approval |
| **FAIL** | The evidence does not justify admission, or a material requirement or safety constraint is contradicted | Record why, identify possible corrective research and return to the preceding stage. Do not proceed under a renamed task |

An unperformed gate has **no outcome**. It is neither a PASS nor a FAIL. Administrative completeness is not technical evidence, and an automated check cannot manufacture the user's implementation approval.

## Requirement traceability

The [requirements register](../requirements/README.md) preserves the user's 220 original items as `VLP-REQ-001` through `VLP-REQ-220`. The [machine-readable register](../requirements/requirements.json) and supporting documents should remain consistent.

For every requirement, the research record needs an accountable core, relevant dependencies, open questions and proposed evidence. A later specification record adds its specification location and eventual conformance criteria. The original text remains available when clarification is necessary.

The source categories are not the module architecture. The [seven engineering cores](../architecture/engineering-cores.md) own the technical work; privacy, control, connection management, performance, evolution, reliability and validation cut across those boundaries.

P0/P1 classification only sequences work. A deferred item retains its identifier, rationale, dependencies, residual consequences and a condition for reconsideration. Conflicting or infeasible requirements need an explicit disposition for review; they must not disappear through rewording, deletion or an implicit “out of scope” label.

## Research Gate evidence package

The package should contain:

1. **Problem and scope:** intended endpoints, deployment environments, useful traffic, trust boundaries, non-goals and success criteria.
2. **Requirements coverage:** all 220 identifiers with ownership, current questions, conflicts and proposed sequencing.
3. **Prior art:** exact sources, relevant versions or commits, known semantics and limitations, and the concrete distinction being investigated for VLP.
4. **Architecture alternatives:** the native-UDP and existing-transport options, their responsibilities, constraints, interoperability implications and costs.
5. **Security analysis:** threat model, identity assumptions, authorisation boundaries, cryptographic candidates, replay and downgrade analysis, denial-of-service exposure and residual risks.
6. **Data and path analysis:** delivery promises, queue and memory limits, migration, congestion, MTU, fragmentation and forwarding questions.
7. **Validation design:** planned comparisons, controlled variables, measurements, evidence formats, and criteria agreed before results are observed.
8. **Decision proposal:** what is supported, what remains uncertain, why specification work is justified, and what could falsify the proposal.

The [source register](../research/source-register.md) should identify evidence provenance. The [validation plan](../research/validation-plan.md) distinguishes planned work from completed observations.

Research can assess existing published specifications, source code and measurements without building VLP. If a decisive uncertainty requires a new experiment, propose its bounded scope and obtain any applicable approval; do not assume the experiment is authorised by the existence of this process document. Claims that require an implementation must remain unproven until appropriate work is authorised and executed.

## Decision record content

A performed gate or material architecture decision should record:

- The decision identifier, date, scope, participants and responsible owner.
- The reviewed document revisions and exact source or evidence references.
- The criteria used and evidence against each criterion.
- Alternatives, tradeoffs, unresolved questions and dissenting findings.
- The outcome, conditions, allowed next work and explicit exclusions.
- The evidence needed to close conditions and who can accept closure.
- Revisit triggers, such as a changed requirement, failed assumption or newly identified vulnerability.

Unverified claims should be labelled as hypotheses, estimates or proposals. Record measured results with their method and limitations. Do not use “tested,” “verified,” “audited,” “production-ready,” or equivalent claims without the corresponding evidence.

## Implementation boundary

Until Implementation Approval, repository work is limited to the authorised research and documentation scope. The following do not arise automatically from repository creation or public availability: runtime source code, transport or cryptographic prototypes, executable test suites, fuzz harnesses, CI workflows, deployment configuration or production changes.

The future approval request must be concrete enough to review: the exact repository, included components, selected specifications, dependencies and licences, security obligations, test plan, and known limitations. Any rollout or deployment proposal also needs its operational scope, recovery plan and applicable authorisation. Approval for one bounded implementation does not waive later verification or operational decisions.

## Reopening decisions

A later contradiction is handled by updating the evidence and reopening the affected decision. The original decision and rationale remain traceable. A previously performed gate does not remain sufficient when its critical assumptions or approved scope materially change.
