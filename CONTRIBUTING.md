# Contributing to the Salesforce Navigator Suite

Thank you for contributing. This guide explains how to add new Navigators and maintain existing ones in a way that is consistent with the established architecture.

Before contributing, read [PROJECT_STANDARD.md](PROJECT_STANDARD.md) in full. It defines the repository architecture, inheritance model, ownership model, vocabulary, and naming conventions that all Navigators must follow.

---

## Repository Philosophy

The Salesforce Navigator Suite is built on one principle: each documentation domain has exactly one owner.

Navigators should become exceptionally accurate within their domain rather than attempting to answer every Salesforce question. A Navigator that stays narrow is more useful than one that tries to cover everything.

When in doubt, scope down.

---

## How to Create a New Navigator

### Step 1 — Confirm the documentation domain

A new Navigator requires a documentation domain that is not already owned by an existing Navigator.

Check the Skill Ownership Matrix in PROJECT_STANDARD.md §6 and the confirmed ownership boundaries in §7. If the domain you want to cover is already owned by an existing Navigator, contribute to that Navigator instead of creating a new one.

If the domain is covered by interim ownership (Agentforce, Data Cloud, Marketing Cloud Personalization, CRM Analytics, MuleSoft), a dedicated Navigator may already be planned — open an issue to discuss before starting.

### Step 2 — Identify the primary official Salesforce source

Every Navigator must have at least one primary official Salesforce-owned documentation source. Sources must come from the Approved Sources list in PROJECT_STANDARD.md §4.

If the documentation domain does not have an official Salesforce-owned source, it cannot have a Navigator.

### Step 3 — Define a clear ownership boundary

Write out explicitly what the Navigator owns and what it does not own. Every "Does NOT own" entry should name which existing Navigator owns that topic instead.

If you cannot write a clean Does NOT own table without creating conflicts with existing Navigators, the ownership boundary is not clear enough.

### Step 4 — Write the Navigator definition file

Create a directory under `skills/` named after the Navigator using kebab-case:

```
skills/salesforce-[product]-navigator/
```

Name the Navigator definition file `SKILL.md`:

```
skills/salesforce-[product]-navigator/SKILL.md
```

Follow the template defined in PROJECT_STANDARD.md §2 exactly. Every section in the template is required. Do not add sections that are not in the template. Do not repeat repository-wide behavior from the standard — Navigator files inherit it.

Use this frontmatter structure:

```yaml
---
name: salesforce-[product]-navigator
navigator_version: [version]
standard_version: [current PROJECT_STANDARD.md version]
description: >
  [Intent classifier. Lead with a third-person capability statement: "This Navigator researches [domain] from official [source] documentation." Follow with a trigger phrase: "Use when the user asks..." Include what the Navigator owns, representative user intents, and explicit ownership of cross-cutting Salesforce products. May be a multi-line YAML block. Avoid keyword lists and marketing copy.]
---
```

### Step 5 — Write trigger tests

Every new Navigator requires trigger tests. Add them to `tests/TRIGGER_TESTS.md` following the format for existing Navigators:

- At least 5 "Should Trigger" examples with realistic Salesforce user questions.
- At least 5 "Should NOT Trigger" examples with the correct Navigator named.
- Include edge cases where two Navigators might both plausibly respond.

### Step 6 — Update supporting files

- Add the new Navigator to the Skills table in `README.md`.
- Add the new Navigator to the Skill Ownership Matrix in `PROJECT_STANDARD.md §6`.
- Add any new confirmed ownership boundaries to `PROJECT_STANDARD.md §7`.
- Add the new Navigator to `CHANGELOG.md` as a Minor version increment.
- If the new Navigator replaces interim ownership, update the interim ownership table in `PROJECT_STANDARD.md §7` and remove the interim scope entries from the affected Navigators.

---

## How to Determine Documentation Ownership

Use this decision tree:

1. **What is the user's primary intent?** Configuration, development, architecture, learning, or release notes?
2. **Which official Salesforce documentation would answer this?** help.salesforce.com, developer.salesforce.com, architect.salesforce.com, trailhead.salesforce.com, or product-specific release notes?
3. **Who owns that documentation source?** Match to the Skill Ownership Matrix in PROJECT_STANDARD.md §6.

Ownership is determined by documentation purpose, not product. A question about Agentforce configuration belongs to Help Navigator (because it lives in help.salesforce.com). A question about Agentforce developer APIs belongs to Developer Navigator (because it lives in developer.salesforce.com).

---

## Naming Conventions

- Every Navigator must end with **Navigator**.
- Use official Salesforce product names, not technology names.
- Use the format: `Salesforce [Product] Navigator` for display names.
- Use the format: `salesforce-[product]-navigator` for directory and file names.

**Correct:** `Salesforce Data Cloud Navigator` / `salesforce-data-cloud-navigator`
**Avoid:** `Salesforce CDP Navigator`, `SF DC Navigator`, `Data Navigator`

---

## Writing Standards

Follow PROJECT_STANDARD.md §3.

- Use official Salesforce terminology. Mention former product names only once.
- Write descriptions as intent classifiers, not documentation summaries. They may be multi-line YAML blocks. Include what the Navigator owns, when to use it, representative user intents, and explicit ownership of cross-cutting Salesforce products. Avoid keyword lists. Prioritize routing clarity. Review descriptions across all Navigators before submitting — a change that improves one Navigator can introduce ambiguity in another. See PROJECT_STANDARD.md §3 and docs/SKILL_ROUTING_RESEARCH.md.
- Guardrails in Navigator files must be domain-specific. Do not repeat repository-wide guardrails from the standard.
- "May reference" wording must follow the standard phrasing: "May reference [source] only for context. This does not transfer ownership."

---

## Description Design

Navigator `description:` fields are the primary routing mechanism. Claude evaluates only the frontmatter description before deciding whether to invoke a Navigator — the body is not loaded until after invocation. Descriptions must be written as intent classifiers, not documentation summaries.

Before writing or modifying a description:
- Read **PROJECT_STANDARD.md §3 — Description Design** for the authoritative principles.
- Read **`docs/SKILL_ROUTING_RESEARCH.md`** for the validated research behind those principles, including experiment methodology, findings, and known unknowns.

When writing a description:
- Lead with a third-person capability statement ("This Navigator researches [domain] from official [source] documentation."), then follow with a trigger phrase ("Use when the user asks..."). Use natural language that reflects how a user would phrase their question.
- Explicitly name the documentation domain the Navigator owns and the products within that domain. Do not rely on implied ownership — if a cross-cutting Salesforce product (Agentforce, Data Cloud, etc.) belongs to this Navigator's domain, name it.
- Include representative user intents as signal, not keyword lists.
- At domain boundaries where routing ambiguity is likely, add a brief negative signal ("Does not own X — that routes to Y Navigator").

Before submitting changes to any description, review all Navigator descriptions together. A change that improves one Navigator's routing confidence can introduce ambiguity in another. Routing quality should be validated through measurable experiments — changes based on subjective wording preferences alone should not be submitted without evidence of improvement.

---

## Validation Checklist Before Opening a Pull Request

- [ ] Navigator definition file follows the template in PROJECT_STANDARD.md §2
- [ ] `navigator_version` and `standard_version` are set correctly
- [ ] Description is written as an intent classifier (not a capability list or documentation summary)
- [ ] Description leads with a third-person capability statement ("This Navigator researches..."), followed by a "Use when the user asks..." trigger phrase
- [ ] Description explicitly names cross-cutting Salesforce products owned by this Navigator
- [ ] Description reviewed against all sibling Navigator descriptions for routing ambiguity
- [ ] Description tested for routing accuracy on the Claude model(s) the Navigator is intended to support (Anthropic recommends testing across Haiku, Sonnet, and Opus where applicable)
- [ ] Scope and Out of Scope are explicit with no conflicts against existing Navigators
- [ ] Routing Rules cover edge cases
- [ ] Trigger tests are added to `tests/TRIGGER_TESTS.md`
- [ ] README.md Skills table updated
- [ ] PROJECT_STANDARD.md §6 Ownership Matrix updated
- [ ] CHANGELOG.md updated
- [ ] No repository-wide behavior is duplicated from the standard
- [ ] No new ownership conflicts introduced

---

## Pull Request Expectations

- One Navigator per pull request.
- Include a brief description of the documentation domain and why it needs its own Navigator.
- Link any relevant Salesforce documentation that confirms the domain scope.
- All trigger tests must be present before review.

---

## Navigator Types

Before creating a new Navigator, determine which type it should be. The repository supports two Navigator types.

### Domain Navigators

Domain Navigators own a single documentation type across all Salesforce products. They route by documentation purpose, not by product.

The five core Domain Navigators in this repository are:
- **Salesforce Help Navigator** — configuration, setup, permissions, licensing
- **Salesforce Developer Navigator** — APIs, SDKs, Apex, code implementation, developer release notes
- **Salesforce Architect Navigator** — integration patterns, reference architectures, design trade-offs
- **Salesforce Release Notes Navigator** — product feature releases, GA/Beta/Pilot status, deprecations
- **Salesforce Trailhead Navigator** — learning content, certification preparation

Domain Navigators are the foundation of the interim ownership model. When a Salesforce product does not have a dedicated Navigator, its documentation is distributed across the relevant Domain Navigators by documentation type.

### Product Specialist Navigators

Product Specialist Navigators consolidate documentation from multiple official Salesforce documentation domains for a single Salesforce product. They exist because certain products have documentation spread across enough distinct properties to justify a unified entry point.

Current Product Specialist Navigators:
- **Salesforce Marketing Cloud Developer Navigator** — consolidates MC Engagement APIs, Account Engagement APIs, AMPscript, SSJS from multiple developer documentation sources
- **Salesforce Marketing Cloud MobilePush Navigator** — consolidates MobilePush SDK, Unified Mobile SDK, and mobile engagement documentation
- **Salesforce Platform Mobile Navigator** — consolidates Salesforce Platform Mobile SDK, SmartStore, and MobileSync documentation

Additional Product Specialist Navigators are planned for future releases.

### When to create a Product Specialist Navigator

Create a Product Specialist Navigator when **all** of the following are true:

1. The Salesforce product has official documentation distributed across multiple Salesforce-owned documentation properties.
2. The documentation volume and complexity justify a unified product entry point over domain-based routing.
3. The ownership boundaries of the new Navigator can be defined without conflicting with existing Navigators.
4. The product is mature enough in Salesforce's documentation that primary sources are stable.

**Do not** create a Product Specialist Navigator when:
- The domain-based architecture already routes the product correctly.
- The product's documentation lives in a single source that an existing Domain Navigator already owns.
- The primary motivation is convenience rather than genuine documentation complexity.

When in doubt, prefer extending Domain Navigator interim ownership over creating a new Product Specialist Navigator prematurely.

---

## Retiring Interim Ownership

Before running this checklist, confirm the product satisfies the **Promotion Criteria** defined in `PROJECT_STANDARD.md §7`. The criteria determine *whether* to promote; this checklist determines *how*. Do not begin the retirement process unless promotion criteria are met.

When a dedicated Navigator is created for a product that previously had interim ownership, follow this process to transfer ownership cleanly and avoid ownership vacuums or conflicts.

### Step 1 — Remove the product from the Interim Ownership section of PROJECT_STANDARD.md

Delete the interim ownership table for the product from §7 of PROJECT_STANDARD.md. The new dedicated Navigator definition will become the canonical ownership record.

### Step 2 — Create the new Navigator definition file

Follow the "How to Create a New Navigator" process above. The new Navigator's Scope section explicitly owns what was previously distributed across Domain Navigators.

### Step 3 — Remove interim scope entries from affected Domain Navigators

Each Domain Navigator that carried interim ownership for this product will have a Scope entry referencing "see PROJECT_STANDARD.md §7 for interim ownership." Remove those entries from the affected Navigator files.

### Step 4 — Verify ownership boundaries remain exclusive

After removal, confirm that no domain is now unowned. Run the Confirmed Ownership Boundaries table in PROJECT_STANDARD.md §7 against the new Navigator to verify there are no gaps or overlaps.

### Step 5 — Update CHANGELOG.md

If the Navigator retires interim ownership for a previously planned product, note this in CHANGELOG.md as a Minor version increment alongside the new Navigator entry.

### Step 6 — Update CHANGELOG.md

Log the retirement of interim ownership and the introduction of the dedicated Navigator as a Minor version increment.

### Step 7 — Run Trigger Tests

Update `tests/TRIGGER_TESTS.md` to add trigger tests for the new Navigator. Verify that existing Domain Navigator tests no longer include the retired interim topics as "Should Trigger" examples.
