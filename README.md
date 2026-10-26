# Nexus for Oracle Fusion Cloud · documentation

Nexus keeps Oracle Fusion Cloud environments in sync without re-keying. It finds what differs between two environments, lets the right people review and approve exactly those records, writes them into the target through Oracle's own import and REST interfaces, and reads the target back to prove the change landed. It covers configuration (Setup & Maintenance tasks) and master data (suppliers and lookups today).

> From "what changed?" to "it is live and verified" in one governed, auditable flow.

## Read the docs

| Page | What you will find |
|---|---|
| [Overview](docs/index.md) | The problem, the five-step flow, the three migration paths |
| [Feature tour](docs/features.md) | Registry, discovery, diff, review, approvals, execution, verification, security, and what is covered today |
| [Walkthrough](docs/walkthrough-suppliers.md) | Three suppliers moved between two development pods, step by step with screenshots |
| [Proven at scale](docs/scale.md) | A 44,000-supplier compare and deployment, with timings |
| [Getting started](docs/getting-started.md) | Run a proof of concept in one to two hours: Docker locally, hosted, or in your own cloud |
| [FAQ](docs/faq.md) | Credentials, failures, undo, databases, access control |

The same pages are published as a site at `https://nexus-for-fusion.github.io/docs/` (search and navigation included).

## Try it

A proof of concept needs two Oracle Fusion Cloud environments you may write to, an integration user in each, a machine with Docker, and a 30-day trial key. [Getting started](docs/getting-started.md) has the steps; write to hello@example.com for a key.

## About these docs

These pages describe the product at a high level and are written for application teams, release managers and system owners, not for developers of Nexus itself. The product source is not published here.

## Licence

Text and images in this repository are © the Nexus authors and are licensed under [CC BY-NC-ND 4.0](LICENSE.md): you may read and share them with attribution, not sell them or publish modified versions. Screenshots of Oracle Fusion Cloud data are illustrative and taken from development environments; supplier names and other identifying details in them are blurred or relabelled.

---

*Nexus is an independent product and is not affiliated with, endorsed by, or sponsored by Oracle. Oracle and Oracle Fusion Cloud are trademarks of Oracle Corporation and its affiliates.*
