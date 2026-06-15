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

| Skill | What it does |
| --- | --- |
| `ceo:clickup-inbox-review` | Triage ClickUp DMs + work channels + active-task comments; surface only what needs Andrés's reply/decision, or confirm he's up to date. Read-only. |

## Layout

```
ceo/
├── .claude-plugin/
│   ├── marketplace.json      # marketplace "ceo" → plugin "ceo" (source ".")
│   └── plugin.json           # plugin "ceo"; skills auto-discovered under ./skills/
├── skills/
│   └── <skill>/SKILL.md      # one folder per CEO skill (invoked as ceo:<skill>)
├── prompts/                  # paste-ready prompts for Claude Desktop routines (NOT loaded
│   └── <skill>.md            #   as skills; resources referenced by the skill docs)
└── README.md
```

## Routines (Claude Desktop)

Some skills also run unattended as scheduled cloud routines. Each one's paste-ready prompt
+ schedule lives in [`prompts/`](./prompts/). Routines run isolated and can only use MCP
connectors enabled at https://claude.ai/customize/connectors — anything ClickUp-based needs
the **ClickUp MCP connector** enabled there.

## Adding a new CEO skill

1. `skills/<new-skill>/SKILL.md` with frontmatter `name` + `description`.
2. If it will be scheduled, add `prompts/<new-skill>.md` with the routine prompt + config.
3. Add a row to the Skills table above. Bump `version` in `.claude-plugin/plugin.json`.
4. `/reload-plugins` (or reinstall) to pick it up.
