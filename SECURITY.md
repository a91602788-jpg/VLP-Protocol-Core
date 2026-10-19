# Security policy

## Project stage

VLP Protocol Core is at the research and specification preparation stage. The repository does not currently provide a protocol implementation or a supported production release. Research notes, candidate designs, and references to established cryptographic standards do not establish that VLP is secure, resistant to traffic analysis, or ready for deployment.

Security review includes design defects and unsafe claims in the documentation, as well as implementation defects if implementation is authorized later. There is no supported-version or remediation-time commitment at this stage.

## Report a vulnerability privately

If GitHub private vulnerability reporting is enabled for this repository, use:

[Report a vulnerability privately](https://github.com/a91602788-jpg/VLP-Protocol-Core/security/advisories/new)

The presence of this link does not confirm that private reporting is enabled or available to you. Its availability has not been verified as part of this repository foundation.

If the private form is unavailable, open a public issue containing only a request for a private contact channel, for example:

> Please provide a private channel for a security report. I will share the details there.

Do not include the suspected weakness, affected component, exploit, packet capture, credentials, or impact details in that public request. Wait until the maintainer provides a private channel before sending the report. The current maintainer account is listed in [GOVERNANCE.md](GOVERNANCE.md).

## What to include through the private channel

- The affected document, component, and commit or version, if known.
- The security property or assumption that appears to fail.
- A minimal reproduction or a precise description of the design issue.
- The required attacker capabilities and the observed or reasoned impact.
- Sanitized evidence, clearly distinguishing observations from hypotheses.
- Any disclosure coordination needs and a way to continue the discussion.

Remove secrets, personal data, and unrelated third-party information. Report only the evidence necessary to understand the issue.

## Research boundaries

Use systems and data you own or have permission to examine. Keep experiments within the authorized scope; a public repository does not authorize testing against someone else's infrastructure. Prefer isolated, reproducible cases that minimize traffic and resource consumption.

Do not publish a proof of concept or sensitive finding through a normal issue, pull request, commit, or discussion while requesting private coordination. Public corrections to general documentation that do not expose a vulnerability can follow the usual contribution process.

## Handling and disclosure

The maintainer coordinates scope, assessment, remediation options, and disclosure with the reporter through the available private channel. A response date, fix deadline, reward, or external audit is not promised by this policy. Public advisories and documentation corrections should describe what was established, the affected revisions, available mitigations, and remaining uncertainty.

Security findings can reopen a research or specification decision under the [decision process](docs/process/decision-process.md). A prior process decision is not a guarantee that a design has no weaknesses.
