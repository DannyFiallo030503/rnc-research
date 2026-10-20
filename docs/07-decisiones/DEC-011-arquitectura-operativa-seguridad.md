# DEC-011 — Preparar arquitectura operativa, acceso administrativo y recuperación

**Estado:** DIRECCIÓN DE PRODUCTO + PROPUESTA DE ARQUITECTURA; detalle institucional pendiente
**Fecha:** 2026-10-15
**Trazabilidad:** `SRC-PRJ-001`, `EVD-099..100`, `REQ-F-014..015`, `REQ-D-005`, `REQ-NF-007`, `Q-022..024`.

## Decisión

La solución objetivo se diseña como un monolito modular en un monorepo, con rutas públicas y administrativas separadas. La administración usa cuentas individuales y autorización extensible por permisos/grupos; el rol de soporte `superadmin` es obligatorio en el producto objetivo. No habrá auto-registro administrativo. Se comprobará autorización en el backend en cada operación protegida.

La base relacional propuesta registra usuarios/permisos, cortes y versiones, metadatos de importación/procedencia, estados de revisión/publicación, catálogo y auditoría. Los archivos originales se conservan fuera del webroot en almacenamiento privado; la base guarda un identificador opaco y huella, no una ruta pública. La zona pública solo consulta agregados autorizados.

El diseño documenta desde Prácticas II cómo desplegar en infraestructura institucional y cómo respaldar/restaurar conjuntamente base y archivos. Las credenciales y copias se custodian separadas del repositorio y de la cuenta normal de aplicación. El caché se reserva a agregados públicos versionados y se invalida al publicar, versionar o revocar.

## Motivo y límites

El responsable del proyecto solicita anticipar login, roles, separación de carpetas backend/frontend dentro del monorepo, despliegue, registro de archivos, almacenamiento y respaldos (`SRC-PRJ-001`). La documentación oficial consultada muestra que Django ofrece cuentas/grupos/permisos y controles que deben completarse al desplegar; Django advierte sobre HTTPS, cargas y límites al nivel del servidor (`SRC-TECH-001`). PostgreSQL documenta distintos modos de respaldo y recuperación, con requisitos que deben operar y ensayarse (`SRC-TECH-023`).

La decisión no aprueba una topología concreta ni despliegue institucional. PostgreSQL y Django siguen candidatos/recomendaciones provisionales (`DEC-010`). RNC/CUJAE deben validar proveedor de identidad, matriz de roles ordinarios, MFA y recuperación, segregación de publicación, hardware/red, ubicación y retención de archivos, objetivos RPO/RTO y responsables de operación. `superadmin` se requiere como rol de soporte según dirección del producto, pero su atribución de cuentas y controles de uso deben acordarse.

No implementa el panel seguro productivo ni carga de datos sensibles. Como preparación se añadió login local y gate de `superadmin` en Django; eso no integra identidad institucional ni constituye un despliegue validado. En la práctica se documentan requisitos, diagramas, estructura objetivo, matriz de acceso y flujo; el prototipo usa datos sintéticos.

## Consecuencias de diseño

- Organizar backend y presentación frontend por responsabilidades; no implica desplegarlos como servicios separados.
- Mantener cuenta y permisos centrales, con grupos/roles agregables sin editar controles en plantillas.
- Mantener un registro de importaciones distinto del almacenamiento binario; preservar procedencia, versión, huella, actor, estado y motivo.
- Proteger archivos fuente contra exposición web y restringir lectura a la tarea autorizada.
- Crear una política de respaldo coherente entre BD y archivo persistente, con restauraciones practicadas y RPO/RTO validados.
- Evitar cachear pantallas administrativas o contenido restringido; versionar e invalidar agregados públicos autorizados.

## Fuentes técnicas primarias

- [Django authentication system](https://docs.djangoproject.com/en/6.1/topics/auth/default/)
- [Django security](https://docs.djangoproject.com/en/6.1/topics/security/) y [deployment checklist](https://docs.djangoproject.com/es/6.1/howto/deployment/checklist/)
- [Django cache framework](https://docs.djangoproject.com/en/6.1/topics/cache/)
- [PostgreSQL backup and restore](https://www.postgresql.org/docs/current/backup.html) y [continuous archiving/PITR](https://www.postgresql.org/docs/current/continuous-archiving.html)
