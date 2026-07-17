# Hyperlender

## Esencia

Plataforma de micropréstamos P2P entre particulares (nombre comercial probable: **Dubidoo**). Conecta prestatarios que solicitan un importe pequeño con prestamistas que financian a cambio de rentabilidad pactada. Ya existe producto técnico con pruebas en el Sandbox de la CNMV; el cuello de botella actual es UX/frontend y llevar a producción de forma ordenada (incluyendo endurecer backend/seguridad).

## Objetivo

- Entrar en el proyecto para **ordenar y llevar a producción** soluciones nuevas: desarrollo propio y/o consultoría con su equipo, según lo que necesiten.
- Valorar y aportar en **mejoras de backend** (no solo UI), a partir de la base existente y del informe de seguridad.
- Estimar presupuesto/plazos de la nueva app (frontend usable reutilizando backend, lógica e integraciones), con feedback de viabilidad sobre la base técnica actual.
- Enfoque: ayudar en lo que haga falta para que la plataforma sea operable, segura y usable.

## Actores

- Jorge (estimación, enfoque de entrada, posible desarrollo/consultoría y mejoras back).
- Equipo HyperLender / Eurostar Media Group (producto existente, interlocución comercial/técnica).
- Usuarios: prestatario y prestamista.
- Marco regulatorio / partners citados en material comercial: CNMV (sandbox), Stripe (pagos), Tecalis (KYC), Plaid (cuentas bancarias), Algoan (scoring).

## Estado actual

- Plataforma desarrollada con pruebas funcionales en Sandbox CNMV; UX/diseño actual deficientes.
- Backend e integraciones principales: según el cliente, base avanzada; el informe de seguridad indica que **aún no está lista para operar con dinero real** ante atacantes reales.
- Acceso web `https://hyperlender.eurostarmediagroup.es/#/login`: sin acceso desde el entorno de Jorge (probable intranet).
- Prototipo visual interactivo (HTML/JS): piloto con entornos prestamista/prestatario tipo “match” (estilo Tinder) y gestión posterior de proyectos/inversiones y devoluciones.
- Presentación comercial (Canva) y diapositivas en `input/`; informe de seguridad y RGPD en `input/`.

## Producto

- Solicitud de préstamo (importe, plazo) → evaluación/scoring → financiación por prestamistas → formalización (smart contract / condiciones) → devolución capital + intereses.
- Prestamista: ver en qué ha invertido, cuánto, evolución; prestatario: lo publicado, asignado o no, acciones de devolución.
- Propuesta de valor comercial: rapidez, transparencia, accesibilidad, rentabilidad negociada, scoring/evaluación, comisión de plataforma por operación.
- Público objetivo (material comercial): nativos digitales, perfiles con capacidad de pago pero sin historial bancario clásico (estudiantes, freelancers, etc.).

## Arquitectura

- Stack observado en informe: backend con Docker; infra Terraform/AWS (EC2, RDS cifrado, EBS); blockchain (Besu/RPC, smart contracts pausables); pagos Stripe/PayPal/(Binance citado); Plaid; Algoan; MFA TOTP; webhooks firmados.
- Sesión hoy expuesta vía `localStorage` + cookie JS (informe).
- Clave privada administrativa única en config del servidor (punto único de compromiso).
- Detalle fino de repos/servicios: pendiente de acceso código o sesión técnica.

## Plan

1. Asimilar contexto (email, diapositivas, informe seguridad) → memoria.
2. Definir approach de entrada: producto (frontend/UX a producción) + hardening backend priorizado (P0 del informe) + modo colaboración (build y/o consultoría con su equipo).
3. Pedir acceso (VPN/intranet, repo, prototipo adjunto si falta en `input/`) y contrastar viabilidad técnica.
4. Propuesta: alcance, prioridades P0/P1, estimación y forma de trabajo.

## Decisiones importantes

- No partir de cero: reutilizar backend/integraciones en la medida de lo posible; rehacer o mejorar la capa de experiencia.
- El informe de seguridad es input clave del approach (no solo “maquillar UI”).
- Postura comercial/técnica: ayudar en lo que necesiten (orden, producción, front, back, seguridad).

## Restricciones

- Sin acceso actual a la plataforma en producción/intranet.
- No inventar stack ni plazos hasta ver código/accesos.
- Operación con dinero real condicionada a corregir al menos P0 del informe.
- Cumplimiento RGPD/LOPDGDD: el informe lo marca como parcial/insuficiente demostrable.

## Dependencias

- Acceso a plataforma (intranet/VPN), prototipo interactivo completo, repos y, si aplica, docs de infra.
- Claridad del cliente sobre modo de colaboración (equipo interno + consultoría vs. desarrollo externalizado).
- Partners: Stripe, Tecalis, Plaid, Algoan, marco CNMV.

## Pendientes

- Conseguir acceso a la app actual y al código / infra.
- Ubicar el prototipo HTML/JS en `input/` o `docs/` si no está versionado aquí.
- Contrastar con el equipo qué del informe ya está en curso.
- Borrador de approach + estimación (front a producción + P0 seguridad/back).

## Lecciones aprendidas

- Base “avanzada” en backend no implica lista para producción financiera: el informe señala rutas críticas (Plaid token al navegador, retiros no atómicos, secretos/admin key, sesiones).

## Próximos pasos

1. Confirmar con el cliente accesos (app, repo, prototipo) y prioridades de negocio.
2. Proponer approach en dos frentes acoplados: **experiencia a producción** + **P0 seguridad/integridad financiera**.
3. Acotar oferta (build / consultoría / mix) y estimación.

## Convenciones

- Carpeta proyecto: `hyperlender` (marca comercial posible: Dubidoo).
- Material: `input/` (email, diapositivas, informe seguridad); entregables en `output/`.
- Prioridades seguridad del informe: **P0** antes de dinero real (Plaid token, retiros PayPal/Binance, montaje `config.json` AWS, clave blockchain/secretos en KMS/Secrets Manager, conciliación/estados, sesiones); luego P1/P2.
