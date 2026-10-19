# VLP Protocol Core

**An open research project for a new secure network protocol.**

[Русский](README.ru.md) · [Requirements](docs/requirements/README.md) · [Architecture](docs/architecture/engineering-cores.md) · [Research](docs/research/README.md) · [Contributing](CONTRIBUTING.md)

VLP explores a protocol with explicit delivery semantics, bounded resource use, authenticated connection management, and measurable traffic-observation resistance. The project is organized around seven engineering cores and a traceable register of 220 research and design topics.

## Project status

| Area | Current state |
| --- | --- |
| Lifecycle | Research and requirements organization |
| Research Gate | Not evaluated |
| Transport and cryptographic foundations | Candidates; no selection approved |
| VLP-0001 / VLP-0002 / VLP-0003 | Reserved specification identifiers |
| Protocol implementation | Not started; requires the recorded implementation approval |
| Protocol security audit, interoperability, performance | No results available |
| Wire version and releases | None assigned |

The repository currently contains project documentation and research records. It does not contain a runnable protocol, a finalized packet format, or deployment instructions. See the [machine-readable status](docs/project-status.json).

## What VLP is investigating

The central hypothesis is that delivery scheduling and traffic-shaping policies can be coordinated under explicit limits on delay, additional bytes, and computational work. That hypothesis must be compared with existing transports and independently layered shaping.

Streams, datagrams, migration, padding, and time-limited delivery are existing concepts. Combining them does not establish novelty. A native UDP transport, a protocol over an existing transport, and a narrower extension must all remain comparable until the Research Gate records the decision and evidence.

## Mobile, server, and relay scenarios

The [deployment proposal](docs/research/deployment-profiles.md) evaluates server-to-server, phone-to-server, phone-to-phone, and constrained-device communication. It separates the data service, route/trust profile, and carrier so their costs and guarantees can be reviewed explicitly.

Direct connections, opaque transit relays, layered multi-hop routes, and asynchronous mixing are research alternatives. Performance adaptation must respect the selected authentication and privacy policy. A change in reachability is not permission to weaken that policy. See the focused notes on [mobile endpoints](docs/research/mobile-endpoints.md), [endpoint security](docs/research/endpoint-security.md), and [routing and privacy](docs/research/routing-privacy.md).

## Seven engineering cores

| Core | Responsibility |
| --- | --- |
| **01 — Protocol Core** | Scope, semantics, roles, state machines, versions, and extension rules |
| **02 — Transport** | Delivery, loss recovery, flow control, congestion control, paths, and MTU |
| **03 — Cryptography** | Cryptographic profiles, key derivation, nonces, integrity, and key lifecycle |
| **04 — Handshake** | Trust establishment, authentication, parameter binding, and connection establishment |
| **05 — Camouflage** | Observable packet and traffic behavior within defined resource budgets |
| **06 — Data Plane** | Packet/frame processing, channels, multiplexing, buffers, and backpressure |
| **07 — Security** | Threat model, attack resistance, resource limits, and evidence requirements |

These are responsibility boundaries, not seven approved libraries, services, or repositories. Privacy, control-plane policy, reliability, performance, and protocol evolution cross those boundaries. The [core architecture document](docs/architecture/engineering-cores.md) describes interfaces and unresolved decisions.

## Start here

1. Read the [decision process](docs/process/decision-process.md): Research → Research Gate → specifications → Specification Review → Implementation Approval.
2. Find a stable identifier in the [220-item requirements register](docs/requirements/README.md).
3. Inspect the [primary-source register](docs/research/source-register.md) and [OSS candidate catalog](docs/research/oss-candidates.md).
4. Propose a bounded research question with evidence and acceptance criteria.
5. Record a decision only after its review; unresolved topics stay visible.

The first three specification identifiers are reserved for **VLP-0001 Architecture**, **VLP-0002 Packet Wire Format**, and **VLP-0003 Handshake**. Their [scope and entry criteria](docs/specifications/README.md) are documented; their technical contents are not approved.

## Reusing open source

Existing implementations can provide reusable components, comparison baselines, and interoperability tools. Every catalog entry is a **candidate, not an adopted dependency**. Before copying or integrating code, record the exact artifact/version, actual license files, transitive dependencies, attribution requirements, maintenance evidence, security review, and a decision explaining the integration boundary.

No third-party implementation is vendored by this foundation change. A project name in the catalog does not grant permission to relicense its code or imply that its security properties transfer to VLP. See [licensing and provenance](docs/LICENSING.md).

## Participate

Research findings, specification criticism, threat-model improvements, and corrections to evidence are welcome. Open a [research proposal](https://github.com/a91602788-jpg/VLP-Protocol-Core/issues/new?template=research-proposal.md) or use the [specification review template](https://github.com/a91602788-jpg/VLP-Protocol-Core/issues/new?template=specification-review.md) when the applicable review stage is open.

Please read [CONTRIBUTING](CONTRIBUTING.md), [GOVERNANCE](GOVERNANCE.md), and [SECURITY](SECURITY.md). English is the shared documentation language; Russian discussion and the original Russian requirements are welcome. No external review, benchmark, or security result should be claimed without a retrievable record.

## License

Original project material is offered under the [Apache License 2.0](LICENSE). Upstream projects, standards, and third-party material retain their own terms. The license selection is part of the foundation pull request for maintainer review; it does not relicense any upstream implementation.
