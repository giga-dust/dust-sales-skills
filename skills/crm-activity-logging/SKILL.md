---
name: crm-activity-logging
description: Log sales activities — calls, notes, meetings, tasks — against CRM contacts and opportunities, with the mandatory link-to-record step that makes them visible in the CRM. Use when the user says "log a call", "log a note", "log a meeting", "create a follow-up task", or "log activity".
---

# CRM Activity Logging

**Required toolsets:** Salesforce

## The two non-obvious rules

**1. Activities are invisible until linked.** An activity record created without a relationship to a contact/lead (`WhoId`) or an account/opportunity (`WhatId`) produces a record nobody can see on the CRM timeline. Always create the activity *with* its record links, or link it immediately after — never stop before the association exists.

**2. Timestamps are not what they seem.** Verify the semantics of each date field before writing:
- On a **task**, the primary date is the **due date**, not the creation time.
- On an **event/meeting**, set explicit start and end datetimes.
- On a **call log**, the timestamp is when the call happened, not when you logged it.
Query the object's fields through the Salesforce toolset first when unsure; do not guess picklist values — read them from the field metadata.

## Create + link, by type

- **Call** — create a completed task of type Call with subject, outcome summary in the description, direction, duration, and the call datetime. Link `WhoId` to the contact and `WhatId` to the opportunity when relevant.
- **Note** — create a note (or content note) with the body, and attach it to the opportunity or account record.
- **Meeting** — create an event with title, start/end datetimes, and outcome. Link to the contact and the opportunity.
- **Task** — create a task with subject, priority, status, type, and the **due date**. Link to the deal or contact it concerns.

After each write, read the record back and confirm the links are present before reporting success.

## Reading open tasks for a contact

Query tasks related to the contact (`WhoId`) and filter out completed statuses client-side. Present subject, status, priority, and due date.

## Bulk: follow-up task per opportunity in a stage

1. Query all opportunities in the target stage with their names and IDs.
2. Create one follow-up task per opportunity ("Follow up: {opportunity name}", priority high, due in 7 days), linking each task to its opportunity.
3. For more than ~100 records, do a **dry run first**: show the user the list of tasks to be created and get confirmation before writing.

## Known constraints

- Activities must be linked at creation time or immediately after, or they are invisible on record timelines.
- Picklist values (task type, call disposition, meeting outcome) are org-specific — read them from field metadata via the Salesforce toolset rather than assuming defaults.
- Sequences/cadences are not managed through this skill; use the team's sales engagement toolset if connected.

---
*Adapted for Dust from `hubspot/agent-cli-skills/sales-execution` (skills.sh). Original targeted the HubSpot CLI; this version targets the Dust Salesforce toolset.*
