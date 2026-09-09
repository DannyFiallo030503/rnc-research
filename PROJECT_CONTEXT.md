# Contexto vivo del proyecto RNC

Estado: ACTIVO
Corte: 2026-09-09
Rama de trabajo: `master`
Remoto: `origin` → `https://github.com/DannyFiallo030503/rnc-research.git`

## Propósito

Este repositorio contiene el conocimiento, la evidencia, las preguntas y las decisiones que sustentan el desarrollo de la plataforma web interactiva del Registro Nacional de Cáncer (RNC) de Cuba para Prácticas II y el Trabajo de Diploma.

No es un repositorio de código de la plataforma. Es el repositorio de conocimiento que permite pasar de evidencia a requisitos, diseño, implementación y pruebas sin perder trazabilidad.

## Situación académica

Todavía no se ha realizado la primera reunión con el RNC. Por eso el proyecto se encuentra en una etapa previa de descubrimiento del negocio.

En esta etapa no se deben inventar reglas del RNC ni cerrar tecnologías por intuición. El trabajo actual es:

1. estudiar el dominio de los registros poblacionales de cáncer;
2. estudiar cómo publica y analiza datos el RNC de Cuba;
3. estudiar sistemas internacionales existentes;
4. estudiar literatura científica y tesis relacionadas;
5. identificar patrones exitosos y fallos documentados;
6. transformar los hallazgos en preguntas y propuestas verificables para la primera reunión.

## Alcance conocido de Prácticas II

El Anexo A establece para la práctica:

- análisis comparativo de plataformas de registros de cáncer;
- fundamentos de tasas crudas, específicas y ajustadas por métodos directo e indirecto;
- intervalos de confianza por Poisson y aproximación normal;
- comparación de librerías y frameworks de cálculo/visualización;
- UX/UI y accesibilidad WCAG;
- comparación de herramientas de visualización interactiva;
- requisitos funcionales y no funcionales;
- modelo de datos;
- fundamentos de seguridad;
- comparación de bases de datos relacionales y NoSQL;
- artefactos de ingeniería;
- selección tecnológica;
- wireframes y prototipos de alta fidelidad;
- validación de prototipos con usuarios;
- implementación del motor de tasas;
- implementación de intervalos;
- consulta interactiva con filtros;
- frecuencias absolutas y relativas;
- exportación CSV, Excel y PDF.

Fuente del alcance: `SRC-RNC-001` y `SRC-RNC-002`.

## Alcance posterior identificado

El Anexo reserva para la etapa posterior, principalmente tesis y Gestión de Proyectos, elementos como dashboards avanzados, mapas coropléticos, series temporales, administración segura completa, roles, auditoría, migración histórica, pruebas finales de rendimiento y seguridad, métricas finales de accesibilidad/usabilidad y capacitación.

No se debe adelantar ese alcance como requisito de Prácticas II salvo que el tutor o el RNC lo solicite explícitamente.

## Regla epistemológica

Una práctica observada en SEER, GLOBOCAN, ECIS, CDC, otro registro o una publicación no se convierte automáticamente en regla del RNC.

Usar el flujo:

`fuente → evidencia → interpretación → propuesta → validación con RNC → requisito/regla → implementación → prueba`

Estados admitidos:

- `CONFIRMADO`: fuente oficial del RNC, documento del proyecto o decisión explícita del proyecto.
- `EVIDENCIA`: evidencia externa relevante.
- `PROPUESTA`: recomendación todavía no aprobada.
- `PENDIENTE`: falta información o validación.
- `DESCARTADO`: alternativa evaluada que no se utilizará y tiene justificación.
- `HISTÓRICO`: evidencia cubana anterior cuya vigencia actual debe comprobarse.

## Conocimiento cubano obtenido hasta ahora

El Anuario Estadístico de Salud 2024 muestra datos de incidencia del RNC para 2022. En sus tablas generales aparecen tasas por 100 000 habitantes y tasas ajustadas por edad a la población estándar mundial por 100 000 habitantes; los datos están marcados como preliminares y la fuente indicada es el Registro Nacional del Cáncer. En las tablas generales de localización de cáncer se emplea la CIE-10 y para la población menor de 20 años se utiliza la International Classification of Childhood Cancer, tercera edición.

Fuente: `SRC-CUBA-AES-2024`.

Existe además un Manual de procedimientos del Registro Nacional del Cáncer en Cuba publicado en 2024. Su registro bibliográfico describe cobertura de recolección, procesamiento, transmisión, almacenamiento, control de calidad, confidencialidad y protección de datos, pero todavía no se dispone del texto completo en este repositorio.

Fuente: `SRC-RNC-003`.

La literatura histórica del RNC cubano describe validación, codificación, detección de duplicados y generación de estadísticas. Se trata de evidencia histórica y debe verificarse contra el procedimiento vigente.

Fuentes: `SRC-RNC-HIST-001`, `SRC-IARC-CUBA-001`.

## Benchmark internacional actual

- `SEER*Explorer`: exploración multidimensional, tablas, gráficos, descargas y metodología estadística explícita.
- `Cancer Today / GLOBOCAN`: comparación por poblaciones, cáncer, sexo y edad; ASR World, tasas crudas, riesgo acumulado, mapas y distintos tipos de gráficos.
- `ECIS`: distingue información histórica de estimaciones y proyecciones y documenta fuentes y métodos.
- `U.S. Cancer Statistics`: documentación fuerte de intervalos, supresión, comparabilidad, retrasos y calidad.
- `CanReg5 / IARC`: referencia de operación de registros, control de calidad, consistencia, análisis e interoperabilidad.
- `North Carolina`: migración desde publicación en PDF hacia visualización web reproducible.
- `Colorado`: combinación de producto público con control interno de completitud y oportunidad.
- `Missouri`: evaluación iterativa de usabilidad con rediseño entre rondas.
- `Cali`: antecedente académico cercano de analíticas visuales sobre un registro poblacional.

## Lecciones principales ya sustentadas

1. La plataforma debe responder preguntas multidimensionales sin obligar al usuario a reconstruir los datos manualmente.
2. Los resultados deben estar acompañados de contexto metodológico y estado del dato.
3. Gráficos y tablas deben coexistir.
4. La accesibilidad no puede dejarse para el final.
5. Usabilidad y utilidad no son lo mismo y deben evaluarse por separado.
6. Las reglas para pocos casos, confidencialidad y estabilidad deben definirse antes de publicar resultados.
7. Calidad, oportunidad y completitud deben considerarse parte del negocio, no solo tareas técnicas.
8. No debe copiarse una regla extranjera sin comprobar su adecuación al RNC cubano.

## Preguntas críticas todavía abiertas

Ver `docs/05-requisitos/mapa-de-preguntas.md`.

Entre las más importantes están:

- definición operativa de caso;
- clasificación y versión de codificación;
- grupos de edad oficiales;
- población estándar exacta;
- definición y fórmula del ajuste indirecto;
- intervalos de confianza aceptados por el RNC;
- política de celdas pequeñas/confidencialidad;
- estado de los datos y publicación de preliminares;
- duplicados y múltiples primarios;
- métricas de calidad que utiliza el RNC;
- frecuencia y proceso de actualización;
- usuarios y preguntas reales que deben resolverse.

## Cómo continuar desde otro chat o con otra IA

Antes de investigar, leer siempre:

1. este archivo;
2. `README.md`;
3. `docs/00-estado-investigacion.md`;
4. `docs/evidence-map.md`;
5. `sources/catalogo.md`;
6. los documentos del área concreta que se vaya a ampliar.

Nunca crear una segunda estructura paralela.

Antes de añadir una fuente, comprobar si ya existe en `sources/catalogo.md`.

Antes de afirmar algo como regla del RNC, comprobar si existe evidencia cubana vigente.

Antes de crear un requisito, comprobar si la idea proviene del Anexo, una fuente oficial, una decisión del proyecto o una propuesta aún pendiente.

Cuando se agregue información nueva, actualizar en la misma tanda los archivos de conocimiento y su mapa de evidencia.

## Estado de la investigación

Fase actual: `Fase 0 — conocimiento del negocio y evidencia previa a la primera reunión`.

Objetivo inmediato: cerrar una base de conocimiento del negocio suficientemente sólida para que la primera reunión con el RNC sirva para validar y completar preguntas, no para descubrir desde cero qué debe significar cada concepto.

Siguiente bloque prioritario: reglas y metodología estadística del registro, calidad de datos, definición de población estándar y comparación más profunda de métricas/publicación.
