# Routing and Guardrail Tests — Salesforce Navigator Suite

Tests to validate that each Navigator triggers on the right prompts, correctly hands off out-of-scope questions, and follows the repository's evidence model when answering.

**Format:**
- ✅ Should trigger = this Navigator should respond
- ❌ Should NOT trigger = another Navigator should respond (correct owner named)

---

## Salesforce Help Navigator

**Should trigger (✅)**
- "How do I create a permission set in Salesforce?"
- "What's the difference between a profile and a permission set group?"
- "Can I enable Einstein Activity Capture for only specific users?"
- "What Salesforce editions include Sales Cloud Einstein?"
- "How do I configure Data Cloud identity resolution rules in Setup?"
- "What are the setup steps to activate an Agentforce agent in my org?"
- "How do I restrict field-level security on a custom object?"
- "Where do I configure sharing rules for Account records?"
- "How do I set up MFA for my Salesforce org?"
- "What is the storage limit for a Developer Edition org?"

**Should NOT trigger (❌)**
- "How do I call the Salesforce REST API?" → **Developer Navigator**
- "What changed in the Spring '25 release for Sales Cloud?" → **Release Notes Navigator**
- "How do I design a hub-and-spoke integration with Salesforce?" → **Architect Navigator**
- "How do I learn to use Salesforce Flow?" → **Trailhead Navigator**
- "How do I call the Marketing Cloud REST API?" → **Marketing Cloud Developer Navigator**
- "How do I implement push notifications with MobilePush SDK?" → **MC MobilePush Navigator**

---

## Salesforce Developer Navigator

**Should trigger (✅)**
- "How do I write an Apex trigger that fires before insert?"
- "What is the governor limit for SOQL queries in a single transaction?"
- "How do I build a Lightning Web Component that calls an Apex method?"
- "Show me how to use the Bulk API 2.0 to upsert records."
- "How do I create an invocable Apex method for use in Flow?"
- "What is the Metadata API used for and how do I call it?"
- "How do I use the GraphQL API to query Salesforce data?"
- "How do I create a custom agent action in Agentforce using Apex?"
- "What is the Data Cloud Ingestion API and how do I authenticate to it?"
- "How do I deploy a Salesforce DX project using the CLI?"

**Should NOT trigger (❌)**
- "How do I configure a permission set in Setup?" → **Help Navigator**
- "What's the recommended integration pattern for SAP to Salesforce?" → **Architect Navigator**
- "What's new in the Salesforce API in Winter '25?" → **Release Notes Navigator**
- "How do I call the MC Journey Builder API?" → **Marketing Cloud Developer Navigator**
- "How do I implement MobileSync offline data with SmartStore?" → **Platform Mobile Navigator**
- "How do I register a device for push notifications using the MC SDK?" → **MC MobilePush Navigator**

---

## Salesforce Architect Navigator

**Should trigger (✅)**
- "What is the recommended integration pattern for real-time data sync between Salesforce and an ERP?"
- "When should I use Platform Events vs Change Data Capture?"
- "What are the trade-offs between a hub-and-spoke and point-to-point integration topology?"
- "How do I design a multi-org architecture for a global Salesforce deployment?"
- "What are the scalability limits I should plan for when using SOQL in high-volume orgs?"
- "What is the recommended data model for B2B Commerce on Salesforce?"
- "How should I architect an Agentforce solution for a high-volume customer service scenario?"
- "What are the security design considerations for a Connected App integration?"
- "When should I use Data Cloud as a real-time data layer vs Salesforce native objects?"
- "What is the medallion architecture pattern and does it apply to Salesforce Data Cloud?"

**Should NOT trigger (❌)**
- "How do I set up a Connected App in Setup?" → **Help Navigator**
- "How do I call the Platform Events API from an external system?" → **Developer Navigator**
- "What new integration patterns were released in Spring '25?" → **Release Notes Navigator**
- "Is there a Trailhead module on integration architecture?" → **Trailhead Navigator**
- "How do I configure MuleSoft Anypoint Platform?" → **Help Navigator** (cross-domain — Salesforce-hosted content only; see PROJECT_STANDARD.md §7)

---

## Salesforce Release Notes Navigator

**Should trigger (✅)**
- "What's new in Salesforce Spring '25 for Sales Cloud?"
- "When did Einstein Copilot go GA?"
- "Is Data Cloud Calculated Insights in GA or still in Beta?"
- "What features were deprecated in the Winter '25 release?"
- "What breaking changes should I know about before upgrading to API version 61.0?"
- "What new Agentforce features shipped in Summer '25?"
- "Did Salesforce release any changes to Apex governor limits recently?"
- "What was announced as Pilot in the last three Salesforce releases for Marketing Cloud?"
- "What is the GA date for Marketing Cloud Next features?"
- "Are there any known issues flagged in the Spring '25 release notes for Flow?"

**Should NOT trigger (❌)**
- "How do I configure the feature that was released in Spring '25?" → **Help Navigator**
- "How do I code against the new API endpoint added in Winter '25?" → **Developer Navigator**
- "How do I learn about what changed in Salesforce releases?" → **Trailhead Navigator**
- "What is the recommended architecture for the new Data Cloud features?" → **Architect Navigator**

---

## Salesforce Trailhead Navigator

**Should trigger (✅)**
- "Is there a Trailhead trail for Salesforce Flow beginners?"
- "What superbadge should I complete to prepare for the Salesforce Administrator exam?"
- "How do I get the Salesforce Certified Sales Cloud Consultant certification?"
- "Is there a hands-on project for learning Lightning Web Components?"
- "What learning path should I follow to go from Salesforce admin to developer?"
- "Are there any Trailhead modules specifically for Data Cloud?"
- "How long does the Admin certification trail take to complete?"
- "What is Trailhead Playground and how do I use it?"
- "Is there an Agentforce learning trail on Trailhead?"
- "What are the prerequisites for the Salesforce Architect certification?"

**Should NOT trigger (❌)**
- "How do I actually implement Flow in my org?" → **Help Navigator**
- "What is the code syntax for SOQL?" → **Developer Navigator**
- "What architecture pattern does Salesforce recommend for integrations?" → **Architect Navigator**
- "What new certifications were announced in the latest Salesforce release?" → **Release Notes Navigator**

---

## Salesforce Marketing Cloud Developer Navigator

**Should trigger (✅)**
- "How do I authenticate to the Marketing Cloud REST API using OAuth 2.0?"
- "Show me how to write an AMPscript personalization string for email."
- "How do I use SSJS to call an external API from a Marketing Cloud CloudPage?"
- "What is the Marketing Cloud Transactional Messaging API and how do I trigger a message send?"
- "How do I use the Journey Builder REST API to inject contacts into a journey?"
- "What is the correct endpoint to retrieve subscriber data from Marketing Cloud SOAP API?"
- "How do I call the Pardot Account Engagement REST API to create a prospect?"
- "What OAuth flow does Marketing Cloud Account Engagement use?"
- "How do I use the SFMC Fuel SDK for Python?"
- "What are the rate limits for the Marketing Cloud REST API?"

**Should NOT trigger (❌)**
- "How do I set up an Email Studio send in Marketing Cloud?" → **Help Navigator**
- "What new Marketing Cloud APIs were released in Spring '25?" → **Release Notes Navigator**
- "How do I design a cross-cloud architecture with Marketing Cloud and Sales Cloud?" → **Architect Navigator**
- "How do I register a device for push notifications?" → **MC MobilePush Navigator**
- "What Trailhead modules exist for Marketing Cloud developers?" → **Trailhead Navigator**

---

## Salesforce Marketing Cloud MobilePush Navigator

**Should trigger (✅)**
- "How do I register a device for Marketing Cloud push notifications on iOS?"
- "What is the correct method to set a contact key in the MC MobilePush SDK for Android?"
- "How do I implement the Unified Mobile SDK for Marketing Cloud on React Native?"
- "How do I enable the Inbox feature in the Marketing Cloud MobilePush SDK?"
- "What are the four modules in the Marketing Cloud Unified Mobile SDK v10?"
- "How do I configure silent push notifications with the MC SDK?"
- "What is the SP Module in the Marketing Cloud Unified Mobile SDK?"
- "How do I handle push notification callbacks in the Android MC SDK?"
- "How do I configure CloudPage messages using the MobilePush SDK?"
- "What is the minimum iOS version supported by the MC Unified Mobile SDK?"

**Should NOT trigger (❌)**
- "How do I set up Marketing Cloud MobilePush in the Marketing Cloud UI?" → **Help Navigator**
- "How do I call the Transactional Messaging API to trigger a push send?" → **MC Developer Navigator**
- "How do I implement SmartStore for offline data?" → **Platform Mobile Navigator**
- "What changed in the MC MobilePush SDK in the latest release?" → **Release Notes Navigator**

---

## Salesforce Platform Mobile Navigator

**Should trigger (✅)**
- "How do I implement SmartStore to cache Salesforce records offline on iOS?"
- "What is MobileSync and how does it sync data with Salesforce from a mobile app?"
- "How do I set up OAuth for a native mobile app connecting to Salesforce?"
- "How do I configure a Connected App for use with the Salesforce Platform Mobile SDK?"
- "How does the Salesforce Mobile SDK handle token refresh for long-lived sessions?"
- "What is the difference between SmartStore and MobileSync?"
- "How do I register a Salesforce Platform Mobile SDK app with a Connected App?"
- "How do I query offline data stored in SmartStore using a SoSL-like query?"
- "What conflict resolution strategies does MobileSync support?"
- "How do I integrate the Salesforce Platform Mobile SDK in a React Native app?"

**Should NOT trigger (❌)**
- "How do I configure the Salesforce mobile app in the Setup menu?" → **Help Navigator**
- "How do I implement push notifications in my Salesforce-connected iOS app?" → **MC MobilePush Navigator** (if using MC) or clarify SDK
- "How do I design the mobile data architecture for offline sync?" → **Architect Navigator**
- "What new features were added to the Salesforce Mobile SDK in Spring '25?" → **Release Notes Navigator**

---

## Edge Cases

These are prompts where two Navigators could both plausibly respond. The correct owner is named.

| Prompt | Correct Navigator | Why |
|---|---|---|
| "How does Data Cloud identity resolution work?" | **Help Navigator** | Configuration/behavior question — documentation lives on help.salesforce.com |
| "How do I call the Data Cloud Query API?" | **Developer Navigator** | API code question — documentation lives on developer.salesforce.com |
| "What is the architecture of a Data Cloud data model?" | **Architect Navigator** | Design/pattern question — documentation lives on architect.salesforce.com |
| "What changed in Data Cloud in Spring '25?" | **Release Notes Navigator** | Release history question |
| "How do I configure an Agentforce agent topic?" | **Help Navigator** | Setup/configuration in Salesforce Setup |
| "How do I write a custom agent action for Agentforce?" | **Developer Navigator** | Developer API / Apex implementation |
| "What is the recommended Agentforce architecture for high-volume?" | **Architect Navigator** | Architecture pattern question |
| "What new Agentforce features shipped in Summer '25?" | **Release Notes Navigator** | Release history question |
| "How do I use Marketing Cloud REST API in AMPscript?" | **MC Developer Navigator** | AMPscript + MC API = MC Developer domain |
| "How do I authenticate the Platform Mobile SDK to a Salesforce org?" | **Platform Mobile Navigator** | Platform Mobile SDK OAuth question |
| "How do I authenticate the MC SDK for push notifications?" | **MC MobilePush Navigator** | MC Unified Mobile SDK question |
| "What is the MC Account Engagement (Pardot) setup?" | **Help Navigator** | Configuration/setup question |
| "How do I call the Pardot REST API?" | **MC Developer Navigator** | Developer API question for Account Engagement |

---

## Cross-Domain Routing

These products span multiple official documentation domains. Questions are routed through the relevant Domain Navigators by documentation type. The authoritative routing table is in [PROJECT_STANDARD.md §7](../PROJECT_STANDARD.md).

### Agentforce

| Prompt | Navigator | Why |
|---|---|---|
| "How do I configure an Agentforce agent topic in Setup?" | **Help Navigator** | Setup/configuration — help.salesforce.com |
| "How do I create a custom Agentforce agent action in Apex?" | **Developer Navigator** | Developer API / Apex — developer.salesforce.com |
| "What is the recommended architecture for Agentforce in a high-volume contact centre?" | **Architect Navigator** | Architecture guidance — architect.salesforce.com |
| "What new Agentforce features shipped in Summer '25?" | **Release Notes Navigator** | Product release summary |
| "Is there a Trailhead trail to learn Agentforce?" | **Trailhead Navigator** | Learning content — trailhead.salesforce.com |

### Data Cloud

| Prompt | Navigator | Why |
|---|---|---|
| "How do I configure Data Cloud identity resolution in Setup?" | **Help Navigator** | Setup/configuration — help.salesforce.com |
| "How do I call the Data Cloud Query API?" | **Developer Navigator** | Developer API — developer.salesforce.com |
| "What is the recommended Data Cloud architecture for a B2C retailer?" | **Architect Navigator** | Architecture guidance — architect.salesforce.com |
| "What changed in Data Cloud in Spring '25?" | **Release Notes Navigator** | Product release summary |
| "Is there a Data Cloud certification on Trailhead?" | **Trailhead Navigator** | Learning content — trailhead.salesforce.com |

### Marketing Cloud Personalization

| Prompt | Navigator | Why |
|---|---|---|
| "How do I configure a Marketing Cloud Personalization campaign?" | **Help Navigator** | Setup/configuration — help.salesforce.com |
| "How do I call the Marketing Cloud Personalization API?" | **Developer Navigator** | Developer API — developer.salesforce.com |
| "How does Marketing Cloud Personalization fit into a multi-cloud architecture?" | **Architect Navigator** | Architecture guidance — architect.salesforce.com |
| "What's new in Marketing Cloud Personalization this release?" | **Release Notes Navigator** | Product release summary |
| "Is there a Trailhead module on Marketing Cloud Personalization?" | **Trailhead Navigator** | Learning content — trailhead.salesforce.com |

### CRM Analytics

| Prompt | Navigator | Why |
|---|---|---|
| "How do I configure a CRM Analytics dashboard?" | **Help Navigator** | Setup/configuration — help.salesforce.com |
| "How do I write a SAQL query for CRM Analytics?" | **Developer Navigator** | Developer / SAQL — developer.salesforce.com |
| "What is the recommended architecture for CRM Analytics with Data Cloud?" | **Architect Navigator** | Architecture guidance — architect.salesforce.com |
| "What changed in CRM Analytics in Winter '25?" | **Release Notes Navigator** | Product release summary |
| "Is there a CRM Analytics Trailhead trail?" | **Trailhead Navigator** | Learning content — trailhead.salesforce.com |

### MuleSoft

> Coverage is limited to Salesforce-hosted documentation. MuleSoft primary documentation (docs.mulesoft.com) requires a dedicated Navigator. See PROJECT_STANDARD.md §7.

| Prompt | Navigator | Coverage Notes |
|---|---|---|
| "How do I configure a MuleSoft connector in Anypoint Platform?" | **Help Navigator** | Salesforce-hosted content only |
| "What is the API-led connectivity architecture pattern for MuleSoft?" | **Architect Navigator** | Via architect.salesforce.com |
| "What changed in MuleSoft this release?" | **Release Notes Navigator** | Salesforce-hosted release notes only |
| "Is there a MuleSoft integration trail on Trailhead?" | **Trailhead Navigator** | Via trailhead.salesforce.com |
---

## Known Cross-Domain Edge Cases

Not every routing ambiguity indicates a problem with Navigator descriptions. Some Salesforce questions naturally span multiple documentation domains and may reasonably be handled by more than one Navigator depending on interpretation. The examples below are intentional cross-domain scenarios, not description defects.

### Q3 — Identity Resolution rollout across multiple business units

> "We need to roll out Identity Resolution across three business units — what configuration approach should we take?"

**Possible interpretations:**
- Configuration approach → **Help Navigator** (Identity Resolution setup in Salesforce Setup)
- Enterprise design strategy → **Architect Navigator** (multi-business-unit rollout as architecture decision)

This is an intentional cross-domain scenario. The question combines a configuration topic (Identity Resolution) with an enterprise scoping concern (three business units, rollout strategy). Either Navigator is a defensible response. Users seeking admin guidance should use the Help Navigator; users seeking architectural recommendations should use the Architect Navigator.

### Q8 — Should Contact Key equal Unified Individual?

> "Should Contact Key equal Unified Individual?"

**Possible interpretations:**
- MobilePush identity implementation → **MC MobilePush Navigator** (Contact Key as SDK concept)
- Data Cloud identity strategy → **Architect Navigator** (identity alignment across systems)

This is an intentional conceptual overlap at the MC MobilePush / Data Cloud boundary. Contact Key and Unified Individual are related concepts in a cross-cloud identity model. Questions about implementing Contact Key in the SDK belong to MC MobilePush Navigator; questions about the identity design strategy belong to Architect Navigator.

### Q5 — What changed in the Data Cloud Query API? (Primary Boundary to Monitor)

> "What changed in the Data Cloud Query API?"

**Expected owner: Developer Navigator**

Developer Navigator explicitly owns developer release notes, API version changes, and Data Cloud APIs. Release Notes Navigator explicitly excludes developer API and SDK changelogs. This boundary is intentional and bidirectional.

This scenario is the primary regression test for the Developer / Release Notes boundary. Future routing validation should evaluate this prompt first when checking for boundary drift between these two Navigators.


---

## Guardrail Tests

These tests validate that each Navigator follows its guardrails correctly — particularly the fetch-failure rule added in PROJECT_STANDARD.md §18 rule 5.

**How to run:** Install the skill in Claude Desktop, ask the prompt, and verify the Navigator's response matches the expected behavior. These are not routing tests — all prompts should trigger the named Navigator. The test is whether the *output* matches the guardrail.

---

### Fetch-Failure Guardrail

**Scenario:** The Navigator triggers correctly, but when it attempts to fetch from its approved source, the page returns a JavaScript-rendered shell (no real content), a timeout, or a loading placeholder.

**Expected behavior:**
- States explicitly which claims could not be verified from official sources
- Does NOT fill the gap with unapproved sources (community blogs, Salesforce Ben, vendor sites, etc.)
- Labels affected claims as **Not Verified** — retrieval failed, so no factual claim can be made (distinct from the claim being absent from the documentation)
- May offer to retry or suggest the user check the official URL directly

**Fail condition:** Navigator returns an answer citing Salesforce Ben, a vendor blog, a community post, or any source not in the Navigator's approved sources list — without disclosing the sourcing failure.

#### Help Navigator — fetch-failure test

**Prompt:** "How do I enable Einstein Conversation Insights for my org?"

**Why this tests the guardrail:** The answer lives on help.salesforce.com, which frequently returns JavaScript-rendered shells when fetched programmatically.

**Expected output:**
- Attempts to fetch from help.salesforce.com
- If fetch fails: states it could not retrieve verified content from official Salesforce Help documentation for this specific feature
- Does NOT cite Salesforce Ben, Trailhead community posts, or vendor blogs as authoritative sources
- May provide the direct URL for the user to check manually

---

#### Developer Navigator — fetch-failure test

**Prompt:** "What are the current API limits for the Salesforce Bulk API 2.0?"

**Why this tests the guardrail:** Limits pages on developer.salesforce.com are frequently updated and may return incomplete content.

**Expected output:**
- Attempts to fetch from developer.salesforce.com
- If fetch fails or returns incomplete content: states which specific limits could not be verified from official documentation
- Labels affected claims as **Not Verified** — retrieval failed; does NOT present any limits as authoritative
- Does NOT present limits as authoritative without a source

---

#### Architect Navigator — fetch-failure test

**Prompt:** "What does the Salesforce Well-Architected Framework say about reliability?"

**Why this tests the guardrail:** architect.salesforce.com pages are JavaScript-rendered and frequently return shells.

**Expected output:**
- Attempts to fetch from architect.salesforce.com
- If fetch fails: explicitly states it could not retrieve the Well-Architected Framework content from the official source
- Does NOT summarize from model memory as if it were retrieved documentation
- Labels affected claims as **Not Verified** — retrieval failed; does NOT summarize from model memory

---

#### Release Notes Navigator — fetch-failure test

**Prompt:** "What features shipped for Agentforce in the Summer '25 release?"

**Why this tests the guardrail:** Release notes pages are regularly updated and may not return full content on fetch.

**Expected output:**
- Attempts to fetch official Salesforce release notes
- If fetch fails: states it could not retrieve Summer '25 release notes from official documentation
- Does NOT fabricate feature announcements or pull from community summaries
- Labels affected claims as **Not Verified** — retrieval failed; does NOT present any feature list as authoritative

---

#### Trailhead Navigator — fetch-failure test

**Prompt:** "What modules are in the Agentforce for Administrators trail?"

**Why this tests the guardrail:** trailhead.salesforce.com is heavily JavaScript-rendered.

**Expected output:**
- Attempts to fetch from trailhead.salesforce.com
- If fetch fails: states it could not retrieve current trail content from official Trailhead documentation
- Does NOT list modules from model memory as if verified
- Labels affected claims as **Not Verified** — retrieval failed; suggests the user check Trailhead directly

---

#### Marketing Cloud Developer Navigator — fetch-failure test

**Prompt:** "What are the authentication scopes available for the Marketing Cloud REST API?"

**Why this tests the guardrail:** developer.salesforce.com/docs/marketing pages may return incomplete content.

**Expected output:**
- Attempts to fetch from developer.salesforce.com/docs/marketing
- If fetch fails: states which authentication scope details could not be verified from official MC developer documentation
- Does NOT cite community posts or vendor API guides as authoritative
- Labels affected claims as **Not Verified** — retrieval failed; does NOT present scope details as authoritative

---

#### MC MobilePush Navigator — fetch-failure test

**Prompt:** "How do I configure silent push notifications in the Marketing Cloud iOS SDK?"

**Why this tests the guardrail:** help.salesforce.com MobilePush pages are JavaScript-rendered.

**Expected output:**
- Attempts to fetch from help.salesforce.com (MobilePush section) or the SDK GitHub repo
- If fetch fails: states it could not verify the silent push configuration steps from official MobilePush documentation
- Does NOT provide steps from model memory without disclosing the sourcing failure
- Suggests the user check the official MobilePush SDK documentation or GitHub directly

---

#### Platform Mobile Navigator — fetch-failure test

**Prompt:** "What is the maximum number of records SmartStore can store per soup?"

**Why this tests the guardrail:** Platform Mobile SDK documentation pages may return incomplete content on fetch.

**Expected output:**
- Attempts to fetch from developer.salesforce.com (Platform Mobile SDK docs) or GitHub
- If fetch fails: states the SmartStore limit could not be verified from official Platform Mobile SDK documentation
- Does NOT state a number from model memory as a documented limit
- Labels affected claims as **Not Verified** — retrieval failed; does NOT state any limit as a documented fact

---

### Source Substitution Guardrail

**Scenario:** The Navigator triggers, the approved source fetch fails, and the Navigator is tempted to substitute an unapproved source.

**Expected behavior:** The Navigator must explicitly flag the sourcing gap — never silently substitute.

| Navigator | Forbidden substitution sources |
|---|---|
| Help Navigator | Salesforce Ben, SaaS Guru, Medium, admin community posts |
| Developer Navigator | Stack Overflow, Salesforce StackExchange, GitHub Issues (non-official) |
| Architect Navigator | Personal architecture blogs, LinkedIn posts, YouTube walkthroughs |
| Release Notes Navigator | Community release summaries, third-party changelogs |
| Trailhead Navigator | Community-created study guides, YouTube course summaries |
| MC Developer Navigator | Unofficial AMPscript references, vendor API guides |
| MC MobilePush Navigator | Third-party SDK tutorials, community SDK posts |
| Platform Mobile Navigator | Community mobile SDK guides, Stack Overflow answers |

**Test:** Ask any Navigator a question where the approved source fetch fails. Verify the response does not cite any source in the "Forbidden substitution sources" column for that Navigator without explicit disclosure that official documentation could not be retrieved.
