# Diagramas del informe: instrucciones operativas para StarUML

Estado: GUIÓN DE DIBUJO; revisión 2026-10-13. Los elementos marcados «propuesta» representan el diseño actual y deben revisarse después de recibir los archivos y reglas del RNC. Fuente de alcance: `SRC-RNC-001`; buena práctica de documentación: `SRC-UNI-001`; requisitos: [`línea base`](../05-requisitos/linea-base-practicas-ii.md); decisiones: [arquitectura evolutiva](arquitectura-evolutiva-rnc.md).

## Preparación del archivo

1. En StarUML, crear un proyecto nuevo y guardarlo como `RNC_Practicas_II.mdj` dentro de `docs/06-arquitectura/`.
2. En **Model Explorer**, crear paquetes `01 Requisitos`, `02 Dominio`, `03 Procesos`, `04 Arquitectura`, `05 Interacciones`, `06 Diseño lógico` y `07 Datos` mediante **Model → Add → Package** (o el menú contextual **Add → Package** de la versión instalada).
3. Crear cada diagrama dentro de su paquete con **Model → Add Diagram → [tipo]**. Renombrar elementos en Model Explorer o con doble clic. Usar el **Toolbox** para colocar nodos y relaciones.
4. Guardar el `.mdj` después de cada diagrama. Para exportar, seleccionar el diagrama y usar **File → Export Diagram As** para PNG/SVG en las versiones que muestran ese menú; también se puede usar **Edit → Copy Diagram As Image** y pegar en el documento. La exportación debe permitir leer todo el texto al tamaño al que aparecerá en el informe.
5. Seguir el [método trazable](metodo-y-clases-staruml.md): requisitos → `DM-01` dominio → `CU-01`/`ACT-02` → `SD-01` → `CD-01` y `CMP-01`. `CD-02`/`SD-03` detallan exportación. Después `CU-02`/`ACT-01` → `CD-03`/`SD-02` para los contratos lógicos de incorporación. El ER con claves definitivas espera la plantilla/grano de datos; despliegue espera infraestructura real.

## 1. `CU-01 Consulta pública de estadísticas` — hacer primero

**Tipo:** Use Case Diagram, paquete `01 Requisitos`. **Objetivo:** mostrar las dos tareas completas del visitante, no cada clic de la interfaz. Se inserta en el capítulo 2, sección 2.3. Traza `REQ-F-001`, `REQ-F-002`, `REQ-F-009`, `REQ-F-011`.

1. Desde el Toolbox arrastrar un **Use Case Subject** rectangular al centro. Nombrarlo `Sitio público de estadísticas del RNC`.
2. Arrastrar un **Actor** a la izquierda, fuera del rectángulo. Nombrarlo `Visitante público`.
3. Dentro del rectángulo poner dos **Use Case** ovalados, uno encima del otro: `Consultar estadísticas` y `Exportar resultado de consulta`.
4. Con **Association** unir `Visitante público` con cada óvalo. La asociación es una línea simple; no necesita punta de flecha.
5. Debajo del Subject poner una **Note**: `Solo cortes definitivos; los filtros, indicadores y formatos son pasos u opciones de estos casos.` Unirla al Subject con **Note Link** si la herramienta lo ofrece.
6. No dibujar `include`, `extend`, jerarquías de actores, `Iniciar sesión` ni `Ver mapa`: no están justificados como objetivos separados de esta primera versión.

**Comprobación:** el actor queda fuera del límite; los dos casos quedan dentro; hay exactamente dos asociaciones actor–caso; no hay permisos ni fórmulas inventadas. Añadir al pie del informe: `Figura 2.x. Casos de uso de la consulta pública. Fuente: elaboración propia a partir de [1], [2] y requisitos validados [cuando exista acta].`

## 1. `ACT-01 Incorporación de archivo definitivo`

**Tipo:** Activity Diagram, paquete `03 Procesos`. Traza `REQ-F-012` y preguntas `Q-007`, `Q-017`.

1. Crear dos particiones verticales: `Trabajador autorizado del RNC (rol por validar)` y `Plataforma RNC`.
2. Calle humana: Initial Node → `Seleccionar archivo de corte definitivo y declarar referencia de origen` → `Solicitar incorporación`.
3. Calle plataforma: `Recibir archivo y metadatos declarados` → `Comprobar tipo, codificación, encabezados y orden del contrato observado` → decisión `[contrato compatible]` / `[contrato incompatible]`.
4. Rama incompatible: `Mostrar informe técnico de incompatibilidades` → Activity Final Node.
5. Rama compatible: `Comprobar evidencia declarada del corte definitivo` → decisión `[evidencia insuficiente]` / `[evidencia suficiente según regla pendiente del RNC]`. Insuficiente informa y termina; suficiente registra conjunto recibido, comprueba disponibilidad/cobertura ONEI y guarda resultado técnico con avisos, sin publicar automáticamente.
6. Calle humana: `Revisar resultado de incorporación` → final. Nota: autorización, evidencia de definitividad, grano, diccionario y retención pendientes. No corregir registros, resolver duplicados ni validar epidemiológicamente.

## 2. `ACT-02 Consulta y presentación de estadísticas`

**Particiones obligatorias del dibujo:** `Visitante público` y `Plataforma pública RNC`. Usa Activity Partition reales del Toolbox, en disposición vertical; cada acción queda en la partición de su responsable. Este diagrama distribuye tareas humanas y automáticas, como los ejemplos de DS/IR consultados; los nombres no fijan roles institucionales. Guarda y cruza cada flujo cuando cambia la responsabilidad.

**Tipo:** Activity Diagram, paquete `03 Procesos`. Traza `UC-01` y `REQ-F-001` a `REQ-F-008`, `REQ-F-011`.

1. Ordenar verticalmente un **Initial Node**, las **Action** `Seleccionar filtros`, `Solicitar consulta`, `Validar selección y corte disponible`, y un **Decision Node**.
2. Desde la decisión, dibujar dos **Control Flow**. Etiquetar las salidas `[selección válida]` y `[selección inválida]`.
3. Rama inválida: **Action** `Mostrar error`; conectar con **Activity Final Node**. Una consulta corregida inicia una ejecución nueva.
4. Rama válida: **Action** `Recuperar datos definitivos y verificar grano`; después otro **Decision Node** con guardas `[sin datos o grano incompatible]` y `[datos compatibles]`.
5. Rama sin datos: **Action** `Informar indisponibilidad del indicador solicitado` y **Activity Final Node**. No desagregar un archivo más allá de su grano.
6. Rama con datos: **Action** `Obtener población ONEI disponible y métodos versionados`, **Action** `Calcular indicadores posibles` y **Action** `Aplicar política de divulgación`.
7. Añadir un tercer **Decision Node**: `[resultado autorizado]` → **Action** `Mostrar tabla, visualización y metadatos` → **Activity Final Node**; `[resultado restringido]` → **Action** `Informar restricción sin revelar cifras` → **Activity Final Node**.
8. Usar **Control Flow** para cada unión. Añadir una **Note**: `Sin denominador ONEI compatible pueden mostrarse conteos autorizados, pero no tasas dependientes. Política de celdas pequeñas y métodos pendientes de validación.`

**Comprobación:** cada camino termina o vuelve a una acción anterior; los datos preliminares no pasan a cálculo/resultado; los nombres de acciones describen trabajo, no pantallas.

## 3. `CMP-01 Componentes lógicos de la plataforma`

**Tipo:** Component Diagram, paquete `04 Arquitectura`. Traza `REQ-F-001` a `REQ-F-013`, `REQ-D-001` a `REQ-D-004` y `REQ-NF-006`.

1. Arrastrar **Component** y nombrar los elementos: `Interfaz pública`, `Servicio de consulta`, `Motor estadístico`, `Catálogo de métodos`, `Servicio de exportación`, `Repositorio de cortes definitivos`, `Prototipo de panel interno`, `Importador de archivos definitivos`, `Validador técnico de archivos`, `Repositorio de población ONEI` y `Política de divulgación`. Representar `Sistema interno RNC` como componente externo, fuera del límite del portal.
2. Ordenar a la izquierda las interfaces y el sistema externo; al centro los servicios/importador/validador/política; a la derecha los repositorios. La **posición no expresa ejecución ni servidores**.
3. Con **Dependency** (flecha discontinua desde quien usa hacia el proveedor) conectar:
   - `Interfaz pública` → `Servicio de consulta` y → `Servicio de exportación`.
   - `Servicio de consulta` → `Repositorio de cortes definitivos`, → `Repositorio de población ONEI`, → `Catálogo de métodos`, → `Motor estadístico` y → `Política de divulgación`.
   - `Prototipo de panel interno` → `Importador de archivos definitivos`.
   - `Importador de archivos definitivos` → `Validador técnico de archivos`, → `Repositorio de población ONEI` y → `Repositorio de cortes definitivos`.
   - `Sistema interno RNC` → `Importador de archivos definitivos`: entrega el archivo definitivo por un mecanismo aún no especificado.
4. Añadir una **Note** al importador: `Adaptador Excel/CSV ahora; integración autorizada futura mediante el contrato FuenteCorteDefinitivo. Solo comprueba el contrato técnico; no modifica el archivo definitivo. Falta de ONEI limita tasas, no invalida conteos.`
5. Añadir una **Note** a `Política de divulgación`: `Reglas de celdas pequeñas y autorización de salidas agregadas pendientes de acuerdo con el RNC.`
6. `Servicio de exportación` recibe de la interfaz un `ResultadoConsulta` ya calculado y autorizado; sus estrategias de formato aparecen en `CD-02`. Documentar la correspondencia: `Interfaz pública` contiene `VistaConsulta`; `Servicio de consulta` contiene `ServicioConsulta` y `ValidadorConsulta`; `Motor estadístico` contiene `MotorIndicadores`; `Catálogo de métodos` implementa `CatalogoMetodologia`; `Política de divulgación` implementará `PoliticaDivulgacion`; `Servicio de exportación` contiene `ServicioExportacion` y los exportadores; `Repositorio de cortes definitivos` contiene `LectorCortesDefinitivos` y `PersistenciaCortesDefinitivos`, realizaciones de los puertos de lectura/escritura; `Repositorio de población ONEI` contiene `LectorPoblacionONEI`, realización de `ProveedorPoblacion`; `Importador de archivos definitivos` contiene `ServicioIncorporacion`, `NormalizadorEntrada` y el adaptador `LectorArchivoDefinitivo`; `Validador técnico de archivos` contiene `ValidadorContrato`. No dibujar implementación concreta de política antes de acordarla. Dibujar interfaces provistas/requeridas solo si se definen sus contratos; no confundir la interfaz UML de clase con un puerto de componente.

**Comprobación:** el sistema interno queda fuera del portal; la consulta usa cortes definitivos, población y métodos versionados y pasa cada salida por la política de divulgación; Excel/CSV es un adaptador de entrada, no servidor; la exportación usa el resultado autorizado; no aparecen corrección de casos ni aprobación de definitividad.

## 4. `SD-01 Consultar estadísticas definitivas`

**Tipo:** Sequence Diagram, paquete `05 Interacciones`. Debe ser coherente con `CU-01`, `ACT-02`, `CD-01` y `CMP-01`.

1. Poner ocho **Lifeline** de izquierda a derecha: `visitante:Visitante público`, `vista:VistaConsulta`, `consulta:ServicioConsulta`, `validador:ValidadorConsulta`, `datos:RepositorioCortesDefinitivos`, `poblacion:ProveedorPoblacion`, `metodos:CatalogoMetodologia`, `motor:MotorIndicadores`, `politica:PoliticaDivulgacion`. El escenario resumido no muestra cada método auxiliar; completar el detalle de catálogo de métodos si la validación de alcance lo requiere. Usar orientación horizontal o dividir la figura en `SD-01a` y `SD-01b` para mantener legibilidad.
2. Crear mensajes de arriba hacia abajo: `visitante → vista: solicitarConsulta(criterios)`; `vista → consulta: consultar(criterios)`; `consulta → validador: validar(criterios)`; respuesta `resultadoValidacion`. Insertar **Combined Fragment** `alt` con `[criterios inválidos]` y `[criterios válidos]`. En la primera, devolver `RespuestaConsulta(errores)` y mostrar aviso. En la segunda, `consulta → datos: obtenerDefinitivos(criterios)`; respuesta `datosBase`.
3. Dentro de la rama válida, otro `alt`: `[sin datos o grano incompatible]` devuelve aviso; `[datos compatibles]` sigue con `consulta → poblacion: obtenerCompatible(criterios)`; respuesta `datosPoblacion [0..1]`; `consulta → metodos: obtenerDefiniciones(criterios)`; respuesta `definiciones`; `consulta → motor: calcular(datosBase, datosPoblacion, definiciones, criterios)`; respuesta `resultadoInterno`.
4. Añadir `consulta → politica: aplicar(resultadoInterno, criterios)`; respuesta `resultadoConsulta`. Otro `alt`: `[resultado autorizado]` devuelve `RespuestaConsulta(resultadoConsulta)` y `vista → visitante: mostrarResultado(resultadoConsulta)`; `[resultado restringido]` devuelve `RespuestaConsulta(sinCifras)` y muestra aviso. `ResultadoInterno` jamás llega a `vista`.
5. Colocar **Note**: `Falta de población puede dejar tasas indisponibles y conservar conteos; política Q-007 aún por acordar. Cada cifra registra corte, edición ONEI, método y versión de política.` El nombre `obtenerDefinitivos` expresa el estado confirmado del origen, no autorización automática de publicación.
6. Si la versión de StarUML dificulta el fragmento `alt`, dibujar primero solo el escenario positivo, titularlo `SD-01a`, y luego un segundo diagrama `SD-01b` para la alternativa; no mezclar dos caminos sin guardas.

**Comprobación:** los mensajes siguen el tiempo vertical; `ResultadoInterno` pasa por `PoliticaDivulgacion` antes de la vista; la ausencia de ONEI afecta solo indicadores que necesitan denominador; no aparecen datos nominales, tecnología concreta ni fórmula no aprobada.

## 5. `CU-02` y `ACT-01` — prototipo interno

Seguir las instrucciones detalladas de [`casos-uso-sistema.md`](casos-uso-sistema.md) y [`guia-diagramas-staruml.md`](guia-diagramas-staruml.md). En `CU-02`, usar un único actor genérico `Trabajador del RNC` y tres casos: `Incorporar archivo definitivo`, `Consultar resultado técnico de incorporación` y `Consultar cortes disponibles`. En `ACT-01`, representar recepción, comprobación técnica, derivación del conjunto canónico y registro de capacidades con/sin ONEI. Añadir una Note `Archivo de origen definitivo e inmutable; grano, contrato y roles por precisar`. **No asignar** al doctor encargado ni al personal de mantenimiento una facultad concreta que aún no está documentada.

## 6. `DM-01`, `CD-01`, `CD-02`, `CD-03`, `SD-02` y `SD-03` — dominio y diseño

Seguir la [especificación detallada de clases y método](metodo-y-clases-staruml.md). `DM-01` separa los conceptos RNC/ONEI de las clases de software; `CD-01` tiene **atributos, operaciones, tipos, visibilidad, asociaciones, composición, multiplicidades y dependencias**; `CD-02` representa los tres exportadores CSV/Excel/PDF con realización de interfaz; `SD-03` verifica la elección del exportador. `CD-03` define los puertos y operaciones de entrada para `SD-02`.

Para `SD-02 Incorporar archivo definitivo`, crear un **Sequence Diagram** en `05 Interacciones`. Dibujar de izquierda a derecha: `trabajador:Trabajador del RNC` (actor), `vista:VistaIncorporacion`, `servicio:ServicioIncorporacion`, `fuente:FuenteCorteDefinitivo`, `validador:ValidadorContrato`, `normalizador:NormalizadorEntrada`, `poblacion:ProveedorPoblacion`, `almacen:AlmacenCortesDefinitivos`. Reutilizar los elementos de `CD-03` y `CD-01` como tipos de las líneas de vida.

1. `trabajador → vista: solicitarIncorporacion(referencia)`; `vista → servicio: incorporar(referencia)`; `servicio → fuente: obtenerPaquete(referencia)`; retorno `paquete:PaqueteDefinitivo`.
2. `servicio → validador: validar(paquete)`; retorno `validacion:ResultadoValidacionArchivo`. Crear fragmento **alt** con guardas `[contrato incompatible o estado no definitivo]` y `[contrato compatible y origen definitivo]`.
3. Rama incompatible: `servicio → vista: ResultadoIncorporacion(errores)` como **return message** y `vista → trabajador: mostrarInforme(resultado)`; terminar sin guardar. El estado definitivo se comprueba a partir de los metadatos del paquete y la evidencia de origen que acuerde el RNC.
4. Rama compatible: `servicio → normalizador: derivar(paquete)`; retorno `conjunto:ConjuntoCanonico`; `servicio → poblacion: comprobarCobertura(conjunto)`; retorno `cobertura:CoberturaPoblacion`; `servicio → almacen: guardar(conjunto, cobertura)`; retorno `idCorte`; `servicio → vista: ResultadoIncorporacion(idCorte, avisos)` como retorno; `vista → trabajador: mostrarInforme(resultado)`.
5. Poner una **Note**: `Falta de ONEI: guardar conteos y avisar tasas indisponibles; ninguna corrección de registros ni publicación automática. Origen, permisos y retención pendientes (Q-007, Q-017).` El diagrama describe interfaces lógicas; sustituir detalles del adaptador cuando se reciba la plantilla real.

## 7. `ER-01 Modelo de datos` — después de recibir archivos

**Esperar:** un ejemplo autorizado de Excel/CSV, el diccionario y las series ONEI. Sin esto solo es honesto dibujar un **modelo conceptual** con `CorteDefinitivo`, `Territorio`, `Sexo`, `EdadSimple`, `GrupoEdad`, `PoblacionONEI`, `PoblacionEstandar`, `PesoEstandar` y `LocalizacionCancer`, más una entidad de casos agregados **o** de registros tumorales según el grano recibido. No colocar claves ni cardinalidades inventadas en el informe como modelo definitivo.

La entidad `PoblacionONEI` debe guardar **denominadores cubanos** por año/territorio/sexo/edad simple. `PoblacionEstandar` identifica la estándar mundial Segi/Doll de IARC/CI5 y `PesoEstandar` conserva sus 18 pesos por quinquenio clásico, que suman 100 000. Nunca mezclar estas columnas en `PoblacionDenominador`. Cuando se confirme el contrato de datos, crear **ER Diagram** en `07 Datos`, añadir **Entity**, atributos, PK/FK y relaciones con sus cardinalidades reales. Si StarUML no ofrece ER Diagram, revisar **Tools → Extension Manager** y la extensión de ER; mientras tanto marcar un Class Diagram como conceptual, no como ER final.

## 8. Despliegue

El diagrama `DEP-01` se hará después de conocer nodos, políticas y recursos de la entidad. La guía universitaria `SRC-UNI-001` pide que represente dónde se ejecuta cada parte, protocolos y requisitos mínimos; dibujar servidores o servicios inventados produciría una arquitectura falsa. El diagrama de componentes `CMP-01` cubre por ahora la vista lógica solicitada en el Anexo.

## Documentación de StarUML comprobada

- [Creación de diagramas](https://docs.staruml.io/user-guide/managing-diagrams) y [Use Case Subject](https://docs.staruml.io/v3/working-with-diagrams/use-case-diagram).
- [Activity Diagram](https://docs.staruml.io/v5/working-with-uml-diagrams/activity-diagram), [Class Diagram](https://docs.staruml.io/working-with-uml-diagrams/class-diagram), [Sequence Diagram](https://docs.staruml.io/master/working-with-uml-diagrams/sequence-diagram) y [Component Diagram](https://docs.staruml.io/v3/working-with-diagrams/component-diagram).
- [ER Diagram](https://docs.staruml.io/v3/working-with-diagrams/entity-relationship-diagram) y [gestión de extensiones](https://docs.staruml.io/v6/user-guide/managing-extensions).

## Comprobación antes de entregar cada figura

- El mismo actor, servicio y repositorio conserva su nombre en los diagramas relacionados.
- Cada diagrama tiene propósito, fuente de requisitos y explicación en el capítulo 2.
- Los supuestos abiertos figuran como Note y como texto del informe.
- Las relaciones y guardas tienen semántica UML correcta y texto legible.
- La figura exportada lleva nombre `ID-descripcion.png` o `.svg`; el archivo `.mdj` queda guardado como editable.
