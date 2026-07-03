# Salesforce Navigator Suite — Skill Routing Research

This document records the engineering reasoning, experiments, and conclusions behind the repository's Navigator description design. It is intended for contributors and advanced users — not end users.

---

## Introduction

This repository contains eight cooperating Claude Skills, each scoped to a specific Salesforce documentation domain. Because multiple skills are available simultaneously, Claude must route each incoming request to the correct Navigator before it can answer.

The routing mechanism works as follows: Claude reads the YAML frontmatter `description:` field of each installed skill before deciding which to invoke. The body of the Navigator file — including `## Purpose`, `## When to Use`, `## Scope`, and all other sections — is loaded only after invocation. Claude never reads Navigator body content to decide *whether* to invoke a skill.

This architectural constraint means that the `description:` field functions as the primary routing signal. Description design is therefore treated as an engineering problem rather than simple documentation. A description that reads clearly to a human reader may still route poorly if it fails to semantically match the range of requests the Navigator is intended to handle.

---

## Background

Anthropic's guidance for skill descriptions follows a principle of progressive disclosure:

- The `description:` frontmatter field is loaded first and is the primary signal Claude uses for skill selection.
- The full `SKILL.md` body is loaded only after the skill is invoked.
- Descriptions should communicate what the skill does and when it should be used.
- Descriptions are semantic intent classifiers, not documentation summaries.

This guidance shaped several architectural decisions in this repository:

- Navigator descriptions are written as natural language rather than keyword lists.
- Each description attempts to convey both the documentation domain and the types of user requests the Navigator handles.
- The body of each Navigator file is written for post-invocation accuracy — it guides how the Navigator answers, not whether it is selected.
- The `## Repository Standards` portability section exists in Navigator bodies for standalone deployment but has no effect on skill selection within the full repository.

An important corollary: changes to Navigator body content — including `## Skill Selection`, `## When to Use`, guardrails, and routing tables — do not affect invocation rate. Only the frontmatter `description:` field influences routing decisions.

---

## Research Questions

The following questions guided the routing experiments:

1. Does description wording measurably affect routing accuracy?
2. Do trigger phrases improve routing over documentation-style descriptions?
3. Does explicit ownership of cross-cutting products reduce routing ambiguity?
4. Do entity-rich descriptions (listing specific Salesforce terminology) outperform generic descriptions?
5. What causes routing collisions between Navigators with overlapping Salesforce terminology?
6. What is the practical boundary between routing improvement and false-positive risk?
7. How much does Claude's independent confidence threshold affect invocation frequency regardless of description quality?

Not all of these questions have been fully resolved. See Remaining Unknowns.

---

## Methodology

Each round compared the current production descriptions against a candidate variant across a set of routing test cases. Comparisons focused on semantic routing quality and boundary case resolution — not invocation frequency.

**Important limitation:** these experiments evaluated routing accuracy given that a skill is selected — they did not evaluate Claude's independent threshold for deciding whether to invoke a skill at all versus answering directly from training knowledge. These are distinct behaviors. Improved descriptions can narrow routing ambiguity but cannot override Claude's tool-use confidence threshold for questions it considers simple enough to answer without invoking a skill.

### Round 1 — Entity-rich descriptions

**Baseline:** Current production descriptions.
**Variant:** Descriptions augmented with lists of specific Salesforce products, features, and terminology.

Rationale: Generic descriptions may fail to match requests that use Salesforce-specific terminology without generic framing. Entity-rich descriptions provide more surface area for semantic matching.

### Round 2 — Natural-language trigger descriptions

**Baseline:** Current production descriptions.
**Variant:** Descriptions rewritten as natural-language trigger statements emphasizing user intent and question types rather than feature lists.

Rationale: Descriptions written as intent classifiers ("use when the user asks about X") may align more closely with how Claude evaluates skill relevance than descriptions written as capability summaries ("this skill covers X").

### Round 3 — Explicit ownership descriptions

**Baseline:** Current production descriptions.
**Variant:** Descriptions with explicit ownership statements for cross-cutting Salesforce products — products whose documentation spans multiple Navigators (Agentforce, Data Cloud, Marketing Cloud, Identity Resolution).

Rationale: When two Navigators both plausibly match a request, Claude must break the tie. Explicit ownership statements reduce reliance on semantic inference at the decision boundary.

---

## Results

### Round 1 — Entity-rich descriptions

- Improved semantic coverage for requests using implicit Salesforce terminology without the word "Salesforce."
- No routing regressions observed on existing correctly-routed cases.
- Benefit concentrated in cases where the user assumed shared context (e.g., "how do I configure a Permission Set" without mentioning Salesforce).

### Round 2 — Natural-language trigger descriptions

- Cleaner boundary resolution on cases where multiple Navigators could plausibly match.
- Reduced reliance on inferred ownership for cross-cutting product questions.
- Descriptions written as intent statements appeared to align more directly with Claude's routing evaluation than capability summaries.

### Round 3 — Explicit ownership descriptions

- First measurably distinct routing improvement.
- 16/16 correct routing on the test set compared to 15/16 for the original descriptions.
- The failing case in the baseline: an Identity Resolution setup question was routed to Architect Navigator instead of Help Navigator. The explicit ownership variant corrected this.
- Marketing Cloud architecture ownership became explicit rather than inferred, resolving a recurring boundary ambiguity between Help Navigator and Architect Navigator for Marketing Cloud questions.

These results should not be overstated. The test set is small. The improvement is meaningful but modest.

---

## Engineering Findings

### Finding 1 — Descriptions function as intent classifiers

Navigator descriptions function primarily as semantic intent classifiers rather than documentation summaries. A description that accurately summarizes the Navigator's content may still route poorly if it does not semantically match the range of user intents the Navigator is intended to serve. Description quality should be evaluated by routing performance, not documentation clarity.

### Finding 2 — Natural-language trigger phrases improve routing confidence

Descriptions written as natural-language trigger statements — "use this Navigator when the user asks about X" — consistently outperformed descriptions written as capability lists or documentation summaries. Intent framing appears to align more directly with how Claude evaluates skill relevance.

### Finding 3 — Entity-rich descriptions improve semantic matching

Including specific Salesforce terminology in descriptions (Apex, SOQL, LWC, Flow, Journey Builder, Agentforce, Contact Key, etc.) improves semantic matching for requests that use Salesforce-specific language without explicitly mentioning Salesforce. This is particularly relevant for experienced Salesforce practitioners who frame questions using product terminology rather than platform names.

### Finding 4 — Explicit ownership of cross-cutting products reduces routing ambiguity

Some Salesforce products (Agentforce, Data Cloud, Marketing Cloud, Identity Resolution) have documentation distributed across multiple domains and therefore appear in the scope of multiple Navigators. When ownership of these products was stated explicitly in descriptions rather than implied by domain coverage, routing accuracy improved at boundary cases.

### Finding 5 — Shared Salesforce terminology is acceptable when ownership is explicit

Multiple Navigators legitimately share high-level Salesforce terminology. This is expected and correct — the same product can generate questions for multiple Navigators depending on the user's intent. Shared terminology does not cause routing problems when ownership within each Navigator's domain is explicitly stated. The objective is not eliminating terminology overlap but eliminating ownership ambiguity.

### Finding 6 — The objective is routing accuracy, not overlap elimination

Early assumptions that routing collisions were caused by overlapping terminology proved incorrect. The primary cause was ambiguous ownership of cross-cutting products, not shared terminology itself. Attempts to eliminate terminology overlap would have reduced description quality and increased false negatives.

### Observation — Not all routing ambiguity is a description problem

Some Salesforce questions are inherently cross-domain and will produce reasonable ambiguity regardless of description design. A question that combines a configuration concern with an enterprise architecture concern, or that touches concepts owned by two different documentation domains, may be legitimately interpretable by more than one Navigator. The objective of description design is to minimize *unnecessary* ambiguity — caused by vague ownership or missing entity signals — not to eliminate *legitimate* multi-domain questions. Routing experiments should distinguish between ambiguity that indicates a description gap and ambiguity that reflects the genuine nature of the question.

---

## Description Design Principles

Based on the findings above, Navigator descriptions in this repository are written according to the following principles.

**A Navigator description should contain:**

1. **What the Navigator does** — which documentation domain it owns and what type of questions it answers.
2. **When it should be used** — the user intents and question types that make this Navigator the correct choice.
3. **Representative user intents** — natural-language examples of the kinds of requests it handles.
4. **High-signal Salesforce terminology** — specific product names, feature names, and API names associated with this Navigator's domain.
5. **Explicit ownership of cross-cutting products** — a clear statement of which cross-cutting Salesforce products this Navigator owns within its documentation domain.

**A Navigator description should not be:**

- A keyword list without syntactic structure.
- A documentation summary that describes content rather than intent.
- A marketing statement about the Navigator's value.
- So long that signal is diluted by noise.

Descriptions should be written as natural language and optimized for routing confidence, not human readability.

---

## Explicit Ownership

The experiments confirmed that explicit ownership of cross-cutting Salesforce products is the highest-leverage intervention available within the description field.

Products where explicit ownership most improved routing accuracy:

- **Agentforce** — appears across Help, Developer, Architect, Release Notes, and Trailhead Navigators. Without explicit domain qualification, boundary cases were ambiguous.
- **Data Cloud** — same distribution as Agentforce.
- **Marketing Cloud** — architecture questions were miscategorized toward Architect Navigator when Help Navigator owned the configuration documentation.
- **Identity Resolution** — setup and configuration questions were routed to Architect Navigator based on the word "resolution" carrying architecture connotations. Explicit Help Navigator ownership of setup documentation corrected this.

The pattern across all four products was the same: when ownership was implied by domain coverage rather than stated explicitly, routing at the boundary was less reliable.

**Design principle:** Explicitly name cross-cutting Salesforce products within the Navigator that owns their documentation domain. Do not rely on implied ownership or semantic inference.

---

## Remaining Unknowns

The following questions remain open and were not resolved by these experiments.

**Invocation frequency vs. routing accuracy**
The experiments measured routing accuracy — given that a skill is invoked, was the correct Navigator selected? They did not measure how often Claude invokes a skill at all versus answering directly. These are distinct behaviors with different causes. Improved descriptions can improve routing accuracy but cannot overcome Claude's independent tool-use confidence threshold. The degree to which description improvements affect invocation frequency is not known.

**Tie-breaking behavior**
When two Navigator descriptions are semantically similar for a given request, how Claude breaks the tie is not well understood. Whether description ordering, length, or specific phrase placement affects tie-breaking is unknown.

**Optimal description length**
Longer descriptions provide more signal but may dilute routing confidence if high-signal content is surrounded by lower-signal content. The optimal description length for routing performance has not been empirically determined.

**Model version sensitivity**
Routing behavior may differ across Claude model versions. The experiments in this repository were conducted against Claude Sonnet (claude-sonnet-4-6). Whether the findings generalize to other model sizes is not known. Anthropic's skill authoring guidance explicitly recommends testing across Haiku, Sonnet, and Opus, noting that what works for Opus may need more guidance for Haiku. The routing improvements documented here have not been validated on Haiku or Opus. Contributors adding or modifying Navigator descriptions should test against the models they intend to support.

**Weighting between triggers and semantic similarity**
How Claude weights explicit trigger phrases against broader semantic similarity is not documented. Whether a single explicit trigger phrase outperforms broader semantic coverage is unknown.

**Negative trigger effectiveness**
Whether negative trigger statements ("do not use this Navigator for X") improve routing accuracy for boundary cases was not tested. This may be a productive area for future research.

---

## Future Research

The following experiments would extend the findings above.

- **Description length optimization** — systematically vary description length to identify the point where additional content reduces rather than improves routing confidence.
- **Negative trigger testing** — evaluate whether explicit negative trigger statements ("this Navigator does not handle X") reduce boundary case errors.
- **Concept ordering** — test whether placing ownership statements earlier in the description improves boundary case routing compared to later placement.
- **Extended routing benchmarks** — expand the test set beyond 16 cases to improve statistical confidence in routing improvements.
- **Cross-version validation** — repeat routing experiments across Claude model versions to identify which findings are stable and which are model-specific.
- **Invocation frequency measurement** — design experiments that specifically measure invocation frequency rather than routing accuracy, to understand the relationship between description quality and Claude's tool-use threshold.
- **Real-world telemetry** — if deployment infrastructure permits, collect real routing data to compare against lab experiment results.
- **Evidence-grounding behavior** — The routing experiments measured whether the correct Navigator was selected. A distinct failure class emerged during implementation: a correctly-selected Navigator may substitute model memory when approved sources cannot be retrieved, rather than disclosing that verification failed. Open questions include how reliably Claude distinguishes a claim absent from the documentation (Not Documented) from one that could not be verified due to retrieval failure (Not Verified), whether evidence-before-synthesis constraints hold consistently under varied retrieval conditions, and how these behaviors vary across Claude model versions. Evidence-grounding is a second independent research area from routing research — one that addresses answer quality after correct invocation rather than invocation accuracy itself.

---

## Conclusion

The routing strategy in this repository evolved through iterative experimentation rather than intuition or convention. Each description design principle is backed by a specific experimental finding rather than a subjective preference.

The most significant validated finding is that explicit ownership of cross-cutting Salesforce products — stated in the description rather than implied by domain coverage — is the highest-leverage intervention for improving routing accuracy. This principle is now part of the repository's permanent description design standards.

Routing decisions in this repository should continue to be evidence-driven. When descriptions are changed, the change should be motivated by a routing hypothesis and evaluated against measurable criteria — not adjusted based on how the description reads to a human.

The remaining unknowns documented above represent the honest boundary of what these experiments established. Future contributors should treat those open questions as research opportunities rather than assumed answers.

These experiments addressed one layer of the trust problem: invocation routing. A separate layer — whether a correctly-invoked Navigator answers from verified evidence rather than model memory — is a distinct research problem that routing experiments do not address. Selecting the correct Navigator is a necessary but not sufficient condition for trustworthy answers. Future repository evolution may investigate both layers independently, with routing architecture and evidence-grounding architecture treated as complementary rather than overlapping concerns.
