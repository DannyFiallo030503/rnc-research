# Revisión de gráficos y contexto de consulta — 20-10-2026

## Alcance y estado

Esta revisión usa únicamente el entorno sintético de `rnc-web`. No valida el contrato de entrada real, las reglas epidemiológicas cubanas, los nombres oficiales de códigos ni la política de divulgación. La unidad y las categorías anatómicas de la demostración son ilustrativas. Deben cotejarse con los requisitos `REQ-F-002..009`, el grano de entrada pendiente (`Q-017`), las reglas de indicadores (`Q-003..009`, `Q-016..018`) y la política de publicación (`Q-007`).

Se revisaron en el navegador los ocho tipos existentes —barras horizontales, columnas, líneas, barras agrupadas, apiladas, porcentuales, circular y anillo— y en backend las combinaciones de los ocho tipos con CSV, XLSX, PNG, SVG y PDF. Los formatos tabulares comparan sus filas con la tabla/series de la misma consulta. Se inspeccionaron visualmente el PNG y el PDF descargados y se corrigió el solapamiento entre nota y eje.

## Reglas de lectura que debe conservar cada salida

- Identificar corte, versión, periodo/rango, territorio, sexo, edad y localización, aun cuando algunos filtros estén en “Todos”.
- Identificar agrupación, indicador, unidad y unidad/escala de los ejes. La selección de todos los periodos debe enumerar el rango disponible.
- Mostrar valores directamente en marcas legibles y mantener la tabla como representación exacta, accesible y exportable.
- En porcentajes por sexo, cada categoría representa 100 % y muestra su reparto interno por sexo. No equivale a la proporción de cada categoría respecto al total de la población.
- Los conteos de personas por localización pueden solaparse: una persona puede tener varios tumores/localizaciones. No sumar las categorías para reconstruir personas únicas.
- Tasas y ajuste por edad del prototipo usan denominadores/métodos sintéticos candidatos; deben permanecer señalados como no oficiales hasta su validación.

La matriz de regresión asegura que CSV/XLSX conservan selección y valores, PNG/SVG/PDF se generan para cada tipo y SVG conserva texto seleccionable. La evidencia no sustituye inspección con usuarios, lector de pantalla, dispositivos físicos o reglas aprobadas por el RNC.

## Siguientes visualizaciones con valor potencial

1. **Serie anual de incidencia.** La línea existente es prioritaria para explorar cambios por año. Antes de aplicarla a datos RNC, confirmar cómo se obtiene el año de diagnóstico/incidencia del formato, si los periodos son comparables y qué revisión/versión de corte se representa.
2. **Edad y sexo.** Barras específicas por edad/sexo y, si el RNC confirma numeradores y denominadores, tasas específicas por edad. Una pirámide puede ayudar a comparar sexos por grupo; debe distinguir con claridad casos, personas y tasas y no ocultar grupos pequeños.
3. **Territorio.** Comparar provincias mediante tabla ordenada y barras. Un mapa coroplético solo después de cotejar código, nombre, límites geográficos, nivel territorial y controles de publicación oficiales; un código o nombre sintético no basta para asignar geometría.
4. **Topografía y morfología.** Ranking por códigos originales y catálogos versionados, mostrando identificador y nombre autorizado. No agrupar ni reinterpretar códigos ICD-O recibidos sin la versión y reglas institucionales correspondientes. Para categorías numerosas, búsqueda/tabla y barras horizontales son preferibles a un gráfico circular.
5. **Composición.** Reservar circular/anillo a pocas categorías mutuamente excluyentes y una pregunta de composición concreta. Para comparar periodos, territorios o magnitudes, preferir líneas o barras; los gráficos circulares no muestran bien diferencias pequeñas.

Estas son propuestas para ordenar el prototipado, no requisitos institucionales nuevos. La selección final requiere una tarea de uso por perfil y validación del RNC/CUJAE; Q-020 permanece abierto.

## Nomencladores y descripciones contextuales

El responsable pide tener disponibles los catálogos tumorales completos y explicar las etiquetas/códigos en la web. La interfaz debe permitir descubrir una descripción al pasar el puntero o enfocar el término, y también en móvil mediante un control accesible. La descripción debe estar ligada a un concepto y a un identificador exacto del sistema/edición; topografía identifica localización, morfología describe histología/comportamiento y grado/estadio son campos distintos. El código recibido se conserva literalmente. Los campos `site_id` y etiquetas actuales son grupos ilustrativos sintéticos, no los catálogos ICD-O.

IARC anunció el 20-07-2026 las tablas finales ICD-O-4 y una estructura de morfología nueva. El Manual RNC VII que se revisó documenta CIE-O-3 e ICCC-3; no hay evidencia para cambiar la codificación operativa de Cuba a ICD-O-4 ni para reemplazar las ediciones históricas. Por tanto, la propuesta para el portal es ofrecer catálogos por sistema y edición, incluidos los históricos necesarios para leer códigos de origen, sin declarar una edición “universal” de entrada. Antes de importar/servir tablas extensas hay que confirmar con RNC las ediciones realmente recibidas y obtener/confirmar los permisos de reproducción y traducción. Los términos IARC consultados requieren permiso escrito explícito para la reproducción sustancial o amplia circulación de su material. Hasta resolverlo, enlazar la consulta oficial y preparar el modelo/UI sin copiar la tabla.

Para cada código visible, la ayuda deberá mostrar al menos código literal, sistema y edición, nombre oficial, descripción autorizada, eje (p. ej. topografía o morfología), estado (vigente/histórico/obsoleto) y fuente/versión. Enlaces de equivalencia entre ediciones se presentan aparte del código de origen y con procedencia; no se deducen por similitud textual. Para que los nombres ingleses puedan mostrarse en español, usar traducción autorizada o traducción institucional revisada y claramente identificada.
