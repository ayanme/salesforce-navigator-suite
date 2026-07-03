# Changelog

All notable changes to the Salesforce Navigator Suite are documented here.
This project uses [Semantic Versioning](https://semver.org/).

---

## [1.2.0] — 2026-07-03

### Evidence Philosophy and Trust Model

Added a repository-wide evidence philosophy (PROJECT_STANDARD.md §19) that formalizes the trust model across all Navigators.

- **§19 Evidence Philosophy and Trust Model** — canonical definition of the evidence gate (approved source + verified evidence = permission to claim), three evidence states, no cross-source substitution, verification gate, evidence-before-synthesis requirement, honest uncertainty preference, and evidence hierarchy.
- **§15 Reasoning Vocabulary** — added **Not Verified** label for retrieval failures (JavaScript-rendered shell, timeout, unavailable page, empty response). Updated **Not Documented** definition to apply only when approved sources were successfully consulted and the claim is absent. These two states must never be conflated.
- **§18 Failure Behavior** — updated to use **Not Verified** (not **Not Documented**) for retrieval failures. Added reference to §19 for the full evidence philosophy.
- **Repository Standards** (all 8 Navigator files) — updated portability summary to include the three evidence states, evidence gate, and no-substitution rule so Navigators function correctly when distributed independently.
- **Research Methodology** (all 8 Navigator files) — reverted to Navigator-specific workflow only. Repository-wide evidence philosophy now lives canonically in PROJECT_STANDARD.md §19.
- **Failure Handling** (all 8 Navigator files) — reverted to Navigator-specific failure message only. Repository-wide failure philosophy now lives canonically in PROJECT_STANDARD.md §18 and §19.
- `standard_version` bumped to 1.2.0 across all 8 Navigator files.

### Repository Documentation

- **`tests/TRIGGER_TESTS.md`** — Guardrail Tests section added: eight fetch-failure test cases (one per Navigator) and a source substitution table documenting forbidden substitution sources per Navigator. File title and subtitle updated to reflect both routing and evidence validation.
- **`CONTRIBUTING.md`** — contributor workflow updated to require both routing tests and guardrail tests: Step 5 expanded to cover both test types, Validation Checklist updated with evidence model items (correct evidence state implementation, Not Verified vs Not Documented distinction, no model memory fallback), Pull Request Expectations updated, Product Specialist Step 6 updated. Duplicate CHANGELOG step removed.
- **`docs/ARCHITECTURE.md`** — inheritance diagram updated to include evidence philosophy and trust model as a first-class PROJECT_STANDARD.md responsibility. Portability layer description updated to reflect the evidence trust model as part of what Repository Standards carries. Repository structure comment for TRIGGER_TESTS.md updated.
- **`docs/SKILL_ROUTING_RESEARCH.md`** — Future Research section extended with an evidence-grounding research item identifying post-invocation answer quality as a second independent research area. Conclusion extended to acknowledge that routing quality and evidence-grounding quality are separate concerns requiring separate investigation.

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
