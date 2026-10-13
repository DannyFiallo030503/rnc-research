# Calidad de datos del registro de cáncer

Estado: EVIDENCIA IARC + PROCEDIMIENTOS CONFIRMADOS POR MANUAL RNC 2024
Última revisión: 2026-10-04

## Marco internacional

IARC identifica cuatro dimensiones principales de calidad para los registros poblacionales de cáncer:

- comparabilidad;
- validez;
- oportunidad;
- completitud.

Estas dimensiones son relevantes porque determinan la confianza que puede tenerse en las estadísticas producidas por el registro.

El volumen XII de *Cancer Incidence in Five Continents* (2024) ofrece un capítulo reciente sobre comparabilidad y calidad (`SRC-IARC-CI5XII-2024`). La obra de 1994 se conserva como antecedente histórico.

## Evidencia del contexto cubano

El Manual de Procedimientos del RNC, versión VII (2024), establece procedimientos e indicadores propios que reemplazan las lagunas que antes se atribuían a falta de texto. Incluye exhaustividad, conciliación de papel/base, completitud, validez y consistencia; detalle, criterios y umbrales en [`06-manual-procedimientos-2024.md`](06-manual-procedimientos-2024.md), pp. 29–35.

El manual vigente documentado describe controles de consistencia y completitud, codificación, validación, detección de duplicidades, retroalimentación entre niveles y análisis anual. La documentación histórica de IARC queda como antecedente, subordinado a la fuente 2024.

La documentación histórica también muestra que el sistema generaba automáticamente frecuencias, tasas específicas, tasas crudas, estandarizadas y truncadas, tendencias y primeras causas de cáncer.

En Villa Clara, la documentación de IARC describe fuentes hospitalarias y certificados de defunción, contribuciones de laboratorios, verificación de consistencia/completitud, codificación ICD-O y detección de duplicados.

## Implicación

La plataforma nueva no debe asumir que el dato de entrada es perfecto ni tratar la calidad como un tema exclusivamente de la base de datos.

Hay que distinguir entre:

1. calidad del registro antes de la publicación;
2. calidad de la transformación de datos;
3. calidad de los cálculos;
4. calidad de la presentación.

## Indicadores y criterios del manual cubano

- CDI/SCD: comportamiento normal inferior al 10 %; búsqueda y recuento por año/provincia/localización.
- Variables esenciales desconocidas (edad, sexo, residencia, topografía): menos del 2 %; gestión de recuperación en 72 horas.
- Verificación histológica/citológica: aceptable por encima del 80 %; morfología desconocida sobre 20 % señalada como mala calidad.
- Validez incluye faltantes, incompatibilidades y correspondencia entre edad/fecha, topografía/morfología, sexo/topografía, base diagnóstica/histología, estadio/TNM y lateralidad.
- Otros indicadores: casos SAI, base más válida, casos por mes/unidad, fuentes por caso, estabilidad de tasas, patrón por edad y cociente M:I. El rango de 80–100 % se aplica a validaciones de consistencia descritas, no a todos los indicadores.
- Los procedimientos internos combinan revisión manual, comparación de formularios con base, herramientas IARC, análisis de mortalidad, supervisiones e informes en distintas periodicidades.

Estos umbrales son criterios internos de control del registro; el manual no indica que sean umbrales para ocultar o mostrar celdas al público.

## Preguntas abiertas

- ¿Qué parte de esos controles debe quedar dentro de la nueva plataforma?
- ¿Qué calidad mínima debe cumplir un conjunto antes de publicarse?
- ¿Cómo se expone (si corresponde) la calidad al usuario sin revelar datos confidenciales?
- ¿Cuál es la versión vigente del calendario y del sistema automatizado?

## Fuentes

- `SRC-IARC-QC-001` — IARC. Quality control at the population-based cancer registry (2014). https://publications.iarc.who.int/Book-And-Report-Series/Iarc-Technical-Publications/Planning-And-Developing-Population-Based-Cancer-Registration-In-Low--And-Middle-Income-Settings-2014
- `SRC-IARC-QC-002` — IARC. Comparability and Quality Control in Cancer Registration (1994, antecedente histórico). https://publications.iarc.who.int/Book-And-Report-Series/Iarc-Technical-Publications/Comparability-And-Quality-Control-In-Cancer-Registration-1994
- `SRC-IARC-CI5XII-2024` — IARC/IACR. Cancer Incidence in Five Continents, volumen XII (2024), capítulo 5 sobre comparabilidad y calidad. https://publications.iarc.who.int/Book-And-Report-Series/Iarc-Scientific-Publications/Cancer-Incidence-In-Five-Continents-Volume-XII-2024
- `SRC-IARC-PBCR-001` — IARC. Planning and Developing Population-Based Cancer Registration in Low- and Middle-Income Settings. https://publications.iarc.who.int/Book-And-Report-Series/Iarc-Technical-Publications/Planning-And-Developing-Population-Based-Cancer-Registration-In-Low--And-Middle-Income-Settings-2014
- `SRC-IARC-CUBA-001` — IARC. Cancer Incidence in Five Continents, Cuba/Villa Clara (2004–2007, histórico). https://publications.iarc.who.int/_publications/media/download/3756/9a1a372c6a6f112d48d63e82f2fee9a6dc1c3844.pdf
- `SRC-RNC-HIST-001` — El Registro Nacional de Cáncer de Cuba. Procedimientos y Resultados. https://rbc.inca.gov.br/index.php/revista/article/download/2331/1454/16527
- `SRC-RNC-003` — Manual de procedimientos. Registro nacional del cáncer en Cuba. https://isbncuba.ccl.cerlalc.org/catalogo.php?mode=detalle&nt=86724
