# Método de modelado y clases para los diagramas del RNC

Estado: propuesta de diseño revisable, 2026-10-06. Base: `SRC-UNI-001`, `SRC-RNC-001` a `SRC-RNC-007`, [línea base de requisitos](../05-requisitos/linea-base-practicas-ii.md) y [arquitectura evolutiva](arquitectura-evolutiva-rnc.md). Este documento indica **qué dibujar** en StarUML y qué decisiones aún requieren datos del RNC.

## Criterio académico comprobado

La guía local *Buenas prácticas para la escritura y defensa del Trabajo de Diploma* (abril de 2026) es orientativa. La pauta de Diseño de Software 2 consultada (`SRC-UNI-002`) sí detalla entregables de corte y final: casos de uso y requisitos; arquitectura; patrones con diagramas de clases; secuencias o colaboración; modelos lógico/físico; y despliegue. Los ejemplos locales de DS/IR muestran swimlanes en actividades repartidas entre participantes. UML 2.5.1 de OMG es la referencia normativa de notación. Estos materiales no prescriben una metodología única para toda la CUJAE; la secuencia de trabajo de abajo es una propuesta trazable y la rúbrica vigente aún debe cotejarse con la tutora.

| Paso | Artefacto | Pregunta y enlace con el siguiente |
|---|---|---|
| 1 | Requisitos y reglas del negocio | ¿Qué está confirmado y qué queda abierto? Cada elemento se marca con un `REQ-*` o una pregunta `Q-*`. |
| 2 | `DM-01` modelo conceptual del dominio | ¿Qué conceptos existen en el RNC/ONEI? No contiene servicios, métodos de software ni tablas físicas. |
| 3 | `CU-01`/`CU-02` y fichas de casos de uso | ¿Qué objetivos logran actores externos? Sus escenarios originan actividades y secuencias. |
| 4 | `ACT-02`/`ACT-01` | ¿Qué tareas, decisiones y caminos alternativos ejecuta cada caso? Guardas respaldadas por reglas. |
| 5 | `SD-01` y, cuando se detalle, secuencias de exportación/entrada | ¿Quién envía cada mensaje? Cada mensaje de software debe corresponder a una operación de clase o interfaz. |
| 6 | `CD-01` clases de diseño y `CMP-01` componentes | ¿Quién asume cada responsabilidad y a través de qué contrato se comunican las partes? Agrupar por paquetes/capas. |
| 7 | `ER-01` y `DEP-01` | ¿Qué datos se persisten y dónde corre la solución? Se concretan con plantilla de datos e infraestructura reales. |

No forzar un patrón en todos los dibujos: casos de uso y actividades describen requisitos y procesos; los patrones de diseño se justifican principalmente en clases/secuencias, y los patrones arquitectónicos en componentes, paquetes y despliegue. Conservar los mismos nombres y operaciones entre vistas.

El orden de la tabla organiza el trabajo, pero `SD-01` y `CD-01` se refinan juntos: al descubrir un mensaje se asigna una operación a la clase responsable; al cambiar una firma se corrige la secuencia. `CMP-01` se revisa contra ambas vistas.

## `DM-01` — modelo conceptual del dominio

Crear un **Class Diagram** en `02 Dominio`, nombre `DM-01 Conceptos estadísticos del RNC`. Usar clases **sin compartimentos de operaciones**. Es un vocabulario, no un esquema de base de datos ni un diseño de código.

| Concepto | Significado documentado | Atributos conceptuales seguros |
|---|---|---|
| `CorteDefinitivo` | Conjunto consultable internamente derivado de un archivo definitivo; la divulgación del resultado agregado se evalúa aparte. | `identificador`, `fuente`, `huella`, `año` por definir. |
| `Territorio` | Cuba, provincia o municipio; las series ONEI se entregarán para esos niveles. | `nivel`, `nombre/código` por validar. |
| `PoblacionONEI` | Denominador oficial por año, territorio, sexo y edad simple. | `año`, `sexo`, `edadSimple`, `cantidad`. |
| `GrupoEdad` | Intervalo etario, incluido 0–4 y el abierto 85+. | `edadInicial`, `edadFinal` opcional. |
| `AgrupacionEdad` | Conjunto clásico fijo o agrupación nueva seleccionada. | `tipo` (clásica/personalizada), `nombre` por definir. |
| `PoblacionEstandar` | Tabla mundial Segi/Doll de IARC/CI5 usada como referencia para ASR(W); distinta de `PoblacionONEI`. | `nombre = Segi/Doll`, `fuente = IARC/CI5`, `totalPesos = 100000`, `versión/referencia`. |
| `PesoEstandar` | Peso asignado a un quinquenio clásico de la estándar mundial. | `grupoEdad`, `peso` (entero). |
| `LocalizacionCancer` | Dimensión de consulta; nomenclador y versión por confirmar. | `código`, `nombre` por validar. |

Añadir `CorteDefinitivo` — `Territorio` mediante **Association** con nombre `abarca`; no fijar multiplicidades de esa relación antes de conocer el grano del corte. Añadir `PoblacionONEI` — `Territorio` con nombre `corresponde a`: en el extremo `Territorio` escribir `1`, en el extremo `PoblacionONEI` escribir `0..*`. Cada observación ONEI es de un territorio y un territorio tiene muchas observaciones a lo largo de años, edades y sexos. Añadir `AgrupacionEdad` — `GrupoEdad` como **Composition**, con `1` en `AgrupacionEdad` y `1..*` en `GrupoEdad`: en este modelo cada tramo pertenece a una definición de agrupación. Poner la nota `Bandas clásicas 0–4, 5–9, …, 85+; no se editan al crear una agrupación nueva` (`REQ-F-013`). Añadir `PoblacionEstandar` ◆— `PesoEstandar` como **Composition**, con `1` en el extremo `PoblacionEstandar` y `18` en el extremo `PesoEstandar`; cada peso refiere a uno de los 18 quinquenios clásicos y el total es 100 000 (`SRC-IARC-CI5-WORLD-2026`).

No añadir aún `Paciente`, `CasoTumor` ni `ConteoAgregadoPublicado`: el archivo entregado puede tener microdatos o agregados (`Q-017`). No unir `PoblacionEstandar` con `PoblacionONEI` como si fueran la misma fuente. La tabla mundial de pesos ya está documentada; falta comprobar con un resultado RNC que se aplica la misma edición, regla de redondeo y tratamiento de edades desconocidas (`Q-004`, `Q-005`).

## `CD-01` — clases de diseño de la consulta

Crear otro **Class Diagram** en `06 Diseño lógico`, nombre `CD-01 Diseño de la consulta pública`. Mostrar los compartimentos de **atributos y operaciones**. Distribuir los elementos en paquetes `Presentación`, `Aplicación`, `Dominio` y `Acceso a datos`. Son responsabilidades propuestas, independientes del framework. Los tipos `Entero`, `Decimal`, `Texto`, `Archivo` y `Lista<T>` expresan contratos lógicos; al implementar se traducirán al lenguaje elegido.

| Paquete y clasificador | Atributos a escribir en el compartimento central | Operaciones a escribir en el compartimento inferior |
|---|---|---|
| Presentación · `VistaConsulta` | `-resultadoActual: ResultadoConsulta [0..1]` (solo salida autorizada) | `+solicitarConsulta(criterios: CriteriosConsulta)`; `+solicitarExportacion(formato: FormatoExportacion)`; `+mostrarResultado(resultado: ResultadoConsulta)`; `+mostrarAviso(mensaje: Texto)` |
| Aplicación · `ServicioConsulta` | — | `+consultar(criterios: CriteriosConsulta): RespuestaConsulta` |
| Aplicación · `ValidadorConsulta` | — | `+validar(criterios: CriteriosConsulta): ResultadoValidacion` |
| Aplicación · `ResultadoValidacion` | `+esValido: Booleano`; `+errores: Lista<Texto>` | — |
| Aplicación · `RespuestaConsulta` | `+estado: EstadoRespuesta`; `+mensajes: Lista<Texto>` | — |
| Dominio · `CriteriosConsulta` | `+año: Entero`; `+sexo: Sexo`; `+localizacion: Texto`; `+indicadoresSolicitados: Lista<TipoIndicador>` | — |
| Dominio · `AgrupacionEdad` | `+tipo: TipoAgrupacion`; `+nombre: Texto` | — |
| Dominio · `GrupoEdad` | `+edadInicial: Entero`; `+edadFinal: Entero [0..1]` | `+contiene(edad: Entero): Booleano` |
| Dominio · `DatosBaseConsulta` | `+idCorte: Texto`; `+grano: Texto`; `+capacidades: Lista<Texto>` | — |
| Dominio · `DatosPoblacion` | `+edicionONEI: Texto`; `+tipoPoblacion: Texto`; `+cobertura: Texto` | — |
| Dominio · `DefinicionIndicador` | `+id: Texto`; `+version: Texto`; `+unidad: Texto`; `+universo: Texto`; `+reglaCalculo: Texto`; `+estandar: Texto [0..1]`; `+fuenteMetodo: Texto`; `+redondeo: Texto` | — |
| Dominio · `ResultadoInterno` | `+idCorte: Texto`; `+edicionONEI: Texto [0..1]`; `+versionesMetodos: Lista<Texto>`; `+avisos: Lista<Texto>` | — |
| Dominio · `ResultadoConsulta` | `+estadoPublicacion: Texto` | — |
| Dominio · `ProcedenciaResultado` | `+idCorte: Texto`; `+edicionONEI: Texto [0..1]`; `+tipoPoblacion: Texto [0..1]`; `+definicionesIndicadores: Lista<Texto>`; `+estandares: Lista<Texto>`; `+versionPolitica: Texto` | — |
| Dominio · `ValorIndicador` | `+tipo: TipoIndicador`; `+valor: Decimal`; `+unidad: Texto` | — |
| Dominio · `MotorIndicadores` | — | `+calcular(datos: DatosBaseConsulta, poblacion: DatosPoblacion [0..1], definiciones: Lista<DefinicionIndicador>, criterios: CriteriosConsulta): ResultadoInterno` |
| Aplicación · `PoliticaDivulgacion` **Interface** | — | `+aplicar(interno: ResultadoInterno, criterios: CriteriosConsulta): ResultadoConsulta` |
| Aplicación · `CatalogoMetodologia` **Interface** | — | `+obtenerDefiniciones(criterios: CriteriosConsulta): Lista<DefinicionIndicador>` |
| Acceso a datos · `RepositorioCortesDefinitivos` **Interface** | — | `+obtenerDefinitivos(criterios: CriteriosConsulta): DatosBaseConsulta` |
| Acceso a datos · `LectorCortesDefinitivos` | — | `+obtenerDefinitivos(criterios: CriteriosConsulta): DatosBaseConsulta` |
| Acceso a datos · `ProveedorPoblacion` **Interface** | — | `+obtenerCompatible(criterios: CriteriosConsulta): DatosPoblacion [0..1]`; `+comprobarCobertura(conjunto: ConjuntoCanonico): CoberturaPoblacion` |
| Acceso a datos · `LectorPoblacionONEI` | — | `+obtenerCompatible(criterios: CriteriosConsulta): DatosPoblacion [0..1]`; `+comprobarCobertura(conjunto: ConjuntoCanonico): CoberturaPoblacion` |

`Sexo`, `TipoIndicador`, `TipoAgrupacion` y `EstadoRespuesta` pueden dibujarse como **Enumeration** si se conocen sus literales aprobados; por ahora escribirlos como tipos. `DatosBaseConsulta` es una respuesta lógica de lectura y **no afirma** si el archivo de origen trae microdatos o agregados. `DatosPoblacion` identifica la edición ONEI que se alinea con el estrato consultado. `DefinicionIndicador` identifica las reglas que producen cada cifra; su lista no convierte automáticamente una regla sin validar en configurable por el visitante. `ResultadoInterno` contiene cálculos todavía no divulgables; **nunca** se entrega a `VistaConsulta` ni a los exportadores. `PoliticaDivulgacion` transforma o restringe esos cálculos y solo entonces se crea `ResultadoConsulta`. `ProcedenciaResultado` identifica las versiones empleadas por los distintos indicadores de la misma consulta; no supone un método único para todos. `RespuestaConsulta` distingue resultado disponible, filtros inválidos y ausencia de datos. Los intervalos de confianza se añadirán a `ValorIndicador` al fijarse nivel y método (`Q-009`).

### Relaciones exactas de `CD-01`

1. `CriteriosConsulta` — `AgrupacionEdad`: **Association** `usa`, `1` en el extremo de `AgrupacionEdad` y `0..*` en el de `CriteriosConsulta`. Cada consulta usa una agrupación; una agrupación puede reutilizarse.
2. `CriteriosConsulta` — `Territorio`: **Association** `selecciona`, `1` en `Territorio` y `0..*` en `CriteriosConsulta`. Si no se importa `Territorio` del modelo de dominio al de diseño, representar `territorio: TerritorioRef` como atributo en `CriteriosConsulta`, **sin duplicar** ambas opciones.
3. `AgrupacionEdad` ◆— `GrupoEdad`: **Composition**; rombo negro en `AgrupacionEdad`, multiplicidades `1` y `1..*` como en `DM-01`.
4. `RespuestaConsulta` ◆— `ResultadoConsulta`: **Composition**; rombo negro en `RespuestaConsulta`, `1` en `RespuestaConsulta` y `0..1` en `ResultadoConsulta`. Una respuesta válida con cifras contiene un resultado; una respuesta de error o ausencia no.
5. `ResultadoConsulta` ◆— `ValorIndicador`: **Composition**; rombo negro en `ResultadoConsulta`, multiplicidades `1` y `0..*`. Puede existir un resultado autorizado que solo informe indicadores indisponibles, sin cifras.
6. `ResultadoConsulta` ◆— `ProcedenciaResultado`: **Composition**; rombo negro en `ResultadoConsulta`, `1` en ambos extremos. Cada salida autorizada lleva un registro estructurado de procedencia y política.
7. `ResultadoConsulta` — `CriteriosConsulta`: **Association** `corresponde a`, `1` en `CriteriosConsulta` y `0..*` en `ResultadoConsulta`. Así puede reproducirse qué selección originó cada resultado; la persistencia de resultados históricos aún no está definida.
8. `LectorCortesDefinitivos` → `RepositorioCortesDefinitivos` y `LectorPoblacionONEI` → `ProveedorPoblacion`: **Interface Realization**, triángulo hueco hacia cada interfaz. Son adaptadores lógicos; almacenamiento y formato exactos se decidirán con los archivos.
9. `VistaConsulta` → `ServicioConsulta`; `ServicioConsulta` → `ValidadorConsulta`, `RepositorioCortesDefinitivos`, `ProveedorPoblacion`, `CatalogoMetodologia`, `MotorIndicadores` y `PoliticaDivulgacion`: **Dependency** desde quien usa hacia el proveedor. Estas flechas representan llamadas, no cardinalidades de datos persistidos. Repartir en `CD-01a Orquestación` si la figura se recarga.
10. `MotorIndicadores` → `DatosBaseConsulta`, `DatosPoblacion` y `DefinicionIndicador`; `PoliticaDivulgacion` → `ResultadoInterno` y `ResultadoConsulta`: **Dependency** de uso de tipos. Pueden omitirse en la figura impresa si las firmas ya expresan el contrato.

Si la herramienta permite reutilizar `Territorio` de `DM-01`, no crear una segunda clase `Territorio` con distinto significado. En una figura impresa, priorizar legibilidad: dividir `CD-01` en `CD-01a Orquestación` y `CD-01b Modelo de consulta` si quedan cruces o texto diminuto; conservar los mismos elementos del proyecto StarUML.

### Patrón y asignación de responsabilidades

`ServicioConsulta` coordina el caso de uso: valida criterios y grano, lee **solo cortes definitivos**, obtiene denominadores ONEI y definiciones versionadas, pide el cálculo y aplica la política de divulgación antes de responder. Si no existe denominador compatible, el motor puede producir conteos y avisar que las tasas no se calcularon. `RepositorioCortesDefinitivos` y `ProveedorPoblacion` aíslan la consulta del formato de almacenamiento o intercambio; los importadores Excel/CSV no realizan el contrato de lectura. El motor concentra cálculos; la política concentra reglas de publicación. La propuesta concreta de arquitectura está en [arquitectura evolutiva](arquitectura-evolutiva-rnc.md). Estas decisiones se comprueban con `CD-01` y `SD-01`; no presentar la mera existencia de capas o interfaces como prueba de que se aplicó un patrón concreto del curso.

## `CD-02` — exportación y variación de formato

Crear **Class Diagram** `CD-02 Diseño de la exportación`, porque CSV, Excel y PDF son tres variantes confirmadas (`REQ-F-009`). Aquí sí se puede justificar un **Strategy** para elegir un generador por formato sin incorporar tres rutas de escritura en `ServicioExportacion`.

| Clasificador | Operaciones |
|---|---|
| `ServicioExportacion` | `+exportar(resultado: ResultadoConsulta, formato: FormatoExportacion): Archivo` |
| `ExportadorResultado` **Interface** | `+generar(resultado: ResultadoConsulta): Archivo` |
| `ExportadorCSV` | `+generar(resultado: ResultadoConsulta): Archivo` |
| `ExportadorExcel` | `+generar(resultado: ResultadoConsulta): Archivo` |
| `ExportadorPDF` | `+generar(resultado: ResultadoConsulta): Archivo` |

1. Crear **Interface Realization** desde cada `ExportadorCSV`, `ExportadorExcel` y `ExportadorPDF` hacia `ExportadorResultado` (línea discontinua, triángulo hueco hacia la interfaz).
2. Crear **Dependency** `ServicioExportacion` → `ExportadorResultado`, etiquetada `selecciona según formato`. Si se define un registro/fábrica de estrategias durante implementación, añadirlo entonces; no dibujar una fábrica sin requisito o diseño confirmado.
3. Crear **Dependency** `VistaConsulta` → `ServicioExportacion`. Dibujar `VistaConsulta` como referencia a la clase ya definida en `CD-01`. Crear **Dependency** de cada exportador a `ResultadoConsulta` para mostrar la entrada común, o dejarlo indicado por la firma si la figura se recarga.
4. Añadir una nota: `Los tres formatos exportan el mismo resultado autorizado e identificador de corte. Contenido exacto y diseño PDF pendientes.`

Crear una secuencia breve `SD-03 Exportar resultado`: `Visitante público → VistaConsulta: solicitarExportacion(formato)`; `VistaConsulta → ServicioExportacion: exportar(resultado, formato)`; `ServicioExportacion → ExportadorResultado: generar(resultado)`; respuesta `Archivo`; `VistaConsulta → Visitante público: entregarArchivo`. En la línea de vida de la estrategia usar `exportador:ExportadorResultado`; la implementación concreta depende del formato. Esta secuencia permite comprobar que la selección no altera el resultado ya autorizado.

## `CD-03` — incorporación de datos definitivos

Crear **Class Diagram** `CD-03 Diseño de la incorporación`, dentro de `06 Diseño lógico`. Reutilizar la interfaz `ProveedorPoblacion` de `CD-01` como elemento del mismo modelo; no crear otra con igual nombre. Este diagrama define contratos lógicos para `SD-02`, sin fijar columnas, datos personales, base de datos ni mecanismo de entrega (`Q-017`).

| Paquete y clasificador | Atributos | Operaciones |
|---|---|---|
| Presentación · `VistaIncorporacion` | — | `+solicitarIncorporacion(referencia: ReferenciaEntrada)`; `+mostrarInforme(resultado: ResultadoIncorporacion)` |
| Aplicación · `ServicioIncorporacion` | — | `+incorporar(referencia: ReferenciaEntrada): ResultadoIncorporacion` |
| Aplicación · `ValidadorContrato` | `+versionContrato: Texto` | `+validar(paquete: PaqueteDefinitivo): ResultadoValidacionArchivo` |
| Aplicación · `ResultadoValidacionArchivo` | `+compatible: Booleano`; `+errores: Lista<Texto>` | — |
| Aplicación · `NormalizadorEntrada` | — | `+derivar(paquete: PaqueteDefinitivo): ConjuntoCanonico` |
| Aplicación · `ResultadoIncorporacion` | `+estado: Texto`; `+idCorte: Texto [0..1]`; `+mensajes: Lista<Texto>` | — |
| Dominio · `PaqueteDefinitivo` | `+idExterno: Texto`; `+periodo: Texto`; `+fuente: Texto`; `+estadoOrigen: Texto`; `+formato: Texto`; `+versionEsquema: Texto`; `+huella: Texto` | — |
| Dominio · `ConjuntoCanonico` | `+idCorte: Texto`; `+grano: Texto`; `+capacidades: Lista<Texto>`; `+versionEsquema: Texto`; `+huellaOrigen: Texto` | — |
| Dominio · `CoberturaPoblacion` | `+edicionONEI: Texto [0..1]`; `+indicadoresConDenominador: Lista<TipoIndicador>`; `+avisos: Lista<Texto>` | — |
| Acceso a datos · `FuenteCorteDefinitivo` **Interface** | — | `+obtenerPaquete(referencia: ReferenciaEntrada): PaqueteDefinitivo` |
| Acceso a datos · `LectorArchivoDefinitivo` | — | `+obtenerPaquete(referencia: ReferenciaEntrada): PaqueteDefinitivo` |
| Acceso a datos · `AlmacenCortesDefinitivos` **Interface** | — | `+guardar(conjunto: ConjuntoCanonico, cobertura: CoberturaPoblacion): Texto` |
| Acceso a datos · `PersistenciaCortesDefinitivos` | — | `+guardar(conjunto: ConjuntoCanonico, cobertura: CoberturaPoblacion): Texto` |

`ReferenciaEntrada` es un tipo opaco que identifica la entrada seleccionada: su forma dependerá del mecanismo acordado. El contenido del paquete no se dibuja como atributo detallado; se transporta bajo el contrato `PaqueteDefinitivo` y se protege según las reglas del RNC. `NormalizadorEntrada` **deriva** la representación estadística y registra procedencia; no corrige casos ni cambia la fuente definitiva. `CoberturaPoblacion` registra qué tasas tienen denominador compatible, sin convertir su falta en rechazo del corte. `AlmacenCortesDefinitivos` escribe y `RepositorioCortesDefinitivos` de `CD-01` lee: son puertos distintos aunque una implementación futura pueda compartir almacenamiento.

### Relaciones exactas de `CD-03`

1. `LectorArchivoDefinitivo` → `FuenteCorteDefinitivo` y `PersistenciaCortesDefinitivos` → `AlmacenCortesDefinitivos`: **Interface Realization**, triángulo hueco hacia la interfaz. Un origen distinto incorporará otra realización de `FuenteCorteDefinitivo`.
2. `VistaIncorporacion` → `ServicioIncorporacion`: **Dependency**. `ServicioIncorporacion` → `FuenteCorteDefinitivo`, `ValidadorContrato`, `NormalizadorEntrada`, `ProveedorPoblacion` y `AlmacenCortesDefinitivos`: cinco **Dependency** desde cliente hacia proveedor. La dirección corresponde al orden de mensajes en `SD-02`.
3. `ConjuntoCanonico` → `PaqueteDefinitivo`: **Dependency** con etiqueta `derivado de`; su huella permite rastrear el origen. No usar **Composition** entre ambos: la política de conservación del archivo original no está decidida.
4. `ResultadoIncorporacion` — `ConjuntoCanonico`: **Association** opcional solo si se decide exponer el conjunto a la interfaz interna. En el modelo inicial usar `idCorte` y no dibujar esa asociación: el informe técnico no necesita transportar el conjunto.

Colocar una **Note** junto al servicio: `Solo acepta origen declarado definitivo y contrato técnico compatible; registra huella, grano y capacidades. La falta de población ONEI limita tasas, no el conteo definitivo. El acceso y conservación del archivo esperan política RNC.` Si el dibujo queda denso, dividirlo en dos vistas del mismo modelo (`CD-03a Puertos de entrada` y `CD-03b Persistencia y cobertura`).

## Reglas de construcción en StarUML

1. En **Model Explorer**, crear paquetes y dentro de cada uno **Class Diagram**. Arrastrar **Class**, **Interface**, **Package** y, solo cuando proceda, **Enumeration** desde el Toolbox.
2. Seleccionar una clase y añadir atributos y operaciones con el menú contextual **Add → Attribute/Operation** o la edición rápida de la versión instalada. Escribir visibilidad, nombre y tipo (`+consultar(criterios: CriteriosConsulta): ResultadoConsulta`). Mostrar ambos compartimentos en la figura.
3. Para una relación estructural usar **Association** y editar nombre, navegabilidad y multiplicidad de **cada extremo** en la barra de propiedades o con doble clic sobre el extremo. Una asociación no equivale a una llamada puntual.
4. Para propiedad exclusiva del todo usar **Composition** y colocar el rombo en el todo. Para uso puntual usar **Dependency** (cliente → proveedor). Para implementar una interfaz usar **Interface Realization** (clase concreta → interfaz). Evitar agregación blanca si no se puede justificar su semántica.
5. Para cada operación de `SD-01`/`SD-02`/`SD-03`, localizar la operación homónima en `CD-01`/`CD-03`/`CD-02`; corregir el diagrama que discrepe. En particular: `consultar`, `validar`, `obtenerDefinitivos`, `obtenerPaquete`, `derivar`, `comprobarCobertura`, `guardar`, `calcular`, `exportar` y `generar`.
6. Exportar la figura legible y explicar en el informe las responsabilidades, dependencias y decisión de diseño que evidencia. Una clase vacía o una colección de flechas sin multiplicidad cuando esta se conoce no constituye un diseño suficiente.

La notación de asociación, composición, dependencia y realización se fundamenta en la [especificación UML de OMG](https://www.omg.org/spec/UML/2.5.1/PDF). Los controles de StarUML para atributos, operaciones, multiplicidades y realización figuran en su [documentación oficial de diagramas de clases](https://docs.staruml.io/working-with-uml-diagrams/class-diagram).

## Comprobación de coherencia entre todos los diagramas

| Regla confirmada | Dónde debe verse |
|---|---|
| Consulta pública sin cuenta | `CU-01` actor `Visitante público`; `ACT-02` y `SD-01` no incluyen autenticación. |
| Solo cortes definitivos y resultados públicos autorizados | `ACT-01` recibe archivos definitivos; `SD-01` llama `obtenerDefinitivos`, calcula un `ResultadoInterno` y pasa por `PoliticaDivulgacion`; `CD-01` distingue `RepositorioCortesDefinitivos` de `ResultadoConsulta`; `CMP-01` separa incorporación de consulta pública. |
| Quinquenios clásicos y agrupaciones adicionales | `DM-01`/`CD-01` distinguen `AgrupacionEdad` y `GrupoEdad`; `CU-01` lo describe en la ficha del caso y `ACT-02` en la selección de filtros. |
| ONEI por edad simple, sexo y territorio | `DM-01` define `PoblacionONEI`; `ER-01` espera el archivo para claves y grano; el motor recibe denominadores compatibles. |
| Exportación CSV/Excel/PDF | `CU-01` caso `Exportar`; `CD-02` tres realizaciones de la estrategia; `SD-03` exporta el resultado autorizado. |
| Panel interno prototipado | `CU-02`, `ACT-01`, `CD-03` y `SD-02` expresan recepción, comprobación técnica y registro de capacidades; columnas y ER físico esperan contrato de archivos. |

### Cuestiones que bloquean precisión, no el dibujo conceptual

- `Q-003`: creación, cobertura y vigencia de agrupaciones nuevas.
- `Q-004`, `Q-005`: cotejo numérico de la estándar mundial con RNC; `Q-006`, `Q-009`: ajuste indirecto e intervalos.
- `Q-016`, `Q-017`: estructura/versiones ONEI, plantilla y grano de archivos RNC.
- `Q-007`, `Q-017`: política de divulgación agregada y responsables de incorporación del archivo ya definitivo.
- Rúbrica/materiales de las asignaturas: pueden exigir otros estereotipos o un orden específico; ajustar el modelo cuando se disponga de ellos, sin atribuirlos ahora a la CUJAE.
