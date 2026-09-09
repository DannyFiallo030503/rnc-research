# Estado actual del conocimiento del negocio

Estado: EVIDENCIA + PENDIENTE

## Contexto del proyecto

El proyecto busca modernizar la difusión de estadísticas del Registro Nacional de Cáncer de Cuba mediante una plataforma web interactiva. Los documentos del proyecto establecen como dimensiones principales año, provincia, sexo, grupo de edad y localización del cáncer, junto con frecuencias, tasas de incidencia e intervalos de confianza.

Fuentes: `SRC-RNC-001`, `SRC-RNC-002`.

## Lo que sabemos

- El RNC tiene como función proveer información para conocer el comportamiento epidemiológico del cáncer en Cuba y apoyar la planificación de acciones de control y recursos sanitarios.
- El portal actual presenta información principalmente en documentos PDF, lo que limita la exploración dinámica.
- El sistema objetivo debe permitir consultar datos por dimensiones epidemiológicas y calcular tasas crudas, específicas y ajustadas.
- Las actividades de Prácticas II incluyen investigación, requisitos, modelo de datos, diseño y el primer núcleo funcional; las capacidades avanzadas se extienden a tesis.

## Lo que todavía no sabemos

Estas cuestiones no deben convertirse en reglas de implementación hasta ser confirmadas:

- definición operativa exacta de caso registrable;
- clasificación y versión de codificación de cáncer;
- grupos de edad oficiales;
- población estándar;
- fórmula/procedimiento del ajuste directo;
- fórmula/procedimiento del ajuste indirecto;
- intervalos de confianza aceptados por el RNC;
- reglas para pocos casos, supresión y confidencialidad;
- tratamiento de múltiples primarios, duplicados y datos faltantes;
- periodicidad y proceso de actualización;
- responsables de validación y publicación.

## Principio de trabajo

Los registros externos sirven como evidencia comparativa. No se convierten automáticamente en reglas del RNC cubano.
