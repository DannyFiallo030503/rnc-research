# Población estándar y comparabilidad de tasas

Estado: EVIDENCIA + PENDIENTE DE VALIDACIÓN RNC
Corte: 2026-09-09

## Por qué importa

Una tasa ajustada por edad depende de una población estándar. Dos tasas calculadas con poblaciones estándar diferentes no son directamente comparables como si fueran el mismo indicador.

CDC advierte explícitamente que tasas ajustadas usando diferentes poblaciones estándar no deben compararse sin considerar esa diferencia.

Fuente: `SRC-CDC-INTERP-2026`.

## Evidencia cubana disponible

El Anuario Estadístico de Salud 2024 publica tasas ajustadas por edad a la población estándar mundial por 100 000 habitantes.

Fuente: `SRC-CUBA-AES-2024`.

## Evidencia SEER

SEER documenta el uso de la población estándar estadounidense de 2000 y mantiene una definición explícita de sus grupos de edad.

Fuente: `SRC-SEER-STDPOP-2026`, `SRC-SEER-MANUAL-2026`.

La lección no es elegir la población de SEER, sino documentar siempre cuál población estándar y qué agrupación etaria se utilizaron.

## Regla propuesta para el futuro sistema

Toda tasa ajustada debería poder asociarse de manera trazable con:

- población estándar;
- versión o referencia de esa población;
- grupos de edad;
- pesos utilizados;
- método de ajuste;
- unidad de la tasa.

Estado: `PROPUESTA`.

## Preguntas que el RNC debe cerrar

`Q-004`: población estándar oficial.

`Q-003`: grupos de edad oficiales.

`Q-005`: definición operativa y fórmula exacta del ajuste directo.

`Q-006`: definición y fórmula exacta del ajuste indirecto.

## Riesgo

Si se codifica el motor antes de cerrar estas definiciones, un cambio posterior puede obligar a modificar el modelo de datos, las pruebas y la interfaz.
