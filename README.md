# Agente clon

Repositorio de trabajo para un agente que actúa como extensión del criterio, estilo y forma de pensar de Jorge. Conserva contexto estable y trabajo por proyectos. Cada proyecto de software puede contener su módulo `codigo/`.

## Estructura

```text
.
├── AGENTS.md                     # Instrucciones operativas para Codex
├── memory/
│   ├── MEMORY.md                 # Memoria transversal e índice de ámbitos
│   └── journals/                 # Aportaciones transversales
├── projects/
│   └── <nombre>/
│       ├── docs/                 # Referencia
│       ├── input/                # Material de entrada
│       ├── output/               # Entregables
│       ├── codigo/               # Módulo de desarrollo, cuando se inicialice
│       └── memory/
│           ├── MEMORY.md         # Memoria consolidada del proyecto
│           └── journals/         # Aportaciones e historial
└── .agents/skills/               # Todas las skills del hub, incluidas las de memoria
```

Git versiona las memorias y los journals de los proyectos. Sus documentos de entrada y entregables siguen excluidos. Los archivos `.gitkeep` permiten conservar las carpetas de journals vacías.

## Cómo se usa la memoria

Antes de una tarea no trivial, el agente consulta el índice en `memory/MEMORY.md` y la memoria del proyecto. Los journals relacionados aportan cambios aún no consolidados; su información debe interpretarse según su estado de validación. La memoria contiene conocimiento del hub o del proyecto; las reglas de actuación pertenecen a `AGENTS.md` y a las skills.

Durante el trabajo, `memory-manager` puede registrar una decisión, restricción, descubrimiento o aprendizaje con valor futuro. Primero comprueba que no esté ya documentado. Crea un archivo independiente y conserva intacta la memoria consolidada. Las tareas rutinarias y los resúmenes de sesión no generan journals.

La consolidación se solicita expresamente con `memory-update`, indicando el ámbito:

```text
$memory-update projects/atlasweb
$memory-update hub
$memory-update todos los ámbitos del hub
```

La skill contrasta las aportaciones con la memoria, integra lo que corresponda, mantiene pendientes las dudas, actualiza el índice cuando procede y documenta qué ha tratado. Los journals originales se conservan; una aportación posterior corrige otra mediante una referencia, sin reescribir el historial. No hay hooks ni tareas automáticas de consolidación.

## Skills de memoria en Codex

Las dos skills se definen y versionan en este repo, junto con las existentes:

```text
.agents/skills/
├── memory-manager/
│   └── SKILL.md
└── memory-update/
    ├── SKILL.md
    └── agents/openai.yaml
```

`memory-manager` puede activarse por relevancia o mediante `$memory-manager`. `memory-update` tiene `policy.allow_implicit_invocation: false` en `agents/openai.yaml`, además de exigir una petición expresa en sus instrucciones. Esta es la adaptación de la invocación manual a Codex; no se utiliza el campo de Claude `disable-model-invocation`. La ubicación dentro del repo y la política están documentadas en la [documentación oficial de skills](https://learn.chatgpt.com/docs/build-skills).

Las skills se comparten al clonar el repo y no requieren instalación global. Si Codex no muestra una skill nueva, reinicia la aplicación.

## Proyectos nuevos y módulos de código

`new-project` conserva su flujo de inicialización y crea la primera memoria. Después se añade su carpeta de journals y se registra el alta pendiente de indexar en un journal raíz. La incorporación al índice espera a `memory-update`.

`init-code-repo` prepara `projects/<nombre>/codigo/` y las instrucciones de desarrollo que sean necesarias, reutilizando lo existente. Git y el esqueleto técnico se preparan si la petición los incluye.

El módulo puede tener memoria propia o no. Su existencia y gestión corresponden exclusivamente a las skills de memoria; `init-code-repo` no crea memorias, journals ni altas en el índice.

Las skills y sus referencias siguen protegidas salvo autorización expresa para modificarlas. Las memorias consolidadas se actualizan únicamente mediante consolidación manual. El material seleccionado de `input/` debe quedar fuera de esa carpeta, que es transitoria.

## Adaptación de la especificación

La guía de implantación está en `setup/sistema_memoria_colaborativa.md`. En este hub, `AGENTS.md` cumple el papel de las instrucciones de Claude. La raíz y los proyectos utilizan la misma estructura `memory/MEMORY.md` y `memory/journals/`, conservando las memorias de proyecto y sus secciones existentes. Las skills residen en `.agents/skills/` para que todo el sistema esté en el repo.

El estado de validación de un journal (`confirmado`, `propuesta` o `pendiente de validación`) se registra aparte de su consolidación (`pendiente`, `consolidado` o `descartado`). Así, consolidar no elimina si la información estaba confirmada o pendiente de comprobar.

No se crean memorias adicionales para directorios sin conocimiento persistente propio. La creación de un ámbito durante el trabajo ordinario empieza por un journal; la memoria consolidada y su entrada en el índice se crean durante una consolidación manual. Esta regla evita la excepción de editar el índice desde la captura que aparecía en la especificación original.
