# Evidencia externa sobre UX, usabilidad y visualización

Estado: EVIDENCIA
Última revisión: 2026-09-09

## 1. Usabilidad de sistemas de registro de cáncer

Un estudio publicado en 2023 identificó 114 problemas de usabilidad mediante Cognitive Walkthrough. El 41 % estaba relacionado con que los usuarios no sabían qué hacer en cada etapa; 24 % con la dificultad para relacionar lo que querían hacer con los controles; y 22 % con la falta de comprensión del proceso del sistema.

### Lección

**PROPUESTA**

- proporcionar orientación contextual;
- usar controles consistentes con el modelo mental del usuario;
- comunicar qué hizo el sistema después de cada acción.

Fuente: `SRC-UX-001`.

## 2. Evaluación iterativa de mapas

Los estudios del Missouri Cancer Registry muestran una primera evaluación, modificación de los mapas y una segunda evaluación. El trabajo utilizó tareas reales, SUS y métricas de efectividad, eficiencia y satisfacción.

### Lección

**PROPUESTA**

El prototipo del RNC debería evaluarse antes de implementarlo completamente y la versión refinada debería volver a comprobarse.

Fuentes: `SRC-MO-001`, `SRC-MO-002`.

## 3. Accesibilidad como requisito del producto

El caso de Colorado documenta mejoras de dashboards para cumplir WCAG 2.1. El proyecto del RNC ya establece investigación de WCAG en el Anexo.

### Lección

**PROPUESTA**

La accesibilidad debe entrar desde los wireframes y prototipos, no solo en una prueba posterior.

Fuente: `SRC-CO-001`.

## 4. No confundir éxito visual con éxito de uso

Missouri obtuvo buena efectividad en varias tareas pero satisfacción baja. Esto demuestra que una visualización puede funcionar técnicamente y aun así resultar poco satisfactoria o poco cómoda.

### Consecuencia

No utilizar solamente opiniones subjetivas ni solamente tasa de éxito. Las pruebas deberían combinar métricas de desempeño y comentarios de usuarios.

## Fuentes

- `SRC-UX-001` — https://pmc.ncbi.nlm.nih.gov/articles/PMC9887869/
- `SRC-MO-001` — https://pmc.ncbi.nlm.nih.gov/articles/PMC5562933/
- `SRC-MO-002` — https://pmc.ncbi.nlm.nih.gov/articles/PMC6788891/
- `SRC-CO-001` — https://www.cancerregistryeducation.org/Files/Org/f3f3d382a7a242549a9999654105a63b/Site/2024-ColoradoPoster.pdf
- `SRC-WCAG-001` — https://www.w3.org/TR/WCAG22/
