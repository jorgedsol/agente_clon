# Atlasweb

## Esencia

Implantación del circuito de extracciones e impresión de etiquetas con Atlasweb en hospitales 6H, sustituyendo de forma progresiva a Servolab. El foco es una metodología de distribución y configuración repetible (piloto H. Henares) para cubrir todas las secciones de todos los hospitales.

## Objetivo

- Sustituir Servolab en la impresión de etiquetas de extracciones.
- Documentar en una guía clara lo montado, lista para implantación masiva.
- Estandarizar el despliegue en tres bloques: impresora, configuración en Atlas y servicio de impresión.

## Actores

- Jorge (pilotos presenciales, configuración, guía de implantación).
- Hospitales 6H / Laboratorio Central (entorno de uso).
- H. Henares: hospital piloto (extracciones, urgencias, hospitalizados).
- IT hospitalario: drivers e impresoras nuevas (nombre estándar «Etiquetas»).
- Usuarios de extracciones (perfil en Atlasweb) y mantenimiento en Atlas de escritorio.

## Estado actual

- Pilotos en H. Henares en varias secciones; equipos y plantillas ya configurados en fases previas.
- Guía de distribución: origen en `input/Extracciones 6H y servicio de impresion.docx`; versión pulida en `output/` (mismas imágenes y estilo).
- Metodología escalable basada en los tres bloques de despliegue documentados.

## Producto

- **Atlasweb**: pantalla de extracciones (visualizar/filtrar peticiones, imprimir etiquetas). URL operativa: `https://laboratoriocentral.salud.madrid.org/atlasweb`.
- **Atlas de escritorio**: mantenimiento de impresiones / plantillas (`Peticion_Preanalitica` para registro preanalítico).
- **Servicio de impresión** («Atlas – Servicio de impresión»): puente local en cada equipo; puerto por defecto 10123 (fallback 10000–11000). Ruta de instalación: `C:\DBSOFT\Cola de impresión`.
- Reutilización de etiquetadoras Servolab (p. ej. TP 2844-Z 203 dpi sin margen; ZT-220 200 dpi con margen) o impresoras nuevas nombradas «Etiquetas».

## Arquitectura

Flujo: Atlasweb (cliente) → servicio de impresión local (hostname del equipo) → consulta en Atlas/BD de plantilla e impresora → orden de impresión → etiquetadora.

Tres bloques de despliegue por puesto:

1. Impresora Windows (drivers + DPI + nombre «Etiquetas»; calibración).
2. Plantilla y binding equipo/impresora en Atlas (`Peticion_Preanalitica`).
3. Instalación del servicio de impresión (.NET + `Instalar.cmd`).

Puntos críticos: hostname, nombre de impresora, DPI/plantilla alineados.

## Plan

1. ~~Subir documento a `input/`~~.
2. ~~Pulir guía en `output/` conservando imágenes y estilo~~.
3. Usar la guía como base de distribución masiva; ajustar con feedback de nuevos hospitales/secciones.

## Decisiones importantes

- Nombre estándar de impresora: «Etiquetas».
- Tipo de impresión en Atlas para extracciones: `Peticion_Preanalitica`.
- Plantilla según DPI/formato (200 vs 203; con/sin margen).
- Servicio local obligatorio en cada equipo de impresión; arranque automático con Windows.
- Entrega documental: pulido de redacción/estructura, sin rediseño visual ni cambio de capturas.

## Restricciones

- No inventar stack ni procedimientos no contrastados en piloto/guía.
- Al editar la guía: conservar imágenes y estilo del documento origen.
- Coherencia obligatoria entre DPI del driver, plantilla Atlas y tipo de rollo.

## Dependencias

- Carpeta de distribución del servicio (NAS/disco/USB): dependencias .NET + app cola de impresión.
- Drivers oficiales de las etiquetadoras; permisos de mantenimiento en Atlas; perfil extracciones en Atlasweb.
- Acceso a `https://laboratoriocentral.salud.madrid.org/atlasweb`.

## Pendientes

- Diagrama de arquitectura/flujo (opcional; la guía lo deja como mejora).
- Interlocutores de despliegue masivo fuera de H. Henares.
- Validar la guía pulida con una pasada real en un puesto nuevo.

## Lecciones aprendidas

- El detalle de nombres (equipo, impresora, plantilla) y DPI rompe el circuito con facilidad.
- Reutilizar la impresora Servolab exige instalar «Etiquetas» sobre el mismo puerto y calibrar.
- La primera impresión puede necesitar varios intentos por la autoconfiguración del servicio.

## Próximos pasos

1. Revisar la guía en `output/` y corregir si algo no cuadra con el piloto.
2. Cerrar metodología de distribución masiva a partir de esa guía.
3. (Opcional) Añadir diagrama de arquitectura al documento.

## Convenciones

- Proyecto: `atlasweb`.
- Input crudo / output entregable; `docs/` para referencia adicional.
- Impresora: siempre «Etiquetas». Ruta servicio: `C:\DBSOFT\Cola de impresión`.
