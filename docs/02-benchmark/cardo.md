# CaRDO

Estado: EVIDENCIA
Corte: 2026-10-04

## Por qué se incorpora

CaRDO es un antecedente reciente específicamente orientado a que los registros de cáncer publiquen estadísticas poblacionales en línea. Es especialmente relevante porque conecta el problema de registro con la publicación web, en lugar de estudiar solo dashboards generales.

Fuentes: `SRC-CARDO-2025`, `SRC-CARDO-HANDBOOK-2025`.

## Capacidades verificadas

CaRDO es un paquete R que usa una aplicación Shiny preconstruida. Estandariza la estructura y los nombres de variables de los datos de entrada para calcular y mostrar estadísticas poblacionales. Los autores describen tasas ajustadas directamente por edad usando grupos quinquenales y población estándar mundial, riesgo acumulado y análisis de tendencias. El procesamiento de datos sensibles ocurre localmente en RStudio; para paneles de incidencia y mortalidad bastan datos agregados. Esas convenciones estadísticas son de CaRDO y **no definen** las del RNC.

## Qué debemos estudiar a fondo

- contrato de datos y posibilidad de adaptarlo a los archivos reales del RNC;
- opciones de publicación y funcionamiento con conectividad lenta;
- cálculo, pruebas y compatibilidad con los grupos clásicos y agrupaciones nuevas del RNC;
- controles de divulgación, mantenimiento y límites reconocidos por los autores.

## Uso en el RNC

Por ahora no se adopta como arquitectura. Se incorpora como referencia especializada para comparar con otras soluciones y con los requisitos cubanos. La existencia de un paquete no sustituye la comparación tecnológica exigida por el Anexo A.
