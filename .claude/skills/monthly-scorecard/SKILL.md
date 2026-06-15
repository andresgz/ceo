---
name: monthly-scorecard
description: Monthly CEO scorecard for Andrés (Swapps) — one digest consolidating the month's key numbers across web traffic & leads (GA4/Search Console), paid campaigns (Google Ads), sales pipeline (ClickUp Deals), finance (QuickBooks P&L, AR/AP, cash), and recurring revenue (swapps-app contracts), month-over-month where possible. Read-only. Posts one digest to the CEO Briefings channel.
---

# monthly-scorecard

A once-a-month, single-page read of the business so Andrés sees the whole picture without
opening five tools. **Read-only**: gather and summarize, change nothing.

> Cloud routines need the relevant MCP connectors enabled at
> https://claude.ai/customize/connectors: **google** (GA4/Search Console), **Google Ads**
> (if available), **QuickBooks**, **swapps-app**, and **ClickUp** (to post).

## What to compile (last full month vs prior month)

1. **Web & funnel (google MCP)** — `ga4_run_report`: sessions, users, `lead_form_success`
   (the canonical lead key event), top channels; `gsc_search_analytics`: clicks/impressions.
2. **Leads** — new leads count + sources (ClickUp Leads channel / Pipedrive), and how many
   became qualified/deals.
3. **Paid campaigns (Google Ads MCP, if connected)** — spend, conversions, cost/lead.
4. **Pipeline (ClickUp Deals `901405812778`)** — deals won/lost + value, win rate, average
   quote turnaround vs the 4h target.
5. **Finance (QuickBooks)** — `get_profit_and_loss` (revenue, expenses, net margin),
   `get_aged_receivables`/`get_aged_payables`, `get_cash_flow` (cash / runway).
6. **Recurring revenue (swapps-app)** — active contracts and approximate MRR.

## Output

One message via `clickup_send_chat_message` to the **CEO Briefings** channel
(`<CEO_BRIEFINGS_CHANNEL_ID>`), `text/md`: a compact scorecard grouped by the 6 areas with
MoM deltas, ending with **1–3 callouts** (what's improving, what to watch). If a connector
is unavailable, include the rest and note the gap rather than failing.

## Schedule

Monthly on the 1st, 08:00 America/Bogota → cron `0 13 1 * *` UTC. Model: Sonnet 4.6 (or an
Opus tier — this one benefits from sharper synthesis).
