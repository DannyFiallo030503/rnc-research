# CanReg5 e IARC: referencia de operación del registro

Estado: EVIDENCIA
Corte: 2026-09-09

## Qué es

CanReg5 es una herramienta de IARC orientada a la gestión de información de registros de cáncer y no solamente a la publicación de estadísticas para el público.

La documentación y los recursos de IARC incluyen materiales para estructura de base de datos, entrada de casos, importación, control de calidad, análisis, migración y otros procesos del registro.

Fuentes: `SRC-IARC-GICR-RESOURCES-2026`, `SRC-IARC-CANREG5-2026`.

## Por qué interesa al proyecto

El benchmark anterior estaba concentrado en portales públicos. CanReg5 permite recordar que el portal de consulta es solo una capa de todo el ecosistema.

Conceptualmente:

`captura/registro → validación → consolidación → análisis → publicación`

No se debe diseñar la interfaz pública suponiendo que el dato llega sin contexto o sin controles previos.

## Lecciones

### Control de calidad antes de publicar

El software de registro incorpora controles de consistencia y validación. Esto refuerza la necesidad de tratar calidad como parte del negocio y no como una tarea exclusiva de presentación.

### Interoperabilidad

Los recursos de IARC contemplan importación y migración, lo que resulta relevante para la futura carga de datos históricos del RNC.

### Separación de capas

Un sistema de captura/gestión de registro y un portal público no tienen exactamente las mismas responsabilidades.

## Qué no debemos asumir

No significa que el nuevo portal del RNC deba reemplazar CanReg5, ni que el RNC utilice actualmente CanReg5 en producción. Solo demuestra que la arquitectura de un registro poblacional requiere funciones que van más allá de un dashboard.

## Pregunta para la reunión

`Q-010`: ¿Qué software y flujo utiliza actualmente el RNC para registrar, validar, consolidar y preparar los datos que terminan en las publicaciones?
