# Salesforce Navigator Suite — Roadmap

This document tracks planned future Navigators for the Salesforce Navigator Suite.
Current architecture, ownership model, and all accepted design decisions are defined in [PROJECT_STANDARD.md](PROJECT_STANDARD.md).

---

## Version 2 — Planned Navigators

### Salesforce Agentforce Navigator
Dedicated Navigator for Agentforce documentation across admin and developer domains.

**Would own:**
- Agentforce admin/config/setup (replacing interim ownership in Help Navigator)
- Agentforce developer documentation, APIs, SDKs, agent actions, custom actions (replacing interim ownership in Developer Navigator)
- Agentforce architecture guidance (replacing interim ownership in Architect Navigator)
- Agentforce product release summaries (replacing interim ownership in Release Notes Navigator)
- Agentforce learning content (replacing interim ownership in Trailhead Navigator)

**Primary Sources (planned):**
- help.salesforce.com (Agentforce section)
- developer.salesforce.com (Agentforce developer docs)
- architect.salesforce.com (Agentforce architecture guidance)

---

### Salesforce Data Cloud Navigator
Dedicated Navigator for Data Cloud documentation across admin and developer domains.

**Would own:**
- Data Cloud admin/config/setup (replacing interim ownership in Help Navigator)
- Data Cloud Query API, Ingestion API, developer documentation (replacing interim ownership in Developer Navigator)
- Data Cloud architecture guidance (replacing interim ownership in Architect Navigator)
- Data Cloud product release summaries and Data 360 release notes (replacing interim ownership in Release Notes Navigator)
- Data Cloud learning content (replacing interim ownership in Trailhead Navigator)

**Primary Sources (planned):**
- help.salesforce.com (Data Cloud section)
- developer.salesforce.com (Data Cloud developer docs)
- architect.salesforce.com (Data Cloud architecture)

---

### Salesforce Marketing Cloud Personalization Navigator
Dedicated Navigator for Marketing Cloud Personalization (formerly Interaction Studio) documentation.

**Would own:**
- Marketing Cloud Personalization configuration and implementation
- Personalization APIs and developer documentation

**Primary Sources (planned):**
- help.salesforce.com (Marketing Cloud Personalization section)
- developer.salesforce.com/docs/marketing (Personalization developer docs)

---

### Salesforce CRM Analytics Navigator
Dedicated Navigator for CRM Analytics (formerly Tableau CRM / Einstein Analytics) documentation.

**Would own:**
- CRM Analytics dashboard and lens documentation
- SAQL and Apex for CRM Analytics
- CRM Analytics APIs

**Primary Sources (planned):**
- help.salesforce.com (CRM Analytics section)
- developer.salesforce.com (CRM Analytics developer docs)

---

### Salesforce MuleSoft Navigator
Dedicated Navigator for MuleSoft integration documentation.

**Would own:**
- MuleSoft Anypoint Platform documentation
- MuleSoft connector documentation
- MuleSoft API design and implementation

**Primary Sources (planned):**
- docs.mulesoft.com
- anypoint.mulesoft.com/exchange

---

## Contribution

To propose a new Navigator, open an issue with:
- The documentation domain the Navigator would own
- The primary official Salesforce source(s)
- A clear ownership boundary that does not conflict with existing Navigators
- A draft description written as an intent classifier (following PROJECT_STANDARD.md §3 and `docs/SKILL_ROUTING_RESEARCH.md`)

See [CONTRIBUTING.md](CONTRIBUTING.md) for the full contribution guide.
