---
name: sales-ops-workflows
description: Manage day-to-day sales workflows — meeting prep, converting emails into tasks, deal tracking, weekly digests, client communications. Use when the user asks to "prep my meeting", "turn this email into a task", "weekly digest", or general sales-ops housekeeping.
---

# Sales Ops Workflows

**Required toolsets:** Gmail · Google Calendar · Google Drive · Salesforce (deal updates) · optional: Slack (delivery)

## Core workflows

- **Meeting prep** — before a client call, pull the calendar event, review attendees, check recent email threads with those attendees, pull the account's CRM record and open opportunities, and produce a one-screen brief: who's coming, where the deal stands, what changed since last touch, suggested talking points.
- **Email-to-task** — convert a follow-up email into a CRM task: extract the ask, the account, and the deadline; create the task linked to the right contact/opportunity (see the `crm-activity-logging` skill).
- **Deal updates** — log deal changes directly in Salesforce rather than a side spreadsheet, so reporting skills see them.
- **Proposal sharing** — upload proposals to the dedicated shared Drive folder and share the link, never ad-hoc attachments.
- **Weekly digest** — a Monday summary of pipeline movement, meetings held vs. booked, and open follow-ups. Attach this skill to an agent with a weekly **schedule/trigger** and deliver by email or Slack.

## Tips

- Triage client email by filtering threads from the client's domain before a call.
- Schedule follow-up calls immediately after meetings to maintain momentum — propose slots from free/busy availability.
- Keep all client-facing documents in one dedicated shared Drive folder per account (or in the account's Pod).

---
*Adapted for Dust from `googleworkspace/cli/persona-sales-ops` (skills.sh). Original required the `gws` CLI and its utility skills; this version uses the Dust Gmail, Google Calendar, Google Drive, and Salesforce toolsets.*
