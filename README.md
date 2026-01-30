# Enterprise Command Center Plugin

Multi-agent orchestration plugin for Claude that coordinates business intelligence analysis across Strategy Cloud and routes actionable insights to enterprise tools.

## 🎬 Demo

[![Enterprise Command Center Demo](https://img.youtube.com/vi/1vYMyvSi_p0/maxresdefault.jpg)](https://www.youtube.com/watch?v=1vYMyvSi_p0)

*Click to watch the full demo on YouTube*

## What It Does

Single prompt → Multiple Strategy queries → 7 enterprise tools updated

```
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

## Key Features

* **Iterative Intelligence** - Queries Strategy multiple times based on what each downstream tool needs
* **Multi-Agent Orchestration** - Combines semantic layer queries with visual dashboard analysis
* **Enterprise Tool Routing** - Automatically creates artifacts in the right systems
* **Autonomous Execution** - No hand-holding required after initial prompt

## Installation

### For Claude Code

**Option 1: Install from GitHub (when added to a marketplace)**
```
/plugin install enterprise-command-center@your-marketplace
```

**Option 2: Install locally for development**
```bash
git clone https://github.com/tzockoll-creator/Enterprise-Command-Center-Skill.git
cd Enterprise-Command-Center-Skill
claude --plugin-dir ./
```

### For Claude.ai

Add the `skills/command-center/SKILL.md` file to your project knowledge.

## Plugin Structure

```
enterprise-command-center/
├── .claude-plugin/
│   └── plugin.json          # Plugin manifest
├── skills/
│   └── command-center/
│       └── SKILL.md         # Main skill (auto-invoked by Claude)
├── commands/
│   └── run-review.md        # User command: /enterprise-command-center:run-review
└── README.md
```

## Usage

### Using the Command (Manual)
```
/enterprise-command-center:run-review
```

Or with customizations:
```
/enterprise-command-center:run-review Focus on sales pipeline only, post to #sales-leadership
```

### Using the Skill (Automatic)

Just ask Claude naturally:
```
Run my weekly business ops review.
```

Claude will automatically invoke the skill based on the context.

### Customized Execution

```
Run my weekly business ops review.

Focus on:
- Sales pipeline only (skip operations)
- Critical findings only
- Post to #sales-leadership instead of #general
- Skip Figma update
```

## Configuration

Configure your environment in project instructions:

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

Connect these MCP servers in Claude:
* Strategy MCP
* Asana
* Atlassian (Jira + Confluence)
* HubSpot
* Slack
* Canva
* Figma

## How It Works

### Round 1: Sales Intelligence

* **Query:** Pipeline velocity, at-risk deals, revenue signals
* **Action:** Update HubSpot deal properties, create follow-up tasks
* **Reasoning:** "Now I need operational data to identify delivery risks..."

### Round 2: Operations Intelligence

* **Query:** Blockers, SLA status, capacity metrics
* **Action:** Create Jira issues, Confluence pages, Asana tasks
* **Reasoning:** "Now reviewing dashboard for visual patterns..."

### Round 3: Executive Intelligence

* **Analysis:** Visual dashboard review for anomalies
* **Action:** Slack summary, Canva presentation, Figma update

## Requirements

* Claude Pro or Team subscription (for MCP access)
* Connected enterprise tool integrations
* Strategy Cloud environment with MCP enabled
* Appropriate permissions in each downstream tool

## Security

* No credentials stored in plugin files
* Uses environment variables for all sensitive configuration
* Respects existing permission models in each tool
* Sanitizes PII before creating artifacts

## Contributing

1. Fork the repository
2. Create a feature branch
3. Submit a pull request

## License

MIT License - See LICENSE file for details

---

Built for demonstrating enterprise AI orchestration capabilities.
