# MeteoShare

## Esencia

Plataforma meteorológica mobile centrada en un mapa interactivo. El mapa es la pantalla principal; la información contextual se consulta en drawers sin abandonar el contexto geográfico.

Tres tipos de nodos (puntos de entrada de información):
- **Nodo base** — datos objetivos vía sistema central de agregación del cliente (Meteoclimatic, Weather Underground, pólenes, embalses; calidad del aire potencial p. ej. AQICN) consumido por **endpoints**.
- **Nodo usuario** — reportes geolocalizados; publicación general libre (con validación colaborativa).
- **Nodo partner** — comunidades/canales verificados; publicación en canal puede requerir validación del moderador.

Hipótesis: ¿la gente consulta y aporta información meteorológica hiperlocal útil?

Alcance geográfico: **cualquier ubicación desde el inicio**. Mundaka = caso de uso / piloto de referencia, no límite técnico.

Cuatro+ capacidades del MVP: mapa · datos contextuales por zona · reportes rápidos · validación colaborativa · comunidades/partners.

---

## Objetivo

MVP funcional en **12 semanas**, iterable después. Priorizar validación de producto; IA, push y segundo plano como evolución.

---

## Actores

- Cliente: EUROSTAR MEDIA GROUP S.L.
- Contacto: Guillermo (tú)
- Propuesta/comunicación: Jorge Domínguez-Sol Sastre (voz «nosotros» en docs formales)
- Partner previo: planificación PWA (~14 épicas / ~19 semanas). Cliente prefiere el plan de 12 semanas.
- Sistema de agregación de datos del cliente: https://meteoshare-mapa.ashypebble-eecefd9c.northeurope.azurecontainerapps.io/

---

## Estado actual

Hilo de emails julio 2026 cerrado en alcance. Propuesta final ajustada. Pendiente: confirmación formal, inicio, Figma y endpoints.

Entregables:
- `input/Meteoshare propuesta de proyecto.docx` — versión base detallada (no tocar; referencia)


Prototipo UX: https://v0-public-link-for-boss.vercel.app/  
Figma: existe (acceso vía partner; gestionar si no se ve).

---

## Producto (MVP)

### UX base
Nav: Mapa · Feed · Publicar · Mis zonas · Perfil (+ comunidades). Drawers sobre mapa. Marcadores diferenciados. Estado zona: Estable / Precaución / Riesgo.

### Journeys
- Consulta → mapa → zona → detalle.
- Publicación <10 s (general o en comunidad).
- Validación colaborativa «Sigue ahí» / «Ya no está» (estilo Waze).
- Comunidades: unirse, publicar en canal, cola de moderación partner.
- Seguimiento: Mis zonas + feed.

### Incluido en MVP
Mapa global · nodos base vía endpoints · reportes · validación comunitaria · feed reducido · zonas guardadas · geo en uso · perfil mínimo · **comunidades/partners** · infra RN + Django.

### Fuera / posterior
- IA (primer foco post-MVP: moderación de **texto**; no imagen/AV como primer paso).
- Push y geo en segundo plano.
- Estaciones físicas como entidad de producto.
- Predicciones/recomendaciones elaboradas.
- Tiendas + hosting/licencias (cliente).

---

## Arquitectura

1. **Presentación** — React Native: mapa, drawers, auth, comunidades, cámara, geo en uso.
2. **Servicios** — Django + DRF: usuarios, zonas, reportes, vigencia, validaciones, comunidades, consumo nodo base.
3. **Datos** — PostgreSQL; OSM; endpoints del agregador y/o APIs de origen. JWT, Docker, Git. Open source preferente.

Integración de datos: **endpoints suficientes** (agregador del cliente u origen). No hace falta entrar en su código para arrancar; evita retrasos. Polling u otras formas: en fase de integración.

---

## Plan

12 semanas, 1 full stack + esfuerzo extra para comunidades **sin mover calendario**.

| Fase | Semanas | Contenido |
|------|---------|-----------|
| 0 | 1 | Arranque, contratos API, modelo (incl. comunidades) |
| 1 | 2 | Auth, nav, drawers |
| 2 | 2 | Mapa OSM + geo en uso |
| 3 | 1,5 | Endpoints nodo base + detalle zona |
| 4 | 2 | Reportes |
| 5 | 2 | Validación colaborativa + comunidades |
| 6 | 1 | Feed + zonas guardadas |
| 7 | 0,5 | Integración, pruebas, entrega |

Arranque del núcleo no bloqueado por endpoints; la integración meteo se acopla cuando existan.

---

## Decisiones importantes

- App nativa confirmada (push/segundo plano futuros refuerzan la decisión).
- Geografía abierta desde día 1.
- Comunidades/partners **dentro** del MVP; se absorbe esfuerzo para mantener 12 semanas.
- Sin IA en MVP; validación = confirmación comunitaria. IA post-MVP sobre texto primero.
- Integración por endpoints, no por inmersión en código del agregador.
- 12 semanas encajan al cliente.
- Sin cifras económicas aún; confidencialidad Eurostar ↔ Jorge.
- Cesión IP al cliente; tiendas/infra a cargo del cliente.

---

## Restricciones

- No inventar endpoints: el cliente los facilita (agregador u origen).
- No meter tarifas hasta acordarlo.
- No mencionar uso de IA como herramienta de trabajo en docs al cliente.
- No comprometer push/segundo plano en el entregable MVP.

---

## Dependencias

- Endpoints del nodo de agregación (o APIs origen) + timeline si aún no están.
- Acceso Figma estable.
- Confirmación formal de la propuesta e inicio.

---

## Pendientes

- Confirmación de propuesta final / formalización de encargo y fecha de inicio.
- Entrega o timeline de endpoints.
- Acceso Figma si aún no está.

---

## Lecciones aprendidas

- Confirmar nativa aunque push quede fuera: desbloquea arquitectura a futuro.
- Ofrecer endpoints (no código) reduce fricción y permite arrancar.
- Comunidades son alcance real; si el calendario ya encaja, absorber esfuerzo es mejor que reabrir plazos.
- IA sobre veracidad de fotos es mala apuesta; texto inadecuado sí es un buen primer paso post-MVP.

---

## Próximo paso

Enviar propuesta actualizada + email de cierre; si confirman, formalizar inicio y pedir endpoints/Figma.
