# Principios metodológicos

Estado: EVIDENCIA + PENDIENTE DE VALIDACIÓN
Corte: 2026-09-09

## Lo que exige el proyecto

El Anexo y la Propuesta establecen tasas crudas, específicas por edad y ajustadas por métodos directo e indirecto, además de intervalos de confianza. Fuentes: `SRC-RNC-001`, `SRC-RNC-002`.

## Evidencia cubana disponible

El Anuario Estadístico de Salud 2024 muestra tasas por 100 000 y tasas ajustadas por edad a la población estándar mundial por 100 000 y marca los datos revisados como preliminares. Fuente: `SRC-CUBA-AES-2024`.

## Principios que no deben romperse

1. Conocer siempre el numerador y el denominador.
2. Conocer la unidad de la tasa.
3. Conocer el periodo de referencia.
4. Conocer la población estándar cuando existe ajuste.
5. Mantener alineados los grupos de edad entre casos, población y estándar.
6. Identificar el estado del dato.
7. Poder reproducir el cálculo a partir de entradas y parámetros.
8. Validar fórmulas y resultados con valores de referencia antes de publicar.

## Población estándar

Ver `02-poblacion-estandar-y-comparabilidad.md`.

## Intervalos

CDC utiliza un marco Poisson y documenta intervalos de 95 %. Esto es evidencia externa, no una especificación definitiva del RNC. Fuente: `SRC-CDC-CI-2026`.

## Pendientes

La primera reunión debe cerrar especialmente:

- grupos de edad;
- población estándar y referencia exacta;
- fórmula del ajuste directo;
- fórmula del ajuste indirecto;
- tratamiento de pocos casos;
- método y nivel de confianza aceptados;
- criterios de validación de resultados.
