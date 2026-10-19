# Specification reservations

## Status

**No formal VLP specification is issued in this directory.** Research is open and the Research Gate has not been performed. The identifiers below are reserved so that the research package can refer to the intended outputs consistently.

Reservation does not allocate packet fields, codepoints, cryptographic suites, protocol versions, extension identifiers or implementation APIs. It does not imply that the proposed architecture has been accepted.

## Reserved documents

| Reserved identifier | Reserved title | Intended scope after Research Gate admission | Current state |
| --- | --- | --- | --- |
| **VLP-0001** | **Architecture** | Protocol goals and boundaries; seven-core responsibility model; endpoint and trust model; selected transport basis; session and channel semantics; control and Data Plane relationships; privacy, resource, failure and evolution requirements | Reserved; specification not authored |
| **VLP-0002** | **Packet Wire Format** | The precise encoding implied by the admitted architecture; framing and parsing rules; bounds; packet or message types; ordering and state dependencies; protection boundaries; extension and compatibility handling; malformed-input behaviour | Reserved; specification not authored |
| **VLP-0003** | **Handshake** | The admitted authentication and key-establishment construction; states and message sequence; identity and trust assumptions; transcript and negotiation binding; retries, timeouts, replay, downgrade and failure handling; permitted resumption behaviour | Reserved; specification not authored |

The eventual meaning of “Packet Wire Format” depends on the transport decision. A QUIC-based VLP would specify its own payload and channel formats without pretending to replace the QUIC packet specification. A native-UDP design would also require a complete VLP transport-packet contract. The title does not preselect either approach.

## Shared questions the three documents must resolve

The future specification set must agree on its states, negotiated parameters, security context, delivery semantics, identifiers, resource limits and failure outcomes. Architecture cannot promise properties absent from the wire format; a handshake cannot negotiate features whose behaviour is undefined; an encoding cannot introduce implicit state transitions absent from the architecture.

Each of the [220 requirements](../requirements/README.md) needs an explicit disposition and a traceable location, or a documented deferral with consequences and revisit criteria. The complete original requirement remains in [requirements.json](../requirements/requirements.json).

Cryptographic constructions and implementation languages are not selected here. Native UDP, Noise and Rust remain research candidates, not specification decisions.

## Prerequisites for authoring

Specification authoring follows a recorded Research Gate admission under the [decision process](../process/decision-process.md). That decision must identify its evidence, approved scope, unresolved issues, conditions and any limits on the work it permits.

Before that admission, design questions and alternatives belong in research notes. Proposals should remain clearly labelled and must not be promoted into normative protocol text, reserved numeric assignments, official compatibility claims, or conformance requirements.

## What follows authoring

VLP-0001, VLP-0002 and VLP-0003 undergo Specification Review as one consistent set. A favourable review permits an implementation-approval request within its recorded scope; it is not itself implementation approval.

There are currently no conformance vectors, interoperability results or implementation claims associated with these reservations. The [validation plan](../research/validation-plan.md) records future evidence needs without asserting that any check has run.
