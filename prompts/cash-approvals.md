# Routine: Aprobaciones & caja (diaria)

Contraparte programada del skill `ceo:cash-approvals`.

## Configuración
- **Frecuencia:** L–V 07:00 America/Bogota → cron `0 12 * * 1-5` (UTC).
- **Source repo:** `andresgz/ceo` (GitHub conectado vía `/web-setup`).
- **Connectors:** Jeeves + QuickBooks + ClickUp (habilitados en claude.ai/customize/connectors).
- **Modelo:** Sonnet 4.6.
- **Destino:** canal CEO Briefings (`6-901417284384-8`).

## Prompt (routine en la nube — llama la skill)
```
Ejecuta la skill "cash-approvals" de este repositorio (.claude/skills/cash-approvals/SKILL.md) usando los MCP de Jeeves, QuickBooks y ClickUp. Es read-only: no apruebes, pagues ni crees nada. Deja UN solo digest en el canal CEO Briefings (6-901417284384-8): aprobaciones pendientes primero, luego cuentas por cobrar/pagar vencidas y alertas de saldo; o "✅ Finanzas al día" si no hay nada.
```

## Desktop (sin soporte de skills)
Los routines de Claude Desktop no ejecutan skills. Si lo usas en Desktop, abre
`.claude/skills/cash-approvals/SKILL.md` y pega su contenido como prompt.
