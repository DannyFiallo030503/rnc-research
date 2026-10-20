# DEC-014 — Exploración de alojamiento para demo web provisional

**Estado:** CRITERIO DE EXPLORACIÓN; no se ha seleccionado proveedor ni publicado la aplicación.
**Fecha:** 2026-10-19
**Trazabilidad:** `SRC-PRJ-004` → `EVD-118..124` → `Q-026`; relacionado con `DEC-011` y `DEC-013`.

## Dirección

Para mostrar el avance desde distintos dispositivos, consultar primero si CUJAE o el RNC pueden ofrecer un subdominio y una VM/servidor de ensayo autorizados. Si no hay entorno disponible, CITMATEL es candidato local para consultar: su página anuncia alojamiento de aplicaciones, bases de datos y páginas web con visibilidad hacia el exterior (`SRC-CITMATEL-HOSTING-2026`, `EVD-119`). La oferta pública no acredita por sí sola compatibilidad con Django/PostgreSQL ni las demás condiciones que requiere esta aplicación.

Vercel es técnicamente compatible con Django y puede generar vistas previas desde Git (`EVD-122`), pero hay que verificar el uso permitido, pago y disponibilidad desde Cuba, así como adaptar persistencia y almacenamiento. No se ha encontrado en los términos consultados una prohibición geográfica explícita para Cuba; tampoco se ha confirmado elegibilidad. GitHub Pages es otra vía para enseñar una versión estática, no la aplicación Django: no ejecuta Python, y bajo GitHub Free el sitio requiere un repositorio público (`EVD-123..124`). GitHub indica que sus servicios cloud están generalmente disponibles para desarrolladores en Cuba, sujeto a restricciones individuales (`SRC-GITHUB-CUBA-2026`).

Render no se considera opción: los términos actuales excluyen a personas o entidades ubicadas o residentes en Cuba (`SRC-RENDER-TOS-2026`, `EVD-120`). Una guía técnica compatible con Django no elimina esa restricción. No se recomienda sortear restricciones de proveedores.

## Alcance de un eventual demo

- Datos exclusivamente sintéticos; nunca cargar `BD PARA DANI.csv`, microdatos, credenciales o cuentas institucionales.
- Mostrar solo el sitio público; excluir panel, autenticación administrativa, cargas y correo real.
- Mantener el entorno separado de una futura instalación institucional y eliminarlo cuando deje de ser necesario.
- Antes de publicar, adaptar y revisar configuración de producción, servidor de aplicación, HTTPS/hosts/CSRF, recursos estáticos, persistencia de base/archivos y método autorizado para preparar la publicación sintética. La configuración local y `seed_demo` no bastan: este último exige `DEBUG=True`, lo cual no es apropiado para un servicio compartido.
- Confirmar costo, dominio, capacidad y límites, Django/Python, PostgreSQL o persistencia equivalente, TLS, copias/restauración, acceso desde redes cubanas y externas, soporte, responsabilidades y condiciones contractuales.

## Motivo del estado abierto

El entorno académico actual es Django/SQLite local, `DEBUG=True` por defecto, almacenamiento local y buzón de correo en archivos (`EVD-121`). No está preparado para publicación compartida ni se ha verificado seguridad de despliegue. La oferta CITMATEL no detalla en línea los requisitos anteriores. Hasta confirmar entorno y condiciones, esta ficha no autoriza el despliegue. `Q-026` conserva las comprobaciones pendientes.
