---
name: cash-approvals
description: Daily CEO finance pulse for Andrés (Swapps) — payments/invoices awaiting HIS approval in Jeeves, account balances, upcoming vendor due dates, plus a quick QuickBooks read of overdue receivables/payables and cash. Surfaces only what needs his decision. Read-only — never approves, pays, or creates anything. Posts one digest to the CEO Briefings channel.
---

# cash-approvals

Daily finance pulse so Andrés sees **what needs his money decision today** without opening
Jeeves or QuickBooks. **Strictly read-only**: never approve, pay, transfer, or create
anything — only report.

> Cloud routines need the **Jeeves** and **QuickBooks** MCP connectors enabled at
> https://claude.ai/customize/connectors, plus **ClickUp** to post the digest.

## What to pull

**Jeeves (operating cash + approvals)**
- `list_billpay_invoices` — invoices/bills **awaiting approval** (his sign-off). Capture
  vendor, amount, due date, status.
- `list_reimbursements` — reimbursements pending approval.
- `list_accounts` — current balances; flag any account running low.
- `list_transactions` — vendor payments **due in the next 7 days**.

**QuickBooks (financial health)**
- `get_aged_receivables` — clients overdue (who owes us, how much, how late).
- `get_aged_payables` — bills overdue / due soon.
- `get_cash_flow` or `get_balance_sheet` — cash position / short runway signal.

## What to surface (priority order)

1. **Approvals waiting on you** — Jeeves invoices/reimbursements pending, with amount + due
   date. These are the action items.
2. **Overdue receivables** — clients past due worth chasing.
3. **Upcoming/overdue payables** — bills due ≤7 days or already late.
4. **Low-balance / runway alert** — only if a balance is below a healthy threshold.

## Output

One message via `clickup_send_chat_message` to the **CEO Briefings** channel
(`6-901417284384-8`), `text/md`. Nothing pending and cash healthy →
`✅ Finanzas al día — sin aprobaciones pendientes (<fecha>)`. Otherwise a short prioritized
list: approvals first (with $), then overdue AR/AP, then alerts. Be concise; no raw dumps.

## Schedule

Weekdays 07:00 America/Bogota → cron `0 12 * * 1-5` UTC. Model: Sonnet 4.6.
