# Decisiones pendientes para requisitos y diseño de la plataforma del RNC

**Actualizado:** 15 de octubre de 2026, tras la comunicación `SRC-RNC-010`. Esta guía diferencia aclaraciones del estudiante, evidencia pública, propuestas del equipo y validaciones institucionales pendientes. Ver [mapa de preguntas](mapa-de-preguntas.md), [aclaraciones del 15-10](../08-reuniones/06-aclaraciones-estudiante-2026-10-15.md) e [investigación de fuentes cubanas](../03-metodologia/03-investigacion-fuentes-cubanas-privacidad-2026-10-06.md).

## Información ya aclarada para el diseño

- Cada fila recibida representa un **tumor de una persona**. Identificadores permiten reconocer tumores múltiples de la misma persona; por ello los indicadores deben declarar si cuentan tumores o personas. No publicar microdatos ni identificadores (`Q-017`).
- Los grupos clásicos estáticos se conservan. La propuesta futura es permitir nomencladores adicionales por rango sin sustituirlos ni restringirlos arbitrariamente. Compatibilidad matemática con tasas ajustadas todavía requiere definición (`Q-003`).
- Los intervalos de confianza no forman parte de las salidas actuales del RNC; el proyecto propone calcularlos con método justificado y adaptar la elección si el RNC indica otro (`Q-009`).
- No se comunicó política escrita de confidencialidad para el portal. Se debe maximizar protección: solo estadísticas agregadas autorizadas, análisis de combinaciones de filtros y controles comunes a tabla, gráfico y exportación (`Q-007`).
- Se prevé una persona responsable (doctor, soporte o secretaría); el estudiante propone superadministración para operaciones y revocación de cortes ante errores de transferencia, con permisos auditados para cambios que alteren métodos o resultados. Es propuesta de roles, no descripción confirmada del proceso oficial (`Q-008`).
- Diseñar para una cadencia variable: habitual de uno o dos años, con posibilidad de movimientos semanales. Conservar versiones, procedencia, publicación y revocación; no codificar calendario fijo (`Q-013`).
- La conexión puede ser baja y la infraestructura modesta. Priorizar exactitud y eficiencia de cálculo junto con gráficos/tablas claros y cuidados; rapidez sigue siendo relevante (`Q-019`, `Q-020`).

## Verificación pública antes de pedir datos

1. El [Anuario Estadístico de Salud 2024](https://files.sld.cu/dne/files/2025/09/AES-2024-para-sitio-3.pdf) y su [presentación MINSAP/Infomed](https://temas.sld.cu/estadisticassalud/2025/09/30/anuario-estadistico-de-salud-2024/) publican cuadros RNC con conteos y tasas, incluida tasa ajustada a población mundial y tasas por edad. La incidencia 2022 está marcada preliminar. Usar esas tablas para contrastar presentación y localizar definiciones; no asumir que equivalen al corte definitivo del proyecto.
2. El [Anuario Demográfico de Cuba 2024 de ONEI](https://www.onei.gob.cu/sites/default/files/publicaciones/2025-07/00-anuario-demografico-2024.pdf) distingue población media y efectiva, y declara que tabulaciones y bases demográficas adicionales están disponibles a quienes las soliciten. Sus cuadros consultados no ofrecen la matriz municipio × edad simple × año; su canal concreto/descarga abierta sigue sin localizarse. ONEI calcula población efectiva anualmente, no mediante un nuevo censo cada uno o dos años. Solicitar solo la URL/catálogo o procedimiento y los campos exactos de cobertura que falten.
3. El Manual RNC VII confirma la emisión de frecuencias absolutas y relativas; un artículo cubano basado en datos RNC publica porcentajes por localización y etapa. Ya se revisaron las fotos (capítulo CI5 de estandarización etaria). Para cada salida del portal aún hay que fijar universo, denominador, desconocidos y redondeo; separar conteos de tumores y de personas.
4. La estándar de ajuste publicada en los anuarios de salud es la mundial; población cubana ONEI funciona como denominador. La población estándar y las tasas públicas sirven para contrastar, pero un ejemplo agregado no basta para validar cada regla de cálculo.

## Puntos concretos para validar cuando se haya agotado la evidencia documental

### Población y métodos estadísticos (`Q-004`–`Q-006`, `Q-009`, `Q-016`, `Q-018`, `Q-021`)

- Localizar edición pública ONEI y verificar territorio, sexo, edad simple, años, códigos y si los valores son población media o efectiva. Si falta cobertura, pedir al responsable RNC/ONEI la referencia exacta, no un archivo duplicado.
- Identificar en los materiales existentes una tasa RNC reproducible, su estándar, redondeo y tratamiento de edades desconocidas. Para ajuste indirecto, el método y la población/tasas de referencia siguen abiertos.
- Cotejar con el RNC el denominador y redondeo de cada salida de frecuencia relativa. Las publicaciones prueban que existen porcentajes, pero no una convención única para todas las tablas. Especificar por separado conteo de tumores y de personas y documentar desconocidos/solapamientos.
- El equipo propondrá métodos y nivel de IC por indicador; contrastará resultados con fuentes metodológicas y ejemplos antes de mostrarlos como cálculo validado.

### Archivo y controles (`Q-017`)

- El CSV de muestra contiene 84 encabezados en orden fijo y las futuras entregas mantendrán la estructura, según aclaración previa. El grano tumor/persona ya está comunicado; falta diccionario autorizado, campos que vinculan tumores a una persona, semántica de columnas/códigos, cobertura y procedencia autorizada.
- Confirmar si ese CSV es un extracto autorizado y distinto del paquete de envío interno que regula el Anexo 3.1 del Manual. No manipular ni mapear encabezados a conceptos geográficos/tumorales sin diccionario.

### Publicación, operación y roles (`Q-007`, `Q-008`, `Q-013`)

- Definir con el responsable institucional política de divulgación agregada, protección contra inferencia por filtros y regla común de supresión para consultas y exportaciones.
- Modelar carga, revisión técnica, publicación versionada y revocación auditada. La revocación retira un corte público; no edita ni corrige casos.
- Confirmar quién opera, quién administra configuración y métodos, quién publica/revoca, y qué acciones requieren revisión o registro. La propuesta de superadministrador es diseño del equipo hasta validarla con el flujo real descrito en el Manual y la propuesta de trabajo.

### Experiencia y operación (`Q-014`, `Q-015`, `Q-019`, `Q-020`)

- Convertir claridad visual, accesibilidad, eficiencia y conectividad limitada en tareas de prototipo y criterios medibles. Los perfiles/tareas, dispositivos, navegadores y condiciones de red para evaluación todavía no se han especificado.

## Material útil para la validación siguiente

- URL/catálogo ONEI o procedimiento de solicitud de la serie por año, municipio, sexo, edad simple y tipo de población; precisar cobertura que falte.
- Confirmación RNC de fórmula/denominador, desconocidos y redondeo para cada frecuencia relativa interactiva.
- Ejemplo agregado reproducible de tasa RNC para cotejar fórmula/estándar/redondeo.
- Diccionario autorizado que relacione claves de persona y tumor sin copiar microdatos a documentación.
- Descripción vigente de responsables/roles y del procedimiento de publicación o retirada de un corte.
