---
name: enterprise-command-center
description: Multi-agent orchestration skill that coordinates parallel analysis across Strategy Cloud's ecosystem—Excel data, semantic layer queries, and live dashboards—then synthesizes findings and routes actions to enterprise tools (Asana, HubSpot, Slack, Jira, Confluence, Canva, Figma). Use when running comprehensive business reviews, correlating dashboard visuals with semantic layer data, analyzing supplemental Excel data alongside Strategy Cloud metrics, creating LOB-specific action items from multi-source insights, or demonstrating enterprise AI orchestration capabilities.
---

# Enterprise Command Center

Multi-agent orchestration skill for Claude that coordinates business intelligence analysis across Strategy Cloud and routes actionable insights to enterprise tools.

## Architecture Overview

```
Single prompt → Multiple Strategy queries → 7 enterprise tools updated

"Run my weekly business ops review"
                │
                ▼
    ┌───────────────────────┐
    │   STRATEGY MCP        │──→ HubSpot (deal risk scores, tasks)
    │   (Semantic Layer)    │──→ Jira (blocker issues)
    │                       │──→ Confluence (investigation pages)
    │                       │──→ Asana (LOB tasks)
    └───────────────────────┘
                │
                ▼
    ┌───────────────────────┐
    │   STRATEGY ANALYST    │──→ Slack (executive summary)
    │   (Visual Dashboard)  │──→ Canva (QBR presentation)
    │                       │──→ Figma (dashboard mockup)
    └───────────────────────┘
```

## Execution Flow

When this skill is invoked, execute the following rounds of intelligence gathering and action routing:

### Round 1: Sales Intelligence (Strategy MCP)

**Query Strategy for:**
- Pipeline velocity and deal progression
- At-risk deals (stalled >14 days, missing next steps)
- Revenue signals and forecast accuracy
- Win/loss patterns by segment

**Route findings to:**
- **HubSpot**: Update deal properties with risk scores, create follow-up tasks for at-risk deals
- **Asana**: Create tasks for sales leadership with specific deal actions

**Reasoning checkpoint:** After completing Round 1, articulate what operational data is needed next: "Now I need operational data to identify delivery risks that could impact these deals..."

### Round 2: Operations Intelligence (Strategy MCP)

**Query Strategy for:**
- Active blockers and escalations
- SLA compliance status
- Resource capacity and utilization
- Project delivery timelines

**Route findings to:**
- **Jira**: Create issues for blockers requiring engineering attention
- **Confluence**: Create investigation pages for complex issues needing documentation
- **Asana**: Create tasks for operations team with priority assignments

**Reasoning checkpoint:** "Now reviewing visual dashboards for patterns not captured in structured queries..."

### Round 3: Executive Intelligence (Strategy Analyst / Dashboard Review)

**Analyze dashboards for:**
- Visual anomalies and trend breaks
- Cross-LOB patterns
- Leading indicators
- Month-over-month comparisons

**Route findings to:**
- **Slack**: Post executive summary to leadership channel
- **Canva**: Generate QBR presentation with key findings
- **Figma**: Update dashboard mockup with annotations

## Configuration

The skill expects the following environment context (set in project instructions or environment):

```
STRATEGY_MCP_URL: "your-strategy-mcp-endpoint"
STRATEGY_DASHBOARD_URL: "your-strategy-cloud-url"
STRATEGY_DASHBOARD_NAME: "Executive Dashboard"
JIRA_PROJECT_KEY: "DEMO"
CONFLUENCE_SPACE_KEY: "PM"
ASANA_PROJECT_NAME: "Strategy Insights"
SLACK_CHANNEL: "#leadership"
```

## Required MCP Connections

Before execution, verify these MCP servers are connected:
- Strategy MCP (semantic layer queries)
- Asana (task creation)
- Atlassian (Jira issues, Confluence pages)
- HubSpot (deal updates, task creation)
- Slack (messaging)
- Canva (presentation generation)
- Figma (design updates)

## Usage Examples

### Basic Execution
```
Run my weekly business ops review.
```

### Customized Execution
```
Run my weekly business ops review.

Focus on:
- Sales pipeline only (skip operations)
- Critical findings only
- Post to #sales-leadership instead of #general
- Skip Figma update
```

### Targeted Analysis
```
Run the Enterprise Command Center for Q4 revenue analysis.
Query Strategy for revenue variance by region, then:
- Update HubSpot deals in Southwest territory
- Create Jira issues for any forecast misses >10%
- Post summary to Slack
```

## Iterative Query Strategy

This skill demonstrates **iterative intelligence gathering**—each round of queries informs the next:

1. **Don't batch all queries upfront.** Let findings from Round 1 shape Round 2 queries.
2. **Show your reasoning.** Articulate why you're querying what you're querying.
3. **Adapt based on findings.** If Round 1 reveals a critical issue, prioritize related queries in Round 2.

## Output Artifacts

Each execution should produce:

| Tool | Artifact | Purpose |
|------|----------|---------|
| HubSpot | Deal property updates | Risk scoring, next step assignments |
| HubSpot | Tasks | Follow-up actions for sales team |
| Jira | Issues | Engineering blockers, technical debt |
| Confluence | Pages | Investigation documentation, runbooks |
| Asana | Tasks | LOB-specific action items with owners |
| Slack | Message | Executive summary with key metrics |
| Canva | Presentation | QBR deck with visualizations |
| Figma | Design update | Dashboard annotations |

## Error Handling

- If a MCP connection fails, note it and continue with available tools
- If Strategy queries return empty results, document the query attempted and suggest refinements
- If downstream tool creation fails, log the intended action for manual follow-up

## Security Considerations

- No credentials are stored in this skill
- All authentication flows through connected MCP servers
- PII is sanitized before creating external artifacts
- Respects existing permission models in each tool
