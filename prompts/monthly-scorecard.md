# Routine: Scorecard mensual de CEO (mensual)

Contraparte programada del skill `ceo:monthly-scorecard`.

## Configuración
- **Frecuencia:** día 1 de cada mes, 08:00 America/Bogota → cron `0 13 1 * *` (UTC).
- **Source repo:** `andresgz/ceo` (GitHub conectado vía `/web-setup`).
- **Connectors:** google (GA4/Search Console), Google Ads (si disponible), QuickBooks, swapps-app, ClickUp.
- **Modelo:** Sonnet 4.6 o un Opus 4.x (mejor síntesis).
- **Destino:** canal CEO Briefings (`<CEO_BRIEFINGS_CHANNEL_ID>`).

## Prompt (routine en la nube — llama la skill)
```
Ejecuta la skill "monthly-scorecard" de este repositorio (.claude/skills/monthly-scorecard/SKILL.md) usando los MCP de google, Google Ads (si está), QuickBooks, swapps-app y ClickUp. Es read-only. Compara el último mes completo contra el anterior. Deja UN solo scorecard en el canal CEO Briefings (<CEO_BRIEFINGS_CHANNEL_ID>) agrupado en web/funnel, leads, ads, pipeline, finanzas y MRR, con deltas MoM y 1-3 callouts. Si falta algún connector, incluye el resto y anota el faltante.
```

## Desktop (sin soporte de skills)
Abre `.claude/skills/monthly-scorecard/SKILL.md` y pega su contenido como prompt.
