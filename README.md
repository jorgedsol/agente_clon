# Agente clon

Repositorio de trabajo para un agente de IA que actúa como extensión de mi criterio, estilo y forma de pensar.

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
└── .agents/
    ├── rules/              # Reglas del agente en este repo
    └── skills/             # Capacidades reutilizables del agente
```

### `memory/`

Gestion de memoria general. 

### `projects/`

Cada proyecto tiene su carpeta. Ahí vive el trabajo concreto y un memory/ con decisiones, restricciones y conocimiento útil de ese proyecto que conserva su memoria.

En git solo se versiona la memoria de cada proyecto (`memory.md`). El resto del contenido de `projects/` queda fuera del repositorio a propósito: el código y los artefactos de cada proyecto no forman parte de este repo.

### `.agents/rules/`

Instrucciones operativas para el agente cuando tiene que gestionar archivos en concreto

### `.agents/skills/`

Skills que amplían lo que el agente puede hacer de forma repetible. Iniciar el repo de código, cuándo leer o actualizar memorias...

## Cómo se usa

1. Abres este repositorio con un agente.
2. Trabajas dentro de `projects/<nombre-proyecto>/`.
3. El agente lee la memoria del proyecto (y, si aplica, la memoria general) antes de actuar.
4. Si aparecen decisiones o restricciones importantes, se actualiza el `memory.md` del proyecto.
5. Si el proyecto es de software y toca programar, pides el pack del repo de código y el agente lo genera con la skill.
