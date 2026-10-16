# Living PRD

> Module 4 · Production Specs. Refactor for readability; extract a living PRD that stays true as the build evolves.

## Problem

_What user problem does this solve? Tie to the validated hypothesis._

A plain-language landing dashboard covering banking apps and tools, with useful filters, visible friction points, and recommended actions, will help bank employees find and use the information rather than abandon the dashboard or rely on unverified alternatives.

Expected evidence is lower employee-dashboard bounce, increased repeat use and drill-down, and evidence that teams explore friction and recommendations during product iterations.

## Users & jobs

- **Primary user:** Bank employees responsible for prioritising and improving customer-facing digital apps and tools. Product leads are the clearest primary decision-making role; growth analysts and marketing managers are supporting users. Bank customers are the people whose experiences are represented, not the dashboard’s intended users.
- **Job to be done:** When deciding what to improve in a banking app or tool, I want to identify relevant customer friction, understand its evidence and context, and assess a recommended investigation so that my team can make a defensible next-step decision.  Supporting jobs:  Narrow the information to a reporting period, business area, and platform. Find a particular tool or friction without navigating multiple unrelated reports. Inspect exact trend values rather than infer them from a chart. Distinguish reach and period change from severity or confirmed harm. Read relevant customer feedback alongside an issue. Explore a proposed action and mark it as considered. Core flow: Demo sign-in → Overview → choose scope or find a tool → inspect friction/tool details and reviews → explore a recommendation → optionally mark considered. Frictions provides a second entry point through ranked issues and a scoped priority signal. Journeys and Segments provide additional illustrative context.

## Scope

- **In:** - Local demo email/password validation leading to Overview.
- Overview with four summary widgets, engagement/task-completion trend, and digital-channel tool list.
- Shared reporting-period, business-area, and platform selection on Overview, Digital channels, and Frictions.
- Tool search and channel/friction-level filtering on the tool list.
- Tool-detail drawer, illustrative reviews, expandable actions, and local considered status.
- Frictions register with contextual explanations, affected-session samples, prior-period changes, recommended investigations, and a scoped priority signal.
- Journeys and Segments navigation with fixed illustrative records.
- Overview skeleton, empty, and simulated fetch-error states.
- Trend CSV download, local interaction counters, and a closed-by-default research/comprehension panel.
- Responsive layout and basic keyboard interactions.
- **Out (explicitly):** - Real bank authentication, work-email ownership checks, SSO, role-based access, or secure production sessions.
- Connections to approved bank analytics, customer-review systems, or operational data sources.
- A complete bank-wide app/tool inventory.
- Production ingestion, metric governance, freshness monitoring, audit trails, or reconciled cross-view data.
- Team assignment, shared decisions, saved investigations, release tracking, or proof that a recommendation was implemented.
- Persistent multi-user research results or centrally collected analytics.
- Real measurement of dashboard bounce, repeat use, source substitution, decision quality, or iteration outcomes.
- Evidence validating the hypothesis, or agreed numerical success/pivot thresholds.
- Filtering Journeys and Segments by the shared scope; those views currently show fixed samples.

## Requirements

| # | Requirement | Priority | Acceptance criteria |
|---|---|---|---|
| 1 | Current: prototype-only sign-in | Must | Given an invalid email format or a password shorter than eight trimmed characters, submission shows a validation error. Given a valid-format email and a made-up password meeting that minimum, the user enters Overview. Passwords are not transmitted or persisted and are cleared after successful submission. The screen warns against using a real work password. |
| 2 | Current: employee-facing landing view | Must | After demo sign-in, Overview presents operational information in plain language. Hypothesis text, interview quotes, and baseline research claims do not appear in the default employee view; research controls remain collapsed. |

## Data & events

_What gets stored, what gets tracked._

| Area | Current data and behaviour | Limitation |
|---|---|---|
| Overview metrics | Deterministically generated daily samples covering 365 days relative to the browser’s date. The latest 30-day all-scope totals are calibrated to 141,840 sessions, 90,776 completions, 85,104 bounces (60%), and 6,140 transfer-verification entries. | No analytics service is queried. Business-area/platform selections apply fixed multipliers, not independently measured segment data. |
| Tool inventory | Nine hardcoded tools with names, channels, business areas, observation dates, friction labels, signals, and actions. | Not a complete or verified banking estate. Date filtering uses each tool’s observation date rather than daily activity. |
| Frictions | Nine tool-linked issues and 730 days of deterministic fabricated daily observations. Scope/date filtering, ranking, totals, and complete-prior-period comparisons execute locally. | Separate sample model from Overview; figures are not measured errors, unique customers, or proven harm. |
| Journeys and Segments | Fixed illustrative records with sample completion/context or customer-group figures. | Not live, and not filtered by the shared scope. |
| Customer reviews | Tool-specific authored text, sample ratings of 2/5 and 3/5, and fixed February 2025 timestamps. | Not imported customer feedback or corroboration of the generated observation windows. |
| Sign-in | Local format/length validation and in-memory navigation state. | No identity verification or secure authentication. Reload returns to sign-in; this is not a production access boundary. |
| Loading/error | A short timer and research controls simulate request states. | No banking-data fetch, genuine connection-loss detection, retry/backoff, or offline recovery. |
| Persistence | Browser session storage keeps local counts, considered tool IDs, and the last comprehension response where storage is available. | Not shared across teammates, not a durable research dataset, and not an audit log. Scope/navigation choices are not saved as durable preferences. |

## Open questions

1. What evidence, if any, validates the problem or hypothesis? Who participated, what tasks were observed, and what were the results?
2. What are the verified sources and time windows for the 74%, 12 charts, six clicks, and 60% baseline claims?
3. What numerical changes in employee-dashboard bounce, return use, task success, and action exploration constitute success? How many participants struggling would trigger the pivot rule?
4. What counts as a meaningful interaction, a completed analysis task, a return visit, and genuine use of a recommendation during an iteration?
5. Which bank, decision-making roles, and business-area owners are in the first evaluation cohort? Who approves metric definitions and operational use?
6. Should business area remain Retail banking/Business banking/Wealth, or represent capabilities such as Transfers and Card management? Should platform remain Mobile app/Web app or distinguish iOS, Android, mobile web, and desktop web?
7. What exactly does Transfer verification measure—attempts, failures, timeouts, or affected sessions? The current Android-specific widget note does not match the broader platform selector and needs resolution before operational use.
8. How should tool observation dates, Overview’s 365-day history, and Frictions’ 730-day history align? What should “Since inception” mean consistently?
9. Should issue ranking prioritise affected sessions, greatest deterioration, severity, business risk, or a governed combination? How should priority behave when every issue is improving?
10. Are affected-session totals unique within and across issues? What denominators are needed to compare rates fairly between tools and platforms?
11. Should Journeys and Segments adopt shared filters and drill-down, or remain contextual supporting views?
12. Which approved systems will supply metrics and reviews, with what freshness, retention, permissions, redaction, and outage handling?
13. What should happen after “Mark considered”—local bookmarking, shared triage, owner assignment, an experiment, or a tracked product change?
14. What production identity/access controls and accessibility/security assurance would be required if the project moves beyond the explicitly prototype-only scope?
15. Should the required error wording “Connection lot.” be corrected to “Connection lost.”? The prototype currently preserves the supplied text exactly.
