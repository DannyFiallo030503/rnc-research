# Estadísticas de cáncer publicadas por Cuba

Estado: EVIDENCIA CUBANA
Corte: 2026-10-04

## Qué se observó

El Anuario Estadístico de Salud 2024 publica estadísticas de incidencia de cáncer correspondientes al año 2022 y señala como fuente al Registro Nacional del Cáncer.

Fuente: `SRC-CUBA-AES-2024`.

## Procedimiento y cuadros que establece el Manual RNC 2024

El Manual de Procedimientos, versión VII, confirma como objetivo oficial las frecuencias y tasas específicas por edad y sexo, tasas crudas y tasas ajustadas a población estándar mundial. Enumera cuadros nacionales y provinciales por sexo, localización/aparato, grupos diagnósticos, edad y año; y cuadros administrativos por provincia informante y unidad (p. 3–4, 36–38). Incluye también frecuencias de base diagnóstica, etapa clínica, CDI/SCD y varios indicadores de calidad.

El manual precisa que la edad pediátrica corresponde a menores de 20 años. Lista algunos estratos adultos (20–29, 30–44, 45–59, 60+) pero no publica una tabla completa de intervalos etarios ni los pesos de estandarización. Confirma la población mundial como estándar sin identificar la tabla/versionado exactos.

**Límite metodológico:** el manual enumera los resultados, pero no da fórmulas reproducibles de tasas, ajuste directo o indirecto, ni intervalos de confianza. No usar el nombre de un indicador como especificación algorítmica. Q-003 a Q-006 y Q-009 registran lo pendiente.

Fuente: `SRC-RNC-003`; detalle en [`06-manual-procedimientos-2024.md`](06-manual-procedimientos-2024.md).

## Tasas y unidades

En las tablas generales se presenta:

- tasa por 100 000 habitantes;
- tasa ajustada por edad a la población estándar mundial por 100 000 habitantes.

El documento marca estos datos como preliminares.

Fuente: `SRC-CUBA-AES-2024`.

## Clasificación de localizaciones publicada

Las tablas generales de incidencia por localización utilizan categorías de la Clasificación Internacional de Enfermedades, décima revisión.

Las tablas para menores de 20 años utilizan la International Classification of Childhood Cancer, tercera edición.

Fuente: `SRC-CUBA-AES-2024`.

La codificación interna del registro es distinta: CIE-O-3 para topografía y morfología en pacientes de 20 años o más diagnosticados desde 2007; ICCC-3 para menores de 20; CIE-10 puede usarse para las categorías de cuadros generales. No colapsar estas funciones en un único campo de clasificación. Fuente: `SRC-RNC-003`, pp. 16–17; `SRC-CUBA-AES-2024`.

## Implicaciones para el sistema

Esto demuestra que el proyecto no parte de una necesidad abstracta. El sistema deberá poder representar, como mínimo, un contexto estadístico que incluya:

- conteo de casos;
- población de referencia;
- tasa cruda;
- tasa ajustada;
- unidad de la tasa;
- población estándar;
- periodo de referencia;
- estado del dato.

Estas características todavía se consideran evidencia del negocio publicado, no requisitos definitivos de interfaz.

## Implicación especialmente importante: estado del dato

El Anuario etiqueta las cifras como preliminares. La regla del producto aclarada por el estudiante es excluirlas: el portal mostrará únicamente cortes definitivos (`SRC-RNC-004`). Sigue pendiente acordar cómo el RNC identifica/aprueba el corte definitivo, registra correcciones y versiona publicaciones; no se expondrán los preliminares.

Pregunta relacionada: `Q-008`.

## Implicación sobre comparación internacional

Una comparación de tasas solo es válida cuando se conoce la población estándar usada. La publicación cubana utiliza población estándar mundial en las tablas revisadas.

Esto no autoriza a imponer esa población estándar a todos los cálculos futuros. La regla exacta de la plataforma debe ser confirmada con el RNC.

Pregunta relacionada: `Q-004`.

## Limitación de las fuentes

El Anuario permite observar una publicación concreta; el Manual describe objetivos, cuadros y flujos, pero no toda la metodología matemática que los produce. No sustituye tablas de cálculo, denominadores, pesos estándar ni ejemplos validados por el RNC.
