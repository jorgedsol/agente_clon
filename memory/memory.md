# Agente clon

> Memoria transversal e índice central del hub.
> Última actualización: 2026-11-13

# PARTE I. MEMORIA GENERAL

## 1. Esencia

Entorno de trabajo de Jorge con un agente que conserva contexto, criterio y conocimiento entre sesiones. Es un hub de proyectos bajo `projects/`; el código de producción vive en repositorios separados.

## 2. Objetivo

Dar continuidad al trabajo sin perder decisiones ni restricciones y permitir aportaciones de varios colaboradores mediante journals independientes y consolidación manual.

## 3. Actores

Jorge es el responsable del hub. Los agentes y colaboradores participan en el trabajo de sus proyectos.

## 4. Estado actual

El hub contiene los proyectos Atlasweb, Hyperlender y MeteoShare, localizables en el índice. Cada uno tiene su memoria propia.

## 5. Producto

Contexto persistente, documentación y entregables por proyecto; capacidades reutilizables mediante skills. La identidad, los principios y el estilo de Jorge están documentados en `.agents/skills/criterio-personal/references/`.

## 6. Arquitectura

La memoria transversal y su índice residen en `memory/memory.md`, con aportaciones en `memory/JOURNALS/`. Los proyectos tienen sus propias carpetas de memoria. Todas las skills del hub residen en `.agents/skills/` dentro del repo.

## 7. Plan

Pendiente.

## 8. Decisiones importantes

- El sistema de memoria adoptado separa las aportaciones incrementales de su consolidación manual.
- La implantación conserva las rutas y secciones de las tres memorias de proyecto existentes.
- El sistema está contenido y versionado en este repo, incluidas sus skills.

## 9. Restricciones

Pendiente.

## 10. Dependencias

Codex como entorno de agente y Git para el historial de memorias, journals y configuración del hub.

## 11. Pendientes

Pendiente.

## 12. Lecciones aprendidas

Pendiente.

## 13. Próximos pasos

Pendiente.

## 14. Convenciones

Los proyectos comparten las carpetas `docs/` para referencia, `input/` para material de entrada, `output/` para entregables y `memory/` para conocimiento persistente. Las rutas del índice son relativas a la raíz del hub.

# PARTE II. ÍNDICE DE MEMORIAS ESPECÍFICAS

Todas las rutas son relativas a la raíz del hub. El detalle pertenece a cada memoria.

## Atlasweb

- **Ruta de memoria:** `projects/atlasweb/memory/memory.md`
- **Ruta de journals:** `projects/atlasweb/memory/JOURNALS/`
- **Alcance:** implantación del circuito de extracciones e impresión de etiquetas con Atlasweb en hospitales 6H.
- **Consultar cuando:** se trabaje en distribución, configuración, guías o aprendizajes del despliegue de Atlasweb.
- **Ámbitos relacionados:** ninguno registrado.

## Hyperlender

- **Ruta de memoria:** `projects/hyperlender/memory/memory.md`
- **Ruta de journals:** `projects/hyperlender/memory/JOURNALS/`
- **Alcance:** plataforma de micropréstamos P2P, enfoque de colaboración, experiencia de uso y preparación para producción.
- **Consultar cuando:** se trabaje en alcance, estimación, propuesta o revisión técnica del proyecto Hyperlender.
- **Ámbitos relacionados:** ninguno registrado.

## MeteoShare

- **Ruta de memoria:** `projects/meteoshare/memory/memory.md`
- **Ruta de journals:** `projects/meteoshare/memory/JOURNALS/`
- **Alcance:** plataforma meteorológica móvil, alcance del MVP, arquitectura y propuesta del proyecto.
- **Consultar cuando:** se trabaje en producto, planificación, propuesta o preparación del desarrollo de MeteoShare.
- **Ámbitos relacionados:** ninguno registrado.

# PARTE III. REGLAS DEL ÍNDICE

El procedimiento de mantenimiento del índice está en `AGENTS.md`, en la raíz del hub, y en `.agents/skills/memory-update/SKILL.md`.
