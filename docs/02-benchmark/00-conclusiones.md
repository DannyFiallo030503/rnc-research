# Conclusiones del benchmark — corte 2026-09-09

Estado: EVIDENCIA + PROPUESTA

Este documento sintetiza el primer benchmark profundo. No convierte ninguna práctica externa en requisito del RNC.

## Patrones con evidencia repetida

### 1. Consulta multidimensional

SEER, GLOBOCAN y USCS permiten combinar varias dimensiones epidemiológicas antes de presentar el resultado.

**Aplicación potencial:** una consulta debe representar claramente el conjunto de filtros y el indicador calculado.

### 2. Tabla + visualización

Los sistemas maduros no dependen exclusivamente de gráficos. SEER y USCS proporcionan tablas y descargas, mientras GLOBOCAN mantiene representaciones tabulares en varias vistas.

**Aplicación potencial:** el valor numérico y la visualización deben poder contrastarse.

### 3. Metodología visible

SEER, GLOBOCAN, ECIS y USCS acompañan los resultados con documentación o accesos a fuentes/métodos.

**Aplicación potencial:** cada indicador debe tener una explicación metodológica accesible.

### 4. Naturaleza del dato

ECIS distingue explícitamente observado, estimado y proyección. SEER también diferencia estadísticas preliminares en su versión actual.

**Aplicación potencial:** el estado del dato debe formar parte del resultado.

### 5. Política para datos pequeños

USCS tiene reglas explícitas de supresión por estabilidad y confidencialidad.

**Aplicación potencial:** el RNC necesita su propia política, que todavía debe definirse con especialistas.

### 6. Usabilidad basada en tareas

Missouri demuestra que una herramienta puede tener buena efectividad y al mismo tiempo baja satisfacción; además, refinó la herramienta y volvió a medir.

El estudio de evaluación de un sistema de registro de cáncer encontró 114 problemas de usabilidad, muchos relacionados con que el usuario no sabía qué hacer, no relacionaba sus objetivos con los controles o no entendía el proceso.

**Aplicación potencial:** probar tareas reales y proporcionar guía y retroalimentación.

### 7. Separar difusión de gestión de calidad

Colorado desarrolló herramientas internas para completitud y oportunidad aparte de los dashboards públicos.

**Aplicación potencial:** el futuro panel administrativo no debe tratarse como una simple copia de la consulta pública.

### 8. Publicación reproducible

North Carolina demuestra una estrategia de publicación que se regenera a partir de scripts cuando los datos cambian.

**Aplicación potencial:** el proceso de actualización debe ser reproducible y auditable.

### 9. El benchmark internacional no sustituye al negocio cubano

La documentación histórica del RNC cubano muestra sus propios procesos y estructuras. Por ejemplo, publicaciones del RNC describen validación, codificación, detección de duplicidades y generación automática de tablas, tasas y tendencias; IARC también documenta aspectos del registro de Villa Clara dentro del RNC.

**Aplicación potencial:** las reglas cubanas tienen prioridad cuando entren en conflicto con patrones externos.

## Primer catálogo de éxitos a perseguir

- resultados estadísticamente interpretables;
- filtros alineados con preguntas reales;
- tabla y gráfico coherentes;
- metodología visible;
- exportación reproducible;
- estado del dato visible;
- política de pequeños conteos definida;
- accesibilidad incorporada desde diseño;
- pruebas de usabilidad antes y después de cambios;
- proceso de actualización reproducible;
- separación entre consulta pública y gestión interna.

## Primer catálogo de fracasos a evitar

- usar el diseño como criterio principal de calidad;
- esconder metodología;
- mostrar solo gráficos;
- mezclar estimaciones y datos observados;
- permitir combinaciones de filtros ambiguas;
- publicar tasas pequeñas sin una política epidemiológica/confidencial;
- considerar que la tarea terminada implica satisfacción;
- dejar la accesibilidad para el final;
- depender de procesos manuales de actualización;
- copiar reglas extranjeras como si fueran reglas del RNC.

## Fuentes principales

- `SRC-SEER-002`
- `SRC-IARC-001`
- `SRC-ECIS-001`
- `SRC-CDC-001`
- `SRC-NC-001`
- `SRC-CO-001`
- `SRC-MO-001`
- `SRC-MO-002`
- `SRC-CALI-001`
- `SRC-UX-001`
- `SRC-IARC-CUBA-001`
- `SRC-RNC-003`
