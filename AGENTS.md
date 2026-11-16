# AGENTS.md

Este repo es un **hub de varios proyectos** bajo `projects/`. No es un repo de producto.

## Proyectos

Si el usuario pide crear un proyecto nuevo y no existe `projects/<nombre>/`, usa la skill `new-project`.

No empieces el trabajo del proyecto hasta que la inicialización haya terminado y existan su carpeta y `memory/memory.md`.

Cuando trabajes dentro de `projects/<nombre>/`:

1. Lee `memory/memory.md` de la raíz para localizar el ámbito y `projects/<nombre>/memory/memory.md` antes de una tarea no trivial. Es la fuente de verdad consolidada del proyecto. Consulta los journals relacionados cuando puedan contener cambios relevantes aún no consolidados y distingue su estado de validación.
2. Sitúa la petición en el alcance documentado.
3. Si faltan datos importantes, pregunta o declara la hipótesis.
4. Prefiere el cambio más pequeño que resuelva el problema.
5. Claridad sobre ingenio. Reutiliza lo que ya hay; no añadas capas ni dependencias por si acaso.
6. No refactorices ni limpies deuda no pedida.
7. Propón una alternativa más simple si la hay.

## Archivos y responsabilidades

- `memory/memory.md` (raíz): conocimiento consolidado transversal e índice de las memorias del hub. No guardar aquí hechos específicos de un proyecto ni instrucciones de actuación.
- `memory/JOURNALS/` (raíz): aportaciones pendientes de consolidación de alcance transversal y altas de ámbitos pendientes de indexar.
- `projects/<nombre>/memory/memory.md`: fuente de verdad consolidada del proyecto. Conserva los encabezados de sección: no renombres, borres ni añadas secciones salvo que yo lo pida. Pide confirmación explícita antes de modificar su estructura, también durante una consolidación.
  - Durante el trabajo ordinario no lo modifiques: registra únicamente conocimiento duradero y relevante en `memory/JOURNALS/` mediante `memory-manager`.
  - No incluyas chats, brainstorming ni notas que caduquen en días.
  - No dupliques ideas entre secciones.
  - Mantenlo compacto.
  - Secciones vacías: encabezado + `Pendiente.`
- `projects/<nombre>/memory/JOURNALS/`: journals independientes del proyecto; se conservan como historial después de revisarlos.
- `AGENTS.md` del proyecto: instrucciones y límites operativos específicos del proyecto. No guardar aquí hechos o decisiones que correspondan a su `memory.md`.
- `projects/<nombre>/docs/`: documentación de referencia.
- `projects/<nombre>/input/`: material de entrada en bruto.
- `projects/<nombre>/output/`: entregables.

No mezcles esos roles.

## Sistema de memoria colaborativa

- Usa `memory-manager` para localizar memorias, consultar contexto y capturar conocimiento relevante. Antes de registrar, lee la memoria del ámbito y los journals relacionados para evitar duplicidades.
- Captura solo decisiones, restricciones, descubrimientos, riesgos o aprendizajes con valor futuro. No crees journals por tareas rutinarias, conversaciones, resúmenes de sesión ni cambios ya documentados.
- No edites memorias consolidadas ni el índice durante el trabajo ordinario. No modifiques journals anteriores para añadir o corregir aportaciones: crea uno nuevo que los referencie.
- Solo consolida cuando el usuario invoque expresamente `memory-update`, por ejemplo `$memory-update projects/atlasweb`. No la actives por iniciativa propia ni mediante hooks o automatizaciones.
- `memory-update` contrasta los journals, actualiza la memoria propietaria y el índice, documenta el tratamiento y conserva los originales. Si hay contradicciones sin resolver, deja esas aportaciones pendientes.
- Registra el detalle en su ámbito propietario y referencia el impacto transversal sin copiarlo entre memorias. No crees memorias para todos los subdirectorios por defecto.
- Si un ámbito nuevo necesita memoria durante el trabajo ordinario, crea solo su carpeta de journals y una aportación; deja la creación de la memoria consolidada y el alta en el índice para `memory-update`.
- Al inicializar expresamente un proyecto con `new-project`, sí se permite crear su primera `memory/memory.md` siguiendo la skill. Añade `memory/JOURNALS/.gitkeep` y registra el alta pendiente de indexar en un journal raíz. No modifiques el índice hasta una consolidación manual.
- Estas reglas sustituyen cualquier paso de actualización directa de memoria indicado por las skills existentes. En particular, el paso de `init-code-repo` que actualiza la memoria del clon debe producir un journal. Conserva intactas las skills protegidas y sus referencias.
- Cuando se solicite un pack nuevo de código, adapta los archivos generados para capturar en journals y consolidar manualmente; no propagues las instrucciones antiguas de actualización directa ni modifiques packs existentes sin autorización.
- Antes de escribir, comprueba que los archivos no han cambiado desde su lectura. Usa nombres únicos y creación exclusiva para los journals; nunca sobrescribas una aportación concurrente.
- No guardes secretos ni credenciales. Redacta las comunicaciones, instrucciones y registros en español salvo denominaciones originales o petición expresa.
- No afirmes que has guardado conocimiento sin comprobar el archivo escrito.
- Mantén en las memorias hechos, contexto y decisiones del ámbito. Las reglas de actuación, permisos, protecciones de archivos y procedimientos pertenecen a `AGENTS.md` o a las skills, sin copiarlos en la memoria.
- Mantén el índice durante la consolidación manual cuando se cree, mueva o retire una memoria o cambie su alcance. Cada entrada debe indicar rutas de memoria y journals relativas a la raíz del hub, alcance, cuándo consultar y ámbitos relacionados. No lo actualices por cada journal ni reproduzcas detalles del proyecto. Comprueba las altas pendientes en `memory/JOURNALS/` y las carpetas de ámbitos no indexados.

Las skills del sistema viven en `.agents/skills/` de este repo y se versionan aquí, sin instalaciones globales ni copias por proyecto. La estructura y los ejemplos de uso están en `README.md`.

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
