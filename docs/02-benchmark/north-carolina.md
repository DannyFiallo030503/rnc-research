# North Carolina Central Cancer Registry

Estado: EVIDENCIA
Última revisión: 2026-09-09

## Caso de estudio

El North Carolina Central Cancer Registry documentó en 2025 una transición desde la publicación histórica de tablas PDF hacia visualizaciones interactivas de incidencia y mortalidad.

## Problema que resolvieron

El registro quería introducir visualización interactiva sin añadir infraestructura o gasto adicional.

## Solución documentada

El caso utiliza:

- scripts Python para ingestión y generación;
- limpieza de datos desde libros Excel;
- generación de archivos estáticos;
- JavaScript y Plotly en el navegador;
- controles JavaScript para cambiar la visualización.

Los datos se incorporan al contenido servido al navegador y el producto final puede publicarse como HTML/JavaScript estático.

## Lecciones fuertes

### Reproducibilidad de la publicación

Los scripts se vuelven a ejecutar cuando se agregan o actualizan datos, generando una nueva versión publicable.

### Infraestructura proporcional al problema

No toda plataforma epidemiológica requiere un servidor de aplicaciones complejo si el caso de uso permite publicación estática.

### PDF no es el único problema

La mejora viene acompañada de un proceso reproducible de transformación del dato, no solo de una nueva capa visual.

## Qué debemos estudiar para el RNC

**PENDIENTE**

- frecuencia real de actualización del RNC;
- si los datos son estáticos o requieren consulta dinámica sobre grandes volúmenes;
- si la generación estática podría servir para la consulta pública;
- separación entre publicación pública y operaciones administrativas.

## Fuentes

- `SRC-NC-001` — Ramaswami, J. Interactive Visualization of Cancer Data. 2025. https://pmc.ncbi.nlm.nih.gov/articles/PMC12742405/
- `SRC-NC-002` — North Carolina Central Cancer Registry, NPCR Success Story. https://www.cancerregistryeducation.org/Files/Org/f3f3d382a7a242549a9999654105a63b/Site/2024-NorthCarolinaPoster.pdf
