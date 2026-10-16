# Engineering Handoff Note

> Module 4 · Production Specs. Open the black box, make the build legible to an engineer.

## What this is

_One paragraph an engineer can read in 60 seconds._

This is a clickable digital-banking dashboard prototype for bank employees deciding which customer-facing tools need improvement. It tests whether plain-language friction signals, filtering, and recommended actions make a dashboard more useful—but the hypothesis has not been validated. The prototype contains six screens, shared reporting filters, an exact-value chart, CSV export, and tool-detail drawers with illustrative customer reviews. Its React/TypeScript code is organised by feature, separating presentation from sample data, calculations, and state. Everything meaningful currently runs in the browser: sign-in is demo-only, figures and reviews are fabricated, and research counters are local. It is suitable for usability testing, not operational decisions or production banking access.

## Architecture (plain language)

- **Frontend:** React, TypeScript, and Vite, running inside the mockup sandbox. six screen components are SignIn, DigitalBankingOverview, DigitalChannels, Journeys, Segments, and Frictions. ToolDetails, CustomerReviews, and ResearchControls are supporting components—not separate screens
- **Backend / data:** A separate Express API exists in artifacts/api-server, currently exposing /api/healthz. The banking prototype does not call that API. No bank analytics, authentication service, or database backs its screens. Overview generates 365 days of synthetic daily activity. Business-area and platform selections apply fixed multipliers. Frictions generates a separate 730-day observation model, then filters, aggregates, ranks, and calculates comparisons locally. Tool descriptions, recommendations, and reviews are authored fixtures. Journeys and Segments are fixed illustrative records. Session storage retains considered tools, research counters, and the latest comprehension response where available. Login and reporting selections are not durable preferences.
- **Key flows:** - Demo entry: Validate email format and a trimmed password length of at least eight characters → open Overview. There is no identity verification.
- Discovery: Date, business-area, and platform selections persist across Overview, Digital channels, and Frictions. Journeys and Segments remain unfiltered.
- Investigation: Open a tool → inspect context and reviews → expand its recommended action → optionally mark it considered.
- Reporting: Hover or focus chart points for exact values; export the selected daily aggregates—not merely the sampled chart points.
- Prototype research: Expand the normally collapsed controls to inspect local counters, preview loading/empty/error states, and record comprehension feedback.

## What's solid vs. what's duct tape

| Area | State | Notes |
|---|---|---|
| Feature-based organisation and pure calculation modules. | solid | _____ |
| Sign-in is an in-memory UI gate, not authentication or authorisation. | rough | _____ |

## Risks & assumptions for the team

No operational use: Do not enter real passwords or use the sample figures to make banking decisions. Reloading returns to sign-in.
Hypothesis measurement is missing: Local clicks do not establish lower employee-dashboard bounce, repeat usage, or influence on team iterations.
Two different bounce concepts: The displayed synthetic bounce KPI concerns customer-channel sessions; the hypothesis concerns employees using this dashboard.
Cross-view figures do not reconcile: Overview and Frictions use different sample models and history lengths. “Since inception” means available sample history, not verified bank history.
Priority is not severity: Current ranking and priority rules do not establish customer harm or business risk. Metric definitions—including “Transfer verification”—need agreement before real integration.
Dates depend on the browser clock: Relative histories move with the current date. Regression tests use a fixed reference date and UTC.
Known labels need clarification: A static Retail banking heading can remain visible under another selected business area. Scope/history clarification and repeatable browser coverage are already in progress; do not assume those changes have landed.
The product scope and unresolved questions are documented in deliverables/digital-banking-prototype-prd.md.

## How to run it

```
Use **Node.js 24**, pnpm, and the installed workspace dependencies. From the project root:

```sh
PORT=8081 BASE_PATH=/__mockup \
pnpm --filter @workspace/mockup-sandbox run dev
```

Both environment settings are required by the Vite configuration.

Open the preview at:

```text
/__mockup/preview/banking-dashboard/BankingPrototype
```

The legacy `/__mockup/preview/banking-dashboard/Dashboard` entry remains compatible.

For demo sign-in, use `tester@bank.example` and a **made-up password of at least eight characters**. No actual account is required.

Run the checks and build:

```sh
pnpm --filter @workspace/mockup-sandbox run test:banking
pnpm --filter @workspace/mockup-sandbox run typecheck

PORT=8081 BASE_PATH=/__mockup \
pnpm --filter @workspace/mockup-sandbox run build
```

The separate API server is not required for the prototype’s data or interactions.
```
