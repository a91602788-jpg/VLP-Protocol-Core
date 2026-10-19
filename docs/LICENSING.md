# Licensing and provenance

## Original project materials

The foundation change includes the unmodified [Apache License 2.0](../LICENSE) for original project material. The license choice is presented to the repository maintainer in the foundation pull request. No existing upstream code is relicensed by that choice.

The authoritative license text controls. This page records the project's reuse workflow and is not an alternative license. See the [Apache Software Foundation license page](https://www.apache.org/licenses/LICENSE-2.0) and [GitHub's repository licensing guidance](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository).

## Before adopting an external component

For the exact proposed dependency, copied file, generated artifact, or vendored subtree, record:

1. Canonical upstream repository and the exact release, commit, and artifact identity.
2. Actual license files and any file-level exceptions at that revision.
3. Transitive dependencies, native bindings, generated code, bundled implementations, and their terms.
4. Required copyright notices, license copies, notices of modifications, and applicable source-distribution obligations.
5. The integration boundary: reference-only study, build-time tool, linked dependency, copied source, or separately distributed executable.
6. Compatibility review for the planned use and distribution model, including relevant patent provisions.
7. Maintenance and security evidence, unresolved concerns, alternatives, and the approval record.

Repository metadata and SPDX labels help discovery but do not replace reading the applicable terms. Do not infer that every file in a monorepo has the same license. A permissive top-level license does not settle the terms of transitive or bundled code.

## References and standards

Linking a protocol, paper, standard, or implementation is a research reference. Its source code and text retain their applicable terms. Use concise original summaries with source attribution. Review the relevant notices separately before copying code components or large excerpts from standards.

The [OSS catalog](research/oss-candidates.md) records candidates, not dependency adoption. The [source register](research/source-register.md) records evidence, not permission to incorporate every referenced artifact.

## Current inventory

- Adopted third-party runtime dependencies: **none**.
- Vendored third-party implementation source: **none**.
- Dependency lockfiles and release SBOM: **not applicable yet; no implementation or release artifact exists**.

Create the dependency inventory and preserve required upstream notices when dependencies are actually approved and introduced. Do not create a fictitious SBOM from a candidate list.

## Contributions

Contributors retain the rights they hold. This change introduces no CLA, copyright assignment, or DCO signing requirement. Contribution handling follows the repository license and [contribution guidelines](../CONTRIBUTING.md). Any additional contribution agreement requires a separate, explicit maintainer decision and clear communication.
