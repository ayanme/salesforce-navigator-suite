# Changelog

All notable changes to the Salesforce Navigator Suite are documented here.
This project uses [Semantic Versioning](https://semver.org/).

---

## [1.0.0] — 2026-06-30

Initial public release.

### Skills

Eight specialist Claude skills, each scoped to a single Salesforce documentation domain:

- **Salesforce Help Navigator** — configuration, setup, permissions, licensing, editions, and feature behavior sourced from help.salesforce.com and admin.salesforce.com
- **Salesforce Developer Navigator** — Apex, LWC, APIs, SDKs, CLI, and developer release notes sourced from developer.salesforce.com
- **Salesforce Architect Navigator** — integration patterns, reference architectures, scalability, and enterprise trade-offs sourced from architect.salesforce.com
- **Salesforce Release Notes Navigator** — new features, GA/Beta/Pilot status, deprecations, and breaking changes across all Salesforce products
- **Salesforce Trailhead Navigator** — modules, trails, superbadges, and certification preparation sourced from trailhead.salesforce.com
- **Salesforce Marketing Cloud Developer Navigator** — Marketing Cloud REST/SOAP APIs, AMPscript, SSJS, Journey Builder APIs, and Account Engagement developer documentation
- **Salesforce Marketing Cloud MobilePush Navigator** — MobilePush SDK, Unified Mobile SDK, device registration, push notifications, and in-app engagement
- **Salesforce Platform Mobile Navigator** — Salesforce Platform Mobile SDK, SmartStore, MobileSync, OAuth flows, and offline data access

### Repository

- `PROJECT_STANDARD.md` — single source of truth for repository governance: skill template, writing standards, documentation trust policy, ownership matrix, routing rules, cross-domain routing assignments, vocabulary, versioning policy, and inheritance model
- `docs/ARCHITECTURE.md` — architecture overview covering the inheritance model, ownership model, routing principles, portability layer, and repository structure
- `docs/SKILL_ROUTING_RESEARCH.md` — engineering research document covering the routing experiment methodology, validated findings, and description design principles behind the Navigator description format
- `CONTRIBUTING.md` — full contribution guide covering Navigator creation, documentation ownership decisions, description design, naming conventions, Navigator types, cross-domain routing transitions, and validation checklist
- `tests/TRIGGER_TESTS.md` — routing validation tests for all 8 Navigators with should/should-not-trigger examples, edge cases, and cross-domain product routing tables

### Architecture

- **Documentation-domain routing model** — each Navigator owns a documentation type (configuration, developer APIs, architecture, learning, release notes), not a product. The same Salesforce product can appear across multiple Navigators; the user's question determines which Navigator responds.
- **Exclusive ownership** — each documentation domain has exactly one Navigator owner; no routing ambiguity by design
- **Cross-domain routing** — Agentforce, Data Cloud, Marketing Cloud Personalization, CRM Analytics, and MuleSoft span multiple documentation domains and are routed through the relevant Domain Navigators by documentation type
- **Portability layer** — each Navigator includes a compressed Repository Standards section so it functions correctly when installed as a standalone skill outside this repository
- **Validated description design** — Navigator descriptions are written as intent classifiers using natural language trigger phrases, explicit cross-cutting product ownership, and bidirectional boundary signals at high-risk domain edges, based on routing experiments documented in `docs/SKILL_ROUTING_RESEARCH.md`
