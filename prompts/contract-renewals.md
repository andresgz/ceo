# Routine: Radar de renovaciones de contratos (semanal)

Contraparte programada del skill `ceo:contract-renewals`.

## Configuración
- **Frecuencia:** lunes 07:00 America/Bogota → cron `0 12 * * 1` (UTC).
- **Source repo:** `andresgz/ceo` (GitHub conectado vía `/web-setup`).
- **Connectors:** swapps-app + ClickUp.
- **Modelo:** Sonnet 4.6.
- **Destino:** canal CEO Briefings (`6-901417284384-8`).

## Prompt (routine en la nube — llama la skill)
```
Ejecuta la skill "contract-renewals" de este repositorio (.claude/skills/contract-renewals/SKILL.md) usando los MCP de swapps-app (contratos) y ClickUp. Es recommend-only: no edites contratos ni envíes notificaciones. Deja UN solo digest en el canal CEO Briefings (6-901417284384-8): contratos que vencen o auto-renuevan en ≤60-90 días, con la acción pendiente y el incremento sugerido (IPC + delta); o "✅ Sin renovaciones próximas".
```

## Desktop (sin soporte de skills)
Abre `.claude/skills/contract-renewals/SKILL.md` y pega su contenido como prompt.
