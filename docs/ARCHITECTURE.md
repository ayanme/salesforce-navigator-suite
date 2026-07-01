# Salesforce Navigator Suite — Architecture

This document explains the design of the Salesforce Navigator Suite for new contributors and maintainers. For authoritative governance rules, see [PROJECT_STANDARD.md](../PROJECT_STANDARD.md).

---

## Repository Philosophy

The Salesforce Navigator Suite is built on one architectural principle: **each documentation domain has exactly one owner**.

Every Navigator is scoped to a single official Salesforce documentation source or domain. It should become exceptionally accurate within that domain rather than attempting to answer every Salesforce question.

This produces better answers than a single generalist skill because:
- Narrower scope = fewer hallucinations
- Explicit ownership = no routing ambiguity
- Modular design = Navigators can be installed individually or as a suite

---

## Inheritance Model

```
PROJECT_STANDARD.md
        │
        │  Defines:
        │  - Repository philosophy
        │  - Skill template
        │  - Writing standards
        │  - Documentation trust policy
        │  - Approved sources
        │  - Ownership matrix
        │  - Routing rules
        │  - Interim ownership assignments
        │  - Vocabulary (reasoning, confidence, status)
        │  - Failure behavior
        │  - Security rules
        │  - Versioning rules
        │
        ▼
Individual Navigator files
        │
        │  Inherit everything from PROJECT_STANDARD.md.
        │  Define ONLY:
        │  - Domain-specific sources
        │  - Domain-specific scope
        │  - Domain-specific routing rules
        │  - Domain-specific guardrails
        │  - Domain-specific failure message
```

**Rule:** If a behavior applies to all Navigators, it belongs in `PROJECT_STANDARD.md`, not in individual Navigator files.

### Portability

The inheritance model above is a conceptual model applied during development. `PROJECT_STANDARD.md` is the repository's source of truth, and Navigator files inherit its repository-wide behavior by design — not through a technical loading mechanism.

In practice, Claude Skills do not automatically load related repository files. When a single Navigator file is copied or shared outside this repository, `PROJECT_STANDARD.md` is not available to it. The Navigator has no technical access to the shared standard it was built against.

To address this, every Navigator intentionally contains a **Repository Standards** section — a small, compressed summary of the minimum repository behavior required for standalone operation. It covers five essentials: approved sources, documentation as truth, validation requirements, reasoning labels, and scope/deferral. This section is consistent and identical across all Navigators.

This is an intentional portability layer, not a duplication of the repository standard. The distinction is deliberate:

- **Repository governance** (ownership matrix, routing rules, interim ownership, versioning policy, contributor guidance, vocabulary definitions, security policy) remains centralized in `PROJECT_STANDARD.md`.
- **Navigator files** contain only the minimum shared behavior required to function correctly when used independently.

This design allows the repository to remain maintainable — shared rules are updated in one place — while ensuring individual Navigators work correctly when distributed outside the repository as standalone Claude Skills.

The portability layer complements the inheritance model rather than replacing it. Inside the repository, `PROJECT_STANDARD.md` is the authority. Outside the repository, each Navigator carries enough context to behave consistently on its own.

---

## Repository Structure

```
salesforce-navigator-suite/
│
├── LICENSE                   # MIT License
├── PROJECT_STANDARD.md       # Repository governance — the single source of truth
├── README.md                 # Public-facing introduction and skill routing table
├── ROADMAP.md                # Planned future Navigators
├── CONTRIBUTING.md           # Contribution guide for new Navigators
├── CHANGELOG.md              # Version history
│
├── docs/
│   ├── ARCHITECTURE.md       # This document
│   └── SKILL_ROUTING_RESEARCH.md  # Routing experiment methodology, findings, and design principles
│
├── tests/
│   └── TRIGGER_TESTS.md      # Routing validation — should/should not trigger per Navigator
│
└── skills/
    ├── salesforce-help-navigator/
    │   └── SKILL.md
    ├── salesforce-developer-navigator/
    │   └── SKILL.md
    ├── salesforce-architect-navigator/
    │   └── SKILL.md
    ├── salesforce-release-notes-navigator/
    │   └── SKILL.md
    ├── salesforce-trailhead-navigator/
    │   └── SKILL.md
    ├── salesforce-marketing-cloud-developer-navigator/
    │   └── SKILL.md
    ├── salesforce-marketing-cloud-mobilepush-navigator/
    │   └── SKILL.md
    └── salesforce-platform-mobile-navigator/
        └── SKILL.md
```

---

## Navigator Groups

```
PROJECT_STANDARD.md
         │
         ├── Core Navigators
         │     ├── Salesforce Help Navigator
         │     │     help.salesforce.com, admin.salesforce.com
         │     │
         │     ├── Salesforce Release Notes Navigator
         │     │     Official Salesforce release documentation
         │     │
         │     ├── Salesforce Trailhead Navigator
         │     │     trailhead.salesforce.com
         │     │
         │     └── Salesforce Architect Navigator
         │           architect.salesforce.com
         │
         ├── Development Navigators
         │     ├── Salesforce Developer Navigator
         │     │     developer.salesforce.com, github.com/salesforce
         │     │
         │     └── Salesforce Marketing Cloud Developer Navigator
         │           developer.salesforce.com/docs/marketing
         │           github.com/salesforce-marketingcloud
         │
         └── Mobile Navigators
               ├── Salesforce Platform Mobile Navigator
               │     developer.salesforce.com (Mobile SDK)
               │     github.com/salesforce
               │
               └── Salesforce Marketing Cloud MobilePush Navigator
                     help.salesforce.com (MobilePush)
                     github.com/salesforce-marketingcloud
```

---

## Ownership Model

Documentation ownership is determined by **documentation purpose**, not product name.

| Documentation Purpose | Owner |
|---|---|
| Configuration, setup, administration | Help Navigator |
| Developer APIs, SDKs, code | Developer Navigator |
| Architecture patterns, design decisions | Architect Navigator |
| Learning, certifications | Trailhead Navigator |
| Release notes, what's new | Release Notes Navigator |
| Marketing Cloud APIs, AMPscript, SSJS | Marketing Cloud Developer Navigator |
| MobilePush SDK, push notifications | Marketing Cloud MobilePush Navigator |
| Salesforce Platform Mobile SDK | Platform Mobile Navigator |

The same product can appear across multiple Navigators. Example: Data Cloud configuration → Help Navigator. Data Cloud APIs → Developer Navigator. Data Cloud architecture → Architect Navigator. The question determines the Navigator, not the product.

### Interim Ownership

Some Salesforce products do not yet have a dedicated Navigator. These products are currently handled through interim ownership — their documentation is distributed across existing Domain Navigators by documentation type, following the same domain-based routing principle above.

Products currently on interim ownership: **Agentforce**, **Data Cloud**, **Marketing Cloud Personalization**, **CRM Analytics**, and **MuleSoft**.

For the authoritative interim routing table, see [PROJECT_STANDARD.md §7](../PROJECT_STANDARD.md).

---

## Routing Principles

1. **One owner per question.** Route to the single Navigator that owns the documentation that would answer the question.
2. **Routing is based on documentation domain, not product.** "Agentforce" is not a routing answer — "configuration" or "developer API" is.
3. **"May reference" is not ownership.** A Navigator may reference another domain for context without claiming ownership.
4. **Interim ownership is defined in PROJECT_STANDARD.md §7.** Individual Navigator files do not repeat interim ownership rationale — they inherit it.

---

## Documentation Domains

| Domain | What It Means | Primary Source |
|---|---|---|
| Help / Configuration | Setup, admin, limitations, licensing | help.salesforce.com |
| Developer | APIs, SDKs, code, platform capabilities | developer.salesforce.com |
| Architecture | Patterns, design, trade-offs, scalability | architect.salesforce.com |
| Learning | Guided content, certifications, exams | trailhead.salesforce.com |
| Release Notes | What changed, when, GA/Beta/Pilot status | Product-specific release notes |
| MC Developer | MC-specific APIs, scripting, integrations | developer.salesforce.com/docs/marketing |
| MobilePush | Mobile SDK for push and engagement | help.salesforce.com (MobilePush) |
| Platform Mobile | Offline-capable native Salesforce SDK | developer.salesforce.com (Mobile SDK) |

---

## Cross-Skill Interaction

Navigators are designed to complement each other, not compete.

**Permitted:**
- Referencing another domain for context
- Naming which Navigator owns a related topic
- Using "May reference [source] only for context. This does not transfer ownership."

**Not permitted:**
- Duplicating another Navigator's documentation
- Overriding another Navigator's ownership
- Expanding scope into another domain

---

## Versioning

Both `PROJECT_STANDARD.md` and Navigator files use Semantic Versioning.

Navigator files track two fields:
- `navigator_version` — the version of this Navigator definition
- `standard_version` — the version of `PROJECT_STANDARD.md` this Navigator was written against

When `PROJECT_STANDARD.md` is updated without changing Navigator files, the `standard_version` mismatch makes it visible at a glance which Navigators need review.

---

## Adding a New Navigator

See [CONTRIBUTING.md](../CONTRIBUTING.md) for the full contribution guide.

The short version:
1. Confirm the documentation domain has no existing owner.
2. Identify a primary official Salesforce source.
3. Write the Navigator definition file following PROJECT_STANDARD.md §2 template.
4. Add trigger tests to `tests/TRIGGER_TESTS.md`.
5. Update `README.md`, `PROJECT_STANDARD.md §6`, and `CHANGELOG.md`.
