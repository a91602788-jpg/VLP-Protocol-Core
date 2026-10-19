# Deployment scenarios, route choices, and performance hypotheses

**Research update: 2026-10-19. All designs below are proposals. Research Gate remains NOT_EVALUATED.** No route profile, cryptographic suite, carrier, API, wire field, runtime dependency, or implementation is adopted by this document. The existing 220 requirement identifiers remain unchanged.

The owner asks for a fast, strongly protected protocol usable on mobile networks and between servers, phones, and other devices, while considering ideas from onion routing, garlic routing, mixnets, and multipath. The research direction is a portable endpoint protocol with explicit service and trust contracts, evaluated with several route and carrier choices. It should be usable by independently developed applications and deployments.

Read this proposal with [mobile endpoints](mobile-endpoints.md), [endpoint security](endpoint-security.md), [routing and privacy](routing-privacy.md), the [seven engineering cores](../architecture/engineering-cores.md), and the [validation plan](validation-plan.md).

## 1. Define the communicating endpoints before choosing the route

Server, phone, desktop, router, and embedded device are deployment descriptions. An initiator starts a particular connection; a responder accepts it. Either application endpoint can send authorized data once the service is established. Relay and exit are separate forwarding roles, with separately enforced permissions.

This proposed application-level symmetry does not imply that every carrier supports symmetric migration or that a phone behind NAT can accept unsolicited inbound traffic. Authentication establishes the peer under the selected trust mechanism; neither its current IP address nor possession of a connection identifier establishes its identity.

| Scenario | Service to investigate first | Routing question | Evidence needed |
| --- | --- | --- | --- |
| Server to server | Reliable streams for transfers and requests; datagrams where loss is permitted | Direct connection as a baseline; explicit relay if the deployment needs one | Goodput and tail latency under concurrent workloads; mutual authentication and authorization; memory and fairness under load |
| Phone to server | Interactive streams and datagrams with bounded queues | Outbound path through mobile NAT; path change, reconnect, and approved fallback | Wi-Fi/cellular transitions, CGNAT, IPv6/NAT64, sleep/wake, radio and CPU cost, time to useful data after a failure |
| Phone to phone | Endpoint-protected messages or media | Whether direct traversal succeeds; when an authorized relay is required | Candidate disclosure, endpoint discovery, both devices sleeping or moving, relay costs and identity verification |
| Router or edge device to server | Small messages, occasional transfers, or a separately defined IP-tunnel service | Stable outbound connection versus reconnect on demand | Bounded CPU/RAM, identity provisioning, revocation, MTU and power constraints |
| Endpoint to endpoint through transit relays | The same explicitly selected interactive service | Which relays can see which addresses and whether they terminate any security context | Endpoint confidentiality, route authorization, correlation exposure, added delay and amplification budgets |
| Asynchronous private communication | Bounded complete messages and a separate offline-delivery contract | Whether a mix network is justified by the adversary and delay tolerance | Anonymity population, mixing assumptions, cover cost, expiry, mailbox access and storage abuse |

These are research scenarios, not six mandatory product features. They do not require accounts at a particular company, a particular identity provider, or one global directory. The eventual specification needs a clear minimum interoperable profile; optional trust and discovery mechanisms need explicit compatibility boundaries.

## 2. Separate three design decisions

### Data service

The receiving application needs to know what the protocol promises about its data.

| Candidate service | Proposed meaning | Important boundary |
| --- | --- | --- |
| Reliable byte stream | Ordered bytes or an explicit failure | No silent removal of expired bytes from the middle of a successful stream |
| Unreliable datagram | Message boundaries preserved, with loss permitted | A sender queue expiry is not an Internet delivery deadline |
| Reliable complete message | A possible later message service with explicit completion/failure | Message limits, reassembly, cancellation and duplicate effects need separate semantics |
| IP packet carriage | A separately negotiated tunnel profile | Addressing, source validation, routes, DNS, ICMP and inner MTU cannot be inferred from stream support |
| Offline message | A possible asynchronous service with expiry and bounded storage | It needs a different availability and acknowledgement contract from a live stream |

A packet ACK, acceptance into a buffer, delivery to an application, and completion of an external action are distinct events. Reconnection cannot generally establish whether a previously issued application operation completed. Application request identifiers and idempotency policies may still be necessary.

### Route and trust profile

The following names are explanatory labels, not assigned wire values or a finalized profile registry.

| Candidate route | Proposed use | What it does and does not establish |
| --- | --- | --- |
| **Direct** | Baseline for server traffic and reachable phone/server sessions | Fewest overlay forwarding steps for the comparison; endpoints know their peer's network address. Actual Internet path quality still determines performance |
| **Transit relay** | Reachability when a direct connection is unavailable or disallowed | An end-to-end context can protect content from the relay. A single relay normally knows its adjacent peers and can correlate forwarding; it is not automatically an anonymity network |
| **Layered multi-hop** | A separately justified attempt to distribute routing knowledge | Requires analyzed packet construction, independently assessed relay roles, authenticated discovery, path policy and an explicit attacker model; it does not automatically defeat timing correlation |
| **Asynchronous mix** | Messages that can tolerate a separate delay and storage model | Investigates mixing and cover traffic under the selected model. It should not silently replace an interactive stream or realtime datagram session |

An exit forwarding to a service that does not implement VLP is a different endpoint boundary from an opaque transit relay. VLP protection ending at the exit does not protect the next leg by itself. Application TLS or another endpoint security mechanism can extend content protection to the actual service. The destination can also identify a user through application credentials even if the network route hides the user's IP address.

For comparison, [Oblivious HTTP, RFC 9458](https://www.rfc-editor.org/rfc/rfc9458.html), sections 2.1 and 6, separates a relay and gateway with different visibility. Its applicability is limited; stateful authenticated requests and traffic analysis do not inherit a blanket unlinkability guarantee. It is prior art for trust separation, not a generic VLP stream transport selected here.

### Carrier

Native UDP, QUIC carriage, and a specified TCP/TLS fallback need comparable evaluations. Responsibilities for reliability, encryption, framing and congestion control must be assigned for each mapping. The fallback cannot simply assume that an ordered byte stream reproduces independent unreliable datagrams or seamless QUIC migration.

Using QUIC does not select HTTP/3. An actual HTTP/3 appearance requires its protocol behavior and an appropriate carrier mapping; a custom VLP-over-QUIC service can still have a distinguishable application and traffic profile. Standard ports or random-looking bytes do not establish indistinguishability.

The architecture should justify additional inner encryption by a real endpoint or trust boundary. If the existing protected carrier already ends at the intended application peer, another blanket encryption layer may only add cost. If the carrier terminates at a relay outside that trust boundary, the content needs an independently authenticated endpoint protection mechanism.

## 3. Adapt performance within a fixed security policy

The most useful hypothesis to investigate is whether one constrained scheduler can coordinate application usefulness, path quality, receiver capacity and appearance cost more effectively than independently layered mechanisms.

The application would express a service preference and resource budget. The enforcing endpoint would validate that request against local permissions. An attacker-controlled peer must not obtain unlimited bandwidth, memory or priority by declaring its traffic urgent.

Candidate local scheduling inputs include:

- Data service and allowed cancellation/expiry behavior.
- Measured RTT, loss and reordering, acknowledged delivery rate and current path validation state.
- Available congestion window, pacing allowance and receiver credit.
- Queue age and permitted local waiting time.
- MTU and all encapsulation overhead.
- CPU, memory, energy and metered-network budgets.
- The agreed appearance profile and any required minimum security properties.

The proposed scheduling order is to reject paths or operations that violate policy, then satisfy carrier and receiver limits, and finally choose among permitted transmissions according to useful delivery and cost. This is a design hypothesis, not a new congestion-control algorithm or a specified mathematical optimizer.

| Condition | Adaptation to investigate | Invariant to preserve |
| --- | --- | --- |
| Bulk transfer competes with interactive data | Fair per-channel scheduling and bounded priority service | Bulk traffic is not indefinitely starved; total send budget remains enforced |
| A datagram is no longer useful in the local queue | Drop it under the selected datagram contract | Do not create holes in reliable streams or claim remote delivery before a deadline |
| The connection becomes idle on a phone | Reduce nonessential activity or reconnect when permitted | A reduced cover rate must not silently weaken a required privacy policy |
| The current path degrades | Apply a policy-permitted validated failover with hysteresis | New path validation and peer identity are distinct checks; no unsafe counter reset |
| Two paths are usable | Compare standby, flow placement, selective duplication and aggregation | Count every byte; enforce per-path and aggregate fairness; protect nonce domains |
| Privacy-preserving paths fail | Report the failure or try another permitted path | Do not silently connect directly and expose information that the selected profile was intended to protect |

Changing path, carrier or performance class needs defined state transitions. Binding negotiated options to an authenticated context prevents undetected negotiation changes; it does not prove that an operator is independent, that a physical network path avoids a particular organization, or that a traffic-analysis adversary is absent.

## 4. Mobile operation is a first-class research scenario

A useful VLP design should account for a phone changing address, losing coverage, sleeping, and returning with stale NAT state. These are different events; a single generic reconnect flag is insufficient.

Research should separate:

1. A NAT port/address rebinding while the peer retains valid session state.
2. Migration to another locally available interface under the carrier's supported rules.
3. Re-establishment of a transport while an independently protected endpoint session survives.
4. A new authenticated session after state expiry or process restart.
5. Application recovery when delivery or operation completion is uncertain.

An interrupted transfer can be resumable only under an explicit service and authentication contract. A live call may have to discard obsolete datagrams and resume useful delivery. Neither case justifies restoring an old traffic key with a lost packet counter or accepting unbounded retransmission history.

Background execution is a deployment constraint. [Android Doze documentation](https://developer.android.com/training/monitoring-device-state/doze-standby) describes suspended network access and deferred work; the protocol cannot guarantee continuous application execution. Keepalive, reconnect and any platform wakeup integration must be measured within the actual permitted platform context. See [mobile-endpoints.md](mobile-endpoints.md) for the Apple boundary and network-condition matrix.

## 5. Strong encryption is a complete connection contract

The candidate baseline should use an analyzed authenticated key-establishment construction, accepted AEAD algorithms, secure randomness, direction and purpose separation, explicit usage limits, and endpoint identity verification. Selecting algorithm names is insufficient to establish those properties.

Research needs separate decisions for long-lived identity keys, ephemeral key agreement, resumption, per-packet protection, authentication of a new path, and recovery after compromise. KeyUpdate, forward secrecy and post-compromise recovery are distinct. The device's IP address is not its cryptographic identity.

The current primary-source comparison includes [TLS 1.3 RFC 9846](https://www.rfc-editor.org/info/rfc9846/), which replaces RFC 8446, and [RFC 10024](https://www.rfc-editor.org/rfc/rfc10024.html), which specifies ECDHE/ML-KEM hybrid groups for TLS 1.3. A TLS-specific hybrid construction cannot be copied into another handshake with its security argument assumed unchanged. See [endpoint-security.md](endpoint-security.md) for construction boundaries, replay, nonce state and PQ costs.

A deployment requiring post-quantum confidentiality must treat that requirement as part of its minimum acceptable profile. It cannot silently drop that requirement when a path or implementation lacks support. Conversely, an optional research candidate is not an already implemented or independently audited VLP security feature.

## 6. Turn “fast and private” into falsifiable questions

These questions require later authorized experiments. They are not completed benchmarks or release acceptance numbers.

| Hypothesis | Comparison needed | Evidence that would reject or narrow it |
| --- | --- | --- |
| An existing carrier can meet the initial VLP service and mobility scope | Equivalent services over selected existing transports versus the proposed native transport | A concrete required service or policy cannot be represented, or measured costs exceed an agreed budget |
| Joint scheduling improves useful delivery under a fixed security policy | Same path, implementation quality, crypto, workload and appearance budget; coordinated versus independently layered policies | No material gain, worse tail latency/fairness, or benefit that depends on relaxing the security policy |
| Validated failover is the best initial mobile multipath use | Single active path, warm standby, flow placement and packet striping | Extra radio/CPU work or reordering outweighs the observed availability benefit |
| An opaque relay improves reachability at acceptable cost | Direct and relay paths with the same final endpoints and security guarantees | Latency, relay bandwidth or metadata exposure exceeds the declared scenario budget |
| A multi-hop or mix profile improves privacy in its stated model | Explicit adversary placement, compromised roles, population, traffic distributions and held-out observations | The result disappears under the stated attacker, realistic traffic population, or permitted resource budget |

The [Anonymity Trilemma research](https://freedom.cs.purdue.edu/projects/trilemma.html) studies bandwidth, latency and anonymity under specified global-observer models. Its dependence on user traffic distributions matters for VLP: an almost empty network cannot borrow the anonymity population of a large deployment. This motivates stated assumptions and separate measurements; it is not a universal numerical performance law for every VLP configuration.

Measure useful delivered payload separately from wire throughput. Record handshake time to authorized useful data, median and tail latency, goodput, loss, deadline misses, queue bounds, fairness, bytes of padding/retransmission, CPU/memory, and energy under a repeatable device-state procedure. For an overlay, also account for summed traffic across all relay legs; access-link overhead alone hides relay costs.

Detection experiments need a declared observation point, false-positive rates, held-out applications and networks, and a fixed enabled profile. A classifier failing on one dataset is not a guarantee of undetectability. Sample sizes, devices, providers, dates and configuration must accompany any future result. No current deployment, speed, battery, anonymity or blocking-resistance result exists for VLP.

## 7. Scope order and requirement traceability

The proposed first specification scope to evaluate is endpoint identity and authorization, one coherent interactive data service, a direct carrier baseline, bounded resources, and explicit mobile failure behavior. A relay may be a first-scope dependency if the accepted reachability requirement needs it. Onion, garlic, mixnet and multipath are research priorities now; their implementation priority depends on the selected use case and threat model.

Anonymity requirements must influence the architecture before the first specification. A later extension cannot repair an initial design that has already exposed a stable identity where its threat model forbids disclosure. At the same time, an asynchronous mix service need not be forced into every low-latency session.

| Research topic | Existing requirement references |
| --- | --- |
| Endpoint roles and deployment scope | VLP-REQ-001, VLP-REQ-002, VLP-REQ-003, VLP-REQ-004, VLP-REQ-005, VLP-REQ-012 |
| Data service and delivery | VLP-REQ-016, VLP-REQ-017, VLP-REQ-018, VLP-REQ-022, VLP-REQ-088, VLP-REQ-098, VLP-REQ-099, VLP-REQ-100, VLP-REQ-101, VLP-REQ-102, VLP-REQ-103, VLP-REQ-104 |
| Mobile paths and performance | VLP-REQ-019, VLP-REQ-020, VLP-REQ-024, VLP-REQ-025, VLP-REQ-026, VLP-REQ-027, VLP-REQ-028, VLP-REQ-029, VLP-REQ-030, VLP-REQ-137, VLP-REQ-139, VLP-REQ-140, VLP-REQ-141, VLP-REQ-142, VLP-REQ-143, VLP-REQ-144, VLP-REQ-145, VLP-REQ-148, VLP-REQ-149, VLP-REQ-155, VLP-REQ-160, VLP-REQ-161 |
| Endpoint protection and authenticated adaptation | VLP-REQ-031, VLP-REQ-039, VLP-REQ-040, VLP-REQ-041, VLP-REQ-042, VLP-REQ-045, VLP-REQ-046, VLP-REQ-048, VLP-REQ-054, VLP-REQ-059, VLP-REQ-060, VLP-REQ-062, VLP-REQ-063, VLP-REQ-105, VLP-REQ-114, VLP-REQ-121, VLP-REQ-125 |
| Route privacy, observability and cost | VLP-REQ-069, VLP-REQ-074, VLP-REQ-075, VLP-REQ-076, VLP-REQ-077, VLP-REQ-080, VLP-REQ-082, VLP-REQ-083, VLP-REQ-084, VLP-REQ-085, VLP-REQ-086, VLP-REQ-087, VLP-REQ-126, VLP-REQ-127, VLP-REQ-128, VLP-REQ-129, VLP-REQ-130, VLP-REQ-131, VLP-REQ-133, VLP-REQ-134, VLP-REQ-135, VLP-REQ-136 |
| External adoption and evidence | VLP-REQ-163, VLP-REQ-167, VLP-REQ-173, VLP-REQ-185, VLP-REQ-186, VLP-REQ-194, VLP-REQ-196, VLP-REQ-197, VLP-REQ-198, VLP-REQ-199, VLP-REQ-200, VLP-REQ-218, VLP-REQ-219, VLP-REQ-220 |

These links identify research coverage only. They do not resolve any requirement, assign extra VLP specification numbers, or replace the original titles. The [decision process](../process/decision-process.md) still requires research review before the reserved specifications and a separate implementation approval after specification review.
