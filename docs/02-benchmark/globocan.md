# IARC Global Cancer Observatory / Cancer Today

Estado: EVIDENCIA
Última revisión: 2026-10-04

## Identificación

Cancer Today es la interfaz de visualización del Global Cancer Observatory de IARC. La versión consultada declara datos GLOBOCAN 2024 con fecha 08-07-2026.

El estudiante confirma que Global Cancer Observatory / Cancer Today es un referente explícito solicitado para el producto del RNC. Esto eleva la ficha a referencia principal del benchmark, pero no convierte sus funciones o metodología en requisitos cubanos.

## Qué permite hacer

La interfaz actual ofrece distintas vistas de exploración, entre ellas:

- mapas;
- gráficos de barras;
- gráficos de dispersión;
- gráficos de distribución;
- comparación entre poblaciones;
- comparación entre tipos de cáncer.

Las consultas pueden combinar:

- población;
- sexo;
- tipo de cáncer;
- grupos de edad;
- incidencia o mortalidad;
- número absoluto;
- tasa cruda;
- tasa estandarizada por edad;
- riesgo acumulado;
- diferentes escalas y formas de agrupación en determinadas vistas.

## Tiempo: Cancer Today y Cancer Over Time

No confundir la vista `Cancer Today` con `Cancer Over Time`. Cancer Today presenta las estimaciones de una edición GLOBOCAN. La herramienta separada Cancer Over Time permite explorar series temporales de incidencia y mortalidad observadas para las poblaciones que tienen datos cargados; IARC describe datos de hasta unas siete décadas y selección de período.

La base actual de Cancer Over Time lista a Cuba con incidencia `—` y mortalidad 1968–2023. Por tanto, que el GCO ofrezca selección de años no significa que su serie de incidencia cubana esté disponible allí, ni que el RNC carezca de registros de incidencia por año. El Manual RNC VII documenta que los envíos se separan por año de diagnóstico, se conservan bases por año y se emiten resultados anuales (pp. 24–25 y Anexo 3.1). La fecha exacta que se toma como año de incidencia debe seguir la definición del RNC.

El prototipo de Prácticas II ya permite filtrar por período/año y analizar varios años desde registros sintéticos. Cada entrega/corte de demostración puede contener más de un período; no representa todavía un contrato de importación validado para los archivos reales del RNC. El esquema observado en el archivo de prácticas no está autorizado ni mapeado; el importador debe esperar confirmación del campo de año de diagnóstico, el corte y el estado provisional/definitivo.

**Implicación de diseño:** el año de incidencia debe ser una dimensión de consulta de primer nivel; los gráficos de tendencia solo deben usar períodos comparables y mostrar cobertura, estado del dato y versión/corte. El año de publicación y la fecha de actualización deben conservarse como metadatos distintos del año de incidencia.

## Patrones relevantes

### 1. Separación clara entre dimensión y medida

Cancer Today permite cambiar población, cáncer, sexo, grupo de edad y medida sin cambiar el concepto general de consulta.

### 2. Comparación como tarea de primer nivel

Hay vistas orientadas específicamente a comparar poblaciones o sitios de cáncer.

### 3. Varias visualizaciones para la misma información

La misma consulta puede convertirse en mapa, barra, dispersión u otra representación según la pregunta.

### 4. Metodología integrada en la experiencia

La plataforma expone accesos a fuentes y métodos. Esto es una señal de que la interpretación estadística no debe quedar escondida.

### 5. Mapas con más de una escala

La interfaz contempla, según la vista, escalas absolutas y de ranking y diferentes número de intervalos.

## Qué debemos adoptar como patrón

**PROPUESTA**

- Tratar población, tiempo, sexo, edad y localización como dimensiones explícitas.
- Diseñar visualizaciones según la pregunta y no según la biblioteca gráfica disponible.
- Habilitar comparaciones cuando tengan sentido epidemiológico.
- Mostrar claramente la medida y unidad de cada visualización.
- Mantener visible la fuente y metodología del indicador.
- Empezar por la tarea pública y el modelo de exploración; justificar cada control y vista comparando beneficios, fricciones y accesibilidad en varios sistemas.

## Qué debemos evitar

**PROPUESTA**

No utilizar una visualización multidimensional solo porque sea visualmente atractiva. La cantidad de opciones de Cancer Today muestra también un riesgo: demasiados controles pueden aumentar la carga cognitiva si la interfaz no está guiada.

El referente sirve como evidencia de diseño, no como prueba de que una propuesta propia sea superior. Esa afirmación deberá apoyarse en comparación explícita y evaluación de tareas con usuarios.

## Qué NO se debe importar como regla del RNC

- GLOBOCAN trabaja principalmente con estimaciones internacionales y sus propias metodologías.
- La tasa estandarizada mundial no puede asumirse como la población estándar del RNC.
- Las categorías de cáncer y grupos de edad deben coincidir con la metodología del RNC.

## Fuentes

- `SRC-IARC-001` — IARC. Global Cancer Observatory / Cancer Today. https://gco.iarc.who.int/today/en/
- `SRC-IARC-002` — Cancer Today. Visualización cartográfica. https://gco.iarc.who.int/today/en/dataviz/globe
- `SRC-IARC-003` — Cancer Today. Comparación mediante gráficos. https://gco.iarc.who.int/today/en/dataviz/scatter-plot
- `SRC-IARC-004` — Cancer Today. Gráficos de barras. https://gco.iarc.who.int/today/en/dataviz/bars
- `SRC-IARC-005` — GCO / Cancer Over Time: base y disponibilidad por población. https://gco.iarc.who.int/overtime/en/database ; lanzamiento/alcance de la serie: https://www.iarc.who.int/news-events/launch-of-new-data-on-iarc-global-cancer-observatory-and-downloads-available-on-ci5plus-exploring-cancer-trends-worldwide/
- `SRC-RNC-003` — Manual de Procedimientos RNC VII (2024), cierre y publicación por año de diagnóstico.
