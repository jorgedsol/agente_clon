---
name: init-code-repo
description: >-
  Genera el pack project_code_init (memory.md, AGENTS.md, agent.mdc) para arrancar
  el repo de código de un proyecto con agente inteligente. Infiera contexto desde
  memory.md y docs del proyecto. Usar cuando el usuario pida iniciar el repo de
  código, project_code_init, pack de agente para programar, scaffolding del agente
  de desarrollo, o empezar a programar un producto software dentro de projects/.
  No usar en proyectos solo de contenido (posts, emails, propuestas, estrategia).
---

# Init code repo

Genera dentro de `projects/<nombre>/project_code_init/` el pack que el usuario copia a la raíz de su **repo de código real** para programar con el mismo sistema de agente (memoria + resumen + una rule).

## Cuándo sí / cuándo no

**Sí** — el proyecto implica desarrollar software (app, API, web, mobile, backend, CLI de producto, etc.) o el usuario pide explícitamente el pack.

**No** — solo generación de contenido (posts, emails, propuestas comerciales, estrategia, docs de cliente sin fase de código). En ese caso explícalo en una frase y no generes el pack.

Si hay duda (p. ej. “automatización” ambigua): pregunta una vez si habrá repo de código propio.

## Estructura objetivo (fija)

```
projects/<nombre>/project_code_init/
├── README.md                 # Solo para el pack (cómo copiar); no va al repo final
├── memory.md                 # Fuente de verdad del producto/técnico
├── AGENTS.md                 # Resumen mínimo → apunta a memory.md
└── .cursor/rules/
    └── agent.mdc             # Una sola rule alwaysApply (cómo trabajar)
```

No crear más rules ni más `.md` de contexto. No duplicar el mismo contenido en varios archivos.

| Archivo | Rol |
|---------|-----|
| `memory.md` | Hechos: producto, stack, decisiones, alcance, plan, no-hacer |
| `AGENTS.md` | ~10–15 líneas: lee memory + límites duros |
| `agent.mdc` | Proceso del agente; sin repetir épicas/arquitectura |
| `README.md` | Instrucciones de copia para el usuario |

Plantillas base: [templates/](templates/). Partir de ellas y **rellenar** con info del proyecto (no dejar TODOs si la info existe).

## Workflow

Copia y marca progreso:

```
- [ ] 1. Gate (¿es proyecto de código?)
- [ ] 2. Localizar proyecto y leer fuentes
- [ ] 3. Inferir y detectar huecos
- [ ] 4. Escribir project_code_init/
- [ ] 5. Actualizar memory del proyecto en el clon
- [ ] 6. Confirmar al usuario cómo usarlo
```

### 1. Gate

Si el proyecto no es de software y el usuario no lo pide explícitamente → no generar.

### 2. Localizar y leer

Trabajar bajo `projects/<nombre>/` del proyecto activo en el chat.

Leer, en este orden de prioridad:

1. `projects/<nombre>/memory/memory.md` (o `memory.md` si esa es la convención)
2. Docs de alcance/propuesta en `docs/`, `input/`, `output/` (docx, md, txt) si aportan stack, alcance o decisiones
3. Conversación actual

No inventar stack, endpoints ni alcance. Si falta un dato crítico, pregunta o deja el campo como pendiente explícito en `memory.md`.

### 3. Inferir

Extraer y consolidar:

- Qué es el producto y para quién
- Hipótesis / objetivo del MVP si existe
- Stack (mobile, backend, DB, auth, infra)
- Decisiones cerradas y restricciones
- Dentro / fuera de alcance
- Arquitectura en capas o módulos
- Plan o fases si existen
- Dependencias externas pendientes
- No-hacer / zonas de cuidado
- Enlaces útiles (prototipo, APIs, Figma)

Separar:

- **Hechos del producto** → `memory.md`
- **Límites duros en una línea** → `AGENTS.md`
- **Comportamiento del agente** (preguntar antes, mocks, alcance) → `agent.mdc` (adaptar al proyecto; no copiar reglas de otro producto tal cual)

### 4. Escribir archivos

1. Crear `projects/<nombre>/project_code_init/` (sobrescribir solo si el usuario lo pide o el pack está vacío/incompleto).
2. Rellenar `memory.md` completo (única fuente de verdad densa).
3. Rellenar `AGENTS.md` corto.
4. Rellenar `agent.mdc` con nombre del proyecto y límites/preguntas específicas.
5. Escribir `README.md` del pack (cómo copiar al repo real).

Calidad:

- Sin duplicar párrafos entre los tres archivos operativos.
- Español, claro, compacto (mismo criterio que el clon).
- `agent.mdc` con frontmatter `alwaysApply: true`.
- No meter identidad/estilo de contenido del clon (`memory/identidad.md`, etc.) en este pack.

### 5. Actualizar memoria del proyecto en el clon

En `projects/<nombre>/memory/memory.md`, añadir o actualizar una línea en entregables/estado:

- `project_code_init/` — pack agente del repo de código (`memory.md` + `AGENTS.md` + `agent.mdc`)

Solo eso; no copiar el contenido técnico entero otra vez.

### 6. Cierre al usuario

Indicar:

1. Ruta del pack generado.
2. Qué copiar a la raíz del repo de código (`memory.md`, `AGENTS.md`, `.cursor/rules/agent.mdc` — no el README del pack).
3. Que el scaffolding de código (`mobile/`, `backend/`, etc.) es el siguiente paso, no parte de este pack.
4. Opcional: workspace multi-root con `agente_clon` + repo de código.

## Anti-patrones

- Generar el pack en un proyecto solo de posts/emails/propuestas.
- Varias rules (`project.mdc` + `memory.mdc` + `engineering.mdc`) — una sola `agent.mdc`.
- `AGENTS.md` largo que repite `memory.md`.
- Inventar endpoints, stack o alcance no documentados.
- Meter el código de producción dentro de `agente_clon` (este pack no es el repo de código; solo lo prepara).

## Referencia rápida de roles

- `memory.md` = qué saber
- `AGENTS.md` = resumen al entrar
- `agent.mdc` = cómo actuar
