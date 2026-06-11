# Terror Review 🔍

Skill / comando para **Claude Code**: auditoría de código con triple lente — **Arquitectura + Backend + Seguridad** — en una sola pasada.

Genera un informe estructurado con hallazgos por severidad, puntuaciones por dimensión, top 5 de acciones prioritarias y patrones positivos del código.

> 🎨 ¿Buscas lo mismo pero para UI/frontend? Mira [design-terror-review](https://github.com/instalacionesc10/design-terror-review) (Visual + Patrones React/Performance + Accesibilidad).

## Qué revisa

| Lente | Cubre |
|-------|-------|
| **Arquitectura** | Violaciones SOLID, acoplamiento/cohesión, dependencias circulares, escalabilidad (N+1, bucles sin límite), organización del código, consistencia con los patrones del proyecto |
| **Backend** | Diseño de API, queries (N+1, índices, SELECTs sin límite, SQL injection), manejo de errores, rendimiento, flujo de datos, validación de inputs |
| **Seguridad** | OWASP Top 10, sanitización de inputs, auth/authz, exposición de datos sensibles (logs, API keys, PII), CORS/headers, CVEs en dependencias |

## Instalación

No tiene dependencias: es un único fichero markdown.

### Global (disponible en todos tus proyectos)

```powershell
# Windows (PowerShell)
New-Item -ItemType Directory -Force "$env:USERPROFILE\.claude\commands" | Out-Null
Invoke-WebRequest "https://raw.githubusercontent.com/instalacionesc10/terror-review/main/commands/terror-review.md" -OutFile "$env:USERPROFILE\.claude\commands\terror-review.md"
```

```bash
# macOS / Linux
mkdir -p ~/.claude/commands
curl -fsSL https://raw.githubusercontent.com/instalacionesc10/terror-review/main/commands/terror-review.md -o ~/.claude/commands/terror-review.md
```

### Por proyecto (compartido con el equipo vía git)

Copia `commands/terror-review.md` a la carpeta `.claude/commands/` del repo del proyecto y commitéalo.

## Uso

Dentro de Claude Code:

```
/terror-review src/modules/payments
```

- **Con argumento**: audita la ruta o módulo indicado.
- **Sin argumento**: infiere el objetivo de los cambios recientes de git (`git diff --name-only HEAD~3`) o te pregunta.

## Salida

1. **Summary** — párrafo con el estado de salud del módulo.
2. **Findings** — tabla con severidad (CRITICAL → INFO), lente, `fichero:línea`, problema y fix recomendado.
3. **Scores** — puntuación 1-10 por dimensión (Arquitectura, Backend, Seguridad) + nota global.
4. **Priority Actions** — top 5 de fixes por impacto, con esfuerzo estimado (S/M/L).
5. **Positive Patterns** — 2-3 cosas que el código hace bien.
