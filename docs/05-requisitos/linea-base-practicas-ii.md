# Línea base de requisitos y entregables — Prácticas II

Estado: BASE DOCUMENTAL v3; pendiente de revisión con tutora y RNC  
Corte: 2026-10-06

## 1. Propósito y fuentes de autoridad

Esta línea base convierte el alcance temporal del Anexo A en capacidades, atributos y entregables rastreables. No reemplaza el Anexo ni cierra reglas que el RNC todavía debe precisar.

Orden para interpretar el alcance:

1. **Anexo A (`SRC-RNC-001`)**: delimita tareas, fechas y qué corresponde a Prácticas II frente a etapas posteriores. Ante dudas de calendario/etapa prevalece sobre la descripción general de la propuesta.
2. **Propuesta de Trabajo (`SRC-RNC-002`)**: fija el producto general y sus objetivos.
3. **Manual RNC v. VII (`SRC-RNC-003`)**: fija procedimientos y reglas documentadas del registro; no especifica por sí solo toda la interfaz ni la metodología matemática.
4. **Aclaraciones del estudiante (`SRC-RNC-004`)**: precisan el acceso público, el referente de diseño y el modo inicial de entrada de datos.
5. **Aclaración escrita de Yinet (`SRC-RNC-005`)**: precisa las bandas quinquenales clásicas, la creación de agrupaciones adicionales y la fuente/granularidad de población para denominadores.
6. **Aclaraciones del estudiante (`SRC-RNC-006`, `SRC-RNC-007`)**: precisan que el sistema interno entrega archivos ya depurados/definitivos y que el nuevo portal no corrige casos; la aclaración posterior distingue estándares internacionales de cáncer y denominadores cubanos ONEI. Las ideas de intervalos, privacidad y calidad web son propuestas.

La trazabilidad de preguntas pendientes está en [`mapa-de-preguntas.md`](mapa-de-preguntas.md); evidencia y estado de cada afirmación en [`../evidence-map.md`](../evidence-map.md).

## 2. Frontera de la primera versión

### Dentro de Prácticas II según el Anexo A

- Analizar plataformas de registros de cáncer, sus diseños y visualizaciones.
- Estudiar tasas crudas, específicas, ajustes directo e indirecto e intervalos Poisson y normal.
- Comparar frameworks/librerías estadísticas y de visualización; estudiar UX/UI, WCAG y herramientas de visualización.
- Identificar requisitos funcionales/no funcionales; diseñar modelo de datos, artefactos de ingeniería y seleccionar tecnologías.
- Crear y validar prototipos de alta fidelidad para consulta y panel de administración.
- Implementar el motor de tasas e intervalos, consultas con filtros, frecuencias absolutas/relativas y exportación CSV, Excel y PDF.
- Producto público; carga inicial desde archivos Excel/CSV producidos por el sistema interno RNC y suministrados manualmente. Según `SRC-RNC-006`, esos archivos ya vienen depurados y definitivos.
- El sitio consultará únicamente los archivos definitivos recibidos. No incorpora corrección de casos, deduplicación ni declaración epidemiológica de estado; el Anuario 2024 contiene otra serie de cáncer 2022 etiquetada preliminar y no debe confundirse con el archivo que se entregará.
- Las tablas clásicas conservan grupos quinquenales fijos de 0–4 a 85+; además, se podrán crear agrupaciones nuevas a partir de edades seleccionadas, sin modificar las bandas clásicas (`SRC-RNC-005`). Las reglas de creación y uso siguen pendientes (`Q-003`).
- La población denominadora será la oficial publicada por ONEI, disponible según Yinet para Cuba, provincia y municipio, por sexo y edad simple; el RNC entregará las series (`SRC-RNC-005`).
- Para ajuste directo por edad se adopta como referencia de trabajo la estándar mundial Segi/Doll de IARC/CI5, coherente con Manual VII y AES 2024; la población ONEI cubana es el denominador de las tasas específicas. Comprobar la reproducción exacta de una tasa RNC con un ejemplo oficial (`SRC-RNC-007`, `SRC-IARC-CI5-WORLD-2026`).
- El prototipo administrativo representa a trabajadores del RNC que incorporan y consultan el estado técnico de archivos ya definitivos; los perfiles indicados son doctor encargado y personal de mantenimiento del sistema, sin permisos específicos confirmados (`SRC-RNC-004`, `SRC-RNC-006`). La implementación segura de ese panel sigue fuera de Prácticas II según el Anexo.

### Posterior a Prácticas II según el Anexo A

Entre las actividades posteriores están dashboards avanzados, mapas coropléticos, series temporales, implementación del panel administrativo seguro, autenticación/roles, auditoría, actualización desde el panel, migración histórica y pruebas finales de usabilidad, rendimiento y seguridad. El prototipo del panel sí pertenece al diseño de Prácticas II; su implementación completa no se adelanta por ello.

### Fuera de la primera versión por aclaración del proyecto

La conexión directa a una base de datos se estudiará en una etapa futura; no es requisito de la carga inicial.

## 3. Requisitos funcionales

Los requisitos marcados `ANEXO` se derivan directamente de tareas del Anexo A; los marcados `PROYECTO` provienen de la aclaración del estudiante; los marcados `DERIVADO` expresan una interpretación necesaria para hacer verificable el objetivo y deben revisarse con la tutora/RNC.

| ID | Requisito | Fuente / estado | Criterio de aceptación inicial | Detalle por cerrar |
|---|---|---|---|---|
| REQ-F-001 | Permitir consulta estadística desde una web de acceso público, dirigida a cualquier persona. | `SRC-RNC-002`, `SRC-RNC-004` — CONFIRMADO | Una persona sin cuenta puede acceder al módulo público y realizar una consulta. | Priorizar tareas y preguntas de uso por perfil (`Q-014`). |
| REQ-F-002 | Permitir filtrar consultas por año, provincia, sexo, grupo de edad y localización del cáncer; ofrecer bandas clásicas y agrupaciones nuevas. | `SRC-RNC-001`, `SRC-RNC-002`, `SRC-RNC-005` — ANEXO + ACLARACIÓN | El usuario puede consultar con grupos quinquenales clásicos 0–4 a 85+ y definir otra agrupación sin alterar los clásicos. | Cómo se seleccionan edades y dónde se permite usar/guardar una agrupación nueva (`Q-003`); demás catálogos/versiones y combinaciones válidas. |
| REQ-F-003 | Generar frecuencias absolutas y relativas para la consulta. | `SRC-RNC-001`, `SRC-RNC-002` — ANEXO | El resultado muestra conteos y porcentajes con el universo/base del porcentaje visible. | Propuesta: casos de la categoría sobre total de casos seleccionados; confirmar desconocidos, grupos solapados y redondeo (`Q-018`). No confundir porcentaje con tasa poblacional. |
| REQ-F-004 | Calcular tasas crudas de incidencia. | `SRC-RNC-001`, `SRC-RNC-002`, `SRC-RNC-005` — ANEXO + FUENTE DE POBLACIÓN ACLARADA | Se calcula una tasa a partir de casos y población ONEI compatibles y se presenta el resultado. | Unidad/escala, redondeo, archivos, edición y regla temporal de las series ONEI (`Q-016`); especificar y citar la fórmula en ENT-02. |
| REQ-F-005 | Calcular tasas específicas por edad para las bandas clásicas y, cuando se aprueben las reglas, las agrupaciones nuevas. | `SRC-RNC-001`, `SRC-RNC-002`, `SRC-RNC-005` — ANEXO + ACLARACIÓN | La tasa de cada grupo usa casos y población ONEI de los mismos estratos de año, territorio, sexo y edad; el grupo clásico final es 85+. | Reglas de agrupación nueva, edición y temporalidad de series ONEI, correspondencia con población estándar y tratamiento de faltantes (`Q-003`, `Q-016`). |
| REQ-F-006 | Calcular tasas ajustadas por edad mediante método directo. | `SRC-RNC-001`, `SRC-RNC-002`, `SRC-RNC-007`, `SRC-IARC-CI5-WORLD-2026` — ANEXO + REFERENCIA INTERNACIONAL | El motor usa tasas específicas cubanas y pesos de la estándar mundial Segi/Doll para los grupos compatibles; declara ASR(W), fuente y versión. | Contrastar un ejemplo publicado por RNC y cerrar redondeo, faltantes y agrupaciones nuevas (`Q-003` a `Q-005`). No convertir la población ONEI en pesos estándar. |
| REQ-F-007 | Calcular tasas ajustadas por edad mediante método indirecto. | `SRC-RNC-001`, `SRC-RNC-002` — ANEXO | Se implementa el indicador indirecto definido y se valida contra un ejemplo aprobado. | Método, población de referencia, indicador e incertidumbre (`Q-006`). |
| REQ-F-008 | Calcular intervalos de confianza con métodos Poisson y aproximación normal, según corresponda. | `SRC-RNC-001`, `SRC-RNC-002` — ANEXO; `SRC-RNC-006` indica que es propuesta nueva, no salida actual RNC | El motor puede producir el intervalo documentado para el indicador aplicable y explicar su método. | Nivel, criterio Poisson/normal, ceros, tasas ajustadas y ejemplo numérico de referencia (`Q-009`); no atribuir metodología al RNC. |
| REQ-F-009 | Exportar datos/resultados de consulta en CSV, Excel y PDF. | `SRC-RNC-001`, `SRC-RNC-002` — ANEXO | Hay una salida en cada formato para un resultado consultado. | Contenido exacto, metadatos, diseño PDF y reproducción de filtros. |
| REQ-F-010 | Incorporar archivos Excel/CSV definitivos producidos por el sistema interno del RNC. | `SRC-RNC-004`, `SRC-RNC-006` — DIRECCIÓN DE PRODUCTO | Una carga con esquema y metadatos compatibles registra procedencia, huella, grano y capacidades y queda disponible para las consultas posibles sin modificar conteos ni casos; una carga incompatible se rechaza con errores técnicos. La falta de ONEI deja tasas dependientes indisponibles, sin invalidar automáticamente conteos. | Estructura CSV de 84 columnas estable confirmada por Danny (`esquema-archivo-recibido.md`); diccionario, grano, cobertura, identificador de corte, responsable de entrega, manejo de errores y conservación del original según política RNC (`Q-017`). No hay acceso directo a BD. |
| REQ-F-011 | Consultar y exportar únicamente datos de los archivos definitivos entregados; no editar el contenido epidemiológico en el portal. | `SRC-RNC-004`, `SRC-RNC-006` — REGLA DE PRODUCTO | Cada resultado identifica el archivo/corte definitivo y su procedencia; el portal no ofrece corrección, deduplicación ni aprobación clínica de registros. | Definir identificador, fechas y política excepcional ante archivo técnicamente errado sin asumir corrección de casos (`Q-008`, `Q-017`). La autorización de desgloses públicos se trata aparte (`Q-007`). |
| REQ-F-012 | Prototipar la incorporación y gestión técnica de archivos definitivos para trabajadores del RNC. | `SRC-RNC-001`, `SRC-RNC-002`, `SRC-RNC-006` — PROTOTIPO EN ALCANCE | El prototipo permite seleccionar archivo, ver metadatos, comprobar formato/integridad, observar resultado de importación y consultar cortes disponibles. | Responsables/permisos y contrato real de archivo; no modelar en este portal corrección de casos, deduplicación ni aprobación epidemiológica. La implementación segura del panel es posterior. |
| REQ-F-013 | Permitir crear agrupaciones de edad adicionales preservando las bandas quinquenales clásicas de 0–4 a 85+. | `SRC-RNC-005`, `SRC-RNC-004` — DIRECCIÓN FUNCIONAL ACLARADA | La selección de edades puede formar una agrupación nueva sin cambiar las tablas clásicas; el diseño contempla grupos abiertos y evita imponer un tope máximo general. | Quién crea/guarda/aprueba agrupaciones, unidad y precisión, cobertura/solapamiento, vigencia y uso en tasas ajustadas (`Q-003`, `Q-004`). |

## 4. Requisitos de datos, calidad y protección

| ID | Requisito / restricción | Fuente / estado | Criterio inicial | Pendiente |
|---|---|---|---|---|
| REQ-D-001 | El modelo de datos debe representar casos y edades, bandas clásicas y agrupaciones adicionales, población denominadora ONEI, estándar mundial y dimensiones de consulta: año, territorio, sexo y localización. | `SRC-RNC-001`, `SRC-RNC-002`, `SRC-RNC-005`, `SRC-RNC-007`, `SRC-IARC-CI5-WORLD-2026` — ANEXO + ACLARACIÓN | Conserva las bandas quinquenales clásicas de 0–4 a 85+, admite grupos nuevos, distingue las series cubanas ONEI por edad simple de los 18 pesos mundiales y registra la fuente de cada una. | Grano del dato, unidad/precisión etaria, versiones de grupos, archivo/edición/temporalidad ONEI y compatibilidad de agrupaciones nuevas con los pesos mundiales (`Q-003`, `Q-004`, `Q-016`). |
| REQ-D-002 | Documentar el grano de cada archivo de entrada y cómo representa casos/tumores para el conteo; preservar la distinción de múltiples primarios cuando los datos de entrada la contengan y excluir identificadores de las salidas públicas. | `SRC-RNC-003`, `SRC-RNC-004` — RESTRICCIÓN DOCUMENTAL + DERIVADO | El modelo declara si recibe datos agregados o por caso, cuál unidad se cuenta y cómo se construye la salida pública sin identificadores. | La estructura observada tiene 84 columnas estables (`esquema-archivo-recibido.md`); el diccionario y el grano/unidad por fila siguen pendientes. |
| REQ-D-003 | Verificar el contrato técnico de cada archivo definitivo al incorporarlo, sin alterar sus casos o conteos. | `SRC-RNC-006` — DIRECCIÓN DE PRODUCTO + DERIVADO | Incompatibilidad de esquema, tipos, año, territorio, cobertura o integridad produce un informe técnico y evita publicar cifras incorrectas. | La muestra y la estructura estable están disponibles; faltan semántica/tipos de campos, reglas de suma/control, tratamiento de reenvío del mismo archivo y coordinación con series ONEI (`Q-017`). La deduplicación clínica corresponde al sistema interno. |
| REQ-D-004 | Mantener por resultado la procedencia del corte RNC, edición/tipo ONEI, definición del indicador, estándar aplicable, filtros y versión de la política de divulgación. | `DEC-009`, `SRC-RNC-006`, `SRC-RNC-007` — DERIVADO PARA REPRODUCIBILIDAD | Pantalla y exportación autorizada identifican las fuentes y versiones que produjeron una cifra; una revisión futura no cambia silenciosamente la interpretación de cifras anteriores. | Campos exactos del archivo y política; forma pública de mostrar metadatos. |
| REQ-NF-001 | Evitar publicación de datos personales identificables y evaluar riesgo de inferencia en resultados agregados combinables. | Manual RNC; Ley 149/2022; Resolución 58/2022 — RESTRICCIÓN LEGAL Y PROPUESTA DE CONTROL | La vista y exportaciones solo exponen agregados permitidos; las combinaciones de filtros se prueban para reidentificación/diferenciación. | Política institucional de supresión, agregación o límite de consulta (`Q-007`); no imponer umbral CDC como regla cubana. |
| REQ-NF-002 | Proponer interfaz responsiva y accesible para web pública. | `SRC-RNC-001`, `SRC-RNC-004`, `SRC-RNC-006`, `SRC-WCAG-001` — DIRECCIÓN + PROPUESTA | Evaluar WCAG 2.2 AA, teclado, contraste, tablas accesibles y tareas en móvil/escritorio con usuarios previstos. | La entidad no fijó nivel; concretar matriz de dispositivos, tareas y pruebas (`Q-014`, `Q-015`). |
| REQ-NF-003 | Estudiar fundamentos de seguridad informática para sistemas de salud. | `SRC-RNC-001`, `SRC-RNC-002` — ENTREGABLE DE ESTUDIO | El informe compara riesgos/controles aplicables y los vincula al tratamiento confidencial de datos. | Controles concretos del producto; implementación del panel seguro está en etapa posterior. |
| REQ-NF-004 | Priorizar la corrección, trazabilidad y reproducibilidad de las estadísticas; mantener la web ligera para conexiones lentas. La rapidez es secundaria y no debe afectar los resultados. | `SRC-RNC-004` — PRIORIDAD DEL PROYECTO | Las salidas se contrastan con casos de referencia aprobados; interfaz y recursos se diseñan para limitar transferencias y seguir utilizables con conectividad lenta. | Casos de referencia, tolerancias numéricas y perfil de conectividad/volumen para evaluar carga y respuesta (`Q-019`). |
| REQ-NF-005 | La presentación visual debe ser cuidada, clara y atractiva para un público amplio. | `SRC-RNC-004` — OBJETIVO DE DISEÑO | Los prototipos se revisan con usuarios previstos y se documentan problemas y cambios de diseño. | Criterios de evaluación visual/usabilidad y tareas por perfil (`Q-014`, `Q-020`). |
| REQ-NF-006 | Mantener separadas las reglas de consulta/cálculo de los formatos de entrada, almacenamiento y política de divulgación para absorber cambios previsibles. | `DEC-009` — PROPUESTA DE DISEÑO | `CD-01`, `CD-03`, `CMP-01`, `SD-01` y `SD-02` muestran contratos de fuente, cortes, población, métodos y divulgación; sustituir el adaptador de entrada no exige cambiar las operaciones de consulta ni fórmulas. | Verificar el límite real con el contrato de archivo; un cambio de grano/capacidades puede requerir cambios funcionales y no se promete compatibilidad absoluta. |

## 5. Entregables de ingeniería y validación

Estos son resultados académicos del Anexo, no funciones de usuario. Cada entregable debe enlazar con los requisitos que analiza o representa.

| ID | Entregable | Trazabilidad |
|---|---|---|
| ENT-01 | Benchmark de plataformas, librerías/frameworks de cálculo/visualización y herramientas interactivas; justificar patrones exitosos y fallos a evitar. | REQ-F-001..009; `SRC-RNC-001`; fichas en `docs/02-benchmark/` |
| ENT-02 | Fundamentos de tasas crudas, específicas, ajustes directo/indirecto e intervalos Poisson/normal; comparar tecnologías para cálculo y visualización. | REQ-F-003..008; reglas pendientes Q-003..006, Q-009, Q-016 |
| ENT-03 | Requisitos funcionales/no funcionales y modelo de datos. | REQ-F-001..013; REQ-D-001..004; REQ-NF-001..006 |
| ENT-04 | Comparación relacional vs NoSQL y selección justificada de frontend, backend, motor de cálculo y base de datos. | REQ-F-001..013; REQ-D-001..004; entrada inicial por archivo; BD fuente futura fuera de alcance inicial |
| ENT-05 | Diagramas de clases, actividades, arquitectura, secuencia y modelo entidad-relación. | Trazar cada diagrama a requisitos y marcar supuestos abiertos. |
| ENT-06 | Wireframes/prototipos de alta fidelidad para consulta pública e incorporación técnica de archivos definitivos; evaluación y refinamiento con usuarios. | REQ-F-001..013; REQ-D-003..004; REQ-NF-001..006; el panel seguro es prototipo en esta fase. |
| ENT-07 | Informe de Prácticas II, presentación y defensa según el calendario del Anexo A. | Alcance íntegro del Anexo A. |

## 6. Decisiones que esta línea base permite iniciar

- Iniciar casos de uso separados para consulta pública y flujo administrativo del prototipo.
- Dibujar el flujo de frontera: sistema interno RNC entrega archivo definitivo → portal verifica esquema/integridad y metadatos → archivo compatible queda disponible para cálculo/consulta → se aplica política de divulgación a resultados públicos. El mecanismo exacto de carga y los responsables quedan pendientes.
- Crear modelo conceptual y diagramas de contexto/componentes con la carga por archivos como entrada inicial y un punto de extensión para BD futura.
- Prototipar filtros/resultados/exportación comparando GCO, SEER y otros referentes, y justificar también patrones que se descarten.
- Construir matriz tecnológica para la aplicación pública y carga Excel/CSV; no seleccionar un conector a BD fuente como necesidad inicial.

## 7. Pendientes que bloquean detalle, no el inicio del diseño

- La estándar mundial y sus pesos están identificados en IARC/CI5; obtener un ejemplo RNC para validar cálculo y redondeo (`Q-004`, `Q-005`). Obtener aparte las series cubanas ONEI por edición, tipo de población, sexo, edad y territorio (`Q-016`).
- Intervalos propuestos y método indirecto: requieren método, nivel y ejemplos aprobados para implementar/validar indicadores, no para dibujar la estructura general.
- La estructura de 84 columnas del CSV ya está disponible y su estabilidad fue confirmada; el diccionario/semántica de columnas, grano de fila e integridad esperada bloquean cerrar el mapeo de campos y las validaciones estadísticas del importador. La detección de duplicados de casos ya ocurre en el sistema interno y queda fuera del portal.
- Política de publicación de conteos pequeños: sigue pendiente; el proyecto confirma publicar solo cortes definitivos, no que se deban suprimir o mostrar todos los conteos pequeños.
- Proponer tareas por perfil, WCAG 2.2 AA y pruebas de responsividad/rendimiento/usabilidad; medirlos y validarlos con usuarios, pues el RNC no detalló esos criterios.
- Sistema/motor de BD RNC: se investiga para una etapa futura; no bloquea la tecnología de entrada por archivos de la primera versión.

## 8. Trazabilidad inversa del Anexo A

Las tareas de análisis comparativo, fundamentos estadísticos, UX/UI/WCAG, visualización, requisitos, modelo de datos, seguridad, bases de datos, artefactos, selección tecnológica, prototipos/validación, motor de tasas e intervalos, consultas/filtros, frecuencias, exportación e informe/defensa quedan cubiertas en ENT-01..07 y REQ-F-001..013 / REQ-D-001..004 / REQ-NF-001..006.

Las tareas listadas por el Anexo después de la defensa de Prácticas II —administración segura implementada, roles/auditoría, mapas, series temporales, migración y pruebas finales— permanecen fuera de esta línea base inicial.
