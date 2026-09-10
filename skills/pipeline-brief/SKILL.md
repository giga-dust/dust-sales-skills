---
name: pipeline-brief
description: Surfaces what moved in the pipeline (and what stalled), explains why, and produces a 2-week action brief. Use when the user asks for a "pipeline brief", "what moved this month", "sales brief", or a periodic review of wins and slow movers. Accepts an optional lookback window of 30, 60, or 90 days.
---

# Pipeline Brief

Run the pipeline analysis and action brief. Pull what advanced (and what didn't), explain why, and produce a ready-to-use action plan that acts on the data.

**Required toolsets:** Salesforce · Slack (delivery) · company data (Gong transcripts, Zendesk/Intercom for risk signals)

Parse arguments:
- `lookback` (default: `30d`) — `30d`, `60d`, or `90d` lookback window

## Step 1 — Pipeline breakdown

1. Query Salesforce opportunities created or modified in the lookback period, grouped by stage and owner.
2. Rank accounts/opportunities by: total value, stage velocity, and engagement (activities logged).
3. Calculate each segment's share of total pipeline vs. the prior equivalent period.

**Movers:** opportunities that advanced a stage or grew in value.
**Stalled:** opportunities with no stage change and no logged activity in the window, or below the median engagement level.

## Step 2 — Seasonality check

1. Compare the current period to the same period in the prior year (Salesforce history).
2. Flag segments with a seasonal pattern (e.g. end-of-quarter spikes, summer slowdowns).
3. Note any new segments or products with insufficient history to detect seasonality.

## Step 3 — Why analysis

For each mover and stalled opportunity, explain the likely driver:
- Champion change, pricing discussion, competitor move, seasonal demand, expansion signal
- Cross-reference with Gong call transcripts and Slack deal-channel activity for the period
- Check Zendesk/Intercom in company data for support friction on at-risk accounts
- Note where attribution is inferred vs. confirmed

## Step 4 — 2-week action brief

Produce a ready-to-use brief:

```
2-Week Action Brief — {date range}

PUSH THESE (movers)
• {account}: {suggested next step} — {channel: email|call|both}

UNBLOCK THESE (stalled)
• {account}: {re-engagement angle or multithread suggestion} — {channel}

ACTION CALENDAR
Week 1:
  Mon: {action}
  Wed: {action}
  Fri: {action}
Week 2:
  Mon: {action}
  Wed: {action}
  Fri: {action}
```

## Connection failures

If Salesforce is unreachable, stop — the analysis requires the CRM. If Gong transcripts are missing from company data, skip call cross-reference in the "why analysis" and note it.

## Approval gates

- **Never auto-send outreach or post to Slack channels automatically.** The brief is for the rep's review only.
- Offer to render the brief as a Frame or post a summary to a Slack channel after the user approves it.

## Output

Present the pipeline analysis, then the action brief. Ask the user if they'd like a Frame version or a Slack summary for their team channel.

---
*Adapted for Dust from `anthropics/knowledge-work-plugins/sales-brief` (skills.sh). Original targeted PayPal/QuickBooks e-commerce revenue; this version targets a B2B Salesforce pipeline.*
