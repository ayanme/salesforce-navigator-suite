# Salesforce Navigator Suite

Navigate Salesforce documentation with specialized Claude Skills.

![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg) ![Claude Skills](https://img.shields.io/badge/Claude-Skills-blueviolet.svg) ![Navigators](https://img.shields.io/badge/Navigators-8-0176d3.svg) ![Sources](https://img.shields.io/badge/Sources-Official%20Salesforce-00A1E0.svg)

A suite of specialized Claude Skills for researching Salesforce using official documentation. Each Navigator is scoped to a single Salesforce documentation domain, prioritizing official Salesforce documentation over community content and model memory.

Built for Salesforce administrators, consultants, architects, and developers who need fast, accurate, source-cited answers directly from official Salesforce documentation.

> *This project is not affiliated with or endorsed by Salesforce, Inc. "Salesforce" is a registered trademark of Salesforce, Inc.*

---

## How It Works

Salesforce documentation is spread across multiple official properties: help.salesforce.com, developer.salesforce.com, architect.salesforce.com, trailhead.salesforce.com, and product-specific release notes. Each Navigator in this suite is scoped to one of those properties and is designed to become exceptionally accurate within that domain rather than attempting to answer every Salesforce question.

**Routing is organized by documentation domain, not Salesforce product.** A question about Agentforce configuration routes to the Help Navigator because the answer lives on help.salesforce.com. A question about the Agentforce developer API routes to the Developer Navigator because the answer lives on developer.salesforce.com. The product name in the question does not determine which Navigator responds — the documentation that would answer the question does.

Navigator descriptions were refined through iterative routing experiments to function as intent classifiers rather than capability summaries. The methodology and findings are documented in [`docs/SKILL_ROUTING_RESEARCH.md`](docs/SKILL_ROUTING_RESEARCH.md).

---

## Navigator Overview

| Navigator | Documentation Focus | Example Questions |
|---|---|---|
| [Help Navigator](skills/salesforce-help-navigator/) | Configuration & Administration | "How do I configure permission sets?" "What editions include this feature?" "How do I set up MFA?" |
| [Developer Navigator](skills/salesforce-developer-navigator/) | APIs, SDKs & Code | "How do I write an Apex trigger?" "What are the REST API limits?" "How do I use the Bulk API?" |
| [Architect Navigator](skills/salesforce-architect-navigator/) | Architecture & Design | "When should I use Platform Events vs CDC?" "How do I design a multi-org architecture?" |
| [Release Notes Navigator](skills/salesforce-release-notes-navigator/) | Product Releases | "What's new in Spring '25?" "Is this feature GA or Beta?" "What was deprecated?" |
| [Trailhead Navigator](skills/salesforce-trailhead-navigator/) | Learning & Certification | "What trail teaches Salesforce Flow?" "How do I prepare for the Admin exam?" |
| [MC Developer Navigator](skills/salesforce-marketing-cloud-developer-navigator/) | Marketing Cloud APIs & Scripting | "How do I authenticate to the MC REST API?" "How do I write AMPscript?" |
| [MC MobilePush Navigator](skills/salesforce-marketing-cloud-mobilepush-navigator/) | MobilePush SDK | "How do I register a device for push notifications?" "How do I set a Contact Key in the SDK?" |
| [Platform Mobile Navigator](skills/salesforce-platform-mobile-navigator/) | Salesforce Mobile SDK | "How do I implement SmartStore offline storage?" "How do I set up OAuth for a mobile app?" |

> **Products without a dedicated Navigator** — Agentforce, Data Cloud, Marketing Cloud Personalization, CRM Analytics, and MuleSoft do not yet have dedicated Navigators. Questions about these products are routed through existing Domain Navigators based on documentation type (configuration → Help Navigator, APIs → Developer Navigator, architecture → Architect Navigator, etc.). See [PROJECT_STANDARD.md §7](PROJECT_STANDARD.md) for the full interim routing table.

---

## Compatibility

Claude Skills require the **Claude desktop app**. Skill support varies by plan and region. Before installing, verify that your Claude plan and application version support custom Skills at [claude.ai](https://claude.ai).

---

## Installation

### Option 1 — Install an Individual Navigator

Use this when you only need one documentation domain.

1. Download or clone this repository
2. Open **Claude Desktop → Settings → Capabilities → Skills**
3. Click **Add Skill** and point to the skill directory (e.g. `skills/salesforce-help-navigator/`)

You can also zip the skill directory as a `.skill` file and add it via **Add Skill**.

### Option 2 — Install the Full Suite

Use this when you want the complete routing architecture with all 8 Navigators working together.

1. Clone this repository
2. Open **Claude Desktop → Settings → Capabilities → Skills**
3. Add each directory under `skills/` as a separate skill

Each Navigator operates independently. The suite is designed so Navigators complement each other — when a question falls outside one Navigator's scope, it identifies which Navigator to use instead.

> **Packaged releases** — Pre-packaged `.skill` files for each Navigator are planned for future releases. Until then, install directly from the source directories above.

---

## Design Principles

All Navigators follow the [Project Standard](PROJECT_STANDARD.md):

- **Documentation-domain routing, not product routing** — each Navigator owns a documentation type (configuration, developer APIs, architecture, learning, release notes), not a product. The same Salesforce product can appear across multiple Navigators depending on what the user is asking. Routing is determined by the documentation that would answer the question, not the product name in the question.
- **Accuracy over completeness** — never invent information to fill gaps
- **Approved sources only** — each Navigator has a strict, explicit allowlist
- **Source-cited answers** — every claim references an official Salesforce URL
- **Version-aware** — GA vs Beta vs Pilot always identified
- **Clear failure handling** — out-of-scope questions are routed to the correct Navigator

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for the full contribution guide, including how to create new Navigators, the description design methodology, and the process for retiring interim ownership.

---

## Roadmap

See [ROADMAP.md](ROADMAP.md) for planned V2 Navigators including dedicated skills for Agentforce, Data Cloud, Marketing Cloud Personalization, CRM Analytics, and MuleSoft.

---

## License

MIT — see [LICENSE](LICENSE)
