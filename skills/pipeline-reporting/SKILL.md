---
name: pipeline-reporting
description: Produce sales reports from the CRM — daily briefing, pipeline snapshot by stage or owner, win/loss analysis, revenue by close month — and render them as a Frame. Use when the user asks "what's closing this week", "pipeline snapshot", "win rate by rep", or "daily sales briefing".
---

# Pipeline Reporting

**Required toolsets:** Salesforce · Frames (rendering) · optional: Snowflake (deep analysis), Slack (delivery)

## Source of truth

The Salesforce toolset's own object and field metadata is authoritative. Before aggregating:
- Stage names are org-specific — read them from the opportunity stage metadata, and use the `IsClosed` / `IsWon` flags rather than matching stage names by string.
- Amounts come back as strings in some tool outputs — convert to numbers before arithmetic.
- Owner IDs are opaque — resolve them to names via the user/owner object once, then join client-side.
- Result pages cap out — if a query returns exactly the page limit, paginate before aggregating or your totals will be silently wrong.
- For heavy historical analysis, prefer the Snowflake connection over paging the CRM API.

## 1. Daily briefing

- **Closing in the next 7 days:** open opportunities with a close date inside the window — name, amount, close date, owner.
- **Updated in the last 24h:** open opportunities modified since yesterday — name, amount, stage, last modified.
- **Open-pipeline summary line:** count and total value of all open opportunities.

Deliver as a short message, or post to the team's Slack channel on request. For a recurring version, attach this skill to an agent with a morning **schedule/trigger**.

## 2. Pipeline snapshot

- **By stage:** count and total amount per stage, sorted by value, with stage names resolved from metadata.
- **By owner:** count and total amount per owner, with owner names resolved.

Render as a Frame: a bar chart per stage plus a sortable owner table beats a text dump for anything more than five rows.

## 3. Win/loss analysis

Scope with a close-date range. Won = closed and won; lost = closed and not won.

- **Closed won / lost in a period:** list with name, amount, close date, owner.
- **Win rate by rep:** group closed opportunities by owner; report won/total, win rate %, and won value, sorted by won value.
- **Revenue by close month:** group won opportunities by close month; report deal count and revenue per month.

## Known limitations

- Stage probability fields are unreliable across orgs — use the closed/won flags on opportunities instead.
- If there is no team object, group by owner and map owners to teams client-side.

---
*Adapted for Dust from `hubspot/agent-cli-skills/sales-reporting` (skills.sh). Original targeted the HubSpot CLI; this version targets the Dust Salesforce toolset with Frames for rendering.*
