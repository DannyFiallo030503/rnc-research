# SEER / SEER*Explorer

Estado: EVIDENCIA
Última revisión: 2026-10-04

## Identificación

SEER*Explorer es la herramienta interactiva del National Cancer Institute para explorar estadísticas SEER. La página oficial indica que la versión actual incluye estimaciones preliminares de incidencia hasta 2024, publicadas el 22 de junio de 2026.

## Qué permite hacer

La documentación oficial indica que permite:

- crear gráficos personalizados;
- crear tablas personalizadas;
- descargar datos e imágenes;
- compartir enlaces a resultados;
- explorar por sexo, raza, año calendario y edad;
- para determinados sitios, explorar estadio e histología.

La cobertura actual incluye incidencia SEER, supervivencia SEER, mortalidad de EE. UU., prevalencia de EE. UU. y riesgo de por vida.

## Patrones relevantes para el RNC

### 1. La consulta es multidimensional

Los filtros no están aislados de los indicadores. La herramienta permite construir una consulta estadística concreta antes de producir la visualización.

### 2. Tabla y gráfico son resultados equivalentes

La interfaz no obliga al usuario a interpretar únicamente una gráfica. La tabla forma parte del producto analítico.

### 3. La descarga es parte de la funcionalidad

El usuario puede extraer datos e imágenes. Esto respalda que exportar no debe tratarse como una función secundaria.

### 4. El resultado puede ser compartido

Los enlaces a resultados facilitan reproducibilidad y comunicación entre usuarios.

### 5. La metodología debe acompañar al dato

SEER mantiene documentación separada sobre definiciones de incidencia y poblaciones estándar. Esto muestra que el cálculo necesita contexto metodológico explícito.

Un artículo del propio programa describe el paso de tablas estáticas a SEER*Explorer y pruebas con perfiles variados, incluidas observaciones de navegación y seguimiento ocular (`SRC-SEER-USABILITY-2024`). Es evidencia histórica del proceso de diseño; las funciones actuales se comprueban en la página oficial.

## Qué debemos adoptar como patrón

**PROPUESTA**

- Diseñar la consulta como una combinación explícita de dimensiones + indicador + medida.
- Mostrar una representación tabular junto a la visualización cuando sea apropiado.
- Permitir exportar el resultado consultado.
- Permitir volver a una consulta concreta mediante parámetros compartibles o una representación equivalente.
- Mostrar el contexto metodológico del indicador sin obligar al usuario a abandonar la consulta.

## Qué NO debemos copiar directamente

**PENDIENTE / NO TRANSFERIBLE AUTOMÁTICAMENTE**

- población estándar de SEER;
- clasificación de cáncer de SEER;
- reglas estadounidenses de inclusión/exclusión;
- cobertura territorial;
- estimaciones de incidencia preliminares;
- estructura de indicadores que el RNC no necesite.

## Riesgos / limitaciones observables

SEER*Explorer administra varios tipos de estadísticas y poblaciones. Esa complejidad es útil como referencia, pero una plataforma del RNC no debe añadir dimensiones solo porque SEER las tenga. La interfaz debe reflejar las preguntas reales de los usuarios del RNC.

## Evidencia de actualidad

La versión oficial consultada en septiembre de 2026 declara explícitamente los datos preliminares hasta 2024 y describe su ciclo de actualización.

## Fuentes

- `SRC-SEER-001` — SEER. Incidence Statistics. https://seer.cancer.gov/statistics/types/incidence.html
- `SRC-SEER-002` — NCI/SEER. SEER*Explorer. https://seer.cancer.gov/statistics-network/explorer/overview.html
- `SRC-SEER-003` — NCI/SEER. Standard Populations. https://seer.cancer.gov/stdpopulations/
- `SRC-SEER-004` — NCI/SEER. Data Archive. https://seer.cancer.gov/statistics-network/explorer/archive.html
- `SRC-SEER-USABILITY-2024` — NCI/SEER. Desarrollo y evaluación de SEER*Explorer. https://pmc.ncbi.nlm.nih.gov/articles/PMC11300012/
