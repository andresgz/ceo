# Routine: Pipeline / Deals pendientes (diaria)

Contraparte programada del skill `ceo:deals-pipeline`.

## Configuración
- **Frecuencia:** L–V 08:00 America/Bogota → cron `0 13 * * 1-5` (UTC).
- **Source repo:** `andresgz/ceo` (GitHub conectado vía `/web-setup`).
- **Connectors:** ClickUp (+ Pipedrive si está disponible).
- **Modelo:** Sonnet 4.6.
- **Destino:** canal CEO Briefings (`<CEO_BRIEFINGS_CHANNEL_ID>`).

## Prompt (routine en la nube — llama la skill)
```
Ejecuta la skill "deals-pipeline" de este repositorio (.claude/skills/deals-pipeline/SKILL.md) usando el MCP de ClickUp (lista Deals 901405812778). Es recommend-only: no cambies deals ni tareas. Deja UN solo digest en el canal CEO Briefings (<CEO_BRIEFINGS_CHANNEL_ID>): deals bloqueados en mí, priorizando los de cierre (aprobado verbalmente / en contratación sin firmar), luego propuestas sin seguimiento y cotizaciones lentas; o "✅ Pipeline al día".
```

## Desktop (sin soporte de skills)
Abre `.claude/skills/deals-pipeline/SKILL.md` y pega su contenido como prompt.
