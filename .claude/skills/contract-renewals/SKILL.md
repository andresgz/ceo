---
name: contract-renewals
description: Weekly radar of client contracts nearing expiry/renewal for Andrés (Swapps) — which contracts renew or need a price-increase notice soon, with the pending action and suggested new rate per account, plus each client's payment standing. From the swapps-app (IDK) contracts API + ClickUp Active Contracts + QuickBooks (A/R). Recommend-only. Posts one digest to the CEO Briefings channel.
---

# contract-renewals

Weekly radar so renewals never slip. Lists contracts **ending or auto-renewing soon**, the
**action owed**, and the **price increase** to apply. **Recommend-only**: never edit
contracts or send notices.

> Cloud routines need the **swapps-app**, **quickbooks** (read-only) and **ClickUp** MCP
> connectors enabled.

## What to pull

**swapps-app (IDK) — source of truth for contracts:**
- `list_contracts` / `get_contract` — end dates, renewal terms, current rate.
- `list_contract_installments` — billing cadence / next charge.
- `list_contract_level_rates` — rate by engineer level (to compute increases).
- `list_clients` — account names.

**ClickUp** Active Contracts list id `181795372` and the Deals list `901405812778` — to see
which renewals already have a deal/task in motion.

**QuickBooks (read-only) — payment standing per account:**
- `search_customers` (match the client name) → `get_customer_balance` and
  `get_aged_receivables` — is the client current or overdue, and by how much.

## What to surface (priority order)

1. **Vencen en ≤60–90 días** sin renovación en curso → iniciar renovación.
2. **Auto-renovación con incremento pendiente** — compute IPC + agreed delta (e.g. the
   `IPC 5.10% + 4 = 9.10%` pattern) and show current → suggested price.
3. **Renovaciones en curso sin contrato firmado** → push to sign.

Per contract: client, end date, action, current vs suggested rate, and a **payment-standing
flag** (🟢 al día / 🟡 mora 1–30 días / 🔴 mora >30 días o saldo grande). For accounts in
arrears, flag to **regularize A/R before sending a price-increase notice** — don't push an
increase onto an overdue account. Derive everything from the data — do not hardcode account
lists.

## Output

One message via `clickup_send_chat_message` to the **CEO Briefings** channel
(`6-901417284384-8`), `text/md`. None upcoming → `✅ Sin renovaciones próximas`.
Otherwise one line per contract, soonest-expiry first. Concise.

## Schedule

Weekly Monday 07:00 America/Bogota → cron `0 12 * * 1` UTC. Model: Sonnet 4.6.
