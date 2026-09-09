# Calidad y oportunidad de los datos de registros de cáncer

Estado: EVIDENCIA
Corte: 2026-09-09

## Marco de calidad IARC

IARC identifica cuatro dimensiones centrales de calidad en registros poblacionales de cáncer:

1. comparabilidad;
2. validez;
3. oportunidad;
4. completitud.

Fuente: `SRC-IARC-QC-001`.

Estas dimensiones son especialmente útiles porque permiten separar problemas que a veces se mezclan. Un registro puede tener datos completos pero llegar tarde; puede ser oportuno pero tener problemas de validez; o puede ser válido pero difícil de comparar por cambios de clasificación.

## Indicadores observados en la literatura de registros

En análisis europeos de calidad se utilizan, entre otros:

- porcentaje de Death Certificate Only (DCO%);
- Primary Site Unknown (PSU%);
- porcentaje con confirmación microscópica (MV%);
- razón mortalidad:incidencia (M:I);
- porcentaje de casos con morfología desconocida (UM%);
- retraso entre fecha de registro y fecha de incidencia.

Fuente: `SRC-ECIS-QI-001`.

No se debe asumir que todos estos indicadores forman parte del RNC. El objetivo en esta fase es identificar qué variables podrían servir para evaluar la calidad y qué preguntas debe responder la reunión con especialistas.

## Oportunidad

La calidad de una publicación depende también de cuándo se dispone del dato. CDC documenta que las bases de datos pueden recibir actualizaciones posteriores y que las fechas de envío de los registros afectan el análisis.

Fuente: `SRC-CDC-002`, `SRC-CDC-003`.

Para el RNC habrá que distinguir al menos:

`año de incidencia` ≠ `año de publicación` ≠ `fecha de actualización` ≠ `estado del dato`.

El Anuario 2024, por ejemplo, presenta datos de incidencia del año 2022 y los marca como preliminares.

Fuente: `SRC-CUBA-AES-2024`.

## Pocos casos y estabilidad

CDC explica que tasas basadas en pocos casos tienen intervalos más amplios y mayor inestabilidad, y utiliza supresión por debajo de 16 casos en sus estadísticas nacionales.

Fuente: `SRC-CDC-001`.

Ese umbral no se debe copiar al RNC. La evidencia solo demuestra que una plataforma de este tipo necesita una política explícita que considere estabilidad y confidencialidad.

Preguntas relacionadas: `Q-007`, `Q-008`.

## Conclusión para el proyecto

La calidad no debe aparecer solamente en un informe técnico final. Debe poder reflejarse en el modelo de datos y en la publicación para que el usuario pueda saber si está viendo:

- un dato preliminar;
- un dato consolidado;
- un valor afectado por supresión;
- un resultado con gran incertidumbre;
- una serie con problemas de comparabilidad.

La forma exacta de mostrarlo es todavía una `PROPUESTA`.
