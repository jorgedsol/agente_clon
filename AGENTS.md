# AGENTS.md

Este repo es un **hub de varios proyectos** bajo `projects/`. No es un repo de producto.

## Proyectos

Si el usuario pide crear un proyecto nuevo y no existe `projects/<nombre>/`, usa la skill `new-project`.

No empieces el trabajo del proyecto hasta que la inicialización haya terminado y existan su carpeta y `memory/memory.md`.

Cuando trabajes dentro de `projects/<nombre>/`:

1. Lee `projects/<nombre>/memory/memory.md` antes de una tarea no trivial. Es la única fuente de verdad sobre ese proyecto.
2. Sitúa la petición en el alcance documentado.
3. Si faltan datos importantes, pregunta o declara la hipótesis.
4. Prefiere el cambio más pequeño que resuelva el problema.
5. Claridad sobre ingenio. Reutiliza lo que ya hay; no añadas capas ni dependencias por si acaso.
6. No refactorices ni limpies deuda no pedida.
7. Propón una alternativa más simple si la hay.

## Archivos y responsabilidades

- `MEMORY.md` (raíz): contexto general del hub, su organización, criterios compartidos y decisiones que afectan a varios proyectos. No guardar aquí hechos específicos de un proyecto.
- `projects/<nombre>/memory/memory.md`: única fuente de verdad del proyecto. Conserva los encabezados de sección: no renombres, borres ni añadas secciones salvo que yo lo pida. Pide confirmación explícita antes de modificar su estructura.
  - Si durante el trabajo aparecen decisiones importantes, cambios de arquitectura, restricciones o conocimiento útil para futuras sesiones, actualízalo solo con lo que siga siendo útil.
  - No incluyas chats, brainstorming ni notas que caduquen en días.
  - No dupliques ideas entre secciones.
  - Mantenlo compacto.
  - Secciones vacías: encabezado + `Pendiente.`
- `AGENTS.md` del proyecto: instrucciones y límites operativos específicos del proyecto. No guardar aquí hechos o decisiones que correspondan a su `memory.md`.
- `projects/<nombre>/docs/`: documentación de referencia.
- `projects/<nombre>/input/`: material de entrada en bruto.
- `projects/<nombre>/output/`: entregables.

No mezcles esos roles.

## Contenido

Si la tarea es de contenido (emails, posts, documentos, estrategia, propuestas, etc.), usa la skill `criterio-personal`. Contiene las indicaciones sobre estrategia, metodología y toma de decisiones.

Si es exclusivamente código o desarrollo de software, no cargues esa skill.

Los textos de `ejemplos.md` de `criterio-personal` son material en bruto: no se usan tal cual ni se copian.

## Código de un producto

El código de producción no vive en este repo.

Si hay que arrancar el pack del repositorio de código de un proyecto, usa la skill `init-code-repo`.

## Git

No hagas commits automáticamente después de implementar cambios.

Deja los cambios sin commit y haz commit únicamente cuando yo lo pida explícitamente.

## Protección de archivos

- Las skills (`criterio-personal`, `new-project`, `init-code-repo`) y sus `references/`: nunca modificar.
- Este `AGENTS.md` global: no modificar sin mi autorización explícita. Pregunta siempre.
- Los `AGENTS.md` de otros niveles: no modificar sin mi autorización explícita. Pregunta siempre.
- Este `main.mdc`: no modificar sin mi autorización explícita. Pregunta siempre.

## Preguntar antes de

- Cambios de modelo de datos incompatibles, cuando aplique.
- Dependencias nuevas relevantes o arquitectura distinta a la documentada en `memory.md`.
- Salirse del alcance documentado.
- Cambiar la estructura de secciones de `memory.md`.
- Sobrescribir un directorio `projects/<nombre>/` que ya existe.