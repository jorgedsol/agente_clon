# JOURNAL: Código como subámbito del proyecto

- **Fecha:** 2026-11-18 18:08 (Europe/Madrid)
- **Ámbito:** hub agente_clon
- **Tipo:** decisión / cambio
- **Estado:** confirmado por Jorge para la organización del código; edición del AGENTS.md global pendiente de autorización expresa
- **Consolidación:** pendiente
- **Origen:** petición expresa de Jorge de adaptar init-code-repo a la organización actual del hub
- **Afecta a:** proyectos de software y .agents/skills/init-code-repo/

## Decisión de organización

El código se organiza en projects/<nombre>/codigo/ como subámbito del proyecto. Su contexto técnico está relacionado con el contexto general del proyecto, sin constituir otro proyecto aislado. La organización Git puede ser independiente sin alterar esa relación de memoria.

La skill init-code-repo y sus plantillas se han adaptado a esta estructura, sustituyendo el pack project_code_init para copiar a otro repositorio. El detalle técnico propio tiene sus journals en codigo/memory/journals/; codigo/memory/MEMORY.md y el alta de esa memoria en el índice quedan para consolidación manual. No se han creado módulos de código ni modificado packs de proyectos existentes con este cambio de la skill.

## Relación con el conocimiento anterior

Sustituye la organización descrita en la primera parte, Esencia, de ../MEMORY.md, que sitúa el código en repositorios separados, en lo relativo a su ubicación dentro del proyecto. La memoria consolidada se conserva intacta hasta una consolidación solicitada. El apartado Código de un producto de ../../AGENTS.md todavía contiene la ubicación anterior; su adaptación se presenta a Jorge para autorización, según su protección expresa.

Referencias mantenidas: ../../.agents/skills/init-code-repo/SKILL.md y ../../README.md.