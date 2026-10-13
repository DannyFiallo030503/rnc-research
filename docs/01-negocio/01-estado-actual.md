# Estado actual del conocimiento del negocio

Estado: ACTUALIZADO CON FUENTE OFICIAL RNC 2024 + PENDIENTE
Corte: 2026-10-04

## Contexto del proyecto

El proyecto busca modernizar la difusión de estadísticas del Registro Nacional de Cáncer de Cuba mediante una plataforma web interactiva. Los documentos del proyecto establecen como dimensiones principales año, provincia, sexo, grupo de edad y localización del cáncer, junto con frecuencias, tasas de incidencia e intervalos de confianza.

Fuentes: `SRC-RNC-001`, `SRC-RNC-002`.

## Confirmado por documentos del proyecto

- El RNC tiene como función proveer información para conocer el comportamiento epidemiológico del cáncer en Cuba y apoyar la planificación de acciones de control y recursos sanitarios.
- El portal actual presenta información principalmente en documentos PDF, lo que limita la exploración dinámica.
- El sistema objetivo debe permitir consultar datos por dimensiones epidemiológicas y calcular tasas crudas, específicas y ajustadas.
- Las actividades de Prácticas II incluyen investigación, requisitos, modelo de datos, diseño y el primer núcleo funcional; las capacidades avanzadas se extienden a tesis.

## Confirmado por el Manual RNC 2024

- Es un registro poblacional de cobertura nacional; incluye residentes cubanos permanentes y los tumores/comportamientos definidos en el manual.
- Codifica topografía/morfología con CIE-O-3 en personas de 20+ desde 2007 e ICCC-3 en menores de 20; edad en años cumplidos al diagnóstico.
- Documenta captación, flujo, validación, cierres, duplicados/múltiples primarios, CDI/SCD, indicadores de calidad, cuadros estadísticos, confidencialidad y supervisión.
- Produce frecuencias y tasas crudas, específicas y ajustadas a población estándar mundial, con desgloses nacionales, provinciales y por unidad.
- Trata los datos identificables como confidenciales; las entregas se hacen anónimas/disociadas y están sujetas a aprobación/condiciones del RNC.

Fuente y referencias de página: `SRC-RNC-003`; [`06-manual-procedimientos-2024.md`](06-manual-procedimientos-2024.md).

## Lo que el manual no especifica y todavía hay que resolver

Estas cuestiones no deben convertirse en reglas de implementación hasta ser confirmadas:

- tabla/pesos/versionado exactos de la población estándar;
- fórmulas reproducibles de tasa cruda, específica, ajuste directo e indirecto;
- método y nivel de los intervalos de confianza;
- umbrales de supresión para resultados agregados y protección ante inferencia por filtros;
- criterios de transición provisional/definitivo, corrección y versionado;
- nombre/versión del software nacional, formatos de intercambio y calendario anual vigente;
- usuarios, consultas reales y nivel de accesibilidad/WCAG.

Ver estado por pregunta en `../05-requisitos/mapa-de-preguntas.md`.

## Aclaración escrita posterior al manual

Yinet confirmó el 2026-09-30 que las tablas clásicas del RNC usan grupos quinquenales de 0–4 a 85+ y que deben poder crearse agrupaciones adicionales sin reacomodar los grupos clásicos. También confirmó que la población usada como denominador es la oficial publicada por ONEI, desglosada para Cuba, provincia y municipio, por sexo y edades simples; el RNC proporcionará los datos. Quedan pendientes las reglas de agrupación, los archivos, años y edición, la definición temporal del denominador y la población estándar para tasas ajustadas. Fuente: `SRC-RNC-005`.

## Principio de trabajo

Los registros externos sirven como evidencia comparativa. No se convierten automáticamente en reglas del RNC cubano.
