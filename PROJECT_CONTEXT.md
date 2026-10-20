# Contexto vivo del proyecto RNC

Estado: ACTIVO
Corte: 2026-10-13
Rama de trabajo: `master`
Remoto: `origin` → `https://github.com/DannyFiallo030503/rnc-research.git`

## Propósito

Este repositorio contiene el conocimiento, la evidencia, las preguntas y las decisiones que sustentan el desarrollo de la plataforma web interactiva del Registro Nacional de Cáncer (RNC) de Cuba para Prácticas II y el Trabajo de Diploma.

No es un repositorio de código de la plataforma. Es el repositorio de conocimiento que permite pasar de evidencia a requisitos, diseño, implementación y pruebas sin perder trazabilidad.

El código de la plataforma se mantiene aparte en `../rnc-web/`, cuyo esqueleto de prototipo comenzó el 2026-10-13 con Django; consulta el README de ese repositorio y mantén como provisionales las decisiones tecnológicas aún no validadas.

## Situación académica

La revisión integral de archivos y referencias del 2026-10-04 está documentada en `docs/00-auditoria-documental-2026-10-04.md`. Los borradores Markdown fuera de este repositorio se conservan como antecedentes; para continuar usar la base viva y el catálogo.

La última documentación del proyecto mantiene pendiente la primera reunión formal con el RNC. El 2026-09-30 se revisó íntegramente el texto convertido del Manual de Procedimientos versión VII (2024); el 2026-10-13 se volvió a cotejar el PDF página por página y se inspeccionaron visualmente los formularios anexos que no se extraen en Markdown. El 2026-09-30 Yinet respondió por escrito sobre grupos de edad y población (`SRC-RNC-005`); esto no equivale a celebrar la reunión formal.

En esta etapa no se deben inventar reglas del RNC ni cerrar tecnologías por intuición. El trabajo actual es:

1. estudiar el dominio de los registros poblacionales de cáncer;
2. estudiar cómo publica y analiza datos el RNC de Cuba;
3. estudiar sistemas internacionales existentes;
4. estudiar literatura científica y tesis relacionadas;
5. identificar patrones exitosos y fallos documentados;
6. transformar los hallazgos en preguntas y propuestas verificables para la primera reunión.

## Alcance conocido de Prácticas II

El Anexo A establece para la práctica:

- análisis comparativo de plataformas de registros de cáncer;
- fundamentos de tasas crudas, específicas y ajustadas por métodos directo e indirecto;
- intervalos de confianza por Poisson y aproximación normal;
- comparación de librerías y frameworks de cálculo/visualización;
- UX/UI y accesibilidad WCAG;
- comparación de herramientas de visualización interactiva;
- requisitos funcionales y no funcionales;
- modelo de datos;
- fundamentos de seguridad;
- comparación de bases de datos relacionales y NoSQL;
- artefactos de ingeniería;
- selección tecnológica;
- wireframes y prototipos de alta fidelidad;
- validación de prototipos con usuarios;
- implementación del motor de tasas;
- implementación de intervalos;
- consulta interactiva con filtros;
- frecuencias absolutas y relativas;
- exportación CSV, Excel y PDF.

Fuente del alcance: `SRC-RNC-001` y `SRC-RNC-002`.

La línea base de requisitos y entregables trazable al Anexo A está en `docs/05-requisitos/linea-base-practicas-ii.md`. Consultarla antes de ampliar alcance, redactar requisitos o crear diagramas.

La propuesta de diseño evolutivo está en `docs/06-arquitectura/arquitectura-evolutiva-rnc.md` (`DEC-009`): monolito modular con puertos para entrada de cortes definitivos, lectura de conteos, población ONEI, métodos y divulgación; Excel/CSV es el primer adaptador y una integración futura puede reemplazarlo sin modificar el núcleo de consulta. Distinguir `ResultadoInterno` de `ResultadoConsulta` autorizado, conservar procedencia/versiones y no desagregar más allá del grano recibido. `CMP-01`, `CD-01`, `SD-01`, `ACT-01` y `ACT-02` deben representar esas fronteras.

La comparación tecnológica inicial está en `docs/06-arquitectura/seleccion-tecnologica.md` y `DEC-010`: recomienda provisionalmente Python/Django, HTML progresivo con una capa visual propia, pandas para exploración tabular, comparar ECharts con Plotly.js y considerar PostgreSQL para producción. Django no limita la apariencia; CSS propio, Bootstrap personalizado y Tailwind quedan para comparar en prototipo. No es selección aprobada ni cierra despliegue; faltan infraestructura, experiencia del equipo, diccionario/grano, evaluación de visualización con conexión limitada y métodos aprobados.

## Alcance posterior identificado

El Anexo reserva para la etapa posterior, principalmente tesis y Gestión de Proyectos, elementos como dashboards avanzados, mapas coropléticos, series temporales, administración segura completa, roles, auditoría, migración histórica, pruebas finales de rendimiento y seguridad, métricas finales de accesibilidad/usabilidad y capacitación.

No se debe adelantar ese alcance como requisito de Prácticas II salvo que el tutor o el RNC lo solicite explícitamente.

## Dirección de producto aclarada por el estudiante (2026-09-30)

- El producto es una web de acceso público; la consulta pública no requiere identificar a cada visitante. Esto no hace públicos los microdatos: el Manual RNC mantiene la confidencialidad de casos individuales y exige entregas anónimas/disociadas (`SRC-RNC-003`, `SRC-RNC-004`).
- La audiencia se considera abierta a cualquier persona; la Propuesta de Trabajo nombra comunidad médica, académica y público general. Aún se deben priorizar preguntas y tareas por perfil (`Q-014`).
- Yinet confirmó bandas quinquenales fijas de 0–4 a 85+ para las tablas clásicas. La plataforma también debe permitir crear otras agrupaciones a partir de edades seleccionadas, sin reacomodar las bandas clásicas (`SRC-RNC-005`). Siguen pendientes el mecanismo de selección, administración, unidad/precisión y aplicación a los cálculos (`Q-003`).
- Los denominadores utilizarán población oficial publicada por ONEI, desglosada para Cuba, provincia y municipio, por sexo y edad simple. El RNC entregará los datos; faltan archivos, años/edición, formato y regla temporal (`SRC-RNC-005`, `Q-016`). Esto es distinto de la población estándar para ajuste por edad (`Q-004`).
- Cancer Today / Global Cancer Observatory es un referente explícito para estudiar el diseño y la interacción. Debe compararse con otros diseños exitosos y con fallos documentados; el resultado se justifica con evidencia y tareas, sin copiar GCO ni afirmar superioridad sin evaluación.
- Entrada inicial de datos: una persona incorporará archivos Excel/CSV ya depurados y definitivos que entrega un sistema interno del RNC (`SRC-RNC-006`). Existe `BD PARA DANI.csv` en la raíz del espacio de trabajo, con 84 columnas; Danny confirmó el 12-10-2026 que todos los archivos mantendrán esa estructura aunque varíe su cantidad de filas. Ver `docs/05-requisitos/esquema-archivo-recibido.md`. El diccionario y grano/unidad por fila siguen pendientes. La conexión directa a BD se estudiará para una etapa posterior; no es requisito de la primera versión.
- El producto consultará únicamente archivos definitivos; el portal no corrige casos, resuelve duplicados clínicos ni vuelve a declarar el estado epidemiológico. El Anuario de Salud 2024 contiene cifras de cáncer 2022 preliminares: son otra publicación y no se ha demostrado que correspondan al archivo que recibirá la plataforma. La política de divulgación de agregados debe acordarse aparte.
- El prototipo administrativo representa recepción y comprobación técnica de archivos definitivos. Los perfiles mencionados son doctor encargado y personal de mantenimiento; sus permisos concretos y la semántica/grano del contrato de entrada quedan pendientes (`Q-017`). La estructura y orden del CSV de entrada ya están observados y confirmados estables por Danny.
- Las comprobaciones del nuevo portal se limitan a formato, integridad, procedencia, cobertura y compatibilidad de denominadores. Un rechazo técnico no modifica el archivo definitivo.
- Objetivos de calidad aclarados: diseño responsivo, presentación visual atractiva y ligera para la conectividad lenta de Cuba; la corrección del dato tiene prioridad sobre la rapidez. Falta definir perfil de evaluación de conectividad, criterios visuales y WCAG (`Q-015`, `Q-019`, `Q-020`).
- Estas aclaraciones habilitan prototipos, diagramas y arquitectura conceptual desde ahora. La política para celdas pequeñas sigue pendiente; que no se conozca una regla específica no elimina las obligaciones de confidencialidad (`Q-007`).

## Regla epistemológica

Una práctica observada en SEER, GLOBOCAN, ECIS, CDC, otro registro o una publicación no se convierte automáticamente en regla del RNC.

Usar el flujo:

`fuente → evidencia → interpretación → propuesta → validación con RNC → requisito/regla → implementación → prueba`

Estados admitidos:

- `CONFIRMADO`: fuente oficial del RNC, documento del proyecto o decisión explícita del proyecto.
- `EVIDENCIA`: evidencia externa relevante.
- `PROPUESTA`: recomendación todavía no aprobada.
- `PENDIENTE`: falta información o validación.
- `DESCARTADO`: alternativa evaluada que no se utilizará y tiene justificación.
- `HISTÓRICO`: evidencia cubana anterior cuya vigencia actual debe comprobarse.

## Conocimiento cubano obtenido hasta ahora

El Anuario Estadístico de Salud 2024 muestra datos de incidencia del RNC para 2022, tasas por 100 000 y tasas ajustadas a población estándar mundial, marcadas preliminares; las tablas generales emplean categorías CIE-10 y las pediátricas ICCC-3 (`SRC-CUBA-AES-2024`). El Manual de Procedimientos versión VII (2024), revisado completo, confirma la definición de caso, la estructura/función del RNC, codificación CIE-O-3 para topografía/morfología en 20+ e ICCC-3 en <20, flujos, detección de duplicados/múltiples primarios, controles e indicadores de calidad, cuadros estadísticos, confidencialidad y supervisiones (`SRC-RNC-003`). Ver síntesis y páginas en `docs/01-negocio/06-manual-procedimientos-2024.md`.

El manual confirma la producción de tasas crudas, específicas y ajustadas a población mundial, pero no ofrece un cálculo completo que permita comprobar la aplicación de los pesos Segi/Doll documentados por IARC/CI5. Tampoco especifica el método indirecto ni intervalos de confianza. No establece umbrales de supresión de celdas públicas, necesidades de usuarios ni un nivel WCAG. Estos límites se registran en `docs/05-requisitos/mapa-de-preguntas.md`; los estándares internacionales de cáncer son la referencia metodológica de trabajo y la normativa cubana rige privacidad y datos poblacionales.

Para nomencladores tumorales, preservar códigos de origen literalmente y vincularlos a conceptos versionados con identificador, nombre, descripción y sistema/edición. Separar topografía, morfología, comportamiento, grado, estadio y otras clasificaciones; una equivalencia entre ediciones requiere procedencia y validación y no sustituye el original. IARC publicó las tablas finales ICD-O-4 en julio de 2026 (`SRC-IARC-ICDO4-2026`), mientras el Manual RNC VII documenta CIE-O-3/ICCC-3. No asumir que ICD-O-4 ya es la regla del RNC, ni que la misma edición representa todos los datos históricos. Antes de incorporar tablas completas a una web pública, revisar licencia y obtener permiso escrito si aplica (`EVD-134..135`, `Q-002`).

La aclaración posterior del estudiante (`SRC-RNC-007`) resolvió la frase «población estándar de Cuba»: para los indicadores de cáncer se usarán referentes internacionales y la población residente cubana ONEI como **denominador**. El Manual VII y el Anuario de Salud 2024 declaran ajuste a la **estándar mundial**; IARC/CI5 publica la tabla Segi/Doll de 18 pesos que suman 100 000 (`SRC-IARC-CI5-WORLD-2026`). Se adopta como referencia para ASR(W), pendiente de cotejo numérico con un ejemplo RNC. El Anuario Demográfico ONEI 2024 ofrece tablas públicas pero no reemplaza el archivo por municipio/edad simple/sexo/año anunciado por Yinet. Ver también `docs/03-metodologia/04-ci5-xii-estandarizacion-edad.md` para el cotejo de CI5 XII, sus fórmulas y referencias.

La literatura histórica del RNC cubano describe validación, codificación, detección de duplicados y generación de estadísticas. Se trata de evidencia histórica y debe verificarse contra el procedimiento vigente.

Fuentes: `SRC-RNC-HIST-001`, `SRC-IARC-CUBA-001`.

## Benchmark internacional actual

- `SEER*Explorer`: exploración multidimensional, tablas, gráficos, descargas y metodología estadística explícita.
- `Cancer Today / GLOBOCAN`: comparación por poblaciones, cáncer, sexo y edad; ASR World, tasas crudas, riesgo acumulado, mapas y distintos tipos de gráficos.
- `ECIS`: distingue información histórica de estimaciones y proyecciones y documenta fuentes y métodos.
- `U.S. Cancer Statistics`: documentación fuerte de intervalos, supresión, comparabilidad, retrasos y calidad.
- `CanReg5 / IARC`: referencia de operación de registros, control de calidad, consistencia, análisis e interoperabilidad.
- `North Carolina`: migración desde publicación en PDF hacia visualización web reproducible.
- `Colorado`: combinación de producto público con control interno de completitud y oportunidad.
- `Missouri`: evaluación iterativa de usabilidad con rediseño entre rondas.
- `Cali`: antecedente académico cercano de analíticas visuales sobre un registro poblacional.

## Lecciones principales ya sustentadas

1. La plataforma debe responder preguntas multidimensionales sin obligar al usuario a reconstruir los datos manualmente.
2. Los resultados deben estar acompañados de contexto metodológico y estado del dato.
3. Gráficos y tablas deben coexistir.
4. La accesibilidad no puede dejarse para el final.
5. Usabilidad y utilidad no son lo mismo y deben evaluarse por separado.
6. Las reglas para pocos casos, confidencialidad y estabilidad deben definirse antes de publicar resultados.
7. Calidad, oportunidad y completitud deben considerarse parte del negocio, no solo tareas técnicas.
8. No debe copiarse una regla extranjera sin comprobar su adecuación al RNC cubano.

## Preguntas críticas todavía abiertas tras revisar el manual

Ver `docs/05-requisitos/mapa-de-preguntas.md`.

Q-001, Q-002, Q-011 y Q-012 tienen respuesta documental en el manual (pendiente solo confirmar vigencia si procede). Las cuestiones que sí bloquean especificación incluyen:

- reglas de creación/uso de agrupaciones adicionales y compatibilidad con los pesos mundiales ya documentados;
- recepción de las series ONEI por año/territorio/edad/sexo, edición y regla temporal;
- fórmulas de tasas y ajuste directo;
- definición y fórmula del ajuste indirecto;
- intervalos de confianza aceptados;
- publicación de conteos pequeños y riesgo de inferencia (confirmar política; no se conoce regla específica);
- contrato técnico de archivos definitivos, identificación/huella, responsables de incorporación y política de divulgación agregada;
- formatos de intercambio y calendario de entrega vigente del sistema interno;
- tareas prioritarias por perfil y nivel WCAG/criterios de accesibilidad;
- diccionario y grano/unidad por fila del CSV de 84 columnas, validación técnica y responsables de incorporación/publicación agregada;
- criterios de aceptación para responsividad, corrección de resultados, presentación y tiempo de respuesta;
- para una etapa posterior, sistema/motor de BD y mecanismo de conexión;

Detalle, respuesta por pregunta y páginas: `docs/05-requisitos/mapa-de-preguntas.md` y `docs/01-negocio/06-manual-procedimientos-2024.md`.

## Cómo continuar desde otro chat o con otra IA

Antes de investigar, leer siempre:

1. este archivo;
2. `README.md`;
3. `docs/00-estado-investigacion.md`;
4. `docs/evidence-map.md`;
5. `sources/catalogo.md`;
6. los documentos del área concreta que se vaya a ampliar.

Nunca crear una segunda estructura paralela.

Antes de añadir una fuente, comprobar si ya existe en `sources/catalogo.md`.

Antes de afirmar algo como regla del RNC, comprobar si existe evidencia cubana vigente.

Antes de crear un requisito, comprobar si la idea proviene del Anexo, una fuente oficial, una decisión del proyecto o una propuesta aún pendiente.

Cuando se agregue información nueva, actualizar en la misma tanda los archivos de conocimiento y su mapa de evidencia.

## Estado de la investigación

Fase actual: `Fase 0 — conocimiento documental y preparación/validación con el RNC`.

Objetivo inmediato: cerrar una base de conocimiento del negocio suficientemente sólida para que la primera reunión con el RNC sirva para validar y completar preguntas, no para descubrir desde cero qué debe significar cada concepto.

Siguiente bloque prioritario: cerrar las preguntas parciales/abiertas contra el RNC, obtener ejemplos de cálculo y series cubanas ONEI, confirmar calendario/software vigentes, y actualizar el modelo conceptual con la estándar mundial de IARC/CI5.
