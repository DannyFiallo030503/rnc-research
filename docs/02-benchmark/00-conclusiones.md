# Conclusiones del benchmark

Estado: EVIDENCIA + PROPUESTA
Corte: 2026-09-09

## Patrones que se repiten

### 1. Exploración multidimensional

SEER*Explorer y Cancer Today permiten combinar dimensiones epidemiológicas y cambiar la vista sin reconstruir manualmente los datos.

Fuentes: `SRC-SEER-002`, `SRC-IARC-001`.

### 2. Tabla + visualización

Los sistemas maduros no dependen exclusivamente de un gráfico. La tabla permite inspección, comparación, accesibilidad y exportación.

Fuentes: `SRC-SEER-002`, `SRC-CDC-002`, `SRC-IARC-001`.

### 3. Metodología visible

SEER, USCS, ECIS y Cancer Today documentan fuentes, métodos o precauciones de interpretación.

Fuentes: `SRC-SEER-001`, `SRC-CDC-003`, `SRC-ECIS-002`, `SRC-IARC-001`.

### 4. Estado y naturaleza del dato

ECIS diferencia históricos de estimaciones/proyecciones y el Anuario cubano marca su publicación revisada como preliminar.

Fuentes: `SRC-ECIS-001`, `SRC-ECIS-002`, `SRC-CUBA-AES-2024`.

### 5. Control sobre pocos casos

USCS documenta explícitamente cómo la baja frecuencia afecta estabilidad y confidencialidad. Esto obliga a investigar una política equivalente del RNC, no a copiar el umbral estadounidense.

Fuente: `SRC-CDC-001`.

### 6. Evaluación de usuarios

Missouri y la literatura reciente sobre dashboards muestran que funcionalidad técnica y utilidad no son sinónimos. La evaluación debe usar tareas reales y, cuando corresponda, iterar el diseño.

Fuentes: `SRC-MO-001`, `SRC-MO-002`, `SRC-DASH-US-2025`.

### 7. Calidad como parte del sistema

IARC identifica comparabilidad, validez, oportunidad y completitud. Colorado añade la idea de monitorizar calidad internamente, no solo publicar resultados.

Fuentes: `SRC-IARC-QC-001`, `SRC-CO-001`.

### 8. El portal no es todo el ecosistema

CanReg5 recuerda que un registro incluye entrada, consistencia, control de calidad, análisis, migración e interoperabilidad además de publicación.

Fuente: `SRC-IARC-CANREG5-2026`.

## Patrones que debemos evitar

- copiar un diseño externo sin saber qué problema resuelve;
- ocultar la metodología detrás de una cifra;
- tratar como iguales datos observados, preliminares, estimados y proyectados;
- mostrar resultados de pocos casos sin una política explícita;
- validar solo satisfacción y no capacidad de resolver tareas;
- dejar accesibilidad para el final;
- publicar sin conocer el retraso y la fecha de actualización;
- asumir que el método estadístico extranjero es el del RNC.

## Conclusión para Prácticas II

El benchmark debe servir para construir requisitos y decisiones justificadas. No debe convertirse en una colección de capturas o descripciones de sitios.

La salida útil de esta fase es:

`problema del negocio → evidencia externa → patrón observado → riesgo → propuesta → pregunta al RNC`.

## Próximo bloque prioritario

La siguiente investigación debe centrarse menos en añadir portales y más en completar el negocio estadístico:

1. definición de caso;
2. clasificación y codificación;
3. grupos de edad;
4. población estándar;
5. métodos de ajuste;
6. intervalos;
7. pocos casos/confidencialidad;
8. calidad y oportunidad;
9. preguntas reales de usuarios.
