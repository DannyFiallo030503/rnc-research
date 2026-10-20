# Registro de decisiones

| ID | Decisión | Estado | Fecha | Evidencia / fuentes |
|---|---|---|---|---|
| DEC-001 | El Anexo A se utiliza como referencia principal para el alcance temporal de Prácticas II frente a tesis. | CONFIRMADO | 2026-09-09 | SRC-RNC-001 |
| DEC-002 | Reservado: identificador usado en versiones iniciales para «no cerrar tecnologías»; ficha vigente `DEC-003`. | HISTÓRICO / ALIAS | 2026-09-09 | SRC-RNC-001, SRC-RNC-002 |
| DEC-003 | Comparar alternativas antes de fijar frontend, backend, motor estadístico o base de datos. | CUMPLIDA COMO ANÁLISIS; SELECCIÓN TÉCNICA PROVISIONAL | 2026-10-13 | [Ficha](DEC-003-no-cerrar-stack.md), [comparación](../06-arquitectura/seleccion-tecnologica.md), SRC-RNC-001, SRC-RNC-002, SRC-TECH-001..014 |
| DEC-004 | Mantener trazabilidad entre fuentes, evidencias, propuestas y requisitos. | PROPUESTA | 2026-09-09 | [Ficha](DEC-004-evidencia.md) |
| DEC-005 | La primera versión obtiene los datos mediante carga manual de archivos Excel/CSV; la conexión directa a BD se difiere a una etapa posterior. | CONFIRMADO COMO DIRECCIÓN DEL PROYECTO | 2026-09-30 | SRC-RNC-004 |
| DEC-006 | El portal recibe archivos que el sistema interno del RNC ya depuró y declaró definitivos; solo hace comprobaciones técnicas y no modifica casos. | CONFIRMADO COMO DIRECCIÓN DEL PROYECTO | 2026-10-06 | SRC-RNC-006; REQ-F-010..012 |
| DEC-007 | La publicación de agregados requiere una política institucional de divulgación, incluso si el archivo fuente es definitivo. | PROPUESTA PENDIENTE DE VALIDACIÓN | 2026-10-06 | SRC-CUBA-LEY149-2022, SRC-CUBA-RES58-2022; Q-007 |
| DEC-008 | Usar como referencia de trabajo para ASR(W) la estándar mundial Segi/Doll documentada por IARC/CI5; emplear población cubana ONEI como denominador y verificar una tasa RNC. La frase anterior sobre «estándar cubana» queda aclarada. | DIRECCIÓN METODOLÓGICA; COTEJO NUMÉRICO PENDIENTE | 2026-10-06 | SRC-RNC-007, SRC-RNC-003, SRC-CUBA-AES-2024, SRC-IARC-CI5-WORLD-2026; Q-004 |
| DEC-009 | Proponer un monolito modular con contratos para fuente definitiva, cortes, población ONEI, métodos y divulgación; adoptar archivo Excel/CSV como primer adaptador. Mantener un resultado interno separado del resultado público autorizado. | PROPUESTA DE DISEÑO | 2026-10-06 | [Arquitectura evolutiva](../06-arquitectura/arquitectura-evolutiva-rnc.md); SRC-ARCH-HEX-2005; REQ-F-010..012, REQ-NF-001 |
| DEC-010 | Recomendar provisionalmente Python/Django con capa visual HTML/CSS distintiva, pandas para exploración, ECharts como primera candidata de visualización y PostgreSQL como candidato de persistencia productiva; comparar estilos y ECharts/Plotly en prototipo, condicionar la base a infraestructura institucional. | RECOMENDACIÓN TÉCNICA PROVISIONAL; NO APROBADA | 2026-10-13 | [Comparación tecnológica](../06-arquitectura/seleccion-tecnologica.md); EVD-070..074; SRC-TECH-001..017; Q-014, Q-019 |
| DEC-011 | Preparar como objetivo un monolito modular con autenticación administrativa individual, autorización extensible por permisos/roles y rol `superadmin`; persistir usuarios, cortes/versiones, procedencia y auditoría; guardar originales en almacenamiento privado, con despliegue institucional y respaldos restaurables de base y archivos. La solución pública solo sirve agregados autorizados. | DIRECCIÓN DE PRODUCTO + PROPUESTA DE ARQUITECTURA; DETALLE INSTITUCIONAL PENDIENTE | 2026-10-15 | [Ficha](DEC-011-arquitectura-operativa-seguridad.md); `SRC-PRJ-001`, `EVD-099..100`; [arquitectura evolutiva](../06-arquitectura/arquitectura-evolutiva-rnc.md); [arquitectura operativa](../../../rnc-web/docs/ARQUITECTURA-OBJETIVO-OPERACION.md); `REQ-F-014..015`, `REQ-D-005`, `REQ-NF-007`; `Q-022..024` |

## DEC-012 — MVP funcional con datos sintéticos (16-10-2026)

[Decisión y límites](DEC-012-mvp-funcional-sintetico.md). Dirección del responsable: SRC-PRJ-002 / EVD-101..102. Adelanto local del producto, sin modificar el Anexo A ni autorizar microdatos reales.

## DEC-013 — PWA exclusivamente pública y consulta offline (19-10-2026)

[Decisión y límites](DEC-013-pwa-solo-publica.md). Dirección de producto documentada: SRC-RNC-012 / EVD-116..117. Administración online, paquete offline solo con agregados aprobados; implementación y alcance pendientes.

## DEC-014 — Ruta de exploración para demo web provisional (19-10-2026)

[Criterio provisional](DEC-014-demo-web-provisional.md). Solicitud: `SRC-PRJ-004`; evidencia `EVD-118..121`. Consultar primero un entorno de ensayo CUJAE/RNC y, si no existe, compatibilidad/condiciones de CITMATEL. No se elige proveedor ni se despliega aún. Limitar un eventual demo a datos sintéticos y vista pública; Q-026 permanece abierta.

## DEC-015 — Separación de datos sensibles y consulta pública (20-10-2026)

[Propuesta, prototipo y límites](DEC-015-separacion-publicacion-publica-privada.md). `SRC-PRJ-005`, `SRC-PRJ-007`; `EVD-125..128`, `EVD-132`. Prototipo local sintético con artefacto agregado versionado y perfiles de ejecución público/administrativo separados. No es configuración productiva ni política de divulgación aprobada; Q-007 y Q-027 abiertas.

## DEC-016 — Descargas públicas, auditoría y logs (20-10-2026)

[Criterio provisional](DEC-016-registro-uso-y-auditoria.md). Consulta `SRC-PRJ-006`; evidencia `EVD-129..131`. Mantener consultas/descargas públicas sin cuenta y no añadir historial individual ni métricas persistentes mientras se define su finalidad. El explorador web aplica `no-store` y `no-referrer`; logs de infraestructura siguen pendientes de configuración. Completar y proteger la auditoría administrativa según política institucional. Q-028 abierta.
