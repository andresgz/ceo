# ceo

CEO operational skills for **Andrés González** (Swapps) — recurring reviews, triage, and
the routine prompts behind them. Packaged as a **Claude Code plugin** so it lives in its
own repo and grows to many skills, each invocable as `ceo:<skill>`.

## Install

```
/plugin marketplace add andresgz/ceo
/plugin install ceo@ceo
```

Local testing before pushing:

```
/plugin marketplace add ~/projects/ceo
/plugin install ceo@ceo
/reload-plugins
```

## Skills

| Skill | Cadence | Connectors | What it does |
| --- | --- | --- | --- |
| `ceo:clickup-inbox-review` | daily | ClickUp | Triage DMs + work channels + active-task comments; surface only what needs Andrés's reply/decision, or "up to date". |
| `ceo:cash-approvals` | daily (L–V) | Jeeves, QuickBooks, ClickUp | Payments/invoices awaiting his approval, balances, due dates, overdue AR/AP. |
| `ceo:deals-pipeline` | daily (L–V) | ClickUp | Deals blocked on him: proposals without follow-up, verbally-approved unsigned, stale quotes. |
| `ceo:contract-renewals` | weekly (Mon) | swapps-app, ClickUp | Contracts nearing expiry/renewal + action and suggested price increase. |
| `ceo:monthly-scorecard` | monthly (1st) | google, Google Ads, QuickBooks, swapps-app, ClickUp | One-page month-over-month read: web/leads, ads, pipeline, finance, MRR. |

All skills are **read-only** (surface/recommend; never act for him) and post one digest to a
dedicated private ClickUp **CEO Briefings** channel. Create that channel once and replace
`<CEO_BRIEFINGS_CHANNEL_ID>` in each SKILL.md + prompt with its id.

## Layout

```
ceo/
├── .claude-plugin/
│   ├── marketplace.json      # marketplace "ceo" → plugin "ceo" (source ".")
│   └── plugin.json           # plugin "ceo"; skills path → ./.claude/skills/
├── .claude/
│   └── skills/
│       └── <skill>/SKILL.md  # one folder per CEO skill — SINGLE source of truth
├── prompts/                  # paste-ready prompts for cloud/Desktop routines (resources,
│   └── <skill>.md            #   NOT loaded as skills)
└── README.md
```

The skills live under `.claude/skills/` (not `skills/`) on purpose — that's the **only**
location a **cloud routine** discovers them when it clones this repo as a source. The
plugin's `skills` path in `plugin.json` points at the same folder, so local install still
exposes them namespaced as `ceo:<skill>`. One copy, both paths.

## Routines (Claude Desktop)

Some skills also run unattended as scheduled cloud routines. Each one's paste-ready prompt
+ schedule lives in [`prompts/`](./prompts/). Routines run isolated and can only use MCP
connectors enabled at https://claude.ai/customize/connectors — anything ClickUp-based needs
the **ClickUp MCP connector** enabled there.

## Adding a new CEO skill

1. `.claude/skills/<new-skill>/SKILL.md` with frontmatter `name` + `description`.
2. If it will be scheduled, add `prompts/<new-skill>.md` with the routine prompt + config.
3. Add a row to the Skills table above. Bump `version` in `.claude-plugin/plugin.json`.
4. `/reload-plugins` (or reinstall) to pick it up.
