---
name: "CS command center"
description: Create and operate a customer-specific Pod that brings together the repository's sales and customer workflows for one account. Use when the user asks to set up a customer command center, prepare a customer Pod, review account health or activity, coordinate customer-facing work, or run the standard customer workflow for a named customer.
---

# CS Command Center

Create a consistent, customer-specific operating layer in a Dust Pod. The command center is a reusable template: instantiate it for any customer, keep all work scoped to that customer, and use the repository's six supporting skills as the standard capability set.

This skill is an orchestration layer, not a replacement for the underlying skills. Use the relevant supporting skill for the requested operation and preserve the customer's context in the Pod.

## Customer template

Before doing customer-specific work, establish or confirm this context:

```yaml
customer:
  name: "<customer name>"
  domain: "<customer domain>"
  crm_account_id: "<CRM account or account ID>"
  lifecycle_stage: "<prospect|pilot|customer|expansion|at-risk|churned>"
  owner: "<internal owner>"
  timezone: "<IANA timezone>"
  pod_id: "<customer Pod ID, if already created>"
```

If the customer is ambiguous, ask for the missing identifier before retrieving or writing customer data. Prefer a stable CRM account ID plus domain over a name alone.

## Pod initialization

When asked to create or initialize the command center for a customer:

1. Confirm the customer identity and the user's intended scope.
2. Create or use one dedicated Pod for that customer. Do not combine unrelated customers in the same command center.
3. Add a durable customer context file or AGENTS.md containing the confirmed template fields, account aliases, internal owner, timezone, lifecycle stage, and links to the CRM record and other approved sources.
4. Organize working material into these areas:
   - **Account context:** company profile, stakeholders, goals, use cases, success criteria, risks, and current status.
   - **Activity and meetings:** call notes, meeting prep, follow-ups, and CRM-linked activity.
   - **Pipeline and reporting:** opportunity state, movement, forecasts, and action briefs.
   - **Enablement:** customer-specific decks, one-pagers, objection handling, demo scripts, ROI work, and proposals.
   - **Governance and next actions:** decisions, owners, due dates, approvals, and open risks.
5. Attach or make available the six supporting skills listed below, subject to workspace permissions and tool availability.
6. Run a lightweight readiness check and report what was created, what is missing, and which capabilities are available.

Do not fabricate customer facts to fill the template. Mark unknown values as `unknown` and identify the source needed to resolve them.

## Supporting skill set

Use the smallest relevant subset for each request, while keeping all six capabilities available in the customer Pod:

| Capability | Supporting skill | Use it for |
|---|---|---|
| CRM activity | `crm-activity-logging` | Logging calls, notes, meetings, and linked follow-up tasks |
| Pipeline movement | `pipeline-brief` | Explaining what moved, what stalled, why, and the next two-week actions |
| Pipeline analytics | `pipeline-reporting` | Daily briefings, snapshots, win/loss analysis, revenue views, and Frames |
| Sales operations | `sales-ops-workflows` | Meeting prep, email-to-task, deal updates, proposals, and recurring digests |
| Customer enablement | `sales-enablement` | Decks, one-pagers, demo scripts, objections, ROI analyses, and playbooks |
| Enterprise motion | `enterprise-sales-motion` | Multi-stakeholder buying, procurement, governance, discovery, and expansion strategy |

Follow the supporting skill's source-of-truth rules, required toolsets, approval gates, and limitations. Do not silently reimplement a supporting workflow with weaker safeguards.

## Standard command-center workflows

### 1. Customer snapshot

For a request such as "give me the customer snapshot":

- Resolve the customer using the confirmed CRM account ID and domain.
- Summarize lifecycle stage, owner, stakeholders, goals, active opportunities, recent activity, open tasks, support or risk signals, and next milestones.
- Separate confirmed facts from inferred risks.
- Link or cite the underlying customer sources when the platform supports citations.
- State which sources were unavailable or out of date.

### 2. Meeting preparation

Use `sales-ops-workflows` for the operational workflow. Combine the calendar event, attendee context, recent customer communications, CRM state, prior notes, open tasks, and the customer's success criteria. Produce a concise brief with:

- attendees and roles;
- what changed since the last touch;
- customer goals and unresolved pain;
- agreed outcomes and open risks;
- recommended agenda, questions, and next step;
- source-backed follow-ups.

### 3. Post-meeting capture

Use `crm-activity-logging` to log the meeting and follow-up tasks against the correct CRM records. Verify that each activity is linked to the customer account and, where relevant, the contact and opportunity. Do not report success until the links have been read back and confirmed.

### 4. Customer and pipeline review

Use `pipeline-brief` for movement and action planning, and `pipeline-reporting` for quantitative reporting or Frames. Scope every query to the customer unless the user explicitly asks for a portfolio or comparative view. Distinguish CRM facts, transcript evidence, support signals, and inference.

### 5. Enablement and expansion

Use `sales-enablement` to produce customer-specific collateral grounded in approved positioning and account context. Use `enterprise-sales-motion` when the request involves procurement, security, governance, multi-threading, executive alignment, expansion, or a repeatable enterprise motion.

Before generating external-facing material, check the customer's approved terminology, current product claims, references, security posture, and commercial constraints. Do not invent proof points, commitments, pricing, roadmap dates, or customer quotes.

## Data boundaries and safety

- Scope reads and writes to the identified customer account, its approved contacts, linked opportunities, and the customer's Pod.
- Never expose one customer's private data in another customer's Pod or deliverable.
- Verify account, contact, opportunity, and event identifiers before writing.
- Treat CRM and connected company data as the source of truth for customer facts. Treat web research as supplementary and label it as such.
- Do not send customer emails, post externally, change deal stages, or create broad bulk tasks without an explicit user request and the relevant workflow's approval gate.
- For bulk actions, preview the records and intended changes first. Ask for confirmation when the underlying skill requires it.
- If a required toolset or source is unavailable, continue only with the safe subset and state the limitation.
- Keep a clear distinction between customer-facing content, internal notes, and unverified hypotheses.

## Output conventions

For any command-center response, start with the customer name and the date of the data pull. Prefer a short executive summary followed by:

1. current state;
2. evidence and recent activity;
3. risks and missing information;
4. recommended next actions with owners and dates;
5. source or tool limitations.

For a newly initialized Pod, return a readiness summary covering the customer identifiers, Pod structure, six supporting skills, connected toolsets, and unresolved setup questions.

## Activation examples

Use this skill for requests such as:

- "Create a CS command center for Acme."
- "Set up a customer Pod for this account with all the sales skills."
- "Prepare the Acme customer snapshot and next actions."
- "Get me ready for tomorrow's Acme meeting and log the follow-ups afterward."
- "Create a customer-specific enablement pack and pipeline review."

---
*Built as an orchestration skill for the six Dust sales skills in this repository. It standardizes a customer-specific Pod without changing the source-of-truth or approval rules of the underlying skills.*
