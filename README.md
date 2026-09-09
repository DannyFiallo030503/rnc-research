# Plataforma web interactiva del Registro Nacional de Cáncer de Cuba

Repositorio de conocimiento, investigación y decisiones del proyecto de Prácticas II y Trabajo de Diploma.

## Empezar aquí

Leer primero:

1. `PROJECT_CONTEXT.md`
2. `docs/00-estado-investigacion.md`
3. `docs/00-criterio-investigacion.md`
4. `docs/evidence-map.md`
5. `sources/catalogo.md`

## Situación actual

El proyecto todavía no ha tenido su primera reunión con el RNC. Estamos en una fase de conocimiento del negocio y evidencia previa.

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
