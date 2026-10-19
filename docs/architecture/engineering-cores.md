# Engineering cores

## Status and purpose

This document defines the responsibilities to investigate for VLP. It is an engineering map, not an approved architecture or a protocol specification. Research is open; the Research Gate has not been performed. Native UDP, QUIC-based carriage, Noise, TLS-based constructions, Rust, and other implementation choices remain candidates until supported by evidence and recorded decisions.

The complete scope is the [220-item requirements register](../requirements/README.md), with stable identifiers in [requirements.json](../requirements/requirements.json). The original requirement text remains traceable when work is prioritised, deferred, clarified, or found to conflict with another requirement. The source categories in that register are organisational headings; they are not additional engineering cores.

VLP has exactly seven engineering cores: **Protocol Core, Transport, Cryptography, Handshake, Camouflage, Data Plane, and Security**. Control, privacy, performance, connection lifecycle, reliability, evolution, and validation cut across them.

The [deployment research](../research/deployment-profiles.md) applies these boundaries to server, phone, relay and constrained-device scenarios. It separates data-service semantics, route/trust choices, and carrier mappings; none is an additional engineering core or an adopted wire profile.

## Responsibility map

| Core | Owns the engineering questions | Boundary with other cores | Expected research output |
| --- | --- | --- | --- |
| **Protocol Core** | Protocol identity and scope; endpoint roles; session and channel models; state consistency; version and extension policy; interoperable error semantics | Coordinates the protocol contract. It does not implement a second transport, cryptographic construction, or application platform | Scope, invariants, architecture alternatives, state-model questions, and a requirement-to-owner map |
| **Transport** | Carriage; packet delivery; loss recovery where applicable; congestion control; pacing; flow control; path validation and migration; MTU discovery | Carries channel data according to the Data Plane contract. Its exact responsibilities depend on whether VLP uses native UDP or a transport such as QUIC | Candidate comparison, delivery and path model, resource budgets, and a transport decision supported by evidence |
| **Cryptography** | Existing cryptographic constructions and libraries; key agreement and derivation; packet confidentiality and integrity; nonce domains; key separation; key updates and destruction | Specifies cryptographic properties and safe usage. Handshake owns the connection-establishment state machine; Security owns the broader threat model | Construction comparison, key-lifecycle analysis, composition risks, and a review plan |
| **Handshake** | Peer authentication; proof of possession where required; negotiation and transcript binding; establishment states; retries, timeouts, resumption and replay questions | Uses the selected cryptographic construction. Successful authentication does not itself grant every routing or channel permission | Candidate handshake flows, identity assumptions, negotiation rules to resolve, and failure-state analysis |
| **Camouflage** | Observable traffic properties; appearance profiles; padding and timing policies; behaviour under probing; compatibility constraints | Does not replace encryption or authorisation. Works within Transport's congestion and pacing budget and Security's limits | Adversary-specific hypotheses, leakage inventory, profile alternatives, and measurable costs and limitations |
| **Data Plane** | Meaning of carried data; stream, message, datagram and IP-tunnel profiles; channel lifecycle; queue policies; endpoint forwarding | Does not promise stronger delivery than Transport provides. Forwarding follows server-enforced permissions and resource limits | Data-model alternatives, channel and forwarding semantics, queue and backpressure analysis |
| **Security** | Threat model; authorisation; abuse and denial-of-service resistance; isolation; resource exhaustion; operational trust boundaries; secure failure behaviour | Reviews every core. Encryption alone does not establish access rights, safe routing, availability, or privacy | Threat model, abuse cases, required safeguards, residual risks, and security review criteria |

Each requirement has one accountable owner in the register and may depend on several cores. Accountability does not justify duplicate implementations of the same mechanism. For example, the Security owner can require replay resistance while Cryptography and Handshake jointly determine how it is achieved.

## Decide which layer is new

Two different architecture candidates need an honest comparison:

| Candidate | VLP would define | The underlying system would provide | Main question |
| --- | --- | --- | --- |
| **VLP carried by QUIC** | Its own session, channel, forwarding and control semantics, payload formats, and policy negotiation | QUIC transport protection, reliable streams, recovery and congestion machinery; extensions can provide datagrams | Do the required semantics and observable behaviour fit the existing transport and its implementation interfaces? |
| **VLP carried directly by UDP** | Its own transport packets and state machine in addition to the VLP session and Data Plane | UDP/IP delivery and selected existing cryptographic constructions | What concrete requirement justifies implementing and reviewing an additional transport? |

A protocol with its own semantics over QUIC can be a new protocol without being a new transport. Hysteria 2 is an existing example of a separately specified proxy protocol based on QUIC. QUIC already defines multiplexed streams, flow control and connection migration; its DATAGRAM extension also permits expiration of queued datagrams. These features alone are not evidence of VLP novelty. See the [Hysteria 2 protocol specification](https://v2.hysteria.network/docs/developers/Protocol/), [RFC 9000](https://www.rfc-editor.org/rfc/rfc9000.html), and [RFC 9221](https://www.rfc-editor.org/rfc/rfc9221.html).

The research decision should identify a measurable benefit in a stated operating environment, its cost, and the alternatives that were considered. Changing names, magic bytes, encryption labels, or packet headers is not sufficient evidence of an engineering advantage. An original transport does not require inventing a cipher or key-exchange primitive.

## Data and delivery semantics to resolve

These are candidate semantics to investigate, not a mandatory feature list for the first implementation:

| Candidate data service | Meaning to make explicit | Questions that cannot be left implicit |
| --- | --- | --- |
| Reliable byte stream | Ordered bytes until completion or an explicit failure | Independent cancellation, buffer limits, flow control, final-size consistency, and fair scheduling |
| Unreliable message or datagram | Preserved message boundaries with permitted loss and no automatic payload retransmission | Maximum size, queue limits, receiver overload, context ownership, duplication policy, and congestion accounting |
| Deadline-sensitive data | Data can lose usefulness while waiting | Whether expiration applies only to the local send queue or also to delivery; how partial delivery is represented; clock assumptions |
| IP tunnel | Carriage of complete IPv4 or IPv6 packets under a forwarding policy | Address assignment, routes, source validation, MTU, ICMP handling, fragmentation, and isolation |
| Control operation | A state change with an explicit outcome | Authorisation, ordering, repeated requests, cancellation, timeout, and acknowledgement semantics |

A local queue deadline does not guarantee Internet delivery before a deadline. Omitting bytes from a reliable byte stream cannot silently turn it into a partially reliable message service. A transport acknowledgement does not establish that the receiving application completed a requested operation.

Transparent IP tunnelling and TCP connection proxying are separate profiles. Their delivery and forwarding semantics need separate decisions; a single globally ordered reliable tunnel should not be selected by default for every kind of traffic.

## Cross-core invariants to investigate

- **One security context has explicit boundaries.** Keys, packet numbers, channel identifiers, negotiated options and peer permissions need defined lifetimes. A path or appearance change is not permission to reset cryptographic state unsafely.
- **Authorisation precedes protected operations.** The server controls allowed channels, destinations, routes, quotas and priority classes. Client-provided hints do not create privileges.
- **Resource use is bounded.** Queues, parser allocations, reassembly, control requests, packet history and unfinished handshakes need limits and defined failure behaviour.
- **Congestion and flow control have different jobs.** Network capacity and receiver capacity must both be respected. Unreliable payloads still consume network resources.
- **Appearance changes have a budget.** Padding and other additional traffic count towards bandwidth and packet-processing costs. Timing policies cannot bypass congestion control or create unbounded queues.
- **Privacy includes observable metadata.** Encryption does not hide endpoint addresses, all packet lengths, timing, traffic volume, or every failure response. Logs and diagnostics need a separate data-minimisation policy.
- **Evolution is authenticated where it affects security.** Negotiation, extension handling, downgrade behaviour and compatibility must be reviewed together. An unsupported option needs defined handling rather than accidental parser behaviour.
- **Acknowledgement levels are distinct.** Packet receipt, acceptance into a buffer, channel establishment and completion of an external operation are different events.

These are research constraints. Their eventual wire-level expression belongs in reviewed specifications, not in this page.

## MTU is an architecture issue

The budget must include outer IP and UDP headers, transport headers, cryptographic overhead, VLP framing and any appearance overhead. It must be reconsidered when the path or profile changes.

The QUIC minimum of a 1200-byte UDP payload is not a recommendation to configure a TUN interface with an MTU of 1200. IPv6 tunnelling introduces a minimum inner-link MTU requirement of 1280 bytes. QUIC DATAGRAM frames do not themselves fragment messages; [RFC 9484, section 7.2](https://www.rfc-editor.org/rfc/rfc9484.html#section-7.2) discusses the resulting IP-tunnel constraints. VLP must research either sufficient path capacity, explicitly bounded protocol fragmentation, or a clear refusal of an unsupported tunnel profile. The specific mechanism is undecided.

## Scope and sequencing

P0 and P1 indicate proposed sequencing, not removal from the 220 requirements. P0 should aim for the smallest coherent, reviewable contract. P1 can hold additional profiles or advanced mechanisms while preserving their requirements, dependencies, rationale and revisit conditions.

Multipath, FEC, resumption, early data, multiple appearance profiles and adaptive algorithms require separate evidence. They are not automatically accepted merely because they appear in the requirements register. Equally, placing an item outside an initial implementation does not silently reject the user's requirement.

The [decision process](../process/decision-process.md) controls when choices can become specification decisions. The [validation plan](../research/validation-plan.md) describes evidence still to be collected.
