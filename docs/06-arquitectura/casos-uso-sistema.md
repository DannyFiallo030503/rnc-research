# Casos de uso del sistema — consulta pública

Estado: BORRADOR v0.3; derivado del Anexo A y aclaraciones de diseño, pendiente de validación con tutora y RNC

Corte: 2026-10-15

## Propósito y criterio de modelado

Este documento inicia los artefactos de requisitos y diseño para el informe de Prácticas II. Aplica las recomendaciones de `SRC-UNI-001` (guía universitaria de escritura y defensa): documentar requisitos funcionales y de calidad, usar casos de uso del sistema cuando ayuden a representar las funciones, explicar actores y casos, y acompañar los diagramas con una descripción legible. La guía ofrece buenas prácticas; no sustituye las orientaciones de la tutora ni el Anexo A.

El sistema de interés tiene dos áreas: consulta pública y un panel administrativo que se diseña como prototipo para trabajadores del RNC. La consulta pública no requiere cuenta y se dirige a cualquier persona. Los archivos Excel/CSV llegan desde un sistema interno que ya depuró y declaró definitivos los datos (`SRC-RNC-006`); el portal verifica el contrato técnico y no corrige casos ni reproduce el flujo interno.

## Actores

| Actor | Descripción | Estado |
|---|---|---|
| Visitante público | Persona que accede al sitio para consultar estadísticas agregadas y exportar el resultado. | Confirmado por el contexto del proyecto. |
| Trabajador autorizado del RNC | Personal que incorpora y revisa el estado técnico de archivos definitivos mediante el prototipo administrativo. | Función general propuesta; permisos ordinarios y responsabilidades exactas pendientes (`Q-017`, `Q-023`). |
| Superadministrador de soporte | Administra cuentas/roles y acciones globales restringidas en la solución objetivo. | Rol `superadmin` requerido por dirección del producto (`SRC-PRJ-001`); quién recibe la designación y controles institucionales pendientes. |

No se agregan jerarquías de actores ni relaciones `include`/`extend`: con el alcance confirmado no hacen falta. El diagrama público y el administrativo deben mantenerse separados para no mezclar visitantes con trabajadores.

## Construcción del diagrama de casos de uso en StarUML

Crear un **Use Case Diagram** en StarUML con esta estructura:

1. En el **Model Explorer**, seleccionar el modelo o paquete donde se guardarán los requisitos y elegir **Add Diagram → Use Case Diagram**. Nombrarlo `CU-01 Consulta pública de estadísticas`.
2. Añadir un **Subject** (límite del sistema) y nombrarlo `Sitio público de estadísticas del RNC`.
3. Dentro del Subject, añadir dos **Use Case**:
   - `UC-01 Consultar estadísticas`
   - `UC-02 Exportar resultado de consulta`
4. Fuera del Subject, a la izquierda, añadir un **Actor** llamado `Visitante público`.
5. Crear una **Association** entre `Visitante público` y cada caso de uso.
6. No añadir relaciones `include` ni `extend`, ni generalización de actores.
7. Ordenar los elementos para que el actor quede fuera del límite y los casos dentro. Verificar que no haya líneas cruzadas y que el texto se lea al exportar el diagrama.

El diagrama representa dos objetivos completos del visitante: obtener un resultado estadístico y conservarlo fuera del sitio. Los filtros y los indicadores se documentan como pasos/opciones de la consulta, no como casos aislados, pues por sí solos son acciones pequeñas. Los filtros se derivan del Anexo A; los indicadores y su presentación requieren cerrar reglas y validar el prototipo.

### Diagrama separado del flujo administrativo en StarUML

El Anexo incluye el prototipo administrativo y la aclaración del proyecto establece que lo usarán trabajadores del RNC. Crear un segundo **Use Case Diagram**, separado del público:

1. En `01 Requisitos`, añadir **Use Case Diagram** y nombrarlo `CU-02 Flujo administrativo (prototipo)`.
2. Añadir un **Use Case Subject** `Panel administrativo del RNC (prototipo)`.
3. Añadir fuera del límite el actor `Trabajador del RNC`.
4. Dentro del límite, añadir `UC-03 Incorporar archivo definitivo`.
5. Añadir `UC-04 Revisar resultado técnico de incorporación`.
6. Añadir `UC-05 Consultar cortes disponibles`.
7. Asociar el actor a esos objetivos con **Association**. No separar doctor encargado y mantenimiento como actores con permisos distintos hasta conocer sus responsabilidades.
8. Añadir una **Note**: «Prototipo de Prácticas II; datos depurados/definitivos provienen del sistema interno; formato, roles e implementación segura pendientes».
9. No usar `include`/`extend` aún; las relaciones entre pasos se precisan con `ACT-01`.

Estos casos son una base de diseño del prototipo, no una especificación aprobada de permisos ni de panel implementado. Los flujos detallados deben completarse al validar el procedimiento con el RNC.

### Diagrama de acceso y gestión de cuentas en StarUML

El producto objetivo requiere autenticación individual y un rol `superadmin`; el MVP local tiene login y control de acceso inicial, mientras la integración de identidad y controles productivos corresponden a continuidad/tesis. Añadir un tercer **Use Case Diagram** `CU-03 Acceso administrativo y gestión de usuarios`, separado del visitante y del flujo de incorporación:

1. Crear el Subject `Identidad y administración del portal RNC (objetivo)`.
2. Añadir los actores `Trabajador autorizado del RNC` y `Superadministrador de soporte`.
3. Añadir los casos `UC-06 Iniciar/cerrar sesión administrativa`, `UC-07 Ejecutar operación administrativa autorizada`, `UC-08 Gestionar cuentas y asignar roles`, `UC-09 Cambiar configuración global versionada` y `UC-10 Consultar auditoría / revocar publicación`.
4. Asociar el trabajador a iniciar/cerrar sesión y a la operación administrativa autorizada. Asociar el superadministrador a los casos de gestión global/cuentas/auditoría. La matriz final de permisos, segregación y si un actor puede acumular funciones sigue pendiente de `Q-023`.
5. Añadir notas: `No hay auto-registro. En la primera implementación segura se provisiona al menos un superadmin por mecanismo institucional. Cualquier operación se autoriza en backend. Otros roles se agregan como grupos/permisos, sin cambiar la arquitectura. Este diagrama es objetivo de diseño, no función desplegada en Prácticas II.`
6. No dibujar una relación `include` por cada comprobación de permiso; se trata como regla transversal del backend. No usar credenciales reales en el prototipo.

## Especificaciones de casos de uso

### UC-01 — Consultar estadísticas

| Campo | Especificación |
|---|---|
| Actor principal | Visitante público |
| Objetivo | Obtener estadísticas agregadas de cáncer para los criterios seleccionados. |
| Trazabilidad | `REQ-F-001` a `REQ-F-008`; `REQ-NF-001`, `REQ-NF-002`; `Q-003` a `Q-009`, `Q-014` a `Q-016`, `Q-018`. |
| Prioridad | Núcleo del producto de Prácticas II. |
| Estado | Iniciado; solo se mostrarán datos definitivos. Indicadores exactos, catálogos y reglas de publicación agregada siguen pendientes. |

**Precondiciones**

- El sitio está disponible públicamente.
- Existe al menos un conjunto de datos autorizado para publicación y preparado para consulta.

**Flujo básico**

1. El visitante abre la consulta estadística.
2. El sistema ofrece criterios por año, provincia, sexo, grupo de edad y localización del cáncer (`REQ-F-002`).
3. El visitante establece los criterios deseados.
4. El visitante solicita la consulta.
5. El sistema valida que la selección sea admisible y que existan datos publicados para ella.
6. El sistema consulta el archivo/corte definitivo incorporado y calcula o recupera los indicadores aplicables: frecuencias absolutas y relativas, tasas crudas y específicas, ajustes directo/indirecto e intervalos de confianza según las reglas aprobadas o propuestas (`REQ-F-003` a `REQ-F-008`, `REQ-F-011`). No presenta los intervalos como estadística actual del RNC.
7. El sistema presenta el resultado junto con los criterios usados y la información metodológica necesaria para interpretarlo. La forma exacta debe definirse en el prototipo.

**Alternativas y excepciones**

- **A1. Selección incompleta o incompatible:** el sistema indica qué criterio debe corregirse y conserva, cuando sea posible, la selección válida.
- **A2. Sin datos publicados para la selección:** el sistema informa que no hay resultados disponibles; no inventa ni extrapola valores.
- **A3. Resultado sujeto a una regla de confidencialidad:** el sistema aplica la política de divulgación agregada que se acuerde con el RNC. Hasta entonces se modela como propuesta y no se inventa un umbral de supresión (`Q-007`).
- **A4. No puede calcularse un indicador:** el sistema presenta los indicadores disponibles e informa qué resultado no pudo producirse, según reglas aún por definir para datos incompletos, cero casos y denominadores no disponibles.

**Postcondición**

- Se muestra una respuesta asociada a los criterios solicitados, o una explicación de por qué no puede mostrarse.
- No se exponen datos personales identificables (`REQ-NF-001`).

**Reglas por confirmar antes de cerrar el caso**

- Fórmulas, escala, redondeo y denominadores para tasas (`Q-016`).
- Bandas de edad, pesos de la estándar mundial Segi/Doll y verificación con ejemplo RNC (`Q-003` a `Q-005`); la población ONEI cubana es el denominador de las tasas específicas, no esos pesos.
- Método de ajuste indirecto y población de referencia (`Q-006`).
- Nivel y método de los intervalos, y tratamiento de conteos pequeños/cero (`Q-009`).
- Denominador de la frecuencia relativa y datos faltantes (`Q-018`).
- Conteos pequeños y restricciones de publicación agregada (`Q-007`); los datos preliminares ya están excluidos por la regla de producto (`REQ-F-011`).

### UC-02 — Exportar resultado de consulta

| Campo | Especificación |
|---|---|
| Actor principal | Visitante público |
| Objetivo | Descargar el resultado consultado en un formato utilizable fuera del sitio. |
| Trazabilidad | `REQ-F-009`; relacionado con `REQ-F-001` a `REQ-F-008` y `REQ-NF-001`. |
| Prioridad | Requerida por el Anexo A. |
| Estado | Formatos confirmados; contenido de archivos pendiente. |

**Precondición**

- Hay un resultado disponible de una consulta del visitante.

**Flujo básico**

1. El visitante elige exportar el resultado.
2. El sistema ofrece CSV, Excel y PDF.
3. El visitante selecciona un formato.
4. El sistema genera y entrega el archivo correspondiente a la consulta.

**Alternativa**

- **A1. Error al generar el archivo:** el sistema informa que la descarga no pudo completarse y permite intentarlo de nuevo sin perder los criterios de consulta.

**Postcondición**

- El visitante obtiene un archivo correspondiente al resultado y los criterios consultados.
- La exportación respeta las restricciones de confidencialidad del resultado público.

**Detalle pendiente**

Debe acordarse si cada archivo contiene filtros, fecha/versión de datos, definiciones, fuentes, notas de interpretación y metadatos; también deben definirse la disposición del PDF y los nombres de columnas.

## Construcción del flujo de incorporación de archivos definitivos en StarUML

El sistema interno del RNC ya depuró los registros y entrega archivos definitivos. El prototipo recibe esos archivos y comprueba si puede incorporarlos técnicamente; no corrige casos, resuelve duplicados clínicos ni vuelve a declarar la definitividad (`SRC-RNC-006`). Crear un **Activity Diagram** `ACT-01 Incorporación de archivo definitivo`:

1. Colocar **Initial Node** y **Action** `Recibir archivo definitivo del sistema interno`.
2. Añadir **Action** `Comprobar formato, integridad, cobertura y metadatos` y un **Decision Node**.
3. Desde la decisión trazar `[archivo incompatible]` hacia **Action** `Informar rechazo técnico y motivo`, y terminar esa rama en **Activity Final Node**. Un nuevo envío sería otra ejecución del flujo, nunca una corrección del corte definitivo dentro de este portal.
4. Trazar `[archivo compatible]` hacia **Action** `Registrar identificador, fuente, año, versión de esquema y huella` y después **Action** `Derivar conjunto estadístico sin alterar el archivo`.
5. Añadir **Action** `Registrar grano y capacidades de consulta` y **Action** `Comprobar disponibilidad de población ONEI compatible`; colocar un segundo **Decision Node**.
6. Trazar `[denominador ausente o incompatible]` hacia **Action** `Marcar tasas dependientes como no disponibles`; trazar `[denominador compatible]` hacia **Action** `Marcar tasas compatibles como calculables`.
7. Unir ambas ramas con **Merge Node** y añadir **Action** `Guardar corte definitivo y capacidades`; terminar con **Activity Final Node**. Una falta de población ONEI no descarta automáticamente los conteos del corte.
8. Conectar todas las acciones con **Control Flow**; escribir cada guarda junto al flujo saliente. Añadir **Note**: `Contrato del archivo y serie ONEI pendientes; archivo definitivo inmutable; la política de divulgación se aplica al consultar y exportar`.

Usar dos **Activity Partitions** verticales: `Trabajador autorizado del RNC (rol por validar)` y `Plataforma RNC`. Las calles muestran quién realiza cada acción del flujo propuesto; no confirman permisos ni asignan tareas a doctor encargado o mantenimiento. La decisión de divulgar una combinación agregada ocurre en `ACT-02`, distinta del estado definitivo del archivo. Frecuencia exacta, estructura, método de recepción y reglas ante fallos de transferencia siguen abiertos en `Q-008` y `Q-017`.

## Decisiones de modelado para el informe

- No se dibuja un modelo de casos de uso del negocio todavía: el objetivo inmediato es especificar el sistema público; el flujo de archivo requiere confirmar responsables y reglas antes de modelar el proceso institucional como definitivo.
- El panel administrativo se modela en un diagrama aparte como flujo de prototipo. Un segundo diagrama explicita autenticación, `superadmin` y gestión futura de cuentas por decisión del proyecto; la implementación segura y auditoría productiva pertenecen a una etapa posterior.
- No se incluyen dashboards avanzados, mapas coropléticos, series temporales ni migración como funciones de esta primera versión. La autenticación/roles se especifican como arquitectura objetivo (`REQ-F-014`), sin afirmar que se implementaron en Prácticas II.
- Solo se publican datos definitivos. Las reglas metodológicas y de confidencialidad para datos agregados deben aprobarse.

## Siguientes artefactos

1. Validar estos casos y las preguntas de carga con la tutora/RNC.
2. Completar la descripción de requisitos funcionales y medibles de calidad.
3. Seguir la [guía integral de diagramas en StarUML](guia-diagramas-staruml.md), que incluye actividades, arquitectura, secuencia, clases, entidad-relación y despliegue condicional.

## Fuente metodológica

- `SRC-UNI-001`, *Buenas prácticas de escritura y defensa del trabajo de diploma*, abril de 2026, documento local indicado en [`../../sources/catalogo.md`](../../sources/catalogo.md). Sus recomendaciones se aplican de forma orientativa al informe de Prácticas II.
- Anexo A del proyecto (`SRC-RNC-001`) y línea base [`../05-requisitos/linea-base-practicas-ii.md`](../05-requisitos/linea-base-practicas-ii.md).
