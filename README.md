# Plataforma web interactiva del Registro Nacional de Cáncer de Cuba

Repositorio de conocimiento, investigación y decisiones del proyecto de Prácticas II y Trabajo de Diploma.

## Empezar aquí

Leer primero:

1. `PROJECT_CONTEXT.md`
2. `docs/00-estado-investigacion.md`
3. `docs/00-criterio-investigacion.md`
4. `docs/01-negocio/06-manual-procedimientos-2024.md`
5. `docs/05-requisitos/linea-base-practicas-ii.md` — alcance/requisitos y entregables trazables al Anexo A.
6. `docs/evidence-map.md`
7. `sources/catalogo.md`
8. `docs/00-auditoria-documental-2026-10-04.md` — alcance de la revisión, correcciones y fuentes que aún requieren validación.
9. `docs/09-informe/borrador-informe-practicas-ii-rnc.md` — borrador académico editable; también disponible como DOCX.
10. `docs/06-arquitectura/plan-operativo-diagramas-staruml.md` — instrucciones de dibujo en StarUML.
11. `docs/06-arquitectura/metodo-y-clases-staruml.md` — método de modelado, clases completas, relaciones y trazabilidad entre diagramas.
12. `docs/03-metodologia/03-investigacion-fuentes-cubanas-privacidad-2026-10-06.md` — investigación de anuarios, población ONEI y normas de protección de datos.
13. `docs/03-metodologia/04-ci5-xii-estandarizacion-edad.md` — síntesis y cotejo del capítulo CI5 XII de estandarización por edad transcrito en `MasDatos.txt`.
13. `docs/05-requisitos/detalles-pendientes-para-requisitos-y-diseno.md` — guion actualizado para las preguntas restantes; Word fechado disponible en la misma carpeta.
14. `docs/06-arquitectura/arquitectura-evolutiva-rnc.md` — propuesta modular que localiza cambios futuros de fuente, datos, método y divulgación.

## Situación actual

El conocimiento documental incluye el Manual de Procedimientos RNC v. VII (2024), el Anuario de Salud 2024, el Anuario Demográfico ONEI 2024 y la normativa cubana de datos personales. Yinet aclaró los grupos de edad y la fuente de población (`SRC-RNC-005`). El estudiante precisó que un sistema interno entrega archivos ya definitivos, que el RNC no usa actualmente intervalos de confianza y que la política de confidencialidad del portal debe proponerse (`SRC-RNC-006`). Una aclaración posterior (`SRC-RNC-007`) fijó estándares internacionales para los indicadores de cáncer y población cubana ONEI como denominador; IARC/CI5 documenta los pesos mundiales usados como referencia para ASR(W). La primera reunión formal y otras validaciones permanecen pendientes. Consultar el mapa de preguntas para los detalles abiertos.

La investigación actual busca conocer el negocio estadístico de los registros de cáncer, estudiar sistemas reales, identificar patrones de éxito y fracaso y preparar preguntas para validar con los especialistas.

## Estructura

- `docs/01-negocio/`: dominio y funcionamiento del registro.
- `docs/02-benchmark/`: sistemas y publicaciones externas.
- `docs/03-metodologia/`: fundamentos estadísticos y epidemiológicos.
- `docs/04-ux-ui/`: usabilidad, accesibilidad y visualización.
- `docs/05-requisitos/`: preguntas, requisitos y reglas futuras.
- `docs/06-arquitectura/`: diseño técnico posterior.
- `docs/07-decisiones/`: decisiones justificadas.
- `docs/08-reuniones/`: información confirmada por reuniones.
- `sources/`: fuentes y referencias.
- `data/`: datos auxiliares reproducibles.

## Principio de trazabilidad

Ninguna decisión importante debe quedar sin evidencia o justificación.

Una fuente recibe `SRC-*`.

Una evidencia recibe `EVD-*`.

Una pregunta recibe `Q-*`.

Una regla confirmada recibe `RN-*`.

Un requisito confirmado recibe `REQ-*`.

Una decisión recibe `DEC-*`.

## Regla epistemológica

Una práctica de SEER, GLOBOCAN, ECIS, CDC, otro registro o una publicación científica es evidencia externa, no una regla del RNC.

## Flujo

`fuente → evidencia → interpretación → propuesta → validación RNC → requisito/regla → implementación → prueba`

## Cómo continuar en otro chat o con otra IA

No empezar de cero. Leer `PROJECT_CONTEXT.md` y continuar desde `docs/00-estado-investigacion.md`.

Antes de añadir una fuente, revisar `sources/catalogo.md`.

Antes de añadir una afirmación, revisar `docs/evidence-map.md` para evitar duplicados.
