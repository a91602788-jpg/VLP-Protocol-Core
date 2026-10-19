# Research workspace

Research records distinguish a source observation, an engineering proposal, a decision, and an executed validation result. These are different kinds of evidence.

| Document | Purpose |
| --- | --- |
| [Source register](source-register.md) | Primary standards, protocol documentation, and research with boundaries of applicability |
| [OSS candidates](oss-candidates.md) | Potential reuse and comparison targets with observed provenance and license information |
| [OSS candidate data](oss-candidates.json) | Machine-readable candidate records; not a dependency lockfile |
| [Validation plan](validation-plan.md) | Proposed methods and metrics; no protocol tests have been executed |
| [Requirements](../requirements/README.md) | Stable links to all 220 source topics |
| [Decision process](../process/decision-process.md) | Gates, evidence, and authority to move between stages |

## Evidence rules

- A source describing a feature is evidence of that source's statement; it does not prove the feature's security or effectiveness in VLP.
- A repository HEAD observed during research is a snapshot, not an approved dependency pin or supported release selection.
- A requirement marked OPEN has not been resolved, even if a promising candidate exists.
- A validation plan does not constitute an experiment, benchmark, interoperability result, or audit.
- New evidence may reject native UDP or any other candidate. Record the reason and the scope consequence.

## Research proposal contents

Each proposal identifies a bounded question, relevant VLP-REQ identifiers, alternatives, primary sources, uncertainties, intended evidence, resource limits, and the decision it can inform. State whether any proposed activity needs protocol implementation. That activity remains behind the implementation gate even when called an experiment or prototype.

Read-only upstream analysis and documentation work can proceed within the authorized research scope. Active testing against third-party networks is not authorized by a research issue or by this repository.
