# U.S. Cancer Statistics

Estado: EVIDENCIA
Última revisión: 2026-10-04

## Identificación

U.S. Cancer Statistics combina datos de los programas NPCR de CDC y SEER de NCI para producir estadísticas federales oficiales de cáncer. La herramienta de visualización actual fue publicada en junio de 2026.

## Qué permite explorar

La herramienta actual incluye:

- incidencia;
- mortalidad;
- tendencias;
- estadio;
- supervivencia;
- prevalencia;
- sitio de cáncer;
- edad;
- sexo;
- raza/etnia;
- ubicación;
- comparaciones geográficas y entre sitios.

Existe además una sección específica para descargar tablas preanalizadas.

En la edición consultada, la herramienta informa incidencia observada hasta 2023 y mortalidad hasta 2024. Estos son años de datos diferentes de la fecha de actualización del portal (`SRC-CDC-002`).

## Lección de diseño

Las descargas forman parte del ecosistema de análisis, no son un añadido aislado. CDC mantiene tablas históricas descargables y documentación específica para interpretar el conjunto de datos.

## Regla de supresión como evidencia de negocio

CDC publica una política explícita: en las tablas y figuras de U.S. Cancer Statistics no se muestran estadísticas calculadas con conteos inferiores a 16. El motivo declarado combina estabilidad estadística y confidencialidad.

CDC documenta la supresión complementaria en las notas de la **base de uso público**, para evitar que un usuario pueda deducir una celda suprimida a partir de otras celdas y un total (`SRC-CDC-PUBLIC-CAUTION-2026`). La página técnica del visualizador consultada no describe esa regla en detalle.

### Importante para el RNC

**NO COPIAR EL UMBRAL 16.**

La lección transferible es que el RNC necesita una política propia y explícita de:

- pocos casos;
- estabilidad estadística;
- confidencialidad;
- supresión complementaria cuando corresponda.

## Lección adicional

La página técnica de 2026 incluye advertencias de interpretación y una guía para comparar tasas por región. Esto demuestra que la interpretación correcta del resultado debe formar parte del sistema y la documentación.

## Fuentes

- `SRC-CDC-001` — CDC. Suppression of Rates and Counts. https://www.cdc.gov/united-states-cancer-statistics/technical-notes/suppression.html
- `SRC-CDC-002` — CDC. U.S. Cancer Statistics Data Visualizations. https://www.cdc.gov/united-states-cancer-statistics/dataviz/index.html
- `SRC-CDC-003` — CDC. Data Visualizations Tool Technical Notes. https://www.cdc.gov/united-states-cancer-statistics/technical-notes/index.html
- `SRC-CDC-004` — CDC. Download Data Tables. https://www.cdc.gov/united-states-cancer-statistics/dataviz/data-tables.html
- `SRC-CDC-005` — CDC. U.S. Cancer Statistics Public Use Database. https://cdc.gov/united-states-cancer-statistics/public-use/index.html
- `SRC-CDC-PUBLIC-CAUTION-2026` — CDC. Cautionary Notes. https://www.cdc.gov/united-states-cancer-statistics/public-use/cautionary-notes.html
