# Principios metodológicos

Estado: REFERENCIAS INTERNACIONALES + DATOS CUBANOS POR COMPLETAR
Corte: 2026-10-06

## Lo que exige el proyecto

El Anexo y la Propuesta establecen tasas crudas, específicas por edad y ajustadas por métodos directo e indirecto, además de intervalos de confianza. Fuentes: `SRC-RNC-001`, `SRC-RNC-002`.

## Evidencia cubana disponible

El Anuario Estadístico de Salud 2024 muestra tasas por 100 000 y tasas ajustadas por edad a la población estándar mundial por 100 000 y marca los datos revisados como preliminares. Fuente: `SRC-CUBA-AES-2024`.

La aclaración `SRC-RNC-007` fija el criterio de trabajo: recurrir a normas internacionales para registro, clasificación y métodos de cáncer cuando falta detalle local, mientras los casos proceden del RNC y la **población residente denominadora** de Cuba/ONEI. [OMS](https://www.who.int/standards/classifications/other-classifications/international-classification-of-diseases-for-oncology) documenta CIE-O para topografía/morfología; [IARC/CI5](https://ci5.iarc.who.int/ci5-xii/about/) documenta ASR(W) y los pesos mundiales Segi/Doll. Se identifica la versión concreta de cada regla y se contrasta su aplicación con un ejemplo RNC. La ley cubana de protección de datos y la política institucional de publicación agregada se tratan por separado.

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

CDC utiliza un marco Poisson para describir la variabilidad, pero el visualizador calcula intervalos del 95 % mediante el método gamma modificado en SEER*Stat. Esto es evidencia externa, no una especificación del RNC ni una justificación para escoger entre los métodos Poisson y normal pedidos por el Anexo. Fuente: `SRC-CDC-CI-2026`.

## Pendientes

La primera reunión debe cerrar especialmente:

- reglas de creación y uso de agrupaciones de edad adicionales; las bandas clásicas de 0–4 a 85+ ya están confirmadas (`SRC-RNC-005`);
- comprobación de un cálculo RNC con la estándar mundial Segi/Doll y su redondeo;
- fórmula del ajuste indirecto;
- tratamiento de pocos casos;
- método y nivel de confianza aceptados;
- criterios de validación de resultados.
