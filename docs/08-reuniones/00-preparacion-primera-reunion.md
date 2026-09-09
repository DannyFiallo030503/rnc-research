# Preparación de la primera reunión con el RNC

Estado: PENDIENTE
Corte: 2026-09-09

## Objetivo

Llegar a la primera reunión con suficiente conocimiento previo para que los especialistas puedan validar, corregir y completar preguntas concretas.

La investigación externa no sustituye al RNC. Sirve para que las preguntas sean precisas y para evitar decisiones de diseño sin fundamento.

## Lo que ya sabemos por fuentes cubanas

### Publicación

El Anuario Estadístico de Salud 2024 presenta incidencia de 2022 del RNC, con tasas por 100 000 y tasas ajustadas por edad a población estándar mundial por 100 000. Los datos aparecen como preliminares y la fuente indicada es el RNC.

Fuente: `SRC-CUBA-AES-2024`.

### Clasificación publicada

Las tablas generales revisadas utilizan CIE-10 para localizaciones; las tablas de menores de 20 años utilizan ICCC tercera edición.

Fuente: `SRC-CUBA-AES-2024`.

### Procedimiento del registro

Existe un Manual de procedimientos de 2024 que, según su registro bibliográfico, cubre recolección, procesamiento, transmisión, almacenamiento, calidad y confidencialidad. Aún falta revisar el texto completo.

Fuente: `SRC-RNC-003`.

## Preguntas críticas

Ver `docs/05-requisitos/mapa-de-preguntas.md`.

Prioridad máxima:

1. definición de caso;
2. clasificación y versión de codificación;
3. grupos de edad;
4. población estándar;
5. ajuste directo;
6. ajuste indirecto;
7. intervalos de confianza;
8. pocos casos/confidencialidad;
9. estado preliminar/consolidado;
10. proceso de actualización;
11. duplicados y múltiples primarios;
12. necesidades reales de usuarios.

## Evidencia para llevar a la reunión

No basta con preguntar "¿qué quieren en la página?".

Conviene mostrar ejemplos y preguntar por la regla detrás de ellos:

- tabla publicada por el RNC;
- tasa cruda frente a tasa ajustada;
- población estándar mundial;
- dato preliminar;
- clasificación de localizaciones;
- posibles combinaciones de filtros;
- ejemplo de una celda con pocos casos.

## Resultado esperado

Cada respuesta de la reunión deberá transformarse en una de estas salidas:

- `RN-*` si confirma una regla de negocio;
- `REQ-*` si define un requisito;
- `DEC-*` si implica una decisión de diseño/arquitectura;
- actualización de `docs/01-negocio/` si añade conocimiento del dominio;
- cierre de un `Q-*`.

## Regla

No modificar una regla confirmada posteriormente por una fuente externa sin registrar el conflicto y resolverlo explícitamente con el RNC/tutor.
