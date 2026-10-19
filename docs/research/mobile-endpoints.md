# Mobile endpoints, carriers, and performance

## Status and purpose

**Research note; evidence checked on 2026-10-19.** No protocol implementation, experiment, benchmark, mobile application, or gate evaluation is delivered by this note. Research Gate remains `NOT_EVALUATED`; transport, cryptographic construction, language, fallback, relay and multipath choices remain candidates.

The goal is to investigate fast, strongly protected communication across server, phone and other endpoint pairs without assuming permanent addresses, continuous execution, or unlimited battery. “Universal” should describe explicit interoperable profiles and roles, not a promise that every network permits every connection. “Fast” needs workload-specific goodput, latency, resource and fairness evidence.

This work follows the [decision process](../process/decision-process.md) and extends the [validation plan](validation-plan.md). It does not author VLP-0001, VLP-0002 or VLP-0003.

## Existing requirements covered

The following are exact existing identifiers or inclusive ranges in the [220-item register](../requirements/README.md). Coverage means research contribution, not resolution or approval. No identifiers, original titles, priorities or statuses are changed here.

| Research area | Existing identifiers |
| --- | --- |
| Endpoint roles, interaction and profiles | VLP-REQ-003–005, VLP-REQ-009, VLP-REQ-012–020, VLP-REQ-098–104 |
| Mobile paths and connection lifecycle | VLP-REQ-024–030, VLP-REQ-125, VLP-REQ-137–148, VLP-REQ-155–158, VLP-REQ-174–180 |
| Authentication and security-preserving recovery | VLP-REQ-043–048, VLP-REQ-054–068, VLP-REQ-105, VLP-REQ-107–114, VLP-REQ-121–123 |
| Privacy and appearance costs | VLP-REQ-073–078, VLP-REQ-080–087, VLP-REQ-126–136 |
| Performance, resource bounds and evidence | VLP-REQ-117–118, VLP-REQ-149–162, VLP-REQ-181–184, VLP-REQ-185, VLP-REQ-191, VLP-REQ-194, VLP-REQ-196–199, VLP-REQ-219 |

## 1. Separate identity, establishment and forwarding roles

The proposed research model separates four questions:

| Dimension | Question to resolve | Consequence |
| --- | --- | --- |
| Peer identity | Which credential or trust relationship identifies the authorised peer? | Identity is not an IP address, a connection identifier, a device category, or permission to forward arbitrary traffic |
| Establishment role | Which endpoint initiates this connection and which responds? | A machine providing an application service can still initiate an outbound transport connection |
| Application role | Which endpoint requests or supplies an application operation? | Data direction need not follow the establishment direction |
| Forwarding role | Is this node a terminating endpoint, an authorised relay, or an egress? | Forwarding permissions, metadata exposure and key-termination boundaries require separate decisions |

These are role distinctions to investigate, not new wire fields. In particular, calling a device a “server” in the product does not require it to be the QUIC server for every connection.

| Endpoint pair | Candidate establishment arrangement | Unresolved limitation |
| --- | --- | --- |
| Server ↔ server | Either authorised endpoint can initiate towards an advertised reachable peer | Discovery, firewall policy, identity and failover still need a contract |
| Server ↔ phone | The phone initiates an outbound connection; the established channel permits authorised traffic in both directions | Background execution and changed reachability can interrupt the channel |
| Phone ↔ phone | Deliberately selected initiator/responder roles, with separately approved rendezvous or relay support where needed | Two independently changing addresses are not solved by a connection ID |
| Desktop, gateway or constrained device ↔ another endpoint | Select roles from reachability and trust, with explicit resource profiles | No assumption of a public listener, hardware acceleration, stable clocks, or continuous power |

**QUIC v1 boundary:** RFC 9000 permits client connection migration, not general symmetric server mobility. Its preferred-server-address mechanism is a specific facility, not unrestricted server migration. Active migration can also be disabled by a transport parameter; NAT rebinding must still be handled. A VLP design requiring either peer to move at any time must account for these limits or select a separately reviewed extension or reconnection model. [RFC 9000, §§9, 9.6 and 18.2](https://www.rfc-editor.org/rfc/rfc9000.html#section-9).

## 2. Specify data profiles before selecting a carrier

| Candidate VLP profile | Required semantic question | Mobile performance question |
| --- | --- | --- |
| TCP connection proxy | How is a terminated TCP connection mapped to an independently managed reliable byte stream? | Can a large transfer delay unrelated interactive channels? |
| Datagram/message transport | Which message boundaries, size limits, drops, expiration and duplication rules are visible to the caller? | How many useful messages arrive, and how much time is spent waiting locally? |
| IP tunnel | How are complete IP packets, routes, source permissions, MTU, fragmentation and ICMP represented? | Does the tunnel continue to work when path capacity or address family changes? |

QUIC DATAGRAM is unreliable, congestion controlled, and separate from stream flow-control limits. A receiver may drop data it cannot process. Its local expiration facility does not provide a delivery deadline, and a transport ACK does not prove application processing. [RFC 9221, §§5.2–5.4](https://www.rfc-editor.org/rfc/rfc9221.html#section-5.2).

**Research constraint:** do not give a datagram profile an undocumented globally reliable, ordered meaning when changing carriers. An IP tunnel and a TCP proxy need different failure and backpressure analysis. Carrying every inner IP packet over one reliable ordered connection is a candidate requiring justification, not a universal default.

## 3. Distinguish rebinding, migration, reconnection and recovery

| Event | What may change | Candidate handling to assess |
| --- | --- | --- |
| NAT rebinding | The translated address or port seen by the peer | Recognise the existing authenticated connection, validate applicable path properties and enforce resource limits |
| Active migration | The endpoint deliberately uses another local network address | Honour negotiated permissions; validate the new path before granting it equivalent treatment |
| Path failover | Useful traffic switches from a failed path to another permitted path | Measure interruption and recovery; do not describe failover alone as bandwidth aggregation |
| Reconnection | A new transport connection is established | Authenticate the peer and create the appropriate new cryptographic context |
| Session/application recovery | Work is reconciled across connection loss | Define accepted, uncertain, repeated and cancelled operations separately from packet delivery |
| Process restart or device restoration | In-memory transport and cryptographic state can disappear | Do not reload old traffic keys and silently restart nonce, packet-number or replay state |

QUIC connection IDs help with rebinding, but RFC 9308 explains that this does not discover a peer's new address: at least one endpoint must remain reachable at the address known to the other, and deployed routing or firewall state can still prevent recovery. [RFC 9308, §3.2](https://www.rfc-editor.org/rfc/rfc9308.html#section-3.2).

For VLP research, preserve identity, permissions and required confidentiality across every transition. Migration should retain the security state appropriate to the continuing connection. Reconnection should not be implemented by copying a traffic secret into a reset transport. Any proposed resumption needs its own identity binding, replay, expiry and side-effect analysis. A successfully resent packet or reconnected socket does not establish exactly-once execution.

## 4. Carrier constraints and an explicit fallback policy

| Condition to investigate | Candidate response | Required boundary |
| --- | --- | --- |
| CGNAT or inbound filtering | Outbound establishment, or an explicitly selected traversal/relay mechanism | Do not assume unsolicited inbound traffic can reach a phone |
| IPv6-only access, including DNS64/NAT64 | Address-family-independent discovery and endpoint handling | Keep service identity independent of a hardcoded IPv4 literal; define resolver and address-selection policy |
| Dual-stack path changes | Re-evaluate a permitted address/path family | Do not mistake a new address family for a new peer identity |
| UDP unavailable | Fail clearly, or try an approved TLS-over-TCP profile | Preserve the minimum authentication and confidentiality policy; report changed delivery and privacy properties |
| MTU reduction or blocked ICMP | Apply the selected PMTU and bounded fragmentation/error strategy | Do not assume one payload size works on every path or profile |
| Both peers lose their known addresses | Explicit reconnection/discovery or a separately approved rendezvous service | No automatic contact with a new relay or disclosure of additional addresses |

Apple explicitly documents IPv6-only and DNS64/NAT64 compatibility, including the need to review IPv4-specific APIs and hardcoded addresses. That guidance is evidence for a test environment, not proof that a VLP carrier works through every translator. [Apple, Supporting IPv6-only Networks, “IPv6-Only Networks” and “Server updates”](https://developer.apple.com/support/ipv6/).

RFC 9308 identifies fallback as a deployment consideration when UDP is blocked. It also describes feature differences and security consequences of TLS-over-TCP fallback. Its historical UDP-blocking measurements must not be presented as current global or mobile-carrier rates. [RFC 9308, §§2 and 17](https://www.rfc-editor.org/rfc/rfc9308.html#section-2).

**Proposed fallback decision:** define permitted carriers and a minimum security/privacy policy before connecting. Use bounded attempts and retain the authenticated peer identity. If no permitted profile can meet that policy, return an explicit failure. Do not automatically fall back to plaintext, weaker authentication, undisclosed relay routing, or a mode exposing metadata prohibited by the selected policy. A TLS-over-TCP candidate needs its own reviewed channel mapping; it is not QUIC with a different socket type.

## 5. ICE and TURN are optional mechanisms, not universal permission

ICE gathers and checks candidate paths; its address-privacy discussion warns that candidate exchange and connectivity probing can reveal addresses and network characteristics. [RFC 8445, §§5–7 and 19.1](https://www.rfc-editor.org/rfc/rfc8445.html#section-19.1).

TURN supplies relay allocations with permissions. A TURN permission is scoped to an allocation and peer IP address; it is not a VLP identity or application-authorisation decision. [RFC 8656, §§2 and 9](https://www.rfc-editor.org/rfc/rfc8656.html#section-9).

Before adopting either mechanism, research:

- Which participants may discover, signal, probe or allocate relay resources, and how those permissions are enforced.
- Which interfaces and address candidates are allowed to leave the device, including addresses outside the user's selected tunnel.
- Which relay is authorised, who operates it, what addresses and traffic patterns it observes, and its quota, logging and retention policy.
- Whether end-to-end payload protection survives relay use; encryption on one relay hop is not evidence of endpoint-to-endpoint confidentiality.
- How credentials, relay allocations, permissions and NAT state expire, and the resulting idle cost.
- Whether relay-only, direct-only, or approved mixed operation is required by the user's privacy policy.

A relay is a possible reachability aid. It does not by itself provide anonymity, trustworthy end-to-end routing, or a safe multi-hop construction. Multi-hop relay composition and simultaneous transport paths are different research subjects; neither is automatically selected by enabling ICE or TURN.

## 6. Mobile execution and keepalive energy

Android documents that Doze suspends ordinary app network access and defers work; maintenance windows become less frequent over prolonged inactivity. App Standby also restricts background networking. The platform guidance does not support creating a foreground service merely to evade idle classification. [Android Developers, “Understand Doze”, “Doze restrictions” and “Understand App Standby”](https://developer.android.com/training/monitoring-device-state/doze-standby).

Apple documents that ordinary apps become suspended after background processing and that extra execution time is finite. Requesting background time is not an always-on transport entitlement. The runtime and extension category of any future VLP deployment must therefore be reviewed separately; this note does not conclude that all specialised networking modes behave like ordinary UIKit apps. [Apple, Extending your app's background execution time, “Overview”](https://developer.apple.com/documentation/uikit/extending-your-app-s-background-execution-time).

**Proposed research policy:** distinguish an active transfer, user-visible interactive session, idle connection, suspended process and wake/reconnect event. For each, compare no keepalive, on-demand reconnection and permitted adaptive keepalive. Measure useful availability against energy, bytes and wakeups. Do not assume a universal NAT timeout or select a permanent short ping interval as a mobile default.

When execution is suspended, the protocol cannot require a timer to fire on schedule. Treat missed liveness evidence as uncertainty rather than proof of an attack; apply bounded timeout/recovery behaviour. Do not restore an old encryption context unsafely after a process is killed. Neither push messaging nor a particular mobile framework is adopted by this research note.

## 7. Multipath: current status and separate objectives

On **2026-10-19**, the IETF Datatracker showed **draft-ietf-quic-multipath-21**, with IESG state **RFC Ed Queue** and RFC Editor status **In Final Review**. No published RFC number was shown. The intended standards status is not a published RFC, and the expired date printed in the draft header is not sufficient evidence that the work has been abandoned. Recheck status and exact revision before adoption. [IETF Datatracker, document status](https://datatracker.ietf.org/doc/draft-ietf-quic-multipath/).

The draft enables concurrent paths but does not specify address discovery or a universal scheduling algorithm. It describes per-path congestion state, potential unfairness at shared bottlenecks, and the ordered-stream delay consequence of using paths with different delays. [draft-ietf-quic-multipath-21, §§1, 5.3–5.5](https://datatracker.ietf.org/doc/html/draft-ietf-quic-multipath-21#section-5.3).

| Candidate objective | Research distinction | Measurement |
| --- | --- | --- |
| Failover | Maintain or discover a permitted alternative; useful traffic primarily follows one path | Interruption, recovery time and idle cost |
| Aggregation | Carry useful data concurrently over multiple paths | Additional goodput after accounting for overhead, fairness, reordering and energy |
| Traffic-class placement | Place independent channels or messages according to their needs | Interactive p95 latency, bulk goodput and starvation |
| Limited redundancy | Send selected data redundantly under an explicit budget | Useful delivery gain versus duplicate bytes, processing and energy |

Research should compare whole-channel placement with packet striping. For ordered delivery, a late segment on one path can hold back later data from a faster path; this is a scheduling/reassembly issue, not evidence that encryption is slow. Keep queues and reordering memory bounded, account for acknowledgements and probes, and distinguish path capacity from a shared bottleneck. These are candidates for evaluation, not an approved scheduler.

Additional active interfaces also create additional observation points. Analyse address linkage, simultaneous flow correlation and operator visibility before enabling another path. Successful failover does not demonstrate aggregation; higher aggregate sending rate does not demonstrate fair or energy-efficient useful throughput.

## 8. Adaptation needs measured objectives and hard limits

The candidate controller should receive bounded measurements of RTT variation, loss, delivered useful bytes, queue residence, receiver capacity, path cost and energy state. It should adjust only policy-permitted parameters, with hysteresis and limits on probing or oscillation. There is no presumed algorithm that is fastest for every endpoint pair and traffic mix.

Receiver capacity and network congestion are different constraints. QUIC stream flow control limits data admitted by the receiver, while congestion control limits network sending. [RFC 9000, §§4 and 13](https://www.rfc-editor.org/rfc/rfc9000.html#section-4). A VLP datagram profile also needs bounded receiver admission even when the carrier has no stream-style datagram credit mechanism.

Evaluate at least:

- Useful application goodput and total wire bytes, including padding, control, probes, retransmissions and redundant data.
- p50/p95/p99 application and local-queue latency, with sample count and workload; useful-before-expiry datagrams measured separately.
- CPU, peak memory, queue/reassembly limits, energy per useful GiB and idle energy per hour, with the measurement method and device state.
- Fairness against competing ordinary TCP/QUIC traffic, starvation, and behaviour when paths share a bottleneck.
- Completion, interruption and recovery rates; do not omit failed connections from reported performance.

Optimisation must not weaken peer authentication, nonce uniqueness, replay handling, path validation or the required privacy policy. A change of path, speed target, battery state or carrier is not permission to downgrade those properties.

## 9. Candidate test matrix

**All numerical values below are arbitrary proposed laboratory inputs for future approved comparisons. They are not measured carrier properties, promised performance, selected protocol constants or acceptance thresholds. No tests have run.** Refine them for an approved workload before execution.

| Scenario | Proposed controlled inputs | Evidence to collect |
| --- | --- | --- |
| Single-path reference | RTT 20/80/200 ms; down/up capacity 20/5 or 100/20 Mbit/s; loss 0/1/3% | Goodput, latency distribution, CPU, memory and full overhead |
| Bursty impairment | Additional delay 0–100 ms; 100 ms loss bursts; duplication 1%; bounded reordering | Useful datagrams, stream completion, queue bounds and recovery |
| Wi-Fi ↔ mobile transition | Address/port change during transfer; outage 1/10/60 s; old path restored or absent | Whether the event was rebinding, migration or reconnection; state integrity and interruption |
| Dual-stack/NAT64 | IPv4, native IPv6, dual-stack and IPv6-only DNS64/NAT64; hostname and literal-address configurations | Reachability, identity verification, resolver decisions and unsupported cases |
| NAT expiry and sleep | Synthetic mapping expiry 30/120 s; idle 2/10 min; Android Doze and the documented iOS lifecycle | Wake/reconnect behaviour, incorrect death detection, idle bytes and energy |
| UDP blocked | Drop outbound or return UDP; allow only the explicitly approved alternative, or no alternative | Bounded attempts; honest error; preserved security and privacy policy |
| Unequal multipath | Path A RTT 20 ms, path B 150 ms; separate and shared bottlenecks; either path fails | Failover versus aggregation, p95 delay, reordering memory, fairness and energy |
| Slow receiver/mixed load | Interactive messages with bulk transfer; deliberate receiver CPU/buffer pressure | Backpressure, drops, starvation and congestion/receiver-limit separation |
| MTU and profile overhead | Outer MTU 1280/1500 bytes; ICMP delivered or blocked; varied approved padding | Complete payload budget, error/fragmentation behaviour and absence of silent black holes |

Run future network experiments only within separately authorised scope and controlled endpoints. Record exact versions, policies, topology, instrumentation, sample sizes and limitations. The output of this research stage is the comparison design and its source evidence, not benchmark results or implementation approval.

## Primary-source record

The ten sources below were checked for the specific sections used above. Stable RFCs, a changing draft status page, a pinned draft revision and mobile platform guidance have different evidence lifetimes. Apple UIKit article content was available through the official page's indexed text; direct rendering exposed only its JavaScript shell. No device behaviour or deployed implementation was tested.

| Source | Checked sections or scope | Boundary |
| --- | --- | --- |
| [RFC 9000](https://www.rfc-editor.org/rfc/rfc9000.html) | §§4, 9, 9.6, 13, 18.2 | QUIC v1 semantics, not a promise of universal reachability |
| [RFC 9308](https://www.rfc-editor.org/rfc/rfc9308.html) | §§2, 3.2, 17 | Applicability guidance; historical measurements are not current carrier statistics |
| [RFC 9221](https://www.rfc-editor.org/rfc/rfc9221.html) | §§5.2–5.4 | QUIC DATAGRAM semantics, not an application delivery guarantee |
| [RFC 8445](https://www.rfc-editor.org/rfc/rfc8445.html) | §§5–7, 19.1 | ICE candidate handling and privacy; not VLP signalling or authorisation |
| [RFC 8656](https://www.rfc-editor.org/rfc/rfc8656.html) | §§2, 9 | TURN relay and permission model, not end-to-end VLP identity |
| [QUIC multipath Datatracker](https://datatracker.ietf.org/doc/draft-ietf-quic-multipath/) | Document, IESG and RFC Editor status on 2026-10-19 | Mutable publication state; no RFC publication asserted |
| [draft-ietf-quic-multipath-21](https://datatracker.ietf.org/doc/html/draft-ietf-quic-multipath-21) | §§1, 5.3–5.5 | Pinned work-in-progress text, not an adopted VLP extension |
| [Android Doze and App Standby](https://developer.android.com/training/monitoring-device-state/doze-standby) | Doze restrictions; App Standby; persistent connection considerations | Ordinary app lifecycle guidance; no VLP platform implementation validated |
| [Apple background execution](https://developer.apple.com/documentation/uikit/extending-your-app-s-background-execution-time) | Overview | Finite ordinary-app execution; specialised deployment modes need separate review |
| [Apple IPv6-only support](https://developer.apple.com/support/ipv6/) | IPv6-only networks; testing; server updates | Compatibility guidance; no universal NAT64 or application success claim |
