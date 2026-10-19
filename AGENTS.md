# Agent instructions for VLP Protocol Core

## Scope

Work only in this repository for VLP tasks. Follow the user's authorized scope and the recorded [decision process](docs/process/decision-process.md). Inspect the current branch and files before editing; preserve concurrent work and existing decisions.

## Stage discipline

The initial repository stage is research and documentation. Native UDP, Noise, Rust, and other catalog entries are candidates, not approved implementation choices. The three reserved specification identifiers do not mean that the specifications exist or have passed review.

Protocol runtime code, packet parsers, crypto integration, live listeners, prototypes, and packet-generating experiments require the recorded Implementation Approval after the preceding gates. Do not call implementation a research helper to bypass that order. Documentation corrections and authorized read-only research do not need an additional approval flow.

## Evidence and requirements

- Preserve VLP-REQ-001 through VLP-REQ-220 and their original Russian titles.
- Keep the English display register and JSON consistent when updating requirement records.
- Record sources, unresolved limitations, and the actual status of decisions and validation.
- Never fabricate test, benchmark, audit, compatibility, deployment, or gate results.
- Reserve PASS / CONDITIONAL PASS / FAIL for a performed Research Gate or Specification Review with a stated revision, evidence, scope, and permitted next step. Describe ordinary documentation checks by what was checked and what was found.

## Security and provenance

Do not store real keys, credentials, private traffic captures, personal data, or deployment secrets. Use synthetic values in any later approved vectors. Keep authorization, ownership, routing policy, and limits on the enforcing peer. Preserve nonce uniqueness and replay protection in any future approved implementation.

Before importing code or adding dependencies, follow [licensing and provenance](docs/LICENSING.md). Do not replace vetted cryptographic primitives with new designs or infer composition security from a primitive's name.

## Changes and reporting

Use focused changes and explicit file paths; do not use `git add .`, force-push shared history, or mix unrelated projects. Do not publish releases, deploy, merge a pull request, request reviewers, or send messages unless the active task authorizes that action. Report what changed, which checks actually ran, their findings, and remaining risks. Give a gate outcome only when the corresponding gate or specification review was actually performed.
