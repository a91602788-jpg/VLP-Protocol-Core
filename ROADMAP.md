# Roadmap

This roadmap describes work order, not completed milestones or a release schedule. The original 220 topics remain in the [requirements register](docs/requirements/README.md).

## Phase 1 — Research

- Clarify use cases, trust assumptions, adversaries, deployment constraints, and measurable objectives.
- Compare native UDP, an existing transport, and a narrower protocol extension.
- Assess all seven cores and cross-cutting requirements.
- Review upstream sources, licenses, integration boundaries, and maintenance evidence.
- Define reproducible validation methods and criteria before claiming results.
- Record reasons for selecting, deferring, or excluding each optional feature.
- Evaluate the [server/mobile deployment scenarios](docs/research/deployment-profiles.md), including endpoint trust, route visibility, sleep/recovery, fallback and energy. Research onion, garlic, mixnet and multipath before assigning their implementation priority.

**Exit:** a reviewable evidence package for the Research Gate. Current gate status: not evaluated.

## Phase 2 — Specification

After the Research Gate permits the transition, prepare the reserved specifications:

- VLP-0001 — Architecture.
- VLP-0002 — Packet Wire Format.
- VLP-0003 — Handshake.

Connect every normative requirement to its source topic, threat, state transition, and planned validation. Additional specification topics remain organized through the [specification index](docs/specifications/README.md); no further VLP document numbers are assigned here.

**Exit:** Specification Review with findings and explicit resolution of blocking issues.

## Phase 3 — Implementation, only after approval

The maintainer records explicit implementation authorization identifying the reviewed specification revisions and approved scope. A protocol prototype, live listener, parser implementation, transport library, crypto integration, and packet-generating experiment all count as implementation and require this transition.

Within the approved scope, build the reference implementation and meaningful validation: state-machine properties, malformed inputs, replay, downgrade, resource limits, network impairment, and interoperability. Language and dependency choices remain open until selected through the process.

**Exit:** evidence for the agreed implementation criteria; no unconditional security or production-readiness claim follows from compilation or successful unit tests.

## Phase 4 — Independent validation and release consideration

- Independent specification and cryptographic review at the defined boundaries.
- Interoperability between independent implementations of the same specification revision.
- Reproducible performance and traffic-observation measurements.
- Verified release provenance, dependency inventory, vulnerability reporting, and compatibility policy.
- Controlled rollout and recovery procedures for any eventual deployment.

There is no release date, version number, audit completion, or production deployment recorded at this stage.

## Candidate extensions

P2P, NAT traversal, multipath, FEC, additional carriers, session resumption, early data, hybrid post-quantum profiles, and partially reliable messages require individual scope decisions. A dependency between an extension and a mandatory threat requirement can make that extension a release prerequisite. Deferral must never silently weaken the declared threat model.
