# Guía de diagramas de Prácticas II en StarUML

Estado: GUÍA DE TRABAJO v4; modelos sujetos a validación con tutora y RNC  
Corte: 2026-10-13

## 1. Para qué sirve esta guía

El Anexo A exige documentar diagramas de clases, actividades, arquitectura, secuencia y modelo entidad-relación. Los requisitos del sitio público también justifican un diagrama de casos de uso para explicar sus objetivos de usuario. Esta guía ofrece el inventario; la [secuencia de modelado y las clases completas](metodo-y-clases-staruml.md) y el [plan operativo de dibujo](plan-operativo-diagramas-staruml.md) son las instrucciones vigentes.

No se deben producir todos los tipos de diagramas que ofrece UML. Cada diagrama debe responder una pregunta del diseño, tener trazabilidad a requisitos o entregables y explicarse en el informe. El folleto universitario `SRC-UNI-001` recomienda evitar diagramas decorativos, explicar sus elementos y no usar un diagrama de despliegue si no se conocen las condiciones reales de despliegue.

### Método y evidencia universitaria consultada

La guía docente de Trabajo de Curso de Diseño de Software 2 (curso 2025–26, turno diurno; `SRC-UNI-002`) pide para el corte requisitos, casos de uso, arquitectura candidata y descripción de arquitectura. Para la entrega final añade patrones/principios con diagramas de clases, colaboraciones con secuencia o comunicación, modelos lógico y físico de datos, despliegue y estructura de implementación. Es una pauta de asignatura, no una metodología UML propia de toda la CUJAE. Los ejemplos de DS e Ingeniería de Requisitos consultados muestran particiones/calles en actividades que distribuyen acciones entre participantes y sistema. Aplicamos esa convención a ACT-01 y ACT-02 porque ambos tienen responsabilidades humanas y automatizadas diferenciables.

La notación se contrasta con UML 2.5.1 de OMG, que define particiones de actividad y su representación como calles (`SRC-OMG-UML-001`). No se presenta una costumbre observada en ejemplos estudiantiles como regla institucional universal. Para cada diagrama se anota qué pide la asignatura, qué convención se observa y qué decisión del RNC continúa pendiente.

## 2. Inventario priorizado

| Orden | Diagrama | Prioridad | Para qué responde |
|---|---|---|---|
| 1 | Casos de uso del sistema | Necesario para especificar requisitos y describir consulta pública y flujo del prototipo administrativo. | ¿Quién usa cada área y qué objetivos logra? |
| 2 | Actividades | Expresamente incluido en ENT-05; elaborar proceso de consulta y flujo de archivos. | ¿Qué pasos, decisiones y alternativas componen cada proceso? |
| 3 | Arquitectura de componentes/contexto | Expresamente incluido como arquitectura en ENT-05. | ¿Cuáles son las partes del sistema y cómo intercambian información? |
| 4 | Secuencia | Expresamente incluido en ENT-05; al menos escenario principal de consulta. | ¿Qué mensajes intercambian actor, interfaz y clases para lograr una función? |
| 5 | Dominio y clases de diseño | El modelo de dominio aclara conceptos; el de diseño cumple ENT-05. | ¿Qué conceptos existen y qué responsabilidades, atributos, operaciones y relaciones tiene el software? |
| 6 | Entidad-relación | Expresamente incluido en ENT-05. | ¿Qué datos conserva el modelo y cómo se relacionan? |
| 7 | Despliegue | Condicional. Se prepara cuando se conozcan infraestructura, nodos, protocolos y restricciones de la entidad. | ¿En qué nodos reales se ejecutan los componentes y cómo se comunican? |

El diagrama de casos de uso y las instrucciones iniciales de actividad ya están en [`casos-uso-sistema.md`](casos-uso-sistema.md). Esta guía completa el inventario y normaliza el resto. La secuencia exacta depende de validar requisitos; el modelo físico depende de conocer los archivos y denominadores.

## 3. Organización del proyecto StarUML

En el **Model Explorer**, organiza el modelo con paquetes (Package) y crea los diagramas dentro de ellos. Nombre sugerido:

```text
Plataforma pública RNC
├── 01 Requisitos
│   ├── CU-01 Consulta pública de estadísticas
│   └── CU-02 Flujo administrativo (prototipo)
├── 02 Dominio
│   └── DM-01 Conceptos estadísticos del RNC
├── 03 Procesos
│   ├── ACT-01 Incorporación de archivo definitivo
│   └── ACT-02 Consulta y presentación de estadísticas
├── 04 Arquitectura
│   └── CMP-01 Componentes de la plataforma
├── 05 Interacciones
│   ├── SD-01 Consultar estadísticas
│   ├── SD-02 Incorporar archivo definitivo
│   └── SD-03 Exportar resultado
├── 06 Diseño lógico
│   ├── CD-01 Diseño de la consulta pública
│   ├── CD-02 Diseño de la exportación
│   └── CD-03 Diseño de la incorporación
├── 07 Datos
│   └── ER-01 Modelo entidad-relación
└── 08 Despliegue (pendiente de datos de infraestructura)
    └── DEP-01 Despliegue propuesto
```

Para cada diagrama: seleccionar un paquete en el Model Explorer; usar **Model → Add Diagram → [tipo]**; renombrar el diagrama en el explorador; añadir elementos desde el **Toolbox**; editar nombres con doble clic o `Enter`; crear relaciones desde el elemento de origen hasta el destino. Los nombres exactos de tipos UML aparecen en inglés en la herramienta.

## 4. Casos de uso del sistema — `CU-01` y `CU-02`

Seguir las instrucciones detalladas en [`casos-uso-sistema.md`](casos-uso-sistema.md#construcción-del-diagrama-de-casos-de-uso-en-staruml). El modelo inicial contiene el actor `Visitante público`, el límite `Sitio público de estadísticas del RNC` y los casos `UC-01 Consultar estadísticas` y `UC-02 Exportar resultado de consulta`, unidos con **Association**.

Mantener por separado el caso público y el del panel administrativo. El segundo diagrama representa el prototipo, no una especificación de permisos ni evidencia de que el panel seguro se implemente durante Prácticas II. Usar el actor genérico `Trabajador del RNC` hasta confirmar las competencias del doctor encargado y del personal de mantenimiento.

## 5. Diagramas de actividades — `ACT-01` y `ACT-02`

**Convención para estos dos procesos:** crear un **Activity Diagram** de StarUML y dividirlo en particiones (swimlanes) por responsabilidad. No simular calles con rectángulos ni notas. Usar **Activity Partition** del Toolbox y nombrar cada partición. Poner cada acción dentro de la calle responsable; los flujos cruzan calles cuando cambia la responsabilidad. Incluir nodos inicial/final, decisiones con guardas entre corchetes y fusiones cuando varias ramas retoman un flujo.

Las calles expresan responsabilidad en el proceso propuesto, no certifican cargos, permisos ni delegaciones del RNC. En ACT-01 usar `Trabajador autorizado del RNC (rol por validar)` y `Plataforma RNC`; en ACT-02 usar `Visitante público` y `Plataforma pública RNC`. Son las dos responsabilidades sustentadas por el alcance actual. Si el RNC confirma otros participantes, revisar la partición y trazabilidad antes de agregarlos.

### ACT-01 — Incorporación de archivo definitivo

1. Crear dos calles verticales: `Trabajador autorizado del RNC (rol por validar)` y `Plataforma RNC`.
2. Calle humana: **Initial Node** → `Seleccionar archivo de corte definitivo y declarar referencia de origen` → `Solicitar incorporación`.
3. Calle de plataforma: `Recibir archivo y metadatos declarados` → `Comprobar tipo, codificación, encabezados y orden del contrato observado` → **Decision Node** con guardas `[contrato compatible]` y `[contrato incompatible]`.
4. Rama incompatible: `Mostrar informe técnico de incompatibilidades` → **Activity Final Node**. No corregir datos clínicos ni deducir la semántica de campos.
5. Rama compatible: `Comprobar evidencia declarada del corte definitivo` → decisión `[evidencia insuficiente según regla pendiente]` / `[evidencia suficiente según regla pendiente]`. La primera informa que no puede incorporarse como corte definitivo y termina; la segunda registra el conjunto recibido, comprueba disponibilidad/cobertura de denominadores ONEI y guarda el resultado técnico con avisos. No publica automáticamente.
6. Calle humana: `Revisar resultado de incorporación` → final. Añadir una nota con pendientes de autorización, evidencia de definitividad, unidad por fila, diccionario y retención (`Q-007`, `Q-017`).

El chequeo anterior es estructural, no validación epidemiológica. El sistema no decide si un caso es válido, no elimina duplicados y no reemplaza el proceso del registro.

### ACT-02 — Consulta y presentación de estadísticas

1. Crear dos calles verticales: `Visitante público` y `Plataforma pública RNC`.
2. Calle visitante: **Initial Node** → `Seleccionar filtros disponibles` → `Solicitar consulta`.
3. Calle plataforma: `Validar filtros y disponibilidad del corte` → **Decision Node** con `[filtros inválidos]` / `[filtros válidos]`. La rama inválida muestra el mensaje y termina la ejecución; una nueva solicitud inicia otra consulta con filtros ajustados.
4. Rama válida: `Determinar medidas compatibles con el grano del corte` → decisión `[medida no calculable]` / `[medida calculable]`. La primera informa la causa sin desagregar el archivo ni inferir semántica faltante.
5. Rama calculable: `Obtener conteos y, si están disponibles, denominadores y métodos aprobados` → `Aplicar reglas de divulgación aprobadas` → decisión `[salida autorizada]` / `[salida restringida]`.
6. Rama autorizada: `Mostrar tabla, visualización y metadatos del corte`. Rama restringida: `Informar restricción sin revelar cifras`. Ambas terminan después de responder al visitante.
7. Añadir una nota: grano, denominadores compatibles, métodos y política de celdas pequeñas deben validarse con el RNC. No presentar fórmula o supresión pendiente como regla aprobada.

**Comprobación visual de cada actividad:** todas las acciones están dentro de una calle; el nombre de cada calle identifica una responsabilidad; los flujos entre calles tienen sentido; cada salida de decisión tiene guarda; los finales son alcanzables; no hay roles no confirmados presentados como hechos. Exportar con encabezados de calles legibles.

## 6. Arquitectura de componentes — `CMP-01`

Dibujar `CMP-01` con [las instrucciones del plan operativo](plan-operativo-diagramas-staruml.md#3-cmp-01-componentes-lógicos-de-la-plataforma). Los componentes muestran interfaz pública, consulta, motor estadístico, catálogo de métodos, población ONEI, política de divulgación, exportación, repositorio de cortes definitivos e incorporación propuesta. `VistaConsulta` pertenece a la interfaz; `ServicioConsulta` y `ValidadorConsulta` a consulta; `MotorIndicadores` al motor; `ServicioExportacion` y tres estrategias a exportación; `LectorCortesDefinitivos` realiza `RepositorioCortesDefinitivos`; `LectorPoblacionONEI` realiza `ProveedorPoblacion`. Esta correspondencia enlaza `CMP-01` con `CD-01` y `CD-02`.

Las dependencias de componentes se orientan desde consumidor hacia proveedor. El componente de consulta solo lee cortes definitivos y consulta la política de divulgación; el importador de archivos y el sistema interno RNC no se conectan directamente con la interfaz pública. La exportación recibe un resultado autorizado de la interfaz. Describir en el informe por qué se separan estas responsabilidades y qué regla protege cada límite. No convertir archivos ni futuros servidores en componentes actuales.

## 7. Secuencias — `SD-01`, `SD-02` y `SD-03`

`SD-01 Consultar estadísticas` sigue el [plan operativo](plan-operativo-diagramas-staruml.md#4-sd-01-consultar-estadísticas-definitivas): sus líneas de vida son instancias de las clases de `CD-01` y los mensajes `consultar`, `validar`, `obtenerDefinitivos`, `obtenerCompatible`, `obtenerDefiniciones`, `calcular` y `aplicar` aparecen como operaciones allí. Los fragmentos `alt` separan criterios inválidos, falta de datos/capacidad y resultado autorizado/restringido. Los componentes de `CMP-01` agrupan estas clases; no se usan nombres de componentes como si fueran clases.

`SD-02 Incorporar archivo definitivo` queda como escenario propuesto del prototipo administrativo. Seguir [los mensajes y guardas del plan operativo](plan-operativo-diagramas-staruml.md). Sus líneas de vida son instancias de `VistaIncorporacion`, `ServicioIncorporacion`, `FuenteCorteDefinitivo`, `ValidadorContrato`, `NormalizadorEntrada`, `ProveedorPoblacion` y `AlmacenCortesDefinitivos`, definidas en `CD-03`/`CD-01`. El contrato de entrada y los responsables siguen pendientes (`Q-017`); el diagrama no atribuye corrección de casos, nueva aprobación de definitividad ni divulgación automática.

`SD-03 Exportar resultado` sigue [el diseño de exportación](metodo-y-clases-staruml.md#cd-02--exportación-y-variación-de-formato): `ServicioExportacion` selecciona una realización de `ExportadorResultado` para CSV, Excel o PDF. El parámetro es el `ResultadoConsulta` ya autorizado. La estrategia elegida produce el archivo; no consulta datos preliminares ni modifica las cifras.

## 8. Clases de dominio y de diseño — `DM-01`, `CD-01`, `CD-02` y `CD-03`

Usar la [especificación completa](metodo-y-clases-staruml.md#dm-01--modelo-conceptual-del-dominio). `DM-01` contiene conceptos del RNC y ONEI sin operaciones de software. `CD-01` modela la consulta con atributos tipados, operaciones, dependencias, asociaciones y multiplicidades. `CD-02` modela la variación de formato con interfaz y tres realizaciones. `CD-03` modela incorporación con un puerto de origen y otro de escritura, y se contrasta con `SD-02`. El esquema físico de datos pertenece a `ER-01`.

## 9. Modelo entidad-relación — `ER-01`

El modelo ER de ENT-05 describe entidades, claves y cardinalidades. No equivale al diagrama de clases de diseño. StarUML incluye un tipo **ER Diagram**: dentro del paquete `07 Datos`, elegir **Model → Add Diagram → ER Diagram** y nombrar el diagrama `ER-01 Modelo lógico de datos`. En la paleta usar **Entity**, añadir columnas y marcar la clave primaria; crear relaciones **One-to-One**, **One-to-Many** o **Many-to-Many** y configurar la cardinalidad de cada extremo. Si el menú ER Diagram no aparece en la versión instalada, revisar **Tools → Extension Manager** y la extensión oficial *Entity Relationship DataModel Generation*; como alternativa temporal, crear un Class Diagram y anotar `PK`/`FK`, indicando que es una representación provisional.

Para el primer modelo lógico, usa solo conceptos respaldados, marcando atributos/relaciones abiertas:

- `CasoTumor` o `RegistroTumor` como unidad estadística por precisar; no fusionar automáticamente persona y tumor.
- `Periodo` (año).
- `Territorio` (provincia; municipio solo si se confirma que se publicará).
- `Sexo`.
- `GrupoEdad` y `NomencladorEdad` (bandas clásicas quinquenales de 0–4 a 85+ y agrupaciones nuevas sin alterar las clásicas; reglas de creación y vigencia por definir, `SRC-RNC-005`).
- `LocalizacionCancer` (clasificación y versión por precisar).
- `PoblacionDenominadorONEI` (territorio, periodo, sexo, edad simple y población residente usada como denominador).
- `PoblacionEstandar` (estándar mundial Segi/Doll, fuente y versión) y `PesoEstandar` (quinquenio y peso; 18 entradas que suman 100 000); son distintos de la población ONEI cubana denominadora.
- `ConteoAgregadoPublicado` o una entidad agregada equivalente solo si los archivos recibidos ya vienen agregados.
- `VersionConjuntoDatos`/`Publicacion` para registrar corte, estado y metadatos si el proceso lo exige.

No dibujar dos modelos alternativos en una misma solución. Primero aclarar el grano de entrada: microdatos por caso/tumor o agregados. Después decidir si el sistema conserva microdatos o consume archivos agregados. No poner nombres, identificadores personales o campos sensibles en el esquema público. Las cardinalidades y claves se dejan como propuesta hasta conocer el contrato de entrada y denominadores (`Q-017`, `Q-016`).

## 10. Despliegue — `DEP-01` solo si se valida infraestructura

El Anexo pide arquitectura, pero el folleto advierte que un diagrama de despliegue debe ajustarse a condiciones reales. La web pública normalmente implica cliente y servicio remoto; aun así, no se inventarán servidores, nube, sistema operativo, puertos ni topología del RNC.

Cuando se obtenga la información, crear **Deployment Diagram** llamado `DEP-01 Despliegue propuesto` con:

- **Node** para navegador/dispositivo cliente.
- Nodos nombrados con los servidores/servicios reales o propuestos y marcados explícitamente como propuesta.
- **Artifact** para aplicación web, servicio API, módulo de cálculo y almacenamiento que se desplieguen en cada nodo.
- **Communication Path** entre nodos y etiqueta de protocolo solo cuando esté aprobado (por ejemplo, no asumir HTTP/HTTPS específico sin la decisión de seguridad/despliegue).
- Notas sobre recursos mínimos, ubicación, respaldo, acceso y restricciones institucionales cuando se conozcan.

Si esas condiciones no se conocen al cierre, documentar en el informe que el despliegue detallado queda fuera del diseño validable de esta práctica y consultar a la tutora cómo satisfacer el punto «arquitectura» con la vista de componentes. No rellenarlo con infraestructura ficticia.

## 11. Diagramas que no se crearán por ahora

- **Casos de uso del negocio:** solo añadir si el análisis del proceso institucional y sus reglas llega a ser parte central del trabajo y se validan actores externos/objetivos de negocio. No poner empleados como actores del negocio por defecto.
- **State Machine:** solo si se definen estados técnicos y transiciones relevantes de incorporación/publicación con responsables y reglas confirmados; no introducir un estado de corrección del archivo definitivo.
- **Communication, Timing, Interaction Overview, Object, Composite Structure:** no aportan evidencia necesaria al alcance conocido; considerar solo si un requisito complejo lo justifica.
- **BPMN:** no duplicar el flujo de actividad UML; usarlo solo si la tutora/RNC necesita explícitamente notación de proceso de negocio.
- **Mapa de sitio y wireframes:** son artefactos UX, no diagramas UML. Se elaboran como entregable de prototipos, en la herramienta de diseño acordada.

## 12. Criterios de calidad y entrega

Antes de dar un diagrama por terminado:

1. Identificar el requisito/entregable que justifica el artefacto.
2. Verificar que actores, componentes, clases y datos usan los mismos nombres en todos los modelos.
3. Señalar supuestos no confirmados con **Note** o en el texto del informe.
4. Revisar semántica y dirección de cada relación UML, multiplicidad y guarda.
5. Evitar cruces, elementos sin nombre, texto ilegible, actores inventados y responsabilidades duplicadas.
6. Exportar desde StarUML con tamaño legible y numerar/citar la figura en el informe.
7. Explicar antes o después de la figura qué comunica y qué decisión permite tomar; no pegar la figura sin análisis.
8. Mantener el archivo fuente `.mdj` y una exportación de cada versión revisada.

## Referencias de herramienta

- Documentación oficial StarUML, [Use Case Diagram](https://docs.staruml.io/v3/working-with-diagrams/use-case-diagram), [Activity Diagram](https://docs.staruml.io/v5/working-with-uml-diagrams/activity-diagram), [Sequence Diagram](https://docs.staruml.io/v3/working-with-diagrams/sequence-diagram), [Component Diagram](https://docs.staruml.io/v3/working-with-diagrams/component-diagram), [Deployment Diagram](https://docs.staruml.io/v3/working-with-diagrams/deployment-diagram).
- Documentación oficial StarUML, [Entity-Relationship Diagram](https://docs.staruml.io/v3/working-with-diagrams/entity-relationship-diagram) y [registro de extensiones](https://staruml.io/extensions/).
- `SRC-UNI-001`, guía universitaria local de escritura/defensa, recomendaciones sobre requisitos, artefactos, legibilidad, arquitectura y despliegue.
- `ENT-05` del Anexo A, transcrito en [`../05-requisitos/linea-base-practicas-ii.md`](../05-requisitos/linea-base-practicas-ii.md).
