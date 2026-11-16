---
name: memory-manager
description: Consulta memorias distribuidas y captura decisiones, restricciones o aprendizajes duraderos en journals independientes. Úsala para recuperar contexto o registrar conocimiento relevante en un proyecto con este sistema. No consolida ni modifica memorias existentes.
---

# Consulta y captura de memoria

Esta skill forma parte del hub y se versiona en `.agents/skills/memory-manager/`. Respeta las instrucciones y los límites del repositorio.

## Localizar y consultar

1. Lee las instrucciones del repositorio e identifica su raíz y el ámbito de la tarea.
2. Lee la memoria general y su índice. Respeta las rutas declaradas; en el hub `agente_clon` son:
   - General e índice: `memory/memory.md`; journals transversales: `memory/JOURNALS/`.
   - Proyecto: `projects/<nombre>/memory/memory.md`; journals: `projects/<nombre>/memory/JOURNALS/`.
   - Subámbito, si lo necesita: `<ámbito>/memory/memory.md` y `<ámbito>/memory/JOURNALS/`.
3. Consulta solo las memorias relacionadas. Si falta una entrada del índice, comprueba las rutas del ámbito antes de afirmar que no existe memoria.
4. Lee los journals relacionados para detectar decisiones aún no consolidadas, duplicados y contradicciones. Distingue conocimiento consolidado, hechos confirmados, propuestas y datos pendientes de validar; un journal nuevo no convierte una propuesta en decisión.

Todas las rutas del índice son relativas a la raíz del hub. No crees variantes ni duplicados de una ruta existente y no dependas de que el sistema de archivos ignore mayúsculas.

## Evaluar y elegir el ámbito

Registra únicamente conocimiento que cambie decisiones futuras, explique una restricción importante, evite repetir un error o permita continuar el trabajo con contexto significativo. Comprueba que no esté ya en la memoria ni en sus journals.

No registres actividad rutinaria, cambios cosméticos, conversaciones, resúmenes de sesión, tareas ordinarias ni información efímera o fácilmente recuperable sin contexto adicional. No escribas un journal si no aporta valor duradero nuevo.

Elige el ámbito propietario más específico. Si afecta a otros, describe el impacto y enlaza sus memorias. Solo crea además un journal transversal cuando haya una consecuencia global importante; referencia el original sin copiar su contenido.

Si falta memoria en un ámbito, crea únicamente su carpeta de journals y la aportación. No crees una memoria consolidada ni cambies el índice: el alta corresponde a `memory-update` manual. Si se necesita incorporar ese ámbito al índice, registra la propuesta de alta en los journals generales con su ruta, alcance y condiciones de consulta. La inicialización expresa mediante `new-project` es una excepción autorizada para crear la primera memoria; sigue las instrucciones del hub.

## Crear una aportación

- Revisa el contenido actual de la memoria y de los journals relacionados justo antes de escribir.
- Crea un archivo independiente con nombre `YYYY-MM-DD-HHMM-titulo-descriptivo.md`, usando la fecha y zona horaria del usuario; en el hub, `Europe/Madrid`.
- Usa creación exclusiva, sin sobrescritura. Si colisiona, añade un sufijo o identificador breve y vuelve a crear de forma exclusiva.
- Escribe en español, sin secretos ni credenciales. No copies conversaciones.
- Conserva el estado de validación separado del estado de consolidación. Un hecho confirmado empieza con `Consolidación: pendiente`.
- Para corregir una aportación anterior, crea una nueva que explique qué sustituye y enlace el registro original. No edites el anterior.
- Verifica el archivo escrito antes de informar de que se ha guardado.

### Plantilla del journal

Omite apartados que no aporten información; no inventes datos para completarlos. Conserva los metadatos de estado y consolidación.

```markdown
# JOURNAL: Título descriptivo

- **Fecha:** YYYY-MM-DD HH:MM (Europe/Madrid; adaptar al usuario)
- **Ámbito:** nombre y ruta del ámbito propietario
- **Tipo:** decisión / cambio / descubrimiento / restricción / aprendizaje / riesgo / dependencia
- **Estado:** confirmado / propuesta / pendiente de validación
- **Consolidación:** pendiente
- **Origen:** decisión del usuario, documento o trabajo que sustenta el registro
- **Afecta a:** ámbitos o documentos relacionados

## 1. Contexto

Situación necesaria para entender el registro sin consultar el chat.

## 2. Información relevante

Hecho o cambio nuevo, con referencias a sus fuentes.

## 3. Decisión o conclusión

Decisión adoptada o indicación expresa de que sigue pendiente.

## 4. Justificación

Motivos y valor futuro.

## 5. Impacto

Consecuencias locales y transversales.

## 6. Restricciones y condiciones

Condiciones y excepciones que deben conservarse.

## 7. Relación con conocimiento existente

- Memorias o apartados relacionados:
- Journals anteriores relacionados:
- Información que actualiza o sustituye:

## 8. Información que debe incorporarse a la memoria

Conocimiento duradero propuesto para su consolidación.
```

## Límites y cierre

Nunca modifiques una memoria consolidada o el índice, fusiones aportaciones, marques journals como tratados ni elimines registros. No invoques `memory-update` por iniciativa propia. Esta skill solo consulta y crea journals.

Al guardar, indica brevemente qué conocimiento se ha registrado, su ámbito, su ruta y por qué tiene valor futuro. Si no se ha creado ningún journal, comunícalo solo si resulta útil; no fabriques aportaciones para cerrar la tarea.
