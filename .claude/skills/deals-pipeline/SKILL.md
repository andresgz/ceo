---
name: deals-pipeline
description: Daily sales-pipeline review for Andrés (Swapps) — deals/opportunities waiting on HIM (proposals sent with no follow-up, verbally-approved without a signed contract, stale quotes, deals stuck), from the Pipedrive CRM + the ClickUp Deals mirror. Recommend-only; never changes deals. Posts one digest to the CEO Briefings channel.
---

# deals-pipeline

Daily look at the sales pipeline to surface **deals that are blocked on Andrés** so nothing
goes cold. **Recommend-only**: never change statuses, send proposals, or edit tasks.

> Cloud routines need the **pipedrive** and **ClickUp** MCP connectors enabled. Pipedrive
> is the upstream CRM (source of truth for deals); the ClickUp Deals list mirrors it and
> may lag. Read both, **read-only**.

## What to pull

**Pipedrive (CRM — source of truth), read-only:**
- `list_deals` / `search_deals` — open deals by stage and value.
- `list_activities` — next/overdue activity per deal → a deal with **no next activity
  scheduled** is the classic "blocked / going cold" signal.
- `get_deal` — full context for the stuck/ambiguous ones (owner, stage, last update).
- `list_pipelines` / `list_stages` — to read stage names if needed.

**ClickUp Deals** list id `901405812778` (mirror — cross-check):
- `clickup_filter_tasks` (list_ids `["901405812778"]`, order_by `updated`) — scan deals by
  status and tags. Relevant tags: `pipedrive`, `quoting`, `needs-owner`.
- For ambiguous ones, `clickup_get_task` / `clickup_get_task_comments` for context.
- If the CRM and the mirror disagree, trust Pipedrive and note the drift.

## What to surface (priority order)

1. **`propuesta enviada` con seguimiento vencido** — proposals sent with no movement in
   >5 days → follow up.
2. **`aprobado verbalmente` / `en contratación` sin contrato firmado** → push to close.
3. **Cotizaciones lentas** — quotes past the **4h target** or estimations still pending.
4. **`needs-owner`** — deals/quotes without an owner.
5. **Nuevos sin asignar** — new deals/leads not yet picked up.

For each: deal name, current status, days stuck, and the concrete next action (and who).

## Output

One message via `clickup_send_chat_message` to the **CEO Briefings** channel
(`6-901417284384-8`), `text/md`. Nothing blocked → `✅ Pipeline al día`. Otherwise
a prioritized list (closing-stage deals first, then follow-ups, then intake). Concise.

## Schedule

Weekdays 08:00 America/Bogota → cron `0 13 * * 1-5` UTC. Model: Sonnet 4.6.
