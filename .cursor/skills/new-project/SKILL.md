---
name: new-project
description: >-
  Crea un proyecto nuevo bajo projects/ con la estructura estándar (docs, input,
  memory, output) y la primera versión de memory/memory.md a partir del blueprint.
  Usar cuando el usuario pida iniciar un proyecto nuevo, crear proyecto en
  projects/, new-project, o arrancar un espacio de trabajo para un cliente/producto
  en el clon. No usar para init-code-repo ni para scaffolding de código.
---

# New project

Crea `projects/<nombre>/` con la siguiente estructura y genera la primera versión de `memory/memory.md` desde el blueprint.

## Estructura objetivo (fija)

```
projects/<nombre>/
├── docs/                 # Material de referencia (propuestas, documentaciones, capturas…)
├── input/                # Inputs crudos / material de entrada
├── output/               # Entregables generados en el clon
└── memory/
    └── memory.md         # Memoria permanente del proyecto
```

Nombre de carpeta: minúsculas, sin espacios (barra baja si hace falta). Ej.: `meteoshare`, `acme_landing`.

Plantilla de memoria: [resources/blueprint_memory.md](resources/blueprint_memory.md). Conservar las secciones del blueprint; y subsecciones si tiene sentido para el proyecto en concreto o si el usuario lo pide.

## Workflow

Copia y marca progreso:

```
- [ ] 1. Nombre y colisión
- [ ] 2. Crear carpetas
- [ ] 3. Origen del contexto (preguntar)
- [ ] 4. Recoger / leer fuentes
- [ ] 5. Escribir memory.md
- [ ] 6. Confirmar al usuario
```

### 1. Nombre y colisión

Si el usuario no dio nombre de carpeta, preguntar una vez.

Si `projects/<nombre>/` ya existe → no sobrescribir. Avisar y pedir otro nombre o confirmación explícita de qué hacer.

### 2. Crear carpetas

Crear exactamente:

- `projects/<nombre>/docs/`
- `projects/<nombre>/input/`
- `projects/<nombre>/output/`
- `projects/<nombre>/memory/`

### 3. Origen del contexto (obligatorio preguntar)

Antes de rellenar `memory.md`, preguntar al usuario **cómo** quiere aportar contexto para la primera versión. Ofrecer estas opciones (puede combinar):

1. **Contexto en el chat** — resume o pega lo esencial ahora (qué es, para quién, objetivo, restricciones…).
2. **Subir a `input/`** — deja archivos en `projects/<nombre>/input/` (propuesta, emails, notas, capturas…) y avisa cuando estén listos para leerlos.
3. **Estructura vacía** — solo carpetas + `memory.md` con el esqueleto del blueprint (título = nombre del proyecto; secciones vacías o con “pendiente” mínimo).

No asumir la opción. Esperar respuesta antes del paso 5 (salvo que el usuario ya haya dado contexto claro en el mismo mensaje de creación).

### 4. Recoger / leer fuentes

Según lo elegido:

- **Chat:** usar solo lo que el usuario escribió en la conversación.
- **input/:** leer lo que haya en `input/`
- **Vacío:** no inventar contenido.

Reglas:

- No inventar hechos, actores, plazos ni stack.
- Si falta un dato, dejar la sección breve o marcar pendiente en `Pendientes` / `Dependencias`.
- Español, claro, compacto (mismo criterio que el clon: solo lo que siga siendo útil).
- No copiar conversaciones enteras ni brainstorming temporal a `memory.md`.

### 5. Escribir memory.md

1. Partir de [resources/blueprint_memory.md](resources/blueprint_memory.md).
2. Sustituir `Nombre_proyecto` por el nombre real del proyecto.
3. Rellenar secciones con lo inferido de las fuentes; omitir relleno inventado.
4. Guardar en `projects/<nombre>/memory/memory.md`.

Calidad:

- Compacto, sin duplicar la misma idea en varias secciones.
- Secciones sin info conocida: dejar el encabezado y una línea corta (`Pendiente.` o vacío), no párrafos de relleno.

### 6. Cierre al usuario

Indicar:

1. Ruta creada: `projects/<nombre>/`.
2. Que `memory/memory.md` es la memoria del proyecto (el agente la leerá en sesiones siguientes).
3. Dónde meter material: `docs/` (referencia), `input/` (entrada), `output/` (entregables).
4. Si es proyecto de software y más adelante toca programar: skill `init-code-repo` (no forma parte de este paso).

## Anti-patrones

- Crear el proyecto sin preguntar origen de contexto cuando no hay información suficiente.
- Sobrescribir un `projects/<nombre>/` existente sin confirmación.
- Inventar esencia, actores o plan “de ejemplo”.
- Meter identidad/estilo del clon (`memory/identidad.md`, etc.) en el `memory.md` del proyecto.
- Generar `project_code_init/` o código de producto dentro de este flujo.
- Llenar `memory.md` con transcriptos o notas que caduquen en días.
