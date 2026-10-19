# VLP: OSS candidates and protocol baselines

[Подробный каталог на русском](oss-candidates.ru.md) · [Machine-readable catalog](oss-candidates.json)

Research date: **2026-10-19**. Repository: [VLP-Protocol-Core](https://github.com/a91602788-jpg/VLP-Protocol-Core).

**Research Gate: NOT_EVALUATED. All 16 candidates: NOT_ADOPTED.** Implementation approval is a separate decision after research and specification review. This catalog records possible building blocks and existing designs; it does not select runtime dependencies or establish protocol novelty or security.

## Evidence and revision semantics

The research used the GitHub plugin to read repository metadata, the observed default-branch commit, and actual LICENSE, component manifests and technical documentation at that exact commit. Primary protocol documents were also opened. The detailed [Russian catalog](oss-candidates.ru.md) and [JSON](oss-candidates.json) retain file URLs, complete commit SHAs, Git blob SHAs, observations and component-specific risks. JSON descriptions remain in Russian, explicitly marked by `description_language: "ru"`.

An **observed commit is an evidence snapshot, not a dependency pin**, release approval or signature-verification result. A version string in a development branch does not establish the release to adopt. No runtime code, dependency manifests, lockfile, vendored source or SBOM was created for these candidates. Builds, benchmarks, interoperability tests, transitive dependency audits and security assessments were not performed.

License observations concern the specific upstream files linked below and in the detailed catalog. They are not blanket legal conclusions about a complete build, modifications, distribution or compatibility with VLP's proposed license. License/compatibility, maintenance/security, target-platform and release reviews are required before adoption. Upstream licenses are not changed by VLP's license.

## Candidates

“Reuse candidate” means a component worth evaluating, subject to review. “Reference” is the current architectural classification, not a claim that its license prohibits every possible reuse. Every row remains **NOT_ADOPTED**.

| ID | Candidate | Proposed role | Classification | Observed license / evidence | Observed commit |
| --- | --- | --- | --- | --- | --- |
| OSS-001 | [snow](https://github.com/mcginty/snow) | Unmodified Noise handshake candidate for a future Rust core; not a UDP transport. | Reuse candidate | [Apache-2.0 OR MIT](https://github.com/mcginty/snow/blob/8ac60f51cfe3e010c84f0a454cc575ad9204fa12/Cargo.toml) | [8ac60f51cfe3](https://github.com/mcginty/snow/commit/8ac60f51cfe3e010c84f0a454cc575ad9204fa12) |
| OSS-002 | [RustCrypto AEADs: chacha20poly1305, aes-gcm](https://github.com/RustCrypto/AEADs) | AEAD primitives: chacha20poly1305 and aes-gcm, when required by the selected record layer/provider. | Reuse candidate | [Apache-2.0 OR MIT](https://github.com/RustCrypto/AEADs/blob/f90367cf07286ab5db652970e8268fbeab62a682/chacha20poly1305/Cargo.toml) | [f90367cf0728](https://github.com/RustCrypto/AEADs/commit/f90367cf07286ab5db652970e8268fbeab62a682) |
| OSS-003 | [RustCrypto hkdf](https://github.com/RustCrypto/KDFs) | HKDF implementation for a specified key schedule; not the key-schedule design itself. | Reuse candidate | [MIT OR Apache-2.0](https://github.com/RustCrypto/KDFs/blob/19a0df65a558feefed0722dd0de73ef4b966d79f/hkdf/Cargo.toml) | [19a0df65a558](https://github.com/RustCrypto/KDFs/commit/19a0df65a558feefed0722dd0de73ef4b966d79f) |
| OSS-004 | [x25519-dalek](https://github.com/dalek-cryptography/curve25519-dalek) | X25519 Diffie–Hellman key agreement; not digital signatures. | Reuse candidate | [BSD-3-Clause](https://github.com/dalek-cryptography/curve25519-dalek/blob/97a020d185970839ed1d3f3a5c22aca816631786/x25519-dalek/Cargo.toml) | [97a020d18597](https://github.com/dalek-cryptography/curve25519-dalek/commit/97a020d185970839ed1d3f3a5c22aca816631786) |
| OSS-005 | [rustls](https://github.com/rustls/rustls) | TLS carrier / QUIC integration and a TLS 1.3 comparison architecture. | Reuse candidate | [Apache-2.0 OR ISC OR MIT](https://github.com/rustls/rustls/blob/bb2165fa87ef23fb7d12a28c086f078b4f5d412a/LICENSE) | [bb2165fa87ef](https://github.com/rustls/rustls/commit/bb2165fa87ef23fb7d12a28c086f078b4f5d412a) |
| OSS-006 | [Quinn](https://github.com/quinn-rs/quinn) | QUIC carrier or baseline implementation; not a new native UDP core. | Reuse candidate | [MIT OR Apache-2.0](https://github.com/quinn-rs/quinn/blob/ecc0dcfdeaec996d276da31d836f965753b66ea4/Cargo.toml) | [ecc0dcfdeaec](https://github.com/quinn-rs/quinn/commit/ecc0dcfdeaec996d276da31d836f965753b66ea4) |
| OSS-007 | [quiche](https://github.com/cloudflare/quiche) | Alternative QUIC / HTTP/3 carrier and implementation baseline. | Reuse candidate | [BSD-2-Clause](https://github.com/cloudflare/quiche/blob/acf560f2e4a3d9254a1b668a50af0e114c84fe6f/COPYING) | [acf560f2e4a3](https://github.com/cloudflare/quiche/commit/acf560f2e4a3d9254a1b668a50af0e114c84fe6f) |
| OSS-008 | [s2n-quic](https://github.com/aws/s2n-quic) | Alternative QUIC carrier and transport-behavior baseline. | Reuse candidate | [Apache-2.0](https://github.com/aws/s2n-quic/blob/8c1fca6a3e3861b5fc6c570e384cc454fbbde8ea/LICENSE) | [8c1fca6a3e38](https://github.com/aws/s2n-quic/commit/8c1fca6a3e3861b5fc6c570e384cc454fbbde8ea) |
| OSS-009 | [Pion ICE](https://github.com/pion/ice) | Optional ICE traversal service or interoperability harness in Go. | Reuse candidate | [MIT](https://github.com/pion/ice/blob/5fdc5b169d4a06927409f01544fe38f8b3eecd3a/LICENSE) | [5fdc5b169d4a](https://github.com/pion/ice/commit/5fdc5b169d4a06927409f01544fe38f8b3eecd3a) |
| OSS-010 | [Pion STUN](https://github.com/pion/stun) | Optional STUN service / traversal harness in Go. | Reuse candidate | [MIT](https://github.com/pion/stun/blob/d39c70b1e859fabb0e3f937e94d3c7e25fe56c1c/LICENSE) | [d39c70b1e859](https://github.com/pion/stun/commit/d39c70b1e859fabb0e3f937e94d3c7e25fe56c1c) |
| OSS-011 | [Pion TURN](https://github.com/pion/turn) | Authorized TURN relay or controlled interoperability harness in Go. | Reuse candidate | [MIT](https://github.com/pion/turn/blob/b1bcca91802dffac8070b12ce0bee5bf244ffef1/LICENSE) | [b1bcca91802d](https://github.com/pion/turn/commit/b1bcca91802dffac8070b12ce0bee5bf244ffef1) |
| OSS-012 | [liboqs](https://github.com/open-quantum-safe/liboqs) | Isolated PQ algorithm and handshake-size experiments only. | Experimental benchmark only | [MIT in general; component-specific exceptions](https://github.com/open-quantum-safe/liboqs/blob/fd44469daeffe6b28f031f54f9bb66cbae69a572/LICENSE.txt) | [fd44469daeff](https://github.com/open-quantum-safe/liboqs/commit/fd44469daeffe6b28f031f54f9bb66cbae69a572) |
| OSS-013 | [Xray-core / VLESS reference](https://github.com/XTLS/Xray-core) | Existing proxy / transport boundaries and VLESS reference. | Reference | [MPL-2.0](https://github.com/XTLS/Xray-core/blob/92ccc939aaf4f8965f369cf0b142e005aeaa11d5/LICENSE) | [92ccc939aaf4](https://github.com/XTLS/Xray-core/commit/92ccc939aaf4f8965f369cf0b142e005aeaa11d5) |
| OSS-014 | [Hysteria 2](https://github.com/HyNetworks/hysteria) | QUIC-based proxy reference; possible selective component reuse after review. | Reference / selective reuse | [MIT](https://github.com/HyNetworks/hysteria/blob/ca8fbd874fd6ca82413948de6dc5924405e103e1/LICENSE.md) | [ca8fbd874fd6](https://github.com/HyNetworks/hysteria/commit/ca8fbd874fd6ca82413948de6dc5924405e103e1) |
| OSS-015 | [AmneziaWG Go](https://github.com/amnezia-vpn/amneziawg-go) | WireGuard-Go modifications, obfuscation and userspace integration reference. | Reference / selective reuse | [MIT](https://github.com/amnezia-vpn/amneziawg-go/blob/b5928efb6ca19f0153958460c3d141f04abc5c2e/LICENSE) | [b5928efb6ca1](https://github.com/amnezia-vpn/amneziawg-go/commit/b5928efb6ca19f0153958460c3d141f04abc5c2e) |
| OSS-016 | [wireguard-go](https://github.com/WireGuard/wireguard-go) | Userspace WireGuard and platform integration reference. | Reference / selective reuse | [MIT](https://github.com/WireGuard/wireguard-go/blob/2631ce99a06f27120d581611cf125d68bc6aa565/LICENSE) | [2631ce99a06f](https://github.com/WireGuard/wireguard-go/commit/2631ce99a06f27120d581611cf125d68bc6aa565) |

## Material findings and integration risks

- **Snow:** the observed README states that the library has not received a formal audit. VLP must still specify framing, replay handling, state transitions, transcript binding and key updates. Do not automatically enable experimental features or reconstruct a second handshake from primitive crates when a selected provider already handles it.
- **Cryptographic primitives:** AEAD, HKDF and X25519 do not independently provide the complete authenticated protocol, server-side authorization or replay protection. VLP must define nonce uniqueness, key separation, authenticated fields and usage limits. X25519 is key agreement, not a signature algorithm.
- **rustls:** the observed component manifest contains `0.24.0-dev.2`. Development HEAD is not an approved runtime version. TLS over a custom unreliable packet layer requires a specified integration; DTLS 1.3 belongs in the comparison.
- **Quinn:** the observed README lists MSRV `1.80.0`, while the workspace manifest lists `1.88.0`. Resolve this discrepancy against the particular release before adoption. Quinn, quiche and s2n-quic are alternative QUIC stacks. Specify who owns retransmission, congestion control, pacing and flow control to avoid conflicting nested mechanisms; distinguish reliable streams from datagrams.
- **Pion ICE/STUN/TURN:** these are Go components, not immediate Rust dependencies. A process/runtime boundary and an approved traversal use case are needed. P2P is not an assumed requirement. Relay authentication, destination permissions, allocation lifetimes and resource quotas must remain server-side.
- **liboqs:** upstream recommends **against relying on the library in production or to protect sensitive data** and positions it for research/prototyping. This is an upstream recommendation, not a legal prohibition. It is listed only for possible isolated experiments after lab approval. Its root license also identifies component-specific license exceptions. Adding a KEM does not establish a secure authenticated hybrid handshake.
- **Xray-core:** the observed root license is MPL-2.0. Any later file reuse requires a specific analysis of covered files, changes, notices and distribution. Do not silently relicense upstream code under VLP's proposed Apache-2.0. The observed `go.mod` contains `go 1.27`; actual release/toolchain compatibility remains unverified.
- **Hysteria:** the historical `apernet/hysteria` API endpoint returned `Moved Permanently`; the canonical repository is now [HyNetworks/hysteria](https://github.com/HyNetworks/hysteria), repository ID `257434373`. The observed Go module paths still use `github.com/apernet/hysteria/...`. `PROTOCOL.md` requires QUIC and its DATAGRAM extension; reusing Hysteria core would retain those architectural assumptions. A MIT root license does not settle the license profile of every core, extras, app or transitive component.
- **AmneziaWG / WireGuard:** the inspected MIT licenses belong specifically to `amneziawg-go` and `wireguard-go`; they must not be generalized to all clients, kernel code, tools or platform modules. The GitHub WireGuard repository identifies itself as a mirror of [the official upstream](https://git.zx2c4.com/wireguard-go/). Its recorded mirror SHA does not assert that every upstream ref was compared.
- **Camouflage and novelty:** upstream performance or detection-resistance claims are not VLP test results. A fork, a packet-header change or a QUIC wrapper does not by itself establish a new protocol or traffic indistinguishability.

The [Russian candidate cards](oss-candidates.ru.md#карточки-кандидатов) preserve the complete per-component findings and source links; the [JSON](oss-candidates.json) carries the same evidence with stable IDs.

## Protocol baselines

These are comparison references, **not automatically adopted normative requirements for VLP**. Referencing a standard does not settle the terms for copying its text or code components. All sources below were observed on 2026-10-19; adoption and implementation remain separate.

| ID | Primary source | Observed document / revision | Research purpose |
| --- | --- | --- | --- |
| BASE-001 | [Noise Protocol Framework](https://noiseprotocol.org/noise.html) | Revision 34, 2018-07-11; upstream page labels it official/unstable. | Authenticated key exchange and transcript binding; Noise does not specify the complete VLP UDP transport. |
| BASE-002 | [RFC 8446 — TLS 1.3](https://www.rfc-editor.org/rfc/rfc8446) | RFC 8446 | Handshake, key schedule, certificate authentication and early-data limitations. |
| BASE-003 | [RFC 9147 — DTLS 1.3](https://datatracker.ietf.org/doc/html/rfc9147) | RFC 9147 | Datagram channel baseline: record epochs, replay handling and handshake retransmission. |
| BASE-004 | [RFC 9000 — QUIC Transport](https://www.rfc-editor.org/rfc/rfc9000) | RFC 9000 | Packet numbers, streams, migration, path validation and amplification limits. |
| BASE-005 | [RFC 9001 — Using TLS to Secure QUIC](https://datatracker.ietf.org/doc/html/rfc9001) | RFC 9001 | TLS/QUIC integration; not TLS records sent over arbitrary unreliable UDP. |
| BASE-006 | [RFC 9002 — QUIC Loss Detection and Congestion Control](https://www.rfc-editor.org/rfc/rfc9002) | RFC 9002 | Loss recovery, RTT/PTO, congestion control and logical delivery versus packet transmission. |
| BASE-007 | [RFC 9221 — QUIC DATAGRAM](https://www.rfc-editor.org/rfc/rfc9221) | RFC 9221 | Unreliable messages versus reliable streams in a QUIC carrier. |
| BASE-008 | [RFC 8445 — ICE](https://www.rfc-editor.org/rfc/rfc8445) | RFC 8445 | NAT traversal if a separate P2P use case is approved. |
| BASE-009 | [RFC 8489 — STUN](https://www.rfc-editor.org/rfc/rfc8489) | RFC 8489 | STUN transactions; not VLP data-plane encryption or authentication. |
| BASE-010 | [RFC 8656 — TURN](https://www.rfc-editor.org/rfc/rfc8656) | RFC 8656 | Relay allocations, permissions and lifetimes if relay functionality is approved. |
| BASE-011 | [NIST FIPS 203 — ML-KEM](https://csrc.nist.gov/pubs/fips/203/final) | FIPS 203, final publication 2024-08-13; no VLP profile selected. | Standardized KEM reference for PQ research; not a complete authenticated hybrid handshake. |
| BASE-012 | [WireGuard — Protocol & Cryptography](https://www.wireguard.com/protocol/) | Web page observed on 2026-10-19; no immutable revision supplied. | Primary WireGuard handshake and data-plane reference. |

## Before adoption

1. Approve the component's architectural role and establish that it does not duplicate another layer's responsibilities.
2. Review the selected version's licenses, notices, component exceptions and transitive dependencies against the intended modifications and distribution.
3. Review release provenance, maintenance policy, advisories, known limitations, target platforms, toolchain and selected crypto-provider features.
4. Obtain implementation approval after research and specification review. Only then select an actual dependency release/revision and produce manifests, lockfiles and an SBOM from the real build.
5. Run approved interoperability and security/resource-bound checks; upstream reputation and this catalog do not establish VLP security.

**Research Gate remains NOT_EVALUATED. No candidate has been adopted or approved for execution.**
