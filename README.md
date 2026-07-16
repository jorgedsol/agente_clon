# Agente clon

Repositorio de trabajo para un agente de IA en Cursor que actúa como extensión de mi criterio, estilo y forma de pensar.

No es un producto ni una aplicación. Es el entorno donde viven la memoria permanente, las reglas del agente y el trabajo por proyectos.

## Para qué sirve

Cuando trabajo con el agente en un proyecto, este repositorio le da contexto estable:

- quién soy y cómo encaro problemas
- con qué principios decide y prioriza
- cómo debe escribir
- qué evitar

Así las respuestas y el trabajo generado se mantienen coherentes entre sesiones y entre proyectos.

## Estructura

```
.
├── memory/                 # Memoria permanente (identidad, principios, estilo, ejemplos)
├── projects/               # Un directorio por proyecto, con su propia memoria
└── .cursor/
    ├── rules/              # Reglas del agente en este repo
    └── skills/             # Capacidades reutilizables del agente
```

### `memory/`

Documentos de referencia general. Definen identidad, principios de trabajo y estilo de comunicación. Se usan sobre todo en tareas de generación de contenido. No se modifican durante el trabajo habitual.

### `projects/`

Cada proyecto tiene su carpeta. Ahí vive el trabajo concreto y un `memory.md` con decisiones, restricciones y conocimiento útil de ese proyecto.

En git solo se versiona la memoria de cada proyecto (`memory.md`). El resto del contenido de `projects/` queda fuera del repositorio a propósito: el código y los artefactos de cada proyecto no forman parte de este repo.

### `.cursor/rules/`

Instrucciones operativas para el agente: cuándo leer o actualizar memorias, cómo encajar una petición en el contexto del proyecto y cuándo aplicar la memoria de contenido.

### `.cursor/skills/`

Skills que amplían lo que el agente puede hacer de forma repetible. Hoy la principal es **iniciar el repo de código** de un proyecto de software.

## Skill: iniciar el repo de código

Para proyectos de **software** (app, API, web, etc.), el agente puede generar un pack listo para copiar al repo de código real, con el mismo sistema de memoria + reglas.

La skill `init-code-repo` crea `projects/<nombre>/project_code_init/` con:

| Archivo | Rol |
|---------|-----|
| `memory.md` | Fuente de verdad del producto y lo técnico |
| `AGENTS.md` | Resumen mínimo al abrir el repo |
| `.cursor/rules/agent.mdc` | Cómo debe trabajar el agente (siempre activo) |

Se activa pidiendo algo como *iniciar el repo de código*, *project_code_init* o *empezar a programar* dentro de un proyecto en `projects/`. El agente infiere el contexto desde el `memory.md` y la documentación del proyecto; no inventa stack ni alcance.

No aplica a proyectos solo de contenido (posts, emails, propuestas, estrategia).

Después de generar el pack, se copian esos tres archivos a la raíz del repo de código. El scaffolding de código (`mobile/`, `backend/`, etc.) es el siguiente paso, fuera de este repositorio.

## Cómo se usa

1. Abres este repositorio en Cursor.
2. Trabajas dentro de `projects/<nombre-proyecto>/`.
3. El agente lee la memoria del proyecto (y, si aplica, la memoria general) antes de actuar.
4. Si aparecen decisiones o restricciones importantes, se actualiza el `memory.md` del proyecto.
5. Si el proyecto es de software y toca programar, pides el pack del repo de código y el agente lo genera con la skill.

## Qué no es

- No sustituye los repositorios de código de cada proyecto.
- No documenta el detalle de un proyecto concreto: eso va en su `memory.md` o en su propio repo.
- No es un chatbot genérico: está orientado a trabajar con mi criterio y mis proyectos.
