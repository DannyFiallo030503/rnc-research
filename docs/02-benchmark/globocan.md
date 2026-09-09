# IARC Global Cancer Observatory / Cancer Today

Estado: EVIDENCIA
Última revisión: 2026-09-09

## Identificación

Cancer Today es la interfaz de visualización del Global Cancer Observatory de IARC. La versión consultada declara datos GLOBOCAN 2024 con fecha 08-07-2026.

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

## Qué debemos evitar

**PROPUESTA**

No utilizar una visualización multidimensional solo porque sea visualmente atractiva. La cantidad de opciones de Cancer Today muestra también un riesgo: demasiados controles pueden aumentar la carga cognitiva si la interfaz no está guiada.

## Qué NO se debe importar como regla del RNC

- GLOBOCAN trabaja principalmente con estimaciones internacionales y sus propias metodologías.
- La tasa estandarizada mundial no puede asumirse como la población estándar del RNC.
- Las categorías de cáncer y grupos de edad deben coincidir con la metodología del RNC.

## Fuentes

- `SRC-IARC-001` — IARC. Global Cancer Observatory / Cancer Today. https://gco.iarc.who.int/today/en/
- `SRC-IARC-002` — Cancer Today. Visualización cartográfica. https://gco.iarc.who.int/today/en/dataviz/globe
- `SRC-IARC-003` — Cancer Today. Comparación mediante gráficos. https://gco.iarc.who.int/today/en/dataviz/scatter-plot
- `SRC-IARC-004` — Cancer Today. Gráficos de barras. https://gco.iarc.who.int/today/en/dataviz/bars
