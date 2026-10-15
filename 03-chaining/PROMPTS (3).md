# PROMPTS.md: Living Prompt Pack

> Module 3 · Prompt Chaining. Re-architect the build with prompt chains; capture the reusable ones here.

## How to use this pack

_Each prompt is a reusable step. Chain them: the output of one becomes the input to the next._

## Prompt chain: Dashboard detailed screens

### Step 1: Expand, build new screens in a strict sequence
```
Build the next phase of this app in a strict sequence:
1. Expand on the Digital banking overview screen: Add a business area and platform selector on this overview so that you can filter the data you would like to view. 
2. Expand on the Digital banking overview screen on the daily engagement/task-completion trend chart:  When you hover on the trend chart, it show you the exact number that you have hovered over.
3. Add additional entry points on the left tab:  The additional tabs to be added are Journeys, Segments, Frictions.  Write the logic so when each of these tabs are clicked on, show data relevant to the tab clicked on.  
4. A login screen where a user logs in using their work email address and password. Build it so that the login screen links to the Digital banking overview screen if the user manages to successfully login.
5. Add a review section on the digital channels widget:   When a user clicks on a row and additional information is displayed, add a section on this additional information space that shows any reviews that customers have raised. Each reviews should contain a 5 star rating,  date and time when the review was provided, any additional information complement the friction being raised.
```

### Step 2: Behavior, hard-code the states
```
Apply the following logic constraints to the Digital banking overview screen flow:
- Use skeleton screens for the Four summary widgets—sessions, bounce rate, task completions, and transfer verification—plus a daily engagement/task-completion trend chart loading state.
- If no data is present, show the empty state: "There is currently no data to display.".
- On fetch failure, trigger the error state: "Connection lot. Please refresh the dashboard or come back later.".

Maintain the same design language throughout and tether all behavior strictly to these rules.
```

### Step 3: Refine, one surgical polish
```
The Friction page needs detail on the page to enable the user to understand the issues.
1.  Update the filter elements to incorporate the ability to filter by date, business area and platform to match.
2. Add the priority signal, and the useful distinction like on this page - https://the-dashboard-nobody-reads.replit.app
```

## Reusable techniques learned

- _____
- _____

## What broke (and the fix)

_Where a single mega-prompt failed and chaining fixed it._

_____
