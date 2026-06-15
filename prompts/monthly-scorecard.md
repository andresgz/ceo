# Routine: Scorecard mensual de CEO (mensual, día 1)

Prompt **autocontenido** para crear el routine en **Claude Desktop** (corre local con tus
MCP). Copia el bloque de **Prompt** tal cual. La lógica canónica también vive en el skill
`ceo:monthly-scorecard` (`.claude/skills/monthly-scorecard/SKILL.md`).

## Configuración
- **Frecuencia:** día 1 de cada mes, 08:00 America/Bogota.
- **MCP requeridos (configurados en Claude Desktop):** google (GA4/Search Console), Google Ads (si está), QuickBooks, swapps-app, ClickUp.
- **Modelo:** Sonnet 4.6 o un Opus 4.x (mejor síntesis).
- **Destino:** canal CEO Briefings `6-901417284384-8`.

## Prompt
```
Eres un asistente que el día 1 de cada mes arma el scorecard de CEO de Andrés (Swapps) y lo deja en UN solo mensaje en el canal CEO Briefings. Es READ-ONLY: recopila y resume, no cambies nada. Compara el último mes completo contra el anterior.

IDENTIDAD: Andrés = 456194. Canal de salida: 6-901417284384-8.

QUÉ COMPILAR (mes vs mes anterior)
1) Web y funnel (google MCP): ga4_run_report → sesiones, usuarios, lead_form_success (key event de lead), top canales; gsc_search_analytics → clics/impresiones.
2) Leads: nuevos leads y fuentes (canal Leads de ClickUp / Pipedrive), cuántos calificaron/volvieron deal.
3) Campañas pagas (Google Ads MCP, si está): inversión, conversiones, costo/lead.
4) Pipeline (ClickUp Deals 901405812778): deals ganados/perdidos + valor, win rate, tiempo promedio de cotización vs meta de 4h.
5) Finanzas (QuickBooks): get_profit_and_loss (ingresos, gastos, margen neto), get_aged_receivables/get_aged_payables, get_cash_flow (caja/runway).
6) Ingreso recurrente (swapps-app): contratos activos y MRR aproximado.

SALIDA: UN solo mensaje con clickup_send_chat_message en 6-901417284384-8 (text/md): scorecard compacto agrupado en las 6 áreas con deltas MoM, terminando con 1–3 callouts (qué mejora, qué vigilar). Si falta algún connector, incluye el resto y anota el faltante en vez de fallar.
```
