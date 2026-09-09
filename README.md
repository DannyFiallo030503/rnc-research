# Plataforma web interactiva del Registro Nacional de Cáncer de Cuba

Repositorio de conocimiento, investigación y decisiones del proyecto de Prácticas II y Trabajo de Diploma.

## Propósito

Este repositorio concentra la evidencia que sustenta el análisis del negocio, la definición de requisitos, las decisiones epidemiológicas, UX/UI y las decisiones técnicas del proyecto.

La regla principal es: **ninguna decisión importante debe quedar sin evidencia o justificación**.

## Cómo navegar

- `docs/01-negocio/`: conocimiento del dominio y funcionamiento del registro.
- `docs/02-benchmark/`: sistemas reales, publicaciones y análisis comparativo.
- `docs/03-metodologia/`: tasas, estandarización, intervalos de confianza y conceptos epidemiológicos.
- `docs/04-ux-ui/`: accesibilidad, usabilidad, visualización y patrones de interacción.
- `docs/05-requisitos/`: requisitos funcionales, no funcionales, reglas y preguntas abiertas.
- `docs/06-arquitectura/`: modelo de datos, arquitectura y artefactos de ingeniería.
- `docs/07-decisiones/`: decisiones registradas con contexto, alternativas y evidencia.
- `docs/08-reuniones/`: acuerdos y dudas obtenidos con el RNC y tutores.
- `sources/`: catálogo de fuentes y, cuando corresponda, copias permitidas de documentos originales.
- `data/`: datos auxiliares o conjuntos de datos derivados necesarios para reproducir análisis.

## Regla de evidencia

Cada fuente recibe un identificador estable, por ejemplo `SRC-RNC-001`, `SRC-IARC-001`, `SRC-SEER-001`.

Cada afirmación relevante debe poder apuntar a una fuente usando ese identificador.

Cada decisión relevante recibe un identificador `DEC-001` y debe indicar:

1. qué se decidió;
2. por qué;
3. qué alternativas se evaluaron;
4. qué evidencia la respalda;
5. qué queda pendiente de validación.

## Estado de conocimiento

Usar estas etiquetas dentro de los documentos:

- **CONFIRMADO**: respaldado por fuente oficial, evidencia primaria o decisión explícita del RNC.
- **EVIDENCIA**: respaldado por literatura o sistemas externos, pero no necesariamente aplicable al RNC.
- **PROPUESTA**: recomendación del equipo todavía no aprobada.
- **PENDIENTE**: falta confirmación o información.
- **DESCARTADO**: alternativa evaluada que no se utilizará, con motivo documentado.

Nunca convertir una hipótesis o una práctica de otro registro en una regla del RNC sin marcarla como tal.
