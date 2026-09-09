# Criterio de investigación del repositorio

Estado: CONFIRMADO COMO MÉTODO DEL REPOSITORIO
Corte: 2026-09-09

## Situación actual

No se ha realizado la primera reunión con el RNC. La investigación actual busca construir conocimiento del negocio y evidencia previa, no cerrar requisitos definitivos.

## Jerarquía de evidencia

1. Procedimientos y documentación vigente del RNC de Cuba.
2. Normativa oficial cubana aplicable.
3. Publicaciones oficiales del RNC, MINSAP y organismos cubanos.
4. IARC/WHO y estándares internacionales.
5. Documentación oficial de otros registros.
6. Artículos científicos y tesis.
7. Experiencias técnicas de implementación.

## Estados de conocimiento

### CONFIRMADO

Respaldado por documento del proyecto, fuente oficial cubana vigente o decisión explícita del RNC/proyecto.

### EVIDENCIA

Respaldado por fuentes externas de buena calidad, pero todavía no es una regla cubana.

### PROPUESTA

Recomendación que puede orientar el diseño, pendiente de aceptación.

### PENDIENTE

No existe todavía información suficiente.

### HISTÓRICO

Evidencia cubana anterior cuya vigencia actual debe verificarse.

### DESCARTADO

Alternativa evaluada con razón documentada para no utilizarla.

## Regla de trazabilidad

Cada afirmación relevante debe tener una fuente o indicar claramente que es inferencia/propuesta.

Cada fuente recibe `SRC-*`.

Cada evidencia recibe `EVD-*`.

Cada regla de negocio recibe `RN-*` cuando sea confirmada.

Cada requisito recibe `REQ-*` cuando exista base suficiente.

Cada decisión recibe `DEC-*`.

Cada pregunta abierta recibe `Q-*`.

## Regla de comparación

Una funcionalidad externa nunca se convierte automáticamente en requisito.

Para usar una práctica como propuesta debemos responder:

1. qué problema resuelve;
2. qué evidencia demuestra el beneficio;
3. en qué contexto fue evaluada;
4. qué parte es comparable con Cuba;
5. qué riesgos tiene copiarla;
6. qué adaptación requiere.

## Regla de investigación actual

No ampliar el benchmark solo para aumentar el número de sistemas estudiados. Priorizar evidencia que cierre una pregunta pendiente o contraste una hipótesis.

## Flujo de conocimiento

`fuente → evidencia → interpretación → propuesta → validación RNC → requisito/regla → implementación → prueba`

## Instrucción para futuras IA

Leer primero `PROJECT_CONTEXT.md`, `docs/00-estado-investigacion.md`, `docs/evidence-map.md` y `sources/catalogo.md`.

No crear estructuras paralelas.

No repetir investigaciones ya cubiertas sin señalar qué nueva pregunta se intenta resolver.
