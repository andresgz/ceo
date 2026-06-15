---
name: clickup-inbox-review
description: Review Andrés's ClickUp "inbox" — DMs, work channels, and comments on active work tasks — and surface only what actually needs his reply/decision, or confirm he's up to date. Read-only triage; it never replies for him or edits tasks. Use to run the inbox triage interactively, or to set up/update the daily Claude Desktop routine (the paste-ready prompt lives in this repo's prompts/).
---

# clickup-inbox-review

Daily triage of Andrés's ClickUp (user `456194`, andres@swapps.com): tell him **what
actually needs his reply/decision**, or confirm he's **up to date**. Runs two ways:

- **Interactive** — he asks for the review in a Claude session; this skill drives it.
- **Scheduled (routine)** — a Claude Desktop / cloud routine runs it daily and drops the
  result in ClickUp. The paste-ready routine prompt is
  [`prompts/clickup-inbox-review.md`](../../../prompts/clickup-inbox-review.md) (kept in sync
  with this skill).

> Cloud/Desktop routines run **isolated** and can only use MCP connectors enabled in the
> claude.ai account. The **ClickUp MCP connector must be enabled** at
> https://claude.ai/customize/connectors or the routine cannot read/write ClickUp.

## What to scan

1. **DMs** — `clickup_get_chat_channels`, then recent messages per DM/GROUP_DM
   (`clickup_get_chat_channel_messages`, limit 5, `text/md`). Pending if the *last* message
   is NOT from `456194`, is recent, and expects a reply.
2. **Work channels** (by id): Tech Lead `6-901408478795-8`, Dev Team `6-901413113264-8`,
   Op Managers `6-901414345705-8`, Gerencia `6-901408934548-8`, General `6-901414777930-8`,
   Platform Backlog `6-901414777111-8`, Product + Support Alignment `6-901416910074-8`,
   Support Direction `6-901414854276-8`, Delta Team `6-901413113312-8`, Swapps Platform
   `5-90148035830-8`, AI Integration `6-901417025269-8`, Deals `6-901405812778-8`,
   Leads `6-901414231204-8`. Pending if he's @mentioned / asked / a decision is requested
   and he hasn't answered.
3. **Work task comments** — `clickup_filter_tasks` (assignees `["456194"]`, order_by
   `updated`, reverse true); for active work tasks check `clickup_get_task_comments`.
   Pending if the last comment is from someone else, mentions/asks him, and he hasn't
   replied or reacted.

## Filter out (never report)

- ClickUp AI agents — **negative user ids** (e.g. `-4280373` Innovation Agent, `-4267735`
  Scrum Agent, `-4444525` Education Coach, `-4270804` Support/Estimation Agent, `-4267755`
  Sales Agent, `-4284230` Estimates Agent, `-4261592` Kate).
- Bots/automation: ClickBot (`-1`), Swapps Manager (`88301441`) deal notifications,
  Leads/Pipedrive/Zapier notifications, "Daily Estimation Quality Review" digests,
  deploybot, Sentry, Uptime, RunnerStatus.
- Simple acks (👍, "ok", "gracias", "listo") and FYIs with no ask.
- Personal/family lists (Family Backlog, Adecuaciones, Pagos Familiares, Asistencia
  Domestica, Emily, Educación Sebastián, Inversiones, Contabilidad, Actividades
  Mensuales/Anuales).

## Output

One message via `clickup_send_chat_message` to Andrés's personal/self-notes DM (channel
`dvd8-21694` — verify this is his self-DM). Up to date → `✅ ClickUp al día`. Otherwise a
short prioritized list (decisions/clients first), one line per item with who, what's
needed, and a direct link. **Read-only**: never reply for him or change tasks — only the
summary.

## Schedule (routine)

Daily 07:00 America/Bogota → cron `0 12 * * *` UTC (L–V only: `0 12 * * 1-5`). Model:
Sonnet 4.6 (or an Opus tier for sharper filtering). No git repo needed — pure ClickUp.
