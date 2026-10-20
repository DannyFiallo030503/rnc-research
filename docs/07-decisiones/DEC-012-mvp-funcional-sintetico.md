# DEC-012 — Recorrido funcional del MVP con datos sintéticos

Fecha: 16-10-2026. Estado: aceptado por el responsable del proyecto para desarrollo local; no aprobado institucionalmente por RNC/CUJAE.

Trazabilidad: SRC-PRJ-002 → EVD-101; SRC-TECH-024 → EVD-102; REQ-F-001..015, REQ-D-003..005; DEC-011.

## Decisión

Implementar Inicio con estadísticas de una publicación persistente; un constructor que elige dimensión, indicador y un gráfico compatible; exportación PNG/SVG/PDF/CSV/XLSX; recepción técnica de CSV sintéticos, registro privado, revisión, publicación de un conjunto completo y revocación; usuarios con interfaz propia, roles extensibles, invitaciones, contraseña temporal con cambio obligatorio y recuperación.

La carga usa un contrato nuevo y explícitamente sintético de 10 columnas. No es el contrato RNC de 84 columnas ni un mapeo epidemiológico autorizado. Los campos categóricos almacenan IDs resueltos por catálogos con nombre, descripción, versión y estado; esos IDs son exclusivos del demo y no representan nomencladores oficiales. El archivo ya no lleva nombres de personas. Los identificadores sintéticos permanecen en archivos privados; las respuestas públicas contienen solo agregados. El generador inicial asigna un período de referencia a cada persona; el importador admite la misma identidad sintética en varios años y cuenta personas distintas en la selección completa. Las categorías de una distribución pueden solaparse y no se suman para obtener el total de personas.

### Ajuste del contrato del demo — 2026-10-19

Tras la revisión del esquema de entrada, el contrato pasa a guardar `territory_id`, `sex_id`, `age_group_id` y `site_id` en vez de etiquetas categóricas, y elimina el nombre ficticio. Cada categoría se presenta desde `analytics/catalogs.py`, con metadatos de nomenclador. `territory_id` usa los códigos provinciales del Manual RNC VII, Anexo 1; los IDs de sexo, edad y agrupaciones anatómicas siguen siendo claves sintéticas. El directorio de unidades informantes del Anexo 1 se conserva como transcripción versionada y señala las filas repetidas y discordantes. Sus códigos no se asignan automáticamente a `UNIDIDAD`/`PROVINFO`; falta cotejar ese mapeo con el diccionario autorizado y validar la vigencia RNC. Las agrupaciones anatómicas no sustituyen códigos CIE-O/ICCC-3. Ver el criterio incorporado a `docs/05-requisitos/esquema-archivo-recibido.md`.

#### Corrección de codificación — 2026-10-19

El responsable aclara que TOPO puede llegar con códigos como `509`, que identifica como mama bajo ICD-O-2, y que distintos centros pueden usar clasificadores/ediciones diferentes. El ejemplo se registra como aclaración pendiente de cotejo con el diccionario; no se transforma a otra representación ni se trata como regla RNC confirmada. La ingesta futura debe preservar literalmente cada código fuente y mantener sistema/edición; la web debe consultar conceptos de nomencladores con identificador, nombre, descripción y todos sus códigos relacionados, cada uno con sistema/versión. Topografía, morfología, estadio y otros campos son ejes separados. No se cuenta aún con el diccionario para codificar fielmente el demo como casos ICD-O. Por tanto, las categorías actuales continúan siendo solo grupos ilustrativos sintéticos y no son crosswalks ni nomencladores tumorales validados. Trazabilidad: `SRC-RNC-011` / `EVD-115`; clasificación oficial/cubana documentada en `Q-002`, con correspondencias abiertas.

Actualización de fuentes del 20-10-2026: IARC publicó las tablas finales ICD-O-4 el 20-07-2026 (`SRC-IARC-ICDO4-2026`, `EVD-134`); esto actualiza el panorama internacional y no cambia lo documentado por el Manual RNC VII (CIE-O-3/ICCC-3). Las tablas no se copian a `rnc-web` sin confirmar permiso para reproducción/traducción y qué ediciones utiliza el RNC (`EVD-135`, `Q-002`). La ayuda contextual debe poder consultarse con hover, foco y tacto y dejar visible la procedencia/edición. Los grupos sintéticos actuales conservan su rótulo y no se presentan como códigos oficiales.

Una publicación sustituye el conjunto completo anterior; no se suman entregas. La huella SHA-256 bloquea reenvíos idénticos. Una validación fallida no incorpora filas parcialmente y conserva informe técnico restringido. La revocación retira la versión activa, sin restaurar automáticamente otra ni poder retirar descargas previas.

Roles locales propuestos: operador (cargas), responsable de publicación (cargas/publicación/revocación), soporte superadmin (cuentas y todas las funciones), consulta pública. No son designaciones aprobadas por el RNC. La base de datos autoriza las operaciones; la navegación refleja esas capacidades.

## Seguridad y correo

Invitación y recuperación encolan mensajes; el worker genera enlaces Django con origen configurado, caducidad de una hora y validez que se pierde al cambiar la contraseña. El cambio autenticado exige contraseña actual. Las contraseñas temporales bloquean otras pantallas hasta sustituirse. No enviar contraseñas por correo. En desarrollo, los mensajes se guardan en buzón privado, no se envían a Gmail. El envío real requiere SMTP autorizado.

El límite de intentos usa caché local y no sustituye controles de proxy/caché compartida. La salida de producción requiere secreto explícito y cookies seguras. Quedan por validar TLS/proxy, auditoría resistente a manipulación, MFA para soporte, recuperación operativa, almacenamiento/retención, restauración y pruebas de seguridad institucionales.

## Alcance y aceptación

Se adelanta ingeniería local del producto. La implementación segura del panel y las identidades institucionales continúan en tesis según el Anexo A; no hay cambio académico validado. Validación clínica, método indirecto, política de celdas pequeñas y contrato real siguen pendientes.

Criterios del recorrido: una entrega válida puede revisarse y publicarse; Inicio y consulta usan exactamente esa versión; los formatos conservan filtros, unidad y procedencia; revocar elimina la disponibilidad pública; cuentas sin capacidad no realizan acciones administrativas; contraseña temporal obliga al cambio. No declarar estos criterios probados sin evidencia de ejecución.

Implementación: `rnc-web/public_site/{models,services,statistics,portal,accounts,forms,middleware}.py`, migraciones, comandos `seed_demo` y `deliver_account_mail`, plantillas propias y Chart.js local. Ver README de implementación y revisión visual local del 20-10-2026. La ampliación inicial no ejecutó la suite anterior; las revisiones posteriores solicitadas en SRC-PRJ-003 documentan la cobertura y sus límites.

## Revisión posterior de interfaz y contratos de entrada

SRC-PRJ-003 → EVD-103..104 → validación de REQ-F-009..015 / REQ-NF-001..005. Se retira el enlace lateral redundante a Inicio, se integran menú de cuenta y navegación adaptable y se unifican formularios con errores por campo, ayudas, `aria-describedby`, `aria-invalid`, resumen y conservación de datos no secretos. Las validaciones de navegador previenen caracteres/formato incompatibles según campo; el servidor repite controles. Las contraseñas admiten símbolos. La defensa frente a inyección conserva ORM parametrizado, escape de plantillas/JSON y una política CSP local; no se confunde ausencia de ciertos símbolos con seguridad.

Las pruebas se ejecutan en SQLite/archivos/cuentas/correo temporales. El tamaño móvil representa emulación en Chromium, no un dispositivo físico ni una auditoría con lectores de pantalla. El envío de correo se verifica mediante el buzón privado local y enlaces reales de Django; SMTP real sigue pendiente de configuración. La revisión completa actual queda en `rnc-web/docs/revision-completa-2026-10-20/`; no convertir sus resultados en una aprobación institucional ni en garantía de ausencia de vulnerabilidades.


### Evidencia de la revisión completa — 20-10-2026

Por solicitud SRC-PRJ-003, la revisión del 20-10-2026 aprobó 58 pruebas Django y 1333 comprobaciones en Chromium, con 182 capturas en PC (1440), laptop (1024) y móvil emulado (390). Se comprobaron formularios/errores del servidor, acceso del personal desde Inicio, marco común entre Inicio/Consulta/Administración con enlaces según capacidades, marco público aislado sin enlaces administrativos, sincronización de sesión entre pestañas, alineación de columnas en las tablas de Inicio, cortes, Consulta y usuarios, permisos, persistencia de archivos, correo local, publicación/revocación y ocho gráficos. La matriz adicional verificó cada gráfico con cada uno de los cinco formatos; comprobó filtros completos, metadatos, ejes y valores, y se corrigió visualmente el pie del PNG para separarlo del eje. [Informe reproducible y límites](../../../rnc-web/docs/revision-completa-2026-10-20/README.md). EVD-103..104 / DEC-012; evidencia local sintética, sin SMTP real, dispositivo físico, certificación de seguridad ni validación RNC. No modifica el alcance académico aprobado.
