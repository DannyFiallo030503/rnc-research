# DEC-003 — No cerrar el stack tecnológico antes del análisis

Estado: CUMPLIDA COMO ANÁLISIS; STACK PRODUCTIVO AÚN NO CERRADO
Fecha: 2026-10-13

## Decisión

Comparar alternativas antes de fijar frontend, backend, motor estadístico o base de datos. La comparación inicial está registrada en [selección tecnológica](../06-arquitectura/seleccion-tecnologica.md). La recomendación de prototipo no equivale a aprobación institucional ni de despliegue.

## Motivo

El Anexo exige comparar alternativas y seleccionar posteriormente las tecnologías. Además, todavía faltan decisiones del dominio epidemiológico y del volumen/uso real del sistema.

## Consecuencia

La comparación documental deja como ganador provisional de mejor balance Python/Django con HTML server-rendered/progresivo (`EVD-083`), con Laravel y ASP.NET Core como rivales fuertes, FastAPI/Go como contrastes y Shiny como opción analítica. El estudiante ya ha usado Django y emplea Python en su día a día (`SRC-RNC-009`, `EVD-084`), lo que reduce el aprendizaje inicial esperado y mejora el ajuste al calendario; ese factor es experiencia del equipo y no una preferencia del RNC. La recomendación no afirma superioridad medida de ejecución o conectividad: bytes transferidos, round trips, caché y queries requieren prototipo comparativo. El estudiante aclaró que el RNC no tiene una preferencia previa comunicada sobre tecnología o diseño y espera que el proyecto presente opciones que ayuden a decidir (`SRC-RNC-008`, `EVD-078`). El equipo no debe esperar una selección institucional previa. Se comprobarán restricciones reales de infraestructura y operación cuando se obtenga esa información; si no existe una preferencia o restricción previa, esto no impide seleccionar la alternativa que mejor satisfaga los requisitos. Validar el diccionario/grano y contrastar métodos estadísticos sigue siendo necesario antes de implementar transformaciones o reglas epidemiológicas.

## Evidencia

`SRC-RNC-001`, `SRC-RNC-002`, `SRC-TECH-001..014`; ver `DEC-010` y `EVD-070..073`.

## Aplicación en el repositorio de implementación

El repositorio `rcn-web` inicia un esqueleto de prototipo con Python 3.12 y Django 6.1.2, una vista pública mínima y SQLite solo para desarrollo local. Django 6.1.2 es la versión estable vigente consultada el 2026-10-13 y admite Python 3.12 (`SRC-TECH-001`; [versiones soportadas](https://www.djangoproject.com/download/)). Esta configuración permite comenzar el prototipo; **no cierra el stack productivo ni autoriza despliegue, almacenamiento institucional o carga de microdatos**. La versión deberá revisarse al instalar/desplegar y con la infraestructura disponible en RNC/CUJAE.
