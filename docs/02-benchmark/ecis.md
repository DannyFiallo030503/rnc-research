# ECIS — European Cancer Information System

Estado: EVIDENCIA
Última revisión: 2026-09-09

## Identificación

ECIS es administrado por el Joint Research Centre de la Comisión Europea. La página oficial actual ofrece un Data Explorer con estudios de estimaciones 2024, estimaciones a largo plazo, supervivencia, datos históricos, cáncer infantil y prevalencia.

## Qué permite hacer

El Data Explorer diferencia explícitamente entre:

- estimaciones 2024;
- estimaciones a largo plazo;
- supervivencia estimada;
- incidencia y mortalidad históricas observadas;
- incidencia infantil observada;
- prevalencia estimada.

La documentación de la base de datos indica que las estimaciones de incidencia y mortalidad de 2024 dependen de fuentes y métodos de estimación, y que pueden diferir de datos observados o estimaciones producidas por autoridades nacionales.

## Patrón extremadamente importante

### El tipo de dato es parte del significado del indicador

ECIS no trata como equivalentes:

- datos observados;
- estimaciones;
- proyecciones.

Esta distinción es fundamental para el futuro RNC.

## Qué debemos adoptar

**PROPUESTA**

Cada resultado relevante debería poder identificar:

- naturaleza del dato;
- periodo;
- fuente;
- método cuando sea necesario;
- si es preliminar, observado o estimado.

## Qué debemos evitar

Mezclar resultados observados y estimados dentro de la misma visualización sin indicarlo claramente.

## Actualidad

La documentación actualizada de ECIS señala que las estimaciones 2024 para EU-27 fueron publicadas en diciembre de 2025 y actualizadas el 19 de febrero de 2026. El 29 de abril de 2026 se añadieron estimaciones para otros países europeos y se revisaron algunos datos infantiles.

## Fuentes

- `SRC-ECIS-001` — ECIS. Data Explorer. https://ecis.jrc.ec.europa.eu/data-explorer
- `SRC-ECIS-002` — ECIS. Database description. https://ecis.jrc.ec.europa.eu/database-description
- `SRC-ECIS-003` — ECIS. Home. https://ecis.jrc.ec.europa.eu/
