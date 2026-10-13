# Preparación de la primera reunión con el RNC

Estado: PREPARADA; VALIDACIÓN CON ESPECIALISTAS PENDIENTE
Corte: 2026-09-30

## Objetivo

Llegar a la primera reunión con suficiente conocimiento previo para que los especialistas puedan validar, corregir y completar preguntas concretas.

La investigación externa no sustituye al RNC. Sirve para que las preguntas sean precisas y para evitar decisiones de diseño sin fundamento.

## Lo que ya sabemos por fuentes cubanas

### Publicación

El Anuario Estadístico de Salud 2024 presenta incidencia de 2022 del RNC, con tasas por 100 000 y tasas ajustadas por edad a población estándar mundial por 100 000. Los datos aparecen como preliminares y la fuente indicada es el RNC.

Fuente: `SRC-CUBA-AES-2024`.

### Clasificación publicada

Las tablas generales revisadas utilizan CIE-10 para localizaciones; las tablas de menores de 20 años utilizan ICCC tercera edición.

Fuente: `SRC-CUBA-AES-2024`.

### Procedimiento del registro

Se revisó íntegramente el Manual de Procedimientos versión VII de 2024. Confirma definición de caso, captación/procesamiento, CIE-O-3 e ICCC-3, reglas de duplicados y múltiples primarios, indicadores de calidad, cuadros estadísticos y confidencialidad. Ver `01-negocio/06-manual-procedimientos-2024.md` para páginas, límites y respuestas por pregunta.

Fuente: `SRC-RNC-003`.

## Preguntas críticas

Ver `docs/05-requisitos/mapa-de-preguntas.md`.

Prioridad máxima: presentar lo que dice el manual y pedir confirmación de vigencia; concentrar la reunión en los vacíos:

1. reglas de creación y uso de agrupaciones de edad adicionales, y tabla/pesos de población estándar;
2. fórmulas y ejemplos validados de tasas, ajustes directo e indirecto e intervalos;
3. supresión de resultados agregados y protección contra inferencia;
4. ciclo de estados preliminar/definitivo, correcciones e historial;
5. nombre/versión del sistema automatizado, formatos e integración;
6. calendario estadístico vigente;
7. usuarios, tareas reales y nivel WCAG;
8. confirmar que el Manual v. VII (2024) sigue vigente y cómo resolver posibles erratas/OCR.

Yinet confirmó por escrito los grupos quinquenales clásicos de 0–4 a 85+, la necesidad de crear agrupaciones adicionales y la población denominadora ONEI por territorio, sexo y edad simple (`SRC-RNC-005`). Solicitar las series prometidas y precisar edición, años, formato y regla temporal (`Q-016`).

## Evidencia para llevar a la reunión

No basta con preguntar "¿qué quieren en la página?".

Conviene mostrar ejemplos y preguntar por la regla detrás de ellos:

- tabla publicada por el RNC;
- tasa cruda frente a tasa ajustada;
- población estándar mundial;
- dato preliminar;
- clasificación de localizaciones;
- posibles combinaciones de filtros;
- ejemplo de salida que requiera supresión y de combinaciones de filtros riesgosas.

## Resultado esperado

Cada respuesta de la reunión deberá transformarse en una de estas salidas:

- `RN-*` si confirma una regla de negocio;
- `REQ-*` si define un requisito;
- `DEC-*` si implica una decisión de diseño/arquitectura;
- actualización de `docs/01-negocio/` si añade conocimiento del dominio;
- cierre de un `Q-*`.

## Regla

No modificar una regla confirmada posteriormente por una fuente externa sin registrar el conflicto y resolverlo explícitamente con el RNC/tutor.
