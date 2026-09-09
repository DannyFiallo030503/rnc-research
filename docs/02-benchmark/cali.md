# Registro Poblacional de Cáncer de Cali / Analíticas visuales

Estado: EVIDENCIA
Última revisión: 2026-09-09

## Por qué es especialmente relevante

La tesis de Paola Andrea Collazos Rodríguez, de la Universidad del Valle, aborda directamente analíticas visuales sobre un registro poblacional de cáncer.

El trabajo propone una arquitectura para almacenamiento, recuperación, análisis y visualización y adapta analíticas a tres perfiles:

- público general;
- personal de registros de cáncer;
- médico especialista.

## Diseño y datos

La tesis documenta:

- selección de variables necesarias para las analíticas;
- consultas y vistas en PostgreSQL;
- uso de tablas de diccionario para datos precodificados;
- separación entre datos sensibles y datos utilizados para visualización;
- dashboards y gráficos para distintos perfiles.

## Evaluación

La tesis incluye evaluación del aplicativo web mediante encuestas. Para una de las analíticas se utilizaron preguntas sobre:

- utilidad para procesos de calidad;
- adecuación visual al perfil;
- facilidad de entendimiento;
- claridad de gráficos específicos;
- claridad de series temporales;
- observaciones abiertas.

La versión consultada de la tesis reporta resultados mayoritariamente positivos en esas evaluaciones, aunque el tamaño de las muestras de evaluación es pequeño. No debe tratarse como prueba general de usabilidad.

## Lecciones fuertes

### 1. Los perfiles importan

No todos los usuarios necesitan exactamente la misma analítica.

### 2. Los datos visualizados pueden requerir una capa semántica

Las vistas específicas pueden simplificar el consumo por las visualizaciones.

### 3. La evaluación está vinculada a tareas y preguntas

La tesis no se limita a mostrar capturas; incluye evaluación de la comprensión y utilidad.

## Qué debemos adoptar como patrón

**PROPUESTA**

Antes de diseñar la interfaz, identificar qué preguntas necesita responder cada perfil del RNC.

## Qué debemos evitar

No tomar la arquitectura, tecnología o estructura de usuario de Cali como requisito del RNC. Es un antecedente académico y operativo muy cercano, pero corresponde a otro registro, otro país y otro alcance.

## Fuentes

- `SRC-CALI-001` — Collazos Rodríguez, P. A. Analíticas visuales de la información del registro poblacional de cáncer de Cali. Universidad del Valle. https://bibliotecadigital.univalle.edu.co/entities/publication/150b208f-6508-4bd5-8d76-a7178818199a
- `SRC-CALI-002` — PDF del trabajo de grado. https://bibliotecadigital.univalle.edu.co/bitstream/10893/14519/1/CB-0567682.pdf
