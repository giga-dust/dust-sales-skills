# Dust Sales Skills

A curated set of sales skills adapted for the [Dust](https://dust.tt) platform, sourced from the most-installed sales skills on [skills.sh](https://www.skills.sh/?q=sales) and rewritten in Dust terminology.

Each skill is a reusable instruction set you can add to a Dust agent. Together they cover the core SDR/AE motions: researching and briefing, logging activity, reporting on pipeline, running daily sales ops, producing enablement collateral, and coaching an enterprise motion.

## Dust terminology map

These skills were originally written for CLI/plugin-based agent ecosystems. This repo translates them:

| Original concept | Dust concept |
|---|---|
| Skill / plugin | **Skill** (reusable instruction set attached to an agent) |
| MCP server / CLI binary | **Toolset** (e.g. Salesforce, Gmail, Slack) or **Connection** |
| FILE.md / project context | **AGENTS.md** in a **Pod** |
| Project / workspace folder | **Pod** (shared team home: files, tasks, conversations) |
| Artifact / rendered output | **Frame** (interactive dashboard/visualization) or file |
| Subagent | **Sub-agent** (agent called by another agent) |
| Scheduled command / cron | **Trigger / Schedule** on an agent |
| Local files / knowledge base | **Company data** (connected sources: Slack, Drive, Confluence, Gong…) |

## Skills in this repo

| Skill | What it does | Source |
|---|---|---|
| [`pipeline-brief`](skills/pipeline-brief/SKILL.md) | Periodic pipeline & activity brief: what moved, why, and a 2-week action plan | Adapted from `anthropics/knowledge-work-plugins/sales-brief` |
| [`crm-activity-logging`](skills/crm-activity-logging/SKILL.md) | Log calls, notes, meetings, tasks against CRM records — correctly linked | Adapted from `hubspot/agent-cli-skills/sales-execution` |
| [`pipeline-reporting`](skills/pipeline-reporting/SKILL.md) | Daily briefing, pipeline snapshot, win/loss analysis rendered as a Frame | Adapted from `hubspot/agent-cli-skills/sales-reporting` |
| [`sales-ops-workflows`](skills/sales-ops-workflows/SKILL.md) | Meeting prep, email-to-task, weekly digest across email + calendar + docs | Adapted from `googleworkspace/cli/persona-sales-ops` |
| [`sales-enablement`](skills/sales-enablement/SKILL.md) | Create decks, one-pagers, objection docs, demo scripts, playbooks | Adapted from `coreyhaines31/marketingskills/sales-enablement` |
| [`enterprise-sales-motion`](skills/enterprise-sales-motion/SKILL.md) | Coach a repeatable enterprise sales engine (discovery, procurement, team) | Adapted from `RefoundAI/lenny-skills/enterprise-sales-motion` |

## Fit with YOUR workspace

Cross-comparison of what each skill needs vs. the toolsets and connections available in your Dust workspace today:

| Capability needed | Available in the workspace | Used by |
|---|---|---|
| CRM read/write | ✅ Salesforce toolset | crm-activity-logging, pipeline-reporting, pipeline-brief |
| Call recordings & transcripts | ✅ Gong (synced as company data) | pipeline-brief, sales-enablement |
| Email | ✅ Gmail toolset | sales-ops-workflows |
| Calendar | ✅ Google Calendar toolset | sales-ops-workflows |
| Docs & files | ✅ Google Drive toolset + synced Drive | sales-ops-workflows, sales-enablement |
| Team messaging | ✅ Slack toolset + synced Slack | pipeline-brief, pipeline-reporting (delivery) |
| Enablement knowledge | ✅ Guru + Confluence (company data) | sales-enablement, enterprise-sales-motion |
| Support context | ✅ Zendesk, Intercom (company data) | pipeline-brief (churn/risk signals) |
| Warehouse analytics | ✅ Snowflake connection | pipeline-reporting (deep analysis) |
| Web research | ✅ Web search & browse toolset | sales-enablement, enterprise-sales-motion |
| Dashboards / visual output | ✅ Frames | pipeline-reporting, pipeline-brief |
| E-commerce revenue (PayPal/QuickBooks) | ❌ Not connected | (original `sales-brief` dependency — replaced with Salesforce) |
| HubSpot CRM | ❌ Not connected (Salesforce is the CRM) | (original `sales-execution`/`sales-reporting` dependency — replaced) |

**Bottom line:** every skill in this repo runs on toolsets Vanta already has connected.

## How to use these in Dust

1. Open **Skills** in your Dust workspace and create a new skill, or **New Skills>FromExisting>PasteGithubURL**
2. Paste the `SKILL.md` content as the skill's instructions; use the frontmatter `description` as the skill description (this is what tells agents when to activate it).
3. Attach the toolsets listed under **Required toolsets** to the agent using the skill.
4. Optionally pin the skill to a Pod so the whole team's agents can use it.

## Attribution

Original skills by their respective authors on [skills.sh](https://www.skills.sh). This repo adapts their methodology to Dust concepts and your workspace stack; all credit for the underlying frameworks goes to the original authors.
