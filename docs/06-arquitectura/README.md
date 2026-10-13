# Arquitectura y artefactos de diseño

## Estado

Se puede iniciar ahora el diseño conceptual y documentar supuestos. La [arquitectura evolutiva propuesta](arquitectura-evolutiva-rnc.md) fija módulos, contratos y escenarios de cambio; las decisiones afectadas por archivos reales, política de divulgación e infraestructura siguen provisionales.

## Contexto acordado

- Sitio web de consulta estadística con acceso público para visitantes.
- GCO/Cancer Today es un referente explícito de exploración pública. El benchmark también debe cubrir diseños fallidos y justificar patrones seleccionados/descartados.
- **Primera versión:** el sistema interno del RNC entrega archivos Excel/CSV ya depurados y definitivos; una persona los incorpora a la plataforma. La conexión directa a BD queda para una etapa posterior.
- Diseñar la incorporación detrás de `FuenteCorteDefinitivo`: el adaptador Excel/CSV inicial y una integración autorizada futura entregan el mismo paquete lógico. La consulta usa otros contratos para cortes, población ONEI, métodos y divulgación. No seleccionar ahora un motor de BD fuente que todavía se desconoce.
- Los microdatos no se vuelven públicos por ser pública la web. El Manual RNC establece datos identificables confidenciales y entregas anónimas/disociadas aprobadas por el RNC.

## Primeros artefactos que pueden elaborarse

1. [Casos de uso de consulta pública y prototipo administrativo](casos-uso-sistema.md) — borrador trazado a la línea base.
2. Diagrama de contexto y componentes: consulta pública, panel administrativo conceptual, validación de datos y fuente futura.
3. Diagramas de actividades para consulta e incorporación técnica de archivos definitivos.
4. Modelo conceptual de cortes, territorios, edades y poblaciones ONEI/estándar; la unidad de caso/tumor se agrega tras confirmar el grano de los archivos.
5. Wireframes/prototipo inspirados y contrastados con GCO, SEER, USCS, ECIS y los casos de problemas de usabilidad del benchmark.
6. Matriz comparativa de tecnologías centrada en importación Excel/CSV, validación, trazabilidad/versiones de datos, cálculos requeridos, exportación, accesibilidad, despliegue y mantenimiento. Registrar extensibilidad a una futura conexión de BD como criterio, no como requisito de implementación inicial.

La [arquitectura evolutiva](arquitectura-evolutiva-rnc.md) explica qué permanece estable al cambiar fuentes o reglas. La [secuencia metodológica y especificación de clases](metodo-y-clases-staruml.md) fija conceptos, atributos, operaciones, relaciones y correspondencias entre vistas. Los pasos para dibujar cada figura están en el [plan operativo de StarUML](plan-operativo-diagramas-staruml.md); la [guía de diagramas de Prácticas II](guia-diagramas-staruml.md) resume el inventario y las alternativas.

La [comparación y selección tecnológica](seleccion-tecnologica.md) documenta alternativas, fuentes técnicas, recomendación inicial y validaciones pendientes. Django y PostgreSQL son candidatos provisionales hasta confirmar experiencia e infraestructura institucional.

## Preguntas que condicionan detalles

- Qué plantillas XLSX/CSV, hojas, codificación, columnas, tipos, tamaños y reglas de validación se recibirán.
- Quién recibirá los archivos definitivos y revisará el resultado técnico de la incorporación; los permisos del doctor encargado y del personal de mantenimiento no están definidos.
- Para la etapa posterior: qué sistema/motor de BD, acceso, consultas/vistas y permisos estarían disponibles.
- Qué respuesta recibe el gestor cuando un archivo falla el contrato técnico y cómo se comunica el rechazo al sistema que lo produjo.
- Cómo proteger el origen de datos y preparar salidas agregadas para publicación sin exponer microdatos; se publicarán solamente cortes definitivos.
- Cómo comprobar integridad, estructura y cobertura sin duplicar la depuración clínica que ya realizó el sistema interno.
- Archivos, edición y regla temporal de los denominadores ONEI; reglas para agrupaciones de edad nuevas, pesos de población estándar, ajuste indirecto e intervalos. Las bandas clásicas 0–4 a 85+ ya fueron aclaradas (`SRC-RNC-005`).
- Política para conteos pequeños, trazabilidad de archivos definitivos inmutables y errores de transferencia. Los preliminares no se publican.
- Infraestructura de despliegue y nivel WCAG esperado.

## Criterio

Marcar cada supuesto en los diagramas y mantenerlos coherentes entre modelo de datos, arquitectura, clases, actividades, secuencias, decisión tecnológica e implementación. No presentar una propuesta conceptual como decisión confirmada del RNC.
