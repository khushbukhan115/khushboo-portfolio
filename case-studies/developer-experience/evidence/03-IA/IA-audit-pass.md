# Deliverable 3 · IA Audit Pass

A nine-lens audit of `Deliverable-3-IA-Current-Portal-Improvement.html` before we commit it as the canonical assignment IA. Each lens runs against the existing IA proposal and produces findings tagged Critical / High / Medium / Low. Findings are coded A1.1, A1.2 etc to avoid collision with the F-codes from the original audit (Deliverable 1).

**Audited file:** `Deliverable-3-IA-Current-Portal-Improvement.html`
**Audited by:** Khushboo Khan
**Date:** May 15, 2026
**Audit codes:** A[lens].[finding]

---

## Methodology

Nine lenses applied in sequence. Each lens has a single question. Findings record what is missing, ambiguous, or wrong. Severity reflects impact on the IA's ability to ship without rework, not impact on the overall product.

The audit does not modify D3. It produces a finding list with recommendations. Three findings are flagged as **decision gates** requiring approval before being applied. The remaining eighteen findings are auto-applyable as polish.

---

## Summary

| Lens | Question | Findings | Severity mix |
|---|---|---|---|
| 1 · Group composition | Right items in right groups? | 2 | 1 Med · 1 Low |
| 2 · Cross-link integrity | Every promised route has source and destination? | 2 | 1 Med · 1 Low |
| 3 · F-code coverage | Did the IA actually resolve the audit's 40 findings? | 1 | 1 High |
| 4 · Persona path completeness | All 8 personas walk through cleanly, even off-path? | 4 | 1 High · 2 Med · 1 Low |
| 5 · SDK-axis consistency | Works for every SDK, not just NET? | 3 | 1 High · 2 Med |
| 6 · Missing surfaces | What did D3 not address? | 3 | 1 High · 2 Med |
| 7 · Naming precision | Labels strong, unambiguous, not academic? | 2 | 2 Med |
| 8 · Implementation realism | All surfaces buildable in Part 2 scope? | 1 | 1 Med |
| 9 · Mobile + a11y carry-over | Did D3 carry forward audit findings? | 3 | 2 Med · 1 Low |
| **Total** |  | **21** | **4 High · 13 Med · 4 Low** |

**Zero criticals.** The IA is sound. The findings are polish-level except for three decision gates noted at the end.

---

## Overall verdict

**The IA holds.** Quick Start, Build, Reference, Operate is the right four-group structure. No finding in this audit invalidates the core proposal. Twenty-one findings are clarifications, placements, and explicit-statement gaps. Apply them and the IA becomes airtight.

Three findings are decision gates. They cannot be applied without your approval because they change a placement choice or require a strategic call.

---

## Findings by lens

### Lens 1 · Group composition

**Question:** Are the right items in the right groups? Is anything orphaned, double-homed, or miscategorized?

**A1.1 · Medium · Changelog placement is inconsistent.**
The D3 secondary nav lists Changelog under Reference. The implementation table splits `/resources` into "SDKs & OpenAPI" and "Error codes" but does not place Changelog. Result: Changelog is implied but never explicitly assigned a node.
**Recommendation:** Add Changelog as an explicit row in the implementation table. Home it under Reference › Changelog. Apply: yes.

**A1.2 · Low · Try It Out has two homes without rule of primacy.**
Try It Out appears as a standalone node in Reference and as an inline component on every endpoint page. The IA does not specify which is primary.
**Recommendation:** Inline-on-endpoint is primary. Standalone `Reference › Try It Out` is a playground fallback for users without a specific endpoint in mind. State this explicitly in the IA description. Apply: yes.

---

### Lens 2 · Cross-link integrity

**Question:** Every routing rule promised in D3 (and re-stated in D4). Does each have a clear source surface and destination surface?

**A2.1 · Medium · Routes out of Quick Start are not explicit.**
D3 details routes between Build, Reference, and Operate, but routes from Quick Start to the other three groups are implied rather than stated. When a developer finishes Quick Start › First call, where does the IA send them?
**Recommendation:** Add "Next step" CTAs on Quick Start › First call: "Build a real integration → Build › First integration" and "Browse the API → Reference › Endpoints". Apply: yes.

**A2.2 · Low · Conditional cross-link behavior is undefined.**
The IA promises every endpoint page links to "Used in walkthrough". If no walkthrough exists for an endpoint, what happens?
**Recommendation:** Hide the link by default. If the endpoint has no walkthrough, show "Ask Copilot to draft a walkthrough" instead. Apply: yes.

---

### Lens 3 · F-code coverage

**Question:** The 40 findings in Deliverable 1. Walk each and verify the IA resolves it, or explicitly note it as out-of-scope for IA.

**A3.1 · High · F-code coverage matrix does not exist in D3.**
D3 names a handful of F-codes inside its "Resolves" tags on individual cards, but it never produces a complete matrix mapping all 40 F-codes to IA resolution / content fix / UI fix / a11y fix / out-of-scope. Reviewers cannot verify coverage at a glance. Risk: silent gaps.
**Recommendation:** Add a coverage matrix appendix to D3. Two columns: F-code + resolution path. Group rows by resolution type: "Resolved by IA", "Resolved by content", "Resolved by UI", "Resolved by accessibility pass", "Out of IA scope". Apply: yes. **This is the highest-leverage finding in the audit because it lets a hiring manager verify the IA covers what the audit identified.**

---

### Lens 4 · Persona path completeness

**Question:** All 8 personas walked end to end through D3. Stress-test off-path cases.

**A4.1 · High · Compliance content placement is ambiguous. Decision gate.**
D3 says Compliance is "planned as Operate › Runbook sibling" but never explicitly places it. Reza cannot evaluate without it, and his path is the strongest persona-level argument for the IA.
**Recommendation:** Make a decision. Two viable options.
- Option A: Compliance lives under Quick Start (alongside Overview, Authentication). Pro: Reza sees it before any auth. Con: dilutes Quick Start.
- Option B: Compliance lives under Operate (alongside Runbook). Pro: matches operational-maturity signaling. Con: Reza has to navigate through Operate to find it during evaluation.
**My recommendation:** Option A (Quick Start › Compliance). Reza never reaches Operate during evaluation. He needs the compliance evidence at the entry surface. Decision gate.

**A4.2 · Medium · SDK landing page is not specified.**
What does `/net-standard-library/` (root inside an SDK with no further path) show? D3 does not define this.
**Recommendation:** SDK landing shows: working curl in the SDK's language, capability hint strip ("What can the .NET SDK do"), and direct links to each of the four groups for that SDK. Apply: yes.

**A4.3 · Medium · SDK-switching context preservation is undefined.**
If Diego is on `/net/walkthroughs/first-integration/step-3` and switches the SDK picker to Python, where does he land?
**Recommendation:** Preserve topic context. If the equivalent page exists in the target SDK, route there. If not, fall back to that SDK's Quick Start with a banner: "This walkthrough is not yet available in Python. Start here." Apply: yes.

**A4.4 · Low · Auth-gated vs public Operate surfaces are not specified.**
Status and Deprecations should be public for Diego-Ops's evaluation. Logs and Webhook events are per-account, so they require auth.
**Recommendation:** Document the access model. Status / Deprecations / Rate limits (general) / Runbook are public. Logs / Webhook events / Rate limits (your usage) are auth-gated. Apply: yes.

---

### Lens 5 · SDK-axis consistency

**Question:** Does the four-group structure replicate cleanly inside every SDK, or is some content cross-SDK?

**A5.1 · High · Operate group URL structure is undefined. Decision gate.**
Operate content (Status, Deprecations, Rate limits, Runbook) is cross-SDK. It applies to the API, not to any specific SDK. D3 does not say whether Operate lives at `/operate/...` (portal root) or `/[sdk]/operate/...` (duplicated per SDK).
**Recommendation:** Operate lives at portal root: `/operate/status`, `/operate/deprecations`, etc. Each SDK's left rail links into the same root surfaces. Duplication is wasteful. Logs and Webhook events stay under the user's account scope, not under an SDK. Decision gate because it changes URL conventions.

**A5.2 · Medium · Walkthroughs may be partially SDK-agnostic.**
A walkthrough's narrative is usually the same across SDKs; only the code samples differ.
**Recommendation:** Author walkthroughs once at `/build/walkthroughs/...` with code samples per language. The SDK picker filters which walkthroughs have code in that SDK's language. Apply: yes.

**A5.3 · Medium · Empty-group behavior is not defined.**
If Python SDK has no Recipes yet, does the Recipes node show empty? Hide?
**Recommendation:** Group header shows. Empty sub-state reads: "No Recipes for Python yet. Ask Copilot for a custom one, or browse Recipes in other SDKs." Apply: yes.

---

### Lens 6 · Missing surfaces

**Question:** What does the portal have or need that D3 did not address?

**A6.1 · High · API versioning is not addressed. Decision gate.**
APIs ship v1 and v2 alongside each other. A developer reading `/reference/albums/get` needs to know which version. D3 does not say.
**Recommendation:** Add API version to the SDK picker. The picker becomes a two-part selector: SDK × API version. Default: latest stable. Deprecation calendar in Operate links into the picker. Decision gate because it touches the persistent navigation pattern.

**A6.2 · Medium · Out-of-IA pages (pricing, account, support, login) are not acknowledged.**
A developer portal has surfaces outside the four cognitive groups: pricing, account/profile, support, login, terms.
**Recommendation:** Acknowledge them as out-of-IA. Recommend a top-right utility cluster (Sign in / Pricing / Support) separate from the four-group rail. Footer for terms / privacy / cookies. Apply: yes.

**A6.3 · Medium · Search results page format is not specified.**
D3 mentions Cmd-K opens search grouped by intent. The actual results page layout is not specced.
**Recommendation:** Results page groups by Quick Start / Build / Reference / Operate. Max 3 results per group above the fold. "More in [group]" link expands per group. Empty state suggests Copilot. Apply: yes.

---

### Lens 7 · Naming precision

**Question:** Are the labels strongest possible? Any academic, ambiguous, or borrowed-from-IA-vocabulary names?

**A7.1 · Medium · "SDKs & OpenAPI" is a compound node.**
The current node combines two distinct concepts. SDKs are libraries to install. OpenAPI is a machine-readable spec to download.
**Recommendation:** Split into two siblings under Reference: `Reference › SDKs` and `Reference › OpenAPI spec`. Apply: yes.

**A7.2 · Medium · "Logs & Runbook" is a compound node.**
Logs are a usage log. Runbook is an incident response guide. Different surfaces, different intents.
**Recommendation:** Split into two siblings under Operate: `Operate › Logs` and `Operate › Runbook`. Apply: yes.

---

### Lens 8 · Implementation realism

**Question:** Are all the new Operate and Build surfaces buildable in a Part 2 Figma scope, or are some aspirational?

**A8.1 · Medium · Implementation phasing is not called out.**
The six Operate surfaces vary widely in build cost. Runbook is content-only. Logs require per-key telemetry storage. The Figma can show all six but the engineering ship is staged.
**Recommendation:** Add an "Implementation phasing" section to D3. Wave 1: content-only (Recipes, Migrations, Runbook). Wave 2: status pipeline + deprecation policy (Status, Deprecations). Wave 3: per-key telemetry (Logs, Rate limits, Webhook events). Apply: yes. Reviewers see realistic delivery cadence, not a flat "build everything" list.

---

### Lens 9 · Mobile and accessibility carry-over

**Question:** Did D3 explicitly carry forward the audit's accessibility findings and address mobile / responsive behavior for the four-group rail?

**A9.1 · Medium · Mobile rail behavior is not specified.**
The four-group rail is a desktop pattern. D3 does not say what happens on narrow viewports.
**Recommendation:** Below 980px the rail collapses to a hamburger. Four groups become a sheet menu. Group headers anchor at the sheet top, secondary nodes scroll. Breadcrumb stays in the header but truncates middle. Apply: yes.

**A9.2 · Medium · A11y findings from Deliverable 1 are not explicitly acknowledged.**
F8.1 through F8.6 from the audit are content / UI / component-level. They are not directly resolved by IA. But D3 should state this explicitly so reviewers do not assume coverage.
**Recommendation:** Add a brief "Accessibility scope" note to D3: "Component-level a11y (focus traps, keyboard navigation, contrast) is addressed in the wireframe spec at Deliverable 2 and in the design system handoff, not at the IA level. The IA contributes by giving every navigable surface a clear semantic hierarchy." Apply: yes.

**A9.3 · Low · Breadcrumb mobile truncation behavior is undefined.**
A breadcrumb like `NET Standard Library › Reference › Endpoints › Albums › Get an album` does not fit on a 360px viewport.
**Recommendation:** On mobile, truncate the middle: show first crumb plus current crumb (e.g., `NET ... › Get an album`). Long-press / tap reveals the full chain. Apply: yes.

---

## Decision gates

Three findings change a placement choice or a structural convention and require your approval before being applied. The other eighteen findings are auto-applyable as polish.

**Gate 1 · A4.1 · Compliance placement.**
- Option A: Quick Start › Compliance (my recommendation, serves Reza at evaluation)
- Option B: Operate › Compliance (signals operational maturity)
- Your call.

**Gate 2 · A5.1 · Operate URL structure.**
- Option A: `/operate/...` at portal root (my recommendation, avoids per-SDK duplication)
- Option B: `/[sdk]/operate/...` duplicated per SDK (consistent with SDK-first URL pattern but wasteful)
- Your call.

**Gate 3 · A6.1 · API versioning surface.**
- Option A: SDK picker becomes a two-part SDK × Version selector (my recommendation)
- Option B: Treat each API version as a distinct SDK in the picker (simpler but loses semantic grouping)
- Option C: No versioning surface for now, defer to Wave 2 (acceptable but flags the gap)
- Your call.

---

## Recommended auto-apply fixes

Eighteen findings can be applied without your approval. Each is a documentation gap, an explicit-statement gap, or a placement clarification. Listed below in priority order:

1. A3.1 · Add F-code coverage matrix appendix to D3 (high leverage)
2. A1.1 · Add Changelog to implementation table
3. A1.2 · State Try It Out primacy rule
4. A2.1 · Add Next-step CTAs out of Quick Start
5. A2.2 · Define conditional cross-link behavior
6. A4.2 · Specify SDK landing page contents
7. A4.3 · Specify SDK-switching context preservation
8. A4.4 · Document Operate access model (public vs auth-gated)
9. A5.2 · State walkthroughs are cross-SDK by default
10. A5.3 · Define empty-group behavior
11. A6.2 · Acknowledge out-of-IA utility pages
12. A6.3 · Spec search results page format
13. A7.1 · Split "SDKs & OpenAPI" into two siblings
14. A7.2 · Split "Logs & Runbook" into two siblings
15. A8.1 · Add implementation phasing section
16. A9.1 · Spec mobile rail behavior
17. A9.2 · Add accessibility scope note
18. A9.3 · Spec breadcrumb mobile truncation

---

## What this audit confirms

The IA is structurally sound. Four groups is the right shape. Quick Start was correctly kept. Build, Reference, Operate are clean and unambiguous. The cross-link logic is internally consistent. The persona pass holds.

What the audit catches is the gap between "the IA is right" and "the IA is fully documented". Twenty-one places where the proposal makes a choice but does not state it. Three places where it makes an implicit choice that needs a decision.

Apply the eighteen auto-fixes. Make the three decisions. The IA is ready to ship as the canonical assignment artifact.
