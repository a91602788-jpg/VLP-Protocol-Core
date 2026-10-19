# Validation plan

## Status and boundary

**This is a plan. No VLP runtime, protocol test suite, benchmark, interoperability run or security audit has been executed by creating this document.** The Research Gate has not been performed. Planned checks have no PASS, CONDITIONAL PASS or FAIL outcome.

The plan covers all [220 requirements](../requirements/README.md), not only the source category named Validation. Evidence should map to stable identifiers in [requirements.json](../requirements/requirements.json) and accountable owners among the [seven engineering cores](../architecture/engineering-cores.md).

The [decision process](../process/decision-process.md) governs when work can begin. Existing-source research, future specification review and future implementation validation are separate activities. This page does not authorise new runtime code, tests, fuzz harnesses, workflows, public probing or deployments.

## Evidence classes

| Evidence class | Useful for | Required qualification |
| --- | --- | --- |
| Primary specification or published source inspection | Establishing existing semantics, prior art, constraints, known mechanisms and candidate dependencies | Record the source, relevant section and version or commit; distinguish the specification from a particular implementation |
| Analytical model or calculation | State consistency, size budgets, complexity bounds and explicit assumptions | State inputs, assumptions, derivation and what has not been measured |
| Existing-system observation | Comparing established implementations under controlled conditions | Record actual execution and configuration; public benchmark claims do not become our measurements |
| Specification review | Assessing the admitted VLP design before implementation | Trace findings to the exact document revisions and requirement identifiers |
| Implementation validation | Conformance, performance, fault handling, fuzzing and interoperability | Requires prior implementation approval, an actual implementation and reproducible execution evidence |
| Independent security review | Assessing cryptographic composition and the implemented attack surface | Record the reviewer, scope, method, revisions, findings and limitations; an informal review is not an audit |

The [source register](source-register.md) stores provenance for external material. No candidate should be selected on an unattributed benchmark or a project marketing claim.

## Research questions and comparison design

| Question | Comparison or analysis to prepare | Decision relevance | State |
| --- | --- | --- | --- |
| Is a new transport justified? | Compare required semantics and observables against native UDP and existing QUIC capabilities | Identify the benefit that cannot be obtained acceptably with an existing transport | Planned |
| What is actually distinctive? | Map each proposed distinguishing property against VLESS, AmneziaWG, Hysteria 2 and relevant standards, using exact versions | Separate original hypotheses, known mechanisms and implementation policy choices | Planned |
| Are delivery promises coherent? | Analyse stream, datagram, deadline and IP-tunnel semantics, including overload and cancellation | Avoid contradictory promises or accidental global ordering | Planned |
| Is the security construction reviewable? | Compare established constructions, identity assumptions, key lifetimes and composition boundaries | Exclude undocumented or unsupported cryptographic assumptions | Planned |
| Can camouflage improve the stated objective? | Define adversaries and observations, then compare candidate profiles and their costs | Replace claims of invisibility with bounded, measurable hypotheses | Planned |
| Can the design operate within resource limits? | Model parser work, queues, handshake state, acknowledgement history and fragment reassembly | Establish bounded behaviour under valid and hostile inputs | Planned |
| Does IP carriage work across the target paths? | Calculate complete packet budgets and research PMTU, fragmentation and ICMP behaviour | Identify unsupported paths and avoid false IPv6 or MTU claims | Planned |
| Can the protocol evolve safely? | Review authenticated negotiation, unknown options, mixed versions and extension handling | Prevent accidental downgrades and incompatible interpretations | Planned |

Baselines are comparison subjects, not automatically selected dependencies or code to copy. Their licence, provenance, security state and technical suitability require separate evidence. If a decisive comparison needs an experiment, first define the bounded study and obtain the applicable approval.

## Planned environment matrix

The eventual experiment design should cover the combinations that can change a decision, rather than exhaustively multiplying every configuration. Values and acceptance thresholds must be agreed before execution; no performance target is invented here.

| Dimension | Cases to consider | Risk addressed |
| --- | --- | --- |
| Traffic | Interactive streams; bulk streams; small datagrams; mixed workloads; IP tunnelling where selected | Head-of-line effects, starvation, queue delay, payload semantics |
| Capacity | Low and high bandwidth; asymmetric uplink/downlink; competition with ordinary TCP and QUIC traffic | Congestion behaviour and fairness |
| Delay and loss | Different RTTs; variable delay; isolated and burst loss; duplication; reordering | Recovery, useful datagram delivery and unstable control loops |
| Path changes | NAT rebinding; changed client address; path failure; temporary outage; stale path information | Authenticated migration and bounded recovery |
| Reachability | UDP unavailable; dropped handshake traffic; partial connectivity; unavailable peer | Explicit failure and any separately approved fallback semantics |
| Packet size | IPv4 and IPv6; small path MTU; blocked ICMP; changed overhead; oversized payloads | Fragmentation, black holes and tunnel correctness |
| Endpoints | Slow receiver; CPU saturation; constrained memory; many small channels; idle sessions | Backpressure, scheduling and resource exhaustion |
| Appearance profiles | Baseline and candidate padding/timing policies under identical useful traffic | Cost, fingerprint changes and interaction with transport control |

Public networks and third-party endpoints are not targets for unrestricted adversarial experiments. Use a separately authorised controlled environment with owned endpoints and synthetic data.

## Measurements to predefine

- **Connection establishment:** completion rate and latency to an authenticated, authorised usable channel; retries and failed attempts reported separately.
- **Useful throughput:** application goodput, direction and workload; total wire traffic including handshake, retransmissions, padding and any other added data reported alongside it.
- **Latency:** suitable percentiles, sample counts and distributions for RTT, queue residence and useful application delivery; avoid presenting only averages.
- **Deadline behaviour:** local expirations, received useful messages and missing or late messages under a precisely defined policy. A local queue limit is not an end-to-end latency guarantee.
- **Resources:** CPU cost, peak and steady memory, allocation behaviour, per-connection and per-channel state, idle bandwidth and timer activity.
- **Fairness and overload:** competing-flow impact, starvation, receiver saturation, admitted work, dropped work and recovery after pressure ends.
- **Path handling:** interruption and recovery intervals, data integrity, repeated or lost operations, path-validation failures and MTU discovery outcomes.
- **Appearance costs and limitations:** overhead, latency effects, distinguishability under the stated method, false positives and false negatives where a classifier is used.

Use monotonic time for local durations. One-way latency needs a documented clock-synchronisation method and error budget; otherwise report measurements that do not depend on synchronised clocks. Separate transport acknowledgement from application completion.

## Specification review coverage

After the Research Gate admits formal specification work, review VLP-0001, VLP-0002 and VLP-0003 together. At minimum, the review should examine:

1. **State consistency:** every allowed transition, timeout, cancellation, retry and terminal condition; no operation whose interpretation differs across documents.
2. **Encoding and parsing:** complete size bounds, truncation, length arithmetic, unknown values, duplicate fields, extension handling, authentication boundaries and resource allocation order.
3. **Identity and permission:** what authenticates whom, how possession is demonstrated, when permissions are checked, and how a channel or route is bound to its owner.
4. **Key lifecycle:** derivation domains, direction separation, nonce uniqueness, restart behaviour, key updates, expiry, revocation and destruction assumptions.
5. **Replay and downgrade:** duplicated and reordered handshake/control messages, stale negotiation, resumption and any proposed early data.
6. **Delivery and resources:** reliable versus unreliable semantics, congestion accounting, flow control, bounded queues, fragmentation, acknowledgement history and fairness.
7. **Paths and forwarding:** spoofed migration requests, unauthorised destinations or source addresses, route changes, ICMP handling, MTU and failure behaviour.
8. **Privacy and evolution:** observable identifiers, correlation across paths, diagnostic disclosure, data retention, extension compatibility and mixed-version behaviour.

This review produces findings and gate evidence. It cannot establish that future code conforms to the reviewed design.

## Future implementation validation

The following activities are planned only for a later, explicitly approved implementation. No executable suite is created or asserted to exist here.

| Area | Evidence to require later | Principal failure cases |
| --- | --- | --- |
| Conformance | Vectors derived from the reviewed specification, with independently checked expected results | Ambiguous encodings, invalid states, implementation-specific wire behaviour |
| Cryptographic use | Reviewed construction usage, suitable external vectors, key-lifecycle and negative-case checks | Nonce reuse, wrong key domain, unauthenticated negotiation, unsafe restart |
| Parsers and state machines | Coverage-guided and structured fuzzing appropriate to actual parsers | Out-of-bounds access, unbounded allocation, hangs, length overflow, inconsistent transitions |
| Authentication and authorisation | Adversarial scenarios with distinct identities and permissions | Pre-authentication forwarding, channel ownership confusion, unauthorised routes or priority |
| Reliability and replay | Loss, reordering, duplication and interruption with an explicit expected outcome | Duplicate external operations, delivery gaps, stale identifier reuse, indefinite half-open state |
| Denial of service | Controlled load and malformed-input observations with bounded resource expectations | Amplification, expensive pre-authentication work, queue/reassembly exhaustion, timer storms |
| Paths and MTU | Controlled rebinding, address changes, blocked paths and oversized packets | Forged migration, silent tunnel black holes, invalid IPv6 support claims |
| Interoperability | Independently implemented or independently checked peers against the same reviewed specification | Two peers sharing the same mistaken assumption; version incompatibility |
| Performance | Reproducible comparisons with established baselines and complete configuration disclosure | Comparing unequal workloads, hiding overhead, aggressive unfair sending, unsupported speed claims |
| Privacy and observables | Defined passive and active observations plus log/diagnostic inspection | Persistent correlation, content or credential disclosure, identifiable failure responses |

If only one implementation exists, say so. Looping it back to itself or running two builds of the same implementation does not establish independent interoperability.

## Reproducibility and evidence records

Each executed study should identify its purpose and requirement IDs; approved scope; code and document revisions; dependencies and licences; operating system, hardware and network conditions; exact configuration; workload; seeds where relevant; sample sizes; measurement method; raw evidence locations; exclusions; and limitations.

Record unexpected outcomes and failed runs as well as successful ones. Preserve enough sanitised evidence to reproduce a material result. Use synthetic payloads and test identities; keep credentials, secret keys and real user traffic out of committed logs, captures and reports.

Acceptance criteria must precede result interpretation. Changing a threshold after seeing the result needs an explicit rationale and a new comparison, not retrospective relabelling.

## Admission and unresolved findings

The Research Gate assesses whether the collected evidence supports specification work. The Specification Review assesses the resulting design. Later implementation validation assesses actual code. None substitutes for the others.

Every material finding needs its affected requirement IDs, severity rationale, evidence, owner, proposed resolution and effect on the next gate. An unresolved finding can constrain a bounded next step only when the gate record states the constraint and the evidence needed to close it. Fundamental security, delivery or feasibility contradictions must not be concealed by an unqualified success statement.

The present result is a documented plan and an open research scope. Actual measurements, review outcomes and implementation evidence remain to be collected under the [decision process](../process/decision-process.md).
