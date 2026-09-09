# Estadísticas de cáncer publicadas por Cuba

Estado: EVIDENCIA CUBANA
Corte: 2026-09-09

## Qué se observó

El Anuario Estadístico de Salud 2024 publica estadísticas de incidencia de cáncer correspondientes al año 2022 y señala como fuente al Registro Nacional del Cáncer.

Fuente: `SRC-CUBA-AES-2024`.

## Tasas y unidades

En las tablas generales se presenta:

- tasa por 100 000 habitantes;
- tasa ajustada por edad a la población estándar mundial por 100 000 habitantes.

El documento marca estos datos como preliminares.

Fuente: `SRC-CUBA-AES-2024`.

## Clasificación de localizaciones

Las tablas generales de incidencia por localización utilizan categorías de la Clasificación Internacional de Enfermedades, décima revisión.

Las tablas para menores de 20 años utilizan la International Classification of Childhood Cancer, tercera edición.

Fuente: `SRC-CUBA-AES-2024`.

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

El Anuario etiqueta las cifras como preliminares. Por tanto, el sistema futuro deberá investigar cómo distinguir entre datos preliminares y datos consolidados, y en qué momento cambia ese estado.

Pregunta relacionada: `Q-008`.

## Implicación sobre comparación internacional

Una comparación de tasas solo es válida cuando se conoce la población estándar usada. La publicación cubana utiliza población estándar mundial en las tablas revisadas.

Esto no autoriza a imponer esa población estándar a todos los cálculos futuros. La regla exacta de la plataforma debe ser confirmada con el RNC.

Pregunta relacionada: `Q-004`.

## Limitación de esta evidencia

El Anuario permite conocer qué se publica, pero no explica por sí solo todas las reglas internas mediante las que se construyen los indicadores. No debe utilizarse como sustituto del Manual de procedimientos ni de la validación con especialistas.
