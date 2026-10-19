# Endpoint security across direct and relayed paths

Research date: **2026-10-19**.

**Research Gate: NOT_EVALUATED. All constructions and scope restrictions below are research candidates.** Implementation approval remains separate under the [decision process](../process/decision-process.md). This document introduces no VLP codepoints, packet format, executable prototype or approved cryptographic profile. It records source observations, engineering implications and questions for review.

## 1. Research question and endpoint definition

How can the same project serve server-to-server and phone-to-server traffic with useful performance while stating exactly which participant can decrypt which data?

Define the **security endpoint** as the authenticated participant permitted to receive the protected plaintext. A public IP address, relay, load balancer, transport connection and application service are not automatically the same security endpoint. This definition is a proposed architectural rule; selecting the actual endpoint for each use case is still open.

TLS describes confidentiality between its endpoints and leaves application identity verification to the integrating protocol. QUIC uses TLS handshake material but supplies its own packet protection instead of carrying the TLS record layer. These are useful existing boundaries, not proof that a new VLP composition is secure. [E1, §§1, 4.5; E2, §§4–5]

| Candidate deployment | Where the protected channel ends | Consequence to review |
| --- | --- | --- |
| Direct server-to-server or phone-to-server TLS/QUIC | The two intended application/security endpoints | The carrier can also supply endpoint channel protection. Do not mandate another payload-encryption layer merely to populate a “Security Core”. |
| Relay forwards opaque packets or bytes without terminating the endpoint channel | Still the intended endpoints | A relay in the path does not by itself require a second channel-encryption layer. Preserve endpoint authentication and the channel's state semantics. |
| Phone-to-relay TLS plus separate relay-to-server TLS | Two channels terminating at the relay | The relay can access each channel's plaintext. If it is outside the payload trust boundary, an inner authenticated channel between the intended endpoints is needed. |
| Trusted terminating gateway is deliberately the security endpoint | The gateway | Gateway plaintext access is an explicit trust decision; describe any separately protected onward connection accurately. |
| Multi-hop onion-style carriage | Separate hop/circuit boundaries plus the selected final endpoint | Layering, route authentication, key separation and replay semantics need independent composition analysis. |
| Final exit forwards to an external destination | VLP protection may end at the exit | Protection beyond the exit depends on a further authenticated application channel to the destination. |

The recommendation is to **encrypt for distinct trust boundaries**, rather than impose double encryption on every direct connection. Inner protection has a concrete purpose when outer carriage terminates at an intermediary that must not read the payload. Additional object/message encryption may serve another requirement, but needs its own identity, lifecycle and threat model.

## 2. Identity, proof of possession and permissions

Proposed identity choices to compare:

| Candidate | What it establishes | Work that remains in VLP |
| --- | --- | --- |
| Pinned raw public key / suitable Noise pattern | Peer possession of a key expected by the initiator | Authenticated enrollment, key-to-device/service binding, rotation, revocation and recovery of trust |
| Certificate-based TLS authentication | Peer authentication under a selected certificate-validation policy | Expected service identity, allowed trust anchors, client/device authentication policy, expiry/revocation handling and permissions |
| High-entropy per-peer PSK | Knowledge of the shared secret | Provisioning, peer attribution, storage, rotation, revocation and choice of a forward-secret handshake mode |

Noise verifies key possession but delegates whether a public key is acceptable to the application. Its PSKs are secret, high-entropy material; public keys are not substitutes for PSKs. [E3, §§9, 13–14]

The following are proposed enforcement boundaries, not completed implementation requirements:

- **Authentication is not authorization.** The enforcing server/peer decides which authenticated device or service may open a stream, use a route, contact a destination, allocate a relay or consume a quota.
- A phone can use an independently revocable device credential, with an optional binding to a deployment's account or service policy. No global account system is required. Its current IP, network, connection ID or claimed device label does not establish identity. Where an account exists, separate its recovery credential from each device's operational key.
- A PSK identity is a lookup identifier, not the secret itself. Avoid a fleet-wide secret when individual attribution and revocation are required. A human password is not a suitable substitute for a randomly generated PSK.
- Server-to-server mutual authentication is a candidate for managed workloads. For phones, compare mutual handshake authentication with a server-authenticated channel followed by properly bound device/application authentication. Neither mode is selected here.
- Pins need a pre-existing trust path. Do not accept a replacement pin simply because the old handshake failed. Certificate validation errors must not trigger an “insecure” retry.
- Evaluate platform key storage against the actual credential algorithm and available operations; do not assume every phone can keep an X25519 static key in hardware. Signing credentials, key-agreement keys and symmetric secrets are different objects.
- Do not expose stable device identities in every public packet. Identity privacy, admission controls and efficient peer lookup need a joint design.

For a relay serving several tenants, endpoint authorization and relay allocation policy are separate checks. A valid endpoint credential does not grant arbitrary transit rights, and a valid relay credential does not make the relay a trusted payload recipient.

## 3. Cryptographic candidates and performance

The comparison set is established constructions using **X25519 for key agreement**, **HKDF for a specified derivation schedule**, and **ChaCha20-Poly1305 or AES-GCM for AEAD**. X25519 is not a signature algorithm. Algorithm names do not establish an authenticated protocol or justify a custom combiner.

A suitable unchanged Noise pattern, TLS 1.3 through a maintained implementation, and an existing protected datagram/transport approach remain alternatives. In particular, choosing primitives does not authorize designing a new primitive, truncating tags, inventing a KDF or extracting raw secrets to bypass a library's invariants. The [OSS catalog](oss-candidates.md) contains candidates, not approved dependencies.

**AES-256 is not an automatic minimum for VLP.** The current TLS 1.3 specification requires implementation of its AES-128-GCM suite unless an application profile says otherwise, and also recommends AES-256-GCM and ChaCha20-Poly1305 suites. This is a standards observation, not a selection of VLP's profile or total security level. [E1, §9.1]

Proposed measurements after the applicable approval:

- Measure encryption and decryption on representative phones and servers using the selected provider and CPU features, rather than assume that either AES-GCM or ChaCha20-Poly1305 wins everywhere.
- Separate full/resumed handshake cost from steady-state payload throughput and per-packet processing.
- Include small packets, bidirectional traffic, CPU time, allocation/memory pressure, phone energy and thermal behavior, and end-to-end latency.
- Measure actual carrier overhead and trust-boundary layering separately. A primitive microbenchmark does not predict useful application goodput.
- Preserve the agreed security policy while measuring; reducing verification, nonce safety or authentication work is not a valid performance optimization.

No throughput, latency, battery, interoperability or security-audit result has been produced.

## 4. Forward secrecy, key update and compromise recovery

These properties must not be conflated:

| Property / operation | Meaning in the research model | Limit |
| --- | --- | --- |
| Forward secrecy with respect to long-term credentials | Past sessions remain confidential after a later credential compromise under the handshake's assumptions and appropriate secret erasure | Does not protect plaintext or live session secrets already taken from an endpoint |
| Traffic-key update | Advances the existing channel's traffic-secret state and limits use of one key | Does not inherently add a new secret unknown to someone who already has the current traffic secret |
| Recovery after compromise / PCS | Restores confidentiality under an explicitly stated compromise-and-recovery model | Needs a mechanism providing fresh secret contribution and valid authentication; continued endpoint control defeats the goal |
| Trust repair | Re-establishes which device/service credentials and enrollment authorities are acceptable | A new handshake with a compromised identity key does not repair trust |

TLS traffic-secret updates derive the next generation from the current secret. Noise provides a one-way rekey operation; its rekey does not reset its nonce counter. [E1, §7.2; E3, §11.3]

**Engineering implication:** an attacker holding the relevant current traffic-secret state can follow a deterministic sequence of future updates. Ordinary rekey is therefore not a claim of post-compromise recovery. A fresh authenticated exchange may help after a bounded transient session-secret exposure, but the result depends on which credentials, RNG state and endpoints remained trustworthy.

The recovery design should distinguish at least: one session-secret exposure; a stolen device identity key; a compromised server; and compromise of an enrollment/signing authority. Depending on that scope, recovery can require incident containment, device re-enrollment through an independent trusted path, credential and ticket revocation, and new sessions. Signing a replacement key with an already compromised key alone cannot establish that the attacker has lost access.

Avoid a time-only rekey rule. Packet/byte limits, authentication-failure limits, accepted key generations, loss/reordering behavior and secret erasure all require explicit treatment. No numeric VLP limits are set here.

## 5. Nonce and replay state across paths, processes and restores

QUIC derives a packet nonce using its packet number and IV. Noise's datagram use requires the receiver to track successfully received nonce values and reject repeats. These are source mechanisms with their own assumptions. [E2, §5.3; E3, §11.4]

For a potential native datagram construction, propose the following invariants for later specification review:

1. Every new AEAD encryption must satisfy the selected construction's nonce-uniqueness rules, even when plaintext is unchanged or only authenticated headers differ. Resending cached, byte-identical ciphertext is not a new encryption operation. Partition directions and independent protection contexts explicitly.
2. A network change, relay change, carrier switch or connection-ID change does not by itself permit a counter reset. Multiple paths or send workers sharing a key need one coordinated uniqueness scheme; independent counters need separately justified cryptographic domains.
3. Update replay state only after successful authentication. An unauthenticated far-ahead number must not advance the receive window. Bound work spent trying unknown generations or candidate keys.
4. Logical retransmission and repacketization preserve application delivery semantics while using safe record protection. Forwarding identical ciphertext is not a second encryption operation, but duplicate reception still must not cause duplicate application execution.
5. Treat process restart, phone process eviction, VM rollback, snapshot cloning and restore as separate lifecycle events. Restoring a secret together with an old counter can reproduce a prior key/nonce pair or accepted replay state.
6. The conservative candidate for a restored or uncertain live session is to discard it and establish a fresh authenticated session. Restored RNG state also needs attention: “new handshake” is insufficient if it reproduces old ephemeral secrets after cloning or rollback.
7. Do not make security depend on reliably erasing every historical memory snapshot. Define what can be persisted, which credentials authorize resumption, and how those credentials are invalidated.
8. Keep replay state for endpoint protection distinct from outer hop/carrier state. Neither a valid relay packet nor an accepted outer TLS record proves that the inner application operation is new.

A robust multi-node resumption design also needs explicit ownership of ticket keys, expiration and replay-relevant state. Session persistence is not currently selected as a feature.

## 6. Mobile migration, early data and downgrade policy

QUIC separates connection identifiers from peer addresses and uses path validation when an address changes. Reachability of a new address is not equivalent to a new device identity or a new permission grant. [E4, §§8–9]

For mobile VLP research, propose that authenticated identity and authorization survive a permitted path change, while per-path reachability, MTU, congestion state and resource budgets are re-evaluated. A push notification or reconnect trigger, if introduced later, does not authenticate the endpoint by itself.

**Proposed first implementation scope, subject to the gates: no early application operations.** No outbound connect, route allocation, relay allocation or application forwarding should occur from 0-RTT data. Resumption may still be evaluated separately. The current TLS specification explains that early data lacks a protocol-level forward-secrecy guarantee and can be replayed; the first payload in Noise IK also has weaker replay/recipient-compromise properties than the completed exchange. [E1, §§2.3, 8; E3, §7.7]

Proposed downgrade rules:

- Authenticate algorithm negotiation, version, endpoint identity and security-relevant capabilities in the selected protocol's transcript or specified binding.
- Treat crypto policy and privacy/path policy separately: a cryptographically strong direct path may still violate a policy requiring a relay or onion route.
- A blocked UDP path is not authority to disable certificate checks, replace pins, remove an inner channel, select an unapproved cipher or switch silently to a less private route.
- Carrier fallback is acceptable to investigate only where the same approved confidentiality, authentication and privacy constraints remain satisfied. Otherwise report unavailability or require an authorized policy change.
- Network observations must not rewrite the minimum security policy. Policy changes themselves require an authenticated authority and a reviewable lifecycle.

## 7. PQ status and handshake size

**The primary sources now include published RFCs.** NIST FIPS 203 standardizes ML-KEM. Informational RFC 9954 describes the TLS 1.3 hybrid framework; Standards Track RFC 10024 defines its ECDHE/ML-KEM groups. RFC 9846 explicitly obsoletes RFC 8446. Checked on 2026-10-19, these observations do not select a VLP library or establish compliance. [E1, Abstract; E5; E6; E7]

RFC 10024 gives these **key-exchange share sizes**, excluding the remainder of the TLS handshake and transport framing:

| Existing TLS group | Client share | Server share |
| --- | ---: | ---: |
| X25519MLKEM768 | 1,216 bytes | 1,120 bytes |
| SecP256r1MLKEM768 | 1,249 bytes | 1,153 bytes |
| SecP384r1MLKEM1024 | 1,665 bytes | 1,665 bytes |

RFC 10024's security analysis depends on the TLS message transcript and explicitly warns against assuming that a similar hybridization is secure in other protocols. RFC 9954 does not cover post-quantum authentication. [E6, §1.3; E7, §§4, 6]

**Engineering implications to validate:**

- A 1,216-byte share alone cannot fit in a 1,200-byte UDP payload. Complete messages add further overhead. This does not imply that every path has a 1,200-byte maximum: QUIC's 1,200-byte figure is a required supported minimum, not a universal maximum.
- Mature transport implementations can split handshake data according to their own protocol. A native VLP design must independently bound pre-authentication reassembly, retransmission work, amplification and memory; do not assume arbitrary IP fragmentation solves the problem.
- QUIC prohibits IP-layer fragmentation of its UDP datagrams and uses path-size constraints/discovery. Relay encapsulation further reduces the available inner budget; migration can change it. [E4, §14]
- A standardized KEM is not a certificate, signature, PSK or an authenticated VLP handshake. Establish the required confidentiality horizon and authentication threat before choosing a classical or hybrid candidate.
- Do not transfer a TLS hybrid combiner into a custom Noise or native UDP profile and claim the TLS analysis applies. That would be separate cryptographic composition work.
- Increased handshake size affects loss sensitivity, pre-authentication resource exposure and mobile reconnect cost. No measured VLP impact is yet available.

No experimental or new VLP group identifier is assigned here.

## 8. Onion, mix and exit visibility

Tor's primary design description distinguishes encrypted TLS channels from multi-hop circuits, with separately negotiated symmetric keys for circuit relays. The exit creates the onward connection to the target. This is useful evidence that hop channels and layered circuit protection serve different purposes. [E8]

**Implications for any VLP proposal:**

- Multi-hop carriage needs an explicit compromise/collusion model, identity and route-selection trust, hop-key separation, circuit lifetime, replay handling and resource limits. “Encrypt once per hop” is not a complete reviewed construction.
- Payload confidentiality and traffic anonymity are different claims. More encryption layers do not prove protection against timing/volume correlation, malicious relay selection or colluding observers.
- A mix mode would also need a separate traffic model, scheduling/cover-traffic policy and validation. No latency/anonymity guarantee follows from the label “mix”.
- If the final exit is the inner VLP endpoint, it receives the VLP plaintext. If that plaintext contains an independently authenticated application channel, such as HTTPS continuing to the actual destination, the exit does not thereby receive that application's plaintext. If the onward application is unencrypted, the exit and onward path can access its content.
- The exit can still learn routing information needed to reach the target and observe traffic characteristics. A phone-to-exit tunnel must not be described as endpoint protection to every external service.

A multi-hop or mix extension would need independent specialist review of the full construction and implementation. None has been designed, approved or audited here.

## 9. Traceability and evidence still required

Coverage below points to existing research topics in the [220-item register](../requirements/README.md). It does not close, renumber or replace their original titles.

| Question in this note | Existing topic IDs |
| --- | --- |
| Endpoint boundaries and channel composition | VLP-REQ-003, VLP-REQ-031, VLP-REQ-049, VLP-REQ-095, VLP-REQ-105, VLP-REQ-122 |
| Credentials, proof of possession and authentication policy | VLP-REQ-054, VLP-REQ-055, VLP-REQ-056, VLP-REQ-057, VLP-REQ-061, VLP-REQ-067, VLP-REQ-138 |
| Primitive/profile selection and domain separation | VLP-REQ-032, VLP-REQ-035, VLP-REQ-036, VLP-REQ-038, VLP-REQ-044, VLP-REQ-048, VLP-REQ-051 |
| Forward secrecy, key update and recovery | VLP-REQ-039, VLP-REQ-040, VLP-REQ-043, VLP-REQ-052, VLP-REQ-125, VLP-REQ-140, VLP-REQ-208 |
| Nonce/replay state, paths and restore | VLP-REQ-028, VLP-REQ-045, VLP-REQ-046, VLP-REQ-091, VLP-REQ-107, VLP-REQ-108, VLP-REQ-145 |
| Mobile identity and identifier privacy | VLP-REQ-026, VLP-REQ-089, VLP-REQ-111, VLP-REQ-128, VLP-REQ-129, VLP-REQ-135, VLP-REQ-155 |
| Negotiation, early data and downgrade | VLP-REQ-058, VLP-REQ-059, VLP-REQ-060, VLP-REQ-062, VLP-REQ-063, VLP-REQ-064, VLP-REQ-113, VLP-REQ-121, VLP-REQ-168 |
| PQ, MTU, overhead and performance | VLP-REQ-024, VLP-REQ-025, VLP-REQ-041, VLP-REQ-042, VLP-REQ-114, VLP-REQ-117, VLP-REQ-149, VLP-REQ-151, VLP-REQ-154, VLP-REQ-199 |
| Relays, metadata, onion/mix limits | VLP-REQ-050, VLP-REQ-086, VLP-REQ-087, VLP-REQ-126, VLP-REQ-127, VLP-REQ-133, VLP-REQ-216 |
| Required future analysis and specifications | VLP-REQ-187, VLP-REQ-189, VLP-REQ-191, VLP-REQ-200, VLP-REQ-202, VLP-REQ-205, VLP-REQ-207, VLP-REQ-215, VLP-REQ-220 |

Before specification admission, identify permitted plaintext recipients per use case, credential authorities and revocation behavior, the actual compromise model, minimum crypto/privacy policy and required confidentiality horizon. Compare existing transports against native UDP without assuming the latter wins.

After the applicable implementation approval, proposed validation should cover unauthorized routes/relay allocations, identity replacement, path change, duplicate operations, forged replay-window advancement, key-update loss/reordering, snapshot/RNG rollback, carrier-policy downgrade, PQ handshake resource exhaustion and per-device performance. Test scope must use controlled endpoints and synthetic data, bounded CPU/memory/traffic budgets, and predeclared acceptance criteria. No such execution is reported here.

## Primary sources actually reviewed

The E-labels are local to this note and do not modify the repository source register.

| ID | Primary source | Material reviewed |
| --- | --- | --- |
| E1 | [RFC 9846 — TLS 1.3](https://www.rfc-editor.org/info/rfc9846/) | Abstract and §§1, 2.2–2.3, 4.5, 4.7.3, 7.2, 8, 9.1; current base TLS specification and explicit obsolescence of RFC 8446 |
| E2 | [RFC 9001 — Using TLS to Secure QUIC](https://datatracker.ietf.org/doc/html/rfc9001) | §§4–6; handshake/record boundary, packet protection and key updates |
| E3 | [Noise Protocol Framework, revision 34](https://noiseprotocol.org/noise.html) | §§7.7, 9, 11.3–11.4, 13–14; key possession, PSKs, early-payload limitations, rekey and datagram replay responsibilities |
| E4 | [RFC 9000 — QUIC Transport](https://www.rfc-editor.org/rfc/rfc9000) | §§8–9, 14; path validation, migration, anti-amplification and datagram-size constraints |
| E5 | [NIST FIPS 203 — ML-KEM](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.203.pdf) | Official final PDF; standardized KEM scope. The CSRC landing page returned an access error during this read, so the NIST-hosted PDF was used |
| E6 | [RFC 9954 — Hybrid Key Exchange in TLS 1.3](https://www.rfc-editor.org/info/rfc9954/) | Scope, construction boundaries and exclusion of post-quantum authentication |
| E7 | [RFC 10024 — PQ/T Hybrid Key Agreement Mechanisms for TLS 1.3](https://www.rfc-editor.org/info/rfc10024/) | Published standard status, §§4 and 6; existing groups, share sizes and TLS-specific composition warning |
| E8 | [Tor specifications — A short introduction to Tor](https://spec.torproject.org/intro/index.html) | Distinction between TLS channels, layered circuits and an exit's onward connection; not evidence of VLP anonymity |

All candidate properties remain unproven for VLP. **Research Gate: NOT_EVALUATED; implementation approval remains separate.**

