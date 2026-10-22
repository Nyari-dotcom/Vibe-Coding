# Full-Stack: Data, Access Rules, Edge Cases, Deploy

> Module 5 · Full-Stack. Add data schemas, access rules, and edge cases; stress-test and deploy.

## Deployed link

_The working, shareable link that survives real users._

_____

## Data schema

| Entity | Key fields | Notes |
|---|---|---|
| Digital tool / channel | id, name, channel, businessArea, friction, description, signal, action, actionDetail, team | Hardcoded catalogue of banking tools, friction signals, and recommended actions. |
| Customer review | text, rating, dateTime, dateLabel, context | Mock reviews associated with tools. Ratings and timestamps are illustrative—not collected from customers. |

## Access rules

_Who can see / do what? Where are the auth boundaries?_

Add a repeatable two-user integration check for Clerk-authenticated invitation summary requests and pooled-connection reuse. The fixture regression in artifacts/api-server/tests/invite-summary.database.ts uses the real router/SQL but deliberately replaces Clerk identity lookup; it does not validate the actual authentication-to-database identity chain. Use secure development Clerk sessions (never committed or printed), alternating/concurrent requests from both users, and an unsigned request; verify known separate totals, 401 denial, and that client-supplied identity parameters cannot change ownership. Relevant files: artifacts/api-server/src/app.ts, src/routes/invites.ts, artifacts/mockup-sandbox/browser-tests/banking/fixtures.ts and invitations.spec.ts. Keep synthetic fixtures safely scoped and cleaned, and explicitly skip if secure development sessions are unavailable.

## Edge cases hardened

| Case | Before | After |
|---|---|---|
| Empty / first-run state | Email address - nothing happens | Please fill in this field |
| Bad / malicious input | Email address - incorrect format (there were no parameters in place) | Please match the format requested Example format name @example.com |
| Failure / offline | Sign in with an email address that doesn't exist - nothing happened | Couldn't find your account |

## Stress test results

_What you threw at it, and what held / broke._

_____
