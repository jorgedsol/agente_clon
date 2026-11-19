---
name: init-code-repo
description: >-
  Prepara la carpeta codigo de un proyecto existente y las instrucciones operativas
  necesarias para desarrollar en ella. Usar al pedir iniciar el repositorio de
  código o preparar el módulo de desarrollo. No gestiona la memoria del módulo.
---

# Preparar el módulo de código

Trabaja directamente en `projects/<nombre>/codigo/`.

1. Consulta las instrucciones aplicables y el contexto disponible del proyecto.
2. Si el proyecto aún no existe, completa primero su inicialización con `new-project`.
3. Crea `codigo/` si no existe. Si ya existe, revisa lo que contiene y reutilízalo
   sin sobrescribir archivos ni migrar repositorios por iniciativa propia.
4. Añade un `AGENTS.md` local solo si hacen falta instrucciones específicas de
   desarrollo que no estén cubiertas por las del proyecto. No dupliques contexto.
5. Prepara Git o el esqueleto técnico únicamente si la petición lo incluye,
   respetando el stack y las decisiones documentadas. No hagas commits automáticos.
6. Comprueba lo preparado e informa de la ruta, los cambios y los pendientes reales.

La existencia y gestión de memoria del módulo corresponden exclusivamente a las
skills de memoria. Esta skill no crea memorias, journals, altas de ámbitos ni
entradas de índice, ni decide si el módulo necesita memoria propia.

No genera packs para copiar, plantillas de memoria ni reglas de Cursor por defecto.
No inventa stack, dependencias, endpoints o comandos que todavía no existan.
