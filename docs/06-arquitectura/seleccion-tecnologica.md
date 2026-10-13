# Comparación y selección tecnológica inicial

**Fecha de corte de la revisión:** 13 de octubre de 2026  
**Estado:** recomendación técnica para prototipos y primeros componentes de Prácticas II; no constituye aprobación institucional ni decisión de despliegue.

El estudiante aclaró que el RNC no tiene una selección previa de tecnología o diseño y espera que el proyecto lleve una propuesta que ayude a decidir (`SRC-RNC-008`, `EVD-078`). La comparación y recomendación son, por tanto, parte activa del trabajo: no se posponen hasta que el RNC elija primero. Se comprobarán las restricciones de infraestructura y operación que existan, pero su estado actual desconocido no equivale a una prohibición ni a una preferencia institucional.

## 1. Alcance y restricciones conocidas

Prácticas II incluye la comparación de tecnologías, prototipos, primeros componentes de cálculo de tasas e intervalos, consultas, frecuencias y exportación (`SRC-RNC-001`; `ENT-01`, `ENT-02`). La arquitectura se mantiene como monolito modular y recibe inicialmente archivos Excel/CSV declarados definitivos (`DEC-005`, `DEC-006`, `DEC-009`). No requiere conectarse ahora a la base del RNC ni implementar el panel administrativo seguro previsto para la tesis.

El CSV observado tiene 84 columnas y la estructura fue confirmada como estable, pero todavía se desconocen la semántica de campos y la unidad por fila. Las entregas futuras podrían contener miles de registros. Por eso, el volumen conocido no justifica seleccionar herramientas distribuidas o de grandes datos. El diccionario, los métodos estadísticos, los ejemplos aprobados, la política de publicación, el número de usuarios concurrentes, los navegadores institucionales y el entorno de despliegue siguen abiertos (`Q-003`–`Q-009`, `Q-014`, `Q-019`, `Q-016`).

La comparación prioriza lo que Danny pidió: buena respuesta con la conectividad disponible en Cuba sin perder facilidad y mantenibilidad. Los criterios son:

1. **Experiencia con conectividad lenta:** tamaño descargado en primera visita y visitas siguientes, cantidad de viajes de red, tiempo hasta contenido legible y comportamiento si un recurso tarda.
2. **Facilidad de construir y mantener:** cantidad de componentes, complejidad para el equipo de prácticas y claridad para evolucionar a la tesis.
3. **Adecuación estadística y de datos:** lectura/validación del contrato CSV, cálculos reproducibles y herramientas para análisis tabular.
4. **Tiempo de respuesta del servidor:** coste de consulta y cálculo con el volumen conocido, capacidad ante usuarios concurrentes y límites de memoria.
5. **Seguridad, soporte y despliegue:** funciones disponibles, mantenimiento de dependencias y facilidad para operar en infraestructura institucional.

La velocidad de CPU del lenguaje no sustituye estas dimensiones. Para la persona usuaria importan el tiempo de respuesta extremo a extremo y el peso de la página. La documentación de Django recomienda medir y advierte que consultas a base de datos, caché, plantillas y tráfico de red suelen ser más determinantes que ejecutar Python más rápido (`EVD-079`–`EVD-081`).

## 2. Comparación por capas

### 2.1 Aplicación y backend

| Alternativa | Ventajas para este proyecto | Costos y límites | Evaluación |
|---|---|---|---|
| **Python + Django** | Un solo lenguaje con el trabajo estadístico; estructura de aplicación completa, formularios, plantillas, ORM, seguridad y autenticación disponibles. Encaja con un monolito modular y puede servir la interfaz sin requerir un frontend separado. El estudiante ya ha usado Django y emplea Python a diario, lo que reduce el aprendizaje inicial esperado [SRC-RNC-009]. | Sus funciones administrativas y de autenticación no deben exponerse ni configurarse como panel institucional sin diseño de seguridad. La experiencia previa del estudiante no demuestra que Django tenga mejor rendimiento. | **Candidata base a comparar**: reúne capacidades del portal, herramientas analíticas en Python y experiencia existente del equipo. La documentación muestra sus capacidades, pero no demuestra que gane en velocidad; el esfuerzo real se contrastará durante el prototipo [SRC-TECH-001, SRC-RNC-009]. |
| Python + FastAPI | Buena opción si se confirma una API pública independiente, clientes adicionales o equipos separados; genera documentación OpenAPI automáticamente [SRC-TECH-002]. | Por sí solo no define la interfaz pública ni aporta el flujo completo de formularios, plantillas y administración; habría que elegir y mantener además frontend, autenticación y componentes. | Alternativa válida si aparece una necesidad real de API desacoplada; por ahora agrega piezas sin beneficio confirmado. |
| Python + Flask | Minimalista y flexible; útil para una demostración pequeña [SRC-TECH-003]. | Requiere escoger e integrar más componentes para formularios, estructura, autenticación y administración. La flexibilidad desplaza decisiones al equipo. | No es la primera elección para el producto con incorporación y consulta; sí serviría para un prototipo reducido. |
| Python + Dash o Shiny for Python | Permite levantar con rapidez pantallas reactivas y visualizaciones en Python; ambos tienen guías para aplicaciones interactivas [SRC-TECH-004]. | Su orientación a dashboards puede dificultar un sitio público editorial, accesible, de bajo peso y con flujos de incorporación específicos; el despliegue y los controles institucionales deben evaluarse. | Buena alternativa para probar cálculos y visualizaciones; no recomendada como base de producción sin evaluación de UX, accesibilidad, seguridad y operación. |
| R + Shiny | Muy adecuado para análisis y prototipos estadísticos expresados en R, con infraestructura reactiva [SRC-TECH-005]. | Vincula toda la aplicación a R y Shiny, mientras que la validación del CSV, la interfaz pública, las exportaciones y la futura integración necesitarían experiencia y soporte en ese entorno. | Elegirlo si el equipo o el RNC ya mantienen aplicaciones R/Shiny; eso no está confirmado. |
| Java + Spring, C# + ASP.NET Core o PHP + Laravel | Frameworks maduros con herramientas para aplicaciones web completas; ASP.NET documenta soporte multiplataforma, seguridad y componentes web [SRC-TECH-006]; Laravel documenta autenticación y sesiones [SRC-TECH-007]. | No existe en la evidencia consultada una restricción institucional que los favorezca; la capa de cálculo estadístico y el manejo de datos analíticos quedarían en ecosistemas distintos o exigirían componentes adicionales. | No descartados por capacidad; quedan detrás de Python dado el alcance analítico y el bajo volumen inicial. Reabrir si la infraestructura o experiencia del equipo los exige. |
| JavaScript/TypeScript con Node.js (p. ej., Express/Nest) | Unifica el lenguaje de interfaz y servidor y facilita una SPA/API moderna. | Los cálculos y métodos estadísticos necesitarían librerías especializadas o una segunda capa Python/R; una SPA puede aumentar descarga inicial y complejidad. | No recomendada mientras no haya necesidad de API/clientes separados ni evidencia de que el equipo domina mejor esta vía. |

**Lectura de la comparación:** Python/Django no es universalmente superior. Se perfila como ganador provisional de balance según la comparación global de la sección 5, no como ganador de velocidad medida. La experiencia previa del estudiante con Django y el uso diario de Python son ventajas concretas para el esfuerzo y el calendario de Prácticas II; se registran como ajuste del equipo, no como preferencia del RNC. La selección considera también PHP/Laravel, ASP.NET Core, Spring Boot, Node.js, R/Shiny y opciones compiladas, con sus costos de aprendizaje, bibliotecas e infraestructura.

### 2.1.1 Escenarios comunes para comparar los candidatos

La comparación siguiente aplica las mismas tareas a los candidatos. Son recorridos de diseño razonados, no mediciones ni pruebas de rendimiento. Una alternativa no se considera inferior por tener otro enfoque: hay que comprobar si su ventaja resuelve una necesidad del RNC y si justifica sus costos.

| Escenario concreto | Django + HTML progresivo | Alternativa y qué cambiaría | Costo de la alternativa / condición para preferirla |
|---|---|---|---|
| Una persona selecciona filtros de consulta y recibe una tabla, un gráfico y notas del corte. | Django procesa los filtros en el servidor y devuelve una página con HTML; la misma consulta puede componer la tabla y los datos del gráfico. El navegador puede leer la tabla aunque el JavaScript del gráfico tarde o falle. | FastAPI + React/Vue separa una API JSON del cliente. React/Vue puede actualizar partes de la pantalla sin recargarla. | No se confirmó otro cliente de la API, equipo frontend separado ni interacción que requiera una SPA. Se sumarían contrato API, cliente, compilación y coordinación entre capas. Sería mejor si esas necesidades aparecen o el prototipo prueba una interacción que HTML progresivo no cubre bien. |
| Se recibe un archivo definitivo con miles de filas y se comprueba estructura antes de habilitar sus agregados. | Un formulario Django puede aceptar el archivo y delegar su comprobación a un módulo independiente; el backend Python puede usar el mismo entorno para análisis tabular. | Flask permite ese mismo flujo, pero el equipo decide e integra por separado estructura, formularios y componentes. FastAPI es especialmente natural cuando la carga llega mediante una API. | Flask no reduce piezas frente a Django para este producto, y no se ha confirmado una integración API. El volumen comunicado no exige distribuir el procesamiento. Flask/FastAPI ganarían si se quisiera un servicio pequeño o un contrato de API para sistemas externos. La carga real sigue bloqueada hasta confirmar autorización y semántica del archivo. |
| Se publican páginas de inicio, metodología, definiciones y resultados, además del dashboard. | Las plantillas Django sirven contenido editorial y consultas desde la misma aplicación, con JavaScript progresivo para gráficos y filtros interactivos. | Dash o Shiny permiten prototipar rápido paneles reactivos; R Shiny es atractivo si los métodos y el equipo ya trabajan en R. | El producto descrito también necesita páginas informativas, accesibilidad, bajo peso y un flujo técnico de archivos. No se confirmó experiencia, código estadístico ni infraestructura R. Dash/Shiny serían mejores para validar pronto una vista analítica si el contenido editorial fuera secundario o si el equipo ya tuviera una solución de análisis en ese ecosistema. |
| El equipo decide entregar la aplicación en infraestructura ya operada por la institución. | Django puede ejecutarse como aplicación Python con su servidor de aplicación y base de datos compatible, sujeto a comprobar el entorno real. | Spring, ASP.NET Core o Laravel pueden ser la opción más conveniente si RNC/CUJAE ya dispone de personal, soporte, despliegue y operación para ese stack. | Hoy no se conoce una plataforma institucional preferida. Sin ese dato no se puede afirmar que estos stacks sean mejores; tampoco se deben penalizar por no compartir Python. Si aparece una plataforma soportada o experiencia institucional concreta, se recalifica la matriz y podría cambiar la recomendación. |

#### Cuándo podría ganar cada candidato

- **FastAPI + React/Vue:** alternativa más fuerte cuando hay API reutilizada por varios clientes, frontend separado o interacciones intensivas. En el alcance actual su principal valor —desacoplar esos componentes— no se ha demostrado; el costo de mantener dos capas sí aparece desde el primer día.
- **Flask:** puede resolver todo el flujo, pero Django ya reúne rutas, formularios, plantillas, modelos y componentes de seguridad. Con Flask habría que escoger e integrar más piezas; esa libertad no produce aquí una ventaja funcional conocida. Se reabre si el alcance se reduce a un servicio pequeño o la experiencia del equipo lo favorece.
- **Dash/Shiny:** tienen una ventaja real de velocidad para un dashboard analítico. No se seleccionan como aplicación completa porque el producto también se plantea como portal público con contenido, navegación, accesibilidad y conectividad limitada. Se pueden usar como referencia o prototipo de una pantalla y compararlos con la vista Django.
- **R Shiny:** puede ser la mejor elección si se confirma que los métodos, experiencia, componentes existentes y operación se concentran en R. Hoy esa condición no está confirmada; elegirlo ahora no elimina la necesidad de una capa o integración para el resto del portal.
- **Spring/ASP.NET/Laravel:** son candidatos completos, no alternativas descartadas por falta de seguridad o madurez. No se priorizan por ahora porque el trabajo estadístico propuesto está en Python y no conocemos una ventaja concreta de infraestructura o equipo que compense separar lenguajes. Una restricción institucional podría convertir uno de ellos en primera opción.
- **Node.js con SPA:** resulta atractivo cuando el equipo domina TypeScript y necesita una interfaz cliente rica o varios clientes sobre la misma API. No se identificó esa necesidad; los cálculos requerirían una biblioteca especializada adicional o un servicio Python/R.

La selección debe basarse en el **ajuste al problema actual**, no en una calidad absoluta de cada framework. Por ejemplo, si el RNC informa que solo puede operar aplicaciones ASP.NET, Django deja de ser la mejor propuesta aunque su arquitectura actual sea más simple para el equipo de prácticas.

### 2.1.2 Pros y contras generales, y ajuste preliminar al RNC

| Candidato | Ventajas generales | Costos o desventajas generales | Ajuste preliminar al RNC y conectividad |
|---|---|---|---|
| **Python + Django + plantillas HTML** | Framework integral; formularios, plantillas, autenticación, ORM, validación, caché y paginación reducen la cantidad de piezas que se integran. Comparte lenguaje con el procesamiento estadístico. | Incluye abstracciones que un microservicio pequeño no necesita; ejecución Python no es la más rápida en CPU frente a runtimes compilados. Debe medirse y configurarse bien, especialmente consultas y despliegue. | Puede responder con HTML generado por servidor y añadir solo el JavaScript del gráfico/filtros. Buena combinación de facilidad, un único proyecto y capacidades analíticas. Candidato al mejor balance; sin medición comparativa. |
| **Python + FastAPI + cliente HTML/SPA** | Validación de entradas y contratos de API; concurrencia asíncrona para operaciones I/O; comparte Python y ecosistema estadístico. | FastAPI no aporta por sí solo un portal completo: deben componerse persistencia, plantillas/clientes, sesiones, autenticación, administración y convenciones de estructura. La asincronía no acelera el cálculo de CPU. | Puede ser ligero si se sirve HTML desde el servidor; API + SPA suele añadir un cliente compilado y tráfico JSON. Sería preferible si se confirma API para varios clientes o muchas operaciones concurrentes de I/O. |
| **Python + Flask + Jinja/HTML** | Núcleo pequeño, flexible y sencillo de entender; permite renderizar HTML sin SPA y conserva acceso al ecosistema Python. | La aplicación elige e integra más extensiones y convenciones: formularios, autenticación, ORM, validaciones y administración; la libertad aumenta decisiones de mantenimiento. | La página puede ser tan ligera como en Django si se usa el mismo HTML/CSS/JS. Candidato real para una aplicación pequeña; para este alcance, hay que justificar por qué la flexibilidad vale las integraciones manuales. |
| **PHP + Laravel + Blade** | Framework completo con formularios, validación, ORM, autenticación, plantillas y comandos de optimización de producción; permite HTML renderizado en servidor. | Requiere PHP y su operación; procesamiento estadístico puede necesitar bibliotecas PHP o un servicio separado Python/R. El desempeño depende del servidor PHP y configuración. | Puede entregar páginas pequeñas y cachear recursos/consultas; no es intrínsecamente lento frente a Django. Gana fuerza si el equipo o el alojamiento soporta PHP y ofrece una operación sencilla. Requiere evaluar cómo sostener métodos estadísticos. |
| **C# + ASP.NET Core MVC/Razor** | Runtime con buen soporte de concurrencia, compresión, caché y diagnósticos; framework completo para formularios y páginas HTML; fuerte tipado. | Introduce C#/.NET y su ecosistema para cálculos; el despliegue, actualización y experiencia del equipo deben evaluarse. Más rendimiento potencial de CPU no garantiza una página que cargue antes. | Puede usar el mismo diseño de HTML server-rendered ligero que Django. Candidato fuerte si infraestructura/experiencia .NET existe o la medición muestra CPU como cuello de botella. No hay hoy esa evidencia. |
| **Java + Spring Boot MVC/Thymeleaf** | Ecosistema maduro para aplicaciones grandes, integración y operación institucional; controladores, HTML dinámico y servidor integrado disponibles. | Más conceptos/configuración y demanda de memoria/arranque que se deben medir en la máquina objetivo; para el volumen conocido puede ser complejidad innecesaria. La estadística puede usar Java, pero no aprovecha automáticamente la base Python/R. | Con SSR puede enviar poco contenido y servir bien en baja conectividad. Se justifica si el equipo institucional opera Java o necesita capacidades empresariales concretas; no se descarta por velocidad sin medir. |
| **Node.js + Express/Nest + SSR o SPA** | JavaScript/TypeScript de extremo a extremo; buen manejo de muchas operaciones I/O no bloqueantes; amplia elección de frameworks UI. | Cálculos CPU intensivos bloquean el event loop si no se aíslan; para métodos y procesamiento tabular podría requerir módulos Node especializados o un servicio Python/R. Una SPA puede aumentar el peso inicial. | SSR con HTML y recursos locales puede ser ligero; una SPA pura no es primera candidata para conectividad limitada hasta medir bundle y número de solicitudes. Sería mejor si el equipo domina TypeScript o hay varios clientes de una API. |
| **R + Shiny** | Expresa análisis y gráficos dentro del ecosistema estadístico R; rápida para explorar métodos y construir dashboard reactivo. | Aplicación y despliegue dependen del modelo de Shiny/Posit o de una operación propia; concurrencia y límites del servidor deben probarse. Menor libertad/adecuación para un portal editorial depende del diseño concreto, no debe asumirse. | Candidata fuerte para una pantalla de análisis o si el equipo entrega métodos R ya validados. Como sitio completo, comprobar peso de recursos, funcionamiento con red inestable y costo de autoalojamiento. |
| **Go + `net/http`/plantillas o framework pequeño** | Compila a binario, biblioteca HTTP/plantillas estándar, concurrencia integrada y despliegue simple del artefacto. | Hay que diseñar/seleccionar más piezas para formularios, persistencia, autenticación y aplicación; menor continuidad directa con el ecosistema estadístico Python/R. Requiere formación si el equipo no lo domina. | Puede tener bajo uso de recursos del servidor, pero HTML/CSS/JS y consultas siguen determinando el peso y la demora del usuario. Se justifica si recursos del servidor son un límite medido y se acepta mayor trabajo de integración. |
| **Rust + Axum** | Binarios nativos, control fino de recursos y tipos que ayudan a detectar clases de errores; middleware disponible en el ecosistema Tokio/Tower. | Curva de aprendizaje y compilación mayores; más trabajo de integración para formularios, administración y cálculos; ecosistema de análisis menos directo para este proyecto. | El bajo consumo potencial del servidor no acorta por sí solo la descarga de la página. Solo subiría en prioridad si CPU/memoria fueran una limitación comprobada o el equipo ya tuviera experiencia Rust. |

**C++ no pasa a la lista corta:** su rendimiento en CPU puede ser excelente, pero en este producto no se ha demostrado que el cálculo sea el cuello de botella. Habría que construir e integrar más infraestructura web/administrativa y resolver el acceso a herramientas estadísticas apropiadas; con miles de filas y datos tabulares, ese costo de desarrollo/mantenimiento no está justificado antes de medir. Si una función concreta se vuelve costosa, se podría aislar y optimizar después en un componente nativo sin reescribir toda la web.

### 2.1.3 Qué mejora más la velocidad para usuarios en Cuba

La conectividad es una característica del producto, no una propiedad que se resuelve escogiendo el lenguaje de servidor con mayor rendimiento de CPU. Django documenta optimización de base de datos, caché, respuestas condicionales, compresión y caché del navegador; React también advierte que una aplicación cliente puede mostrar una pantalla vacía hasta cargar y ejecutar JavaScript, mientras que SSR/SSG permite mostrar contenido antes. Estas capacidades se pueden aplicar con varios frameworks (`EVD-079`, `EVD-080`).

| Prioridad | Decisión de diseño para el RNC | Ejemplo concreto |
|---|---|---|
| **1. Primer contenido visible** | Entregar HTML semántico desde el servidor para el título, filtros, tabla/estado y metadatos; usar JavaScript progresivo solo para la interacción/gráfico que lo necesite. | Al abrir la página de resultados, el usuario ya puede leer filtros y encabezados de tabla mientras el gráfico carga. No mostrar una pantalla vacía que dependa de que se descargue y ejecute una SPA completa. |
| **2. Menos bytes en la primera visita** | Mantener CSS/JavaScript pequeños, seleccionar módulos de visualización, servir recursos locales y versionados, evitar fuentes, mapas, iconos y librerías cargadas desde terceros. | Cargar solo el módulo del gráfico de barras usado en la vista; no descargar paquetes cartográficos porque un mapa es una etapa posterior. |
| **3. Menos viajes de ida y vuelta** | Aplicar filtros al enviar el formulario o con una única actualización parcial explícita; no disparar una consulta por cada tecla/cambio. Enviar solo agregados necesarios para esa consulta. | Cambiar sexo, territorio y período y pulsar “Aplicar” genera una consulta; tabla y gráfico usan la misma respuesta. El CSV de casos nunca viaja al navegador. |
| **4. Reutilizar descargas** | Aplicar caché larga y nombres con huella a CSS, JavaScript e imágenes; usar validación/caché de resultados públicos solo si corte, filtros y estado son parte de la clave y la política de divulgación lo permite. | Una segunda visita descarga de nuevo solo un recurso que cambió. No cachear páginas administrativas o contenido no público en cachés compartidas. |
| **5. Reducir el trabajo servidor** | Agregar/filtrar en la base cuando sea apropiado, limitar columnas/filas, indexar consultas recurrentes y medir; cachear o precomputar estadísticas publicables cuando se haya aprobado la semántica. | Una consulta de frecuencia por municipio recibe agregados, no todas las filas de pacientes para contarlas en el navegador. |
| **6. Mantener cómputos acotados** | Cargar/importar y calcular tareas largas fuera del request interactivo si mediciones lo justifican. `async` ayuda a esperar I/O concurrente; no vuelve automáticamente más rápido un cálculo CPU-bound. | Una carga de archivo se valida en un proceso de incorporación y deja un reporte de estado; la web pública consulta el corte procesado. |

La estrategia de envío afecta a **todos** los candidatos. Una página Laravel/Blade, ASP.NET/Razor, Spring/Thymeleaf o Go/HTML puede tener transferencia pequeña; una Django SPA también puede tener una descarga inicial grande. Por eso el candidato de frontend debe seleccionarse junto con la arquitectura SSR/progresiva, no inferirse del lenguaje.

### 2.2 Interfaz pública

| Alternativa | Valor | Decisión preliminar |
|---|---|---|
| HTML semántico, CSS y JavaScript progresivo servido por el backend elegido | Entrega páginas completas y puede hacer interactivas las consultas por partes. Evita introducir un cliente separado, un sistema de compilación y una API solo para alimentar la interfaz. | **Patrón principal a evaluar** por su carga inicial contenida. Mantener tabla HTML legible y usable sin depender del gráfico; compararlo con SSR de cada candidato y con una SPA medida. |
| React, Vue o Angular como SPA con API | Adecuados para interfaces muy interactivas, grandes o compartidas entre web y otros clientes; permiten componentes reutilizables. React se define como biblioteca para interfaces, y Vue como framework progresivo [SRC-TECH-008]. | No se adopta por defecto: se debe demostrar que la interactividad compensa la carga inicial, compilación y llamadas. SSR/SSG pueden mitigar primera pintura pero agregan herramientas y complejidad; reevaluar con mediciones. |
| HTMX o actualización parcial de HTML | Puede añadir interactividad sin transformar el sitio en una SPA completa. | Candidato para prototipo, no una decisión necesaria. Medir peso, complejidad y compatibilidad de navegador junto a JavaScript nativo. |

### 2.2.1 Dirección visual y sistema de estilos

Django **no define el aspecto visual**. Sus plantillas producen la capa de presentación y permiten separarla del código de negocio; la documentación explica cómo componer y cambiar la apariencia desde plantillas [SRC-TECH-001, SRC-TECH-015]. Con ese servidor se puede crear una web muy atractiva, adaptable a móvil y con identidad propia. El resultado depende del diseño, los recursos visuales, la tipografía, los estados de interacción y la implementación HTML/CSS, no de Django.

| Estrategia visual | Ventaja | Costo o riesgo | Evaluación para el proyecto |
|---|---|---|---|
| **CSS propio con variables/tokens y componentes reutilizables** | Máximo control sobre identidad visual, jerarquía, tipografía, espacios, color y densidad; permite servir solo los estilos necesarios. | Requiere más trabajo manual para definir y mantener consistencia, estados y adaptación móvil. | **Candidata principal** para un sitio distintivo y ligero, organizado en componentes de plantillas. |
| Bootstrap con tema personalizado | Grilla mobile-first y componentes listos aceleran el prototipo [SRC-TECH-016]. | Sin personalización puede verse genérico; cargar componentes innecesarios afecta el objetivo de ligereza. | Comparar como acelerador, personalizando el tema y limitando los módulos cargados. |
| Tailwind CSS con tokens propios | Utilidades responsivas y variables de tema ayudan a construir un estilo particular [SRC-TECH-017]. | Requiere paso de compilación CSS y disciplina de diseño para evitar clases dispersas en las plantillas. | Alternativa si el equipo domina el flujo y el prototipo muestra que mejora la velocidad de diseño. |
| SPA con biblioteca de componentes React/Vue/Angular | Ecosistema amplio de componentes, transiciones e interacciones. | Añade compilación, JavaScript y complejidad; no es requisito para una interfaz visualmente atractiva. | Elegir solo si el prototipo demuestra que la interfaz necesita funciones que Django más mejora progresiva no cubra. |

No se recomienda adoptar Bootstrap sin cambios como apariencia final. Se propone una interfaz pública con identidad propia y coherente con una fuente sanitaria: jerarquía clara, filtros ordenados, indicadores legibles, gráficos contextualizados y estados visibles de carga, ausencia, restricción y error. La paleta, tipografía y estilo se definirán con wireframes y prototipo; no se presentan aquí como identidad aprobada por el RNC.

El prototipo visual debe evaluarse en escritorio y móvil, con ampliación, contraste, teclado, foco, lector de pantalla y conexión lenta. La estética debe reforzar la lectura, no sustituirla: toda gráfica tendrá una tabla equivalente y las cifras, filtros y notas metodológicas conservarán legibilidad.

### 2.3 Visualización

| Biblioteca | Ventajas | Límites / criterios | Decisión preliminar |
|---|---|---|---|
| **Apache ECharts** | Amplia variedad de gráficos, licencia Apache 2.0 y opción de construir paquetes personalizados. Documenta funciones ARIA y patrones, aunque se deben activar y evaluar; la tabla paralela sigue siendo necesaria [SRC-TECH-009]. | Debe medirse el peso del paquete elegido y probarse con teclado, lector de pantalla, pantallas pequeñas y conexión lenta. | Candidata a comparar en el primer prototipo, cargada localmente y con solo los módulos requeridos. No insertar CDN ni mapas externos por defecto. |
| Plotly.js | Amplia colección de gráficos, funciona offline y su licencia declarada es MIT [SRC-TECH-010]. | Hay que medir el paquete descargado para los gráficos concretos y revisar si controles/branding de la distribución elegida afectan la presentación. | Alternativa directa que debe probarse en el mismo prototipo; no se descarta sin comparación visual y de peso. |
| D3.js | Máxima libertad para visualizaciones a medida. | Más trabajo de implementación y mantenimiento; innecesario para las visualizaciones convencionales previstas mientras no exista un requisito visual específico. | Reservar para una visualización singular que no resuelva ECharts/Plotly. |
| Chart.js | API sencilla para gráficos comunes. | Menor amplitud para ciertas visualizaciones estadísticas; validar interacción/exportación y accesibilidad requerida. | Alternativa ligera para prototipo; comparar en la misma página antes de cerrar. |

La gráfica nunca será el único formato del resultado. Cada consulta debe ofrecer tabla, títulos/unidades, periodo, estado del corte, método y notas aprobadas. Los mapas y series temporales se encuentran en la etapa posterior, por lo que no justifican cargar ahora módulos cartográficos.

**Ejemplo común para comparar librerías:** construir con el mismo conjunto sintético un gráfico de barras de frecuencia por grupo de edad, con filtros de sexo y localización, y pedir a una persona que identifique el grupo mayor, cambie un filtro y obtenga la tabla equivalente. Comparar ECharts y Plotly.js por peso descargado localmente, legibilidad, navegación, descripción accesible, adaptación a móvil y esfuerzo de integración. Chart.js puede cubrir una barra común con menor superficie funcional; D3 solo se justificaría si el diseño necesitara una codificación visual singular. Sin esta comparación en el mismo escenario, no afirmar que ECharts sea ganador definitivo.

### 2.4 Procesamiento estadístico y archivos

| Alternativa | Uso posible | Evaluación para esta etapa |
|---|---|---|
| Módulo estándar `csv` de Python | Comprobar encabezados, orden, delimitador, comillas y errores de lectura; escribir CSV. Python documenta expresamente la lectura/escritura de dialectos CSV [SRC-TECH-011]. | **Preferido para validar el contrato estructural** de entrada, sin inferir tipos o significado automáticamente. |
| `pandas` | Transformación tabular, agrupaciones y lectura de CSV/XLSX; `read_csv` permite declarar tipos y parámetros [SRC-TECH-012]. | Candidato para el primer prototipo estadístico si facilita el trabajo del equipo; el conjunto de miles de filas no demuestra necesidad de optimización distribuida. Declarar tipos tras recibir el diccionario y fijar versiones. |
| `polars` | Transformación tabular con evaluación lazy y ejecución optimizada. | No aporta una necesidad demostrada en el volumen estimado; comparar solo si mediciones con archivos sintéticos muestran límites de memoria o tiempo con pandas. |
| R (base, `data.table`, `dplyr`, `epiR`/equivalentes) | Ecosistema estadístico amplio y familiar para bioestadística; se puede ejecutar como motor separado. | Requiere decidir cómo integrarlo con la aplicación web y reproducir los mismos contratos. Considerar si la tutoría o el RNC aporta reglas y validadores existentes en R. |
| Fórmulas implementadas explícitamente en Python + bibliotecas numéricas puntuales | Facilita mostrar la fórmula, unidades, entradas y redondeos del método aprobado. | **Recomendación para indicadores**: conservar fórmulas como funciones pequeñas, versionadas y con casos de referencia; usar SciPy solo cuando un método aprobado requiera rutinas numéricas no triviales. No elegir fórmula/IC hasta resolver `Q-004`, `Q-005`, `Q-009`. |

Para Excel, valorar `openpyxl` como lector/escritor de `.xlsx` si ese formato entra efectivamente; el usuario ha confirmado estructura de CSV, no aún plantilla XLSX. CSV se procesa sin cambiar el original y sin registrar valores de salud en logs. El archivo definitivo permanece inmutable; la salida del análisis será derivada y trazable.

### 2.5 Persistencia

| Alternativa | Ventajas | Límites | Decisión preliminar |
|---|---|---|---|
| **PostgreSQL** | Base relacional con restricciones, transacciones, índices, seguridad y licencia permisiva; ofrece características adecuadas para conservar cortes versionados y relaciones entre dimensiones [SRC-TECH-013]. | Requiere un servicio administrado, copias, cuentas, actualizaciones y aceptación por infraestructura institucional. No se conoce aún el motor aprobado. | **Candidato preferido para producción si la entidad puede operarlo.** El modelo físico y la elección final siguen pendientes. |
| SQLite | Muy simple, archivo único, sin servidor y transaccional [SRC-TECH-014]. | Se ajusta mejor a desarrollo local o demostración de un solo servicio; no debe suponerse como almacén institucional multiusuario o de producción sin revisar concurrencia, respaldos y operación. | Usarlo en prototipos locales si reduce fricción, no fijarlo como persistencia productiva. |
| MySQL/MariaDB u otro motor relacional institucional | Alternativa viable para datos tabulares y restricciones relacionales. | Sin información del entorno institucional, no hay base para preferirlo frente a PostgreSQL; soporte real puede invertir la recomendación. | Mantener adaptador de persistencia; decidir con el área técnica del RNC/CUJAE. |
| DuckDB | Analítica local de archivos tabulares, sin servicio separado. | Es más analítico/embebido y no ofrece ventaja confirmada sobre una base transaccional para publicación versionada y flujos de incorporación. | Útil para exploración local si el volumen real lo amerita; no es el almacén de aplicación propuesto. |
| Archivos CSV como almacenamiento persistente | Sin servidor y fácil de inspeccionar. | Dificulta concurrencia, actualización atómica, historial, relaciones, control de acceso y consistencia de cortes. | Solo transporte/entrada/salida, no persistencia de la plataforma. |

MongoDB/documentos no se prioriza: no hay evidencia de datos semiestructurados o esquemas dinámicos que compensen perder restricciones relacionales para cortes, edades, territorios, poblaciones, métodos y versiones.

### 2.6 Exportación

- **CSV:** biblioteca estándar de Python; definir codificación, delimitador, encabezados y protección de texto según necesidades de hoja de cálculo.
- **XLSX:** biblioteca de Python como `openpyxl` o `XlsxWriter`, seleccionada al prototipar formato y estilos; separar la exportación de la consulta estadística.
- **PDF:** comparar impresión desde navegador con generación de servidor. El resultado debe conservar tabla, fuente, fecha, filtros y notas metodológicas sin recalcular ni eludir la política de divulgación.

No se justifica decidir las tres bibliotecas ahora: la interfaz final y el formato de cada salida todavía deben validarse en prototipo.

## 3. Estrategia de rendimiento para conectividad limitada

La propuesta debe optimizar primero lo que siente quien navega y no perseguir la máxima cifra de solicitudes por segundo sin contexto. El primer candidato de diseño para cualquier backend es:

- HTML server-rendered para contenido, filtros, metadatos y tabla, con JavaScript progresivo y reducido para el gráfico y las interacciones que lo necesiten.
- Formularios que agrupen filtros en una petición; actualización parcial solo si no multiplica viajes de red y aporta una mejora visible.
- Recursos CSS/JS alojados localmente, versionados y cacheables; sin CDN obligatorio, fuentes remotas ni dependencias que bloqueen la página.
- Visualización construida con módulos seleccionados, y tabla equivalente accesible. No enviar miles de filas de casos al navegador.
- Consultas y cálculos agregados en el servidor, con columnas/filas mínimas; medir consultas y cachear agregados solo por versión de corte y filtros permitidos.
- Compresión del HTML y de recursos textuales en el servidor/proxy, con revisión de seguridad de las respuestas dinámicas; caché de navegador para recursos estáticos y respuestas públicas conforme a política.
- Medición de primera visita y visita repetida con latencia/ancho de banda acordados, incluyendo un equipo de recursos limitados. La página debe conservar contenido útil si no carga el gráfico.

El backend cambia la carga de CPU/memoria del servidor y la facilidad de desarrollo; el patrón de renderizado y los recursos determinan gran parte de los bytes y solicitudes del navegador. Por eso no hay base para prometer que Django, Go, Rust o C++ proporcionen la web más rápida hasta medir una misma página bajo condiciones iguales.

## 4. Comparación resumida de candidatos

| Candidato | Mayor ventaja general | Mayor costo/riesgo | Veredicto preliminar para el RNC |
|---|---|---|---|
| Django + HTML progresivo | Cobertura de web completa y ecosistema estadístico Python en una aplicación. | Menor CPU bruta que runtimes compilados; hay que controlar consultas y peso de recursos. | Referencia por facilidad/analítica, no ganador de conectividad sin medir. |
| Laravel + Blade | Framework integral y server-rendering con optimizaciones de despliegue. | Estadística principal fuera del ecosistema PHP si se necesita Python/R. | Finalista; puede igualar el perfil de red de Django con HTML optimizado. |
| ASP.NET Core MVC/Razor | Buenas herramientas de concurrencia, compresión, caché y diagnóstico. | Otra cadena de herramientas y posible costo de aprendizaje/integración estadística. | Finalista; puede superar tiempo de servidor, no necesariamente primer byte total ni transferencia. |
| FastAPI + cliente propio | Contratos API y concurrencia I/O en Python. | No incluye por sí mismo una experiencia completa; SPA/cliente separado aumenta piezas. | Comparar si una API reusable o interacción rica aporta suficiente valor. |
| Go + HTML templates | Binario simple, servidor HTTP y templates estándar, buen candidato de baja huella. | Más trabajo manual de aplicación y distancia al ecosistema de análisis estadístico. | Control para evaluar si ahorro medido de CPU/RAM compensa desarrollo. |
| Spring Boot MVC | Integración y capacidades amplias para sistemas institucionales. | Complejidad operacional/conceptual que puede sobrar para el volumen y equipo actuales. | Mantener si aparece experiencia/infraestructura Java o requisito institucional. |
| Node.js + SSR | JavaScript/TypeScript unifica UI y servidor; buen manejo de I/O. | Computación intensiva debe salir del event loop y los frameworks pueden añadir carga de cliente. | Alternativa si el equipo prefiere TypeScript o requiere UI rica; medir tareas CPU. |
| R Shiny | Gran ajuste para producir análisis y gráficos con R rápidamente. | El despliegue y el modelo reactivo/concurrencia deben evaluarse para un portal público completo. | Fuerte para dashboard estadístico o si métodos R existentes deciden el ecosistema. |
| Rust Axum | Control de recursos y rendimiento de bajo nivel. | Mayor curva de aprendizaje e integración de piezas y análisis. | No elegir por CPU teórica; reservar si el perfil medido prueba un cuello crítico. |

Los puntajes ordinales previos se retiran: daban apariencia de precisión sin que se hubiera medido el prototipo ni declarado pesos. La comparación documental permite recomendar provisionalmente un balance, pero no proclamar ganador de velocidad; falta comparar el mismo flujo en hardware y red equivalentes.

## 5. Selección y evaluación comparativa

**Ganador provisional por ajuste documental: Python + Django + HTML server-rendered/progresivo.** La recomendación combina la cobertura de un portal completo, la integración con métodos y bibliotecas analíticas en Python, y la experiencia que el estudiante ya tiene con Django y Python en su trabajo cotidiano (`SRC-RNC-009`, `EVD-084`). Esta experiencia reduce el aprendizaje inicial esperado y mejora la viabilidad del calendario; su efecto concreto en el esfuerzo se observará durante el prototipo. Django no gana por ser el lenguaje más rápido en CPU. En una conexión lenta, la diferencia principal la darán bytes, solicitudes, caché y consultas, no el framework por sí solo. La documentación consultada no permite concluir que Django sea más rápido de extremo a extremo: esa parte se verifica con una prueba equivalente.

Laravel y ASP.NET Core siguen siendo rivales serios: Laravel puede igualar HTML transferido y trae optimización de despliegue; ASP.NET aporta herramientas sólidas de rendimiento y compresión. Hoy no muestran una ventaja del proyecto suficiente para compensar introducir PHP o C# y sus bibliotecas analíticas correspondientes. FastAPI mantiene Python, pero añade piezas para el portal sin resolver mejor la conectividad si también se renderiza HTML. Go/Rust pueden reducir coste de CPU/memoria, pero no los bytes de la red y elevan el costo de desarrollo estadístico/web. Si el prototipo muestra tiempo de cómputo alto o el RNC ya domina/soporta otro stack, esta recomendación puede cambiar.

La selección del proyecto utilizará estos criterios, en este orden y de acuerdo con la prioridad comunicada:

1. **Experiencia con conectividad limitada:** bytes y solicitudes de carga inicial; contenido visible; carga tras aplicar filtros; visita repetida.
2. **Facilidad de implementación/mantenimiento y experiencia del equipo:** horas y piezas necesarias para construir el mismo flujo, claridad del código, dependencia de bibliotecas externas y experiencia previa del estudiante con el stack (`EVD-084`).
3. **Rendimiento del servidor:** TTFB, CPU/RAM y concurrencia mientras carga/agrega un CSV sintético de miles de filas.
4. **Adecuación estadística:** lectura del archivo, tipado, agrupación, precisión/reproducibilidad y disponibilidad de librerías apropiadas.
5. **Operación segura:** despliegue offline/local, actualización, secretos, respaldos, autorización, logs sin datos personales y costo de operación.

### Prueba comparativa necesaria

Implementar una rebanada de baja fidelidad del mismo escenario para cada finalista: abrir página de consulta, aplicar período/territorio/sexo/edad/tipo, ver tabla y gráfico agregados, paginar, exportar y regresar a filtros. Usar solo datos sintéticos. Mantener idénticos contenido, CSS, recursos de gráficos, datos, consultas, máquina y configuración de servidor. Probar:

- perfil de red definido con la tutoría/equipo (ancho de banda, latencia y pérdida si procede), en primera visita y visitas con caché;
- peso transferido, cantidad de solicitudes, tiempo de primer contenido y carga completa, funcionamiento sin JavaScript del gráfico;
- TTFB, duración de agregación, CPU, memoria y concurrencia básica;
- esfuerzo de desarrollo, curva de aprendizaje, claridad de integración analítica y esfuerzo de despliegue.

No reutilizar microdatos del CSV recibido en benchmarks o demos. El archivo sintético con miles de filas se generará en una etapa posterior, según lo previsto.

### Resultado que puede defenderse hoy

- **Patrón de interfaz recomendado para probar:** SSR + mejora progresiva, recursos locales y agregación del lado servidor. Es independiente del lenguaje y apunta directamente al costo de conectividad.
- **Stack provisional ganador por balance:** Python/Django, porque permite mantener aplicación y análisis en un ecosistema, ofrece las piezas de portal necesarias y el estudiante ya conoce Django y usa Python a diario. Esto es una recomendación documental de ajuste del producto y del equipo, no una victoria medida en rendimiento.
- **Candidatos que no se descartan:** Laravel, ASP.NET Core, FastAPI, Go, Spring, Node SSR y Shiny. La comparación documental no prueba que ninguno sea más lento ni peor para RNC; los motivos para no elegirlos hoy son costo de implementación, ajuste del caso o ausencia de una ventaja medida.
- **C++/Rust:** no adoptar por adelantado para “ser rápido”; la optimización solo se justifica en componentes que el benchmark identifique como cuello de CPU/memoria.

Pendientes antes de cerrar la selección académica: diccionario/grano del CSV; método estadístico y casos de referencia RNC; perfil realista de conectividad; alcance de administración y seguridad; revisión de despliegue con RNC/CUJAE; y benchmark equivalente entre Django, Laravel y ASP.NET Core (más Go como control de runtime). Si el resultado no confirma el balance de Django, se seleccionará al candidato que mejor responda a las mediciones. No se requiere que el RNC escoja primero una tecnología: debemos llevarle la comparación y la recomendación sustentada.

## Fuentes técnicas primarias

Las fuentes y fechas de consulta se registran como `SRC-TECH-001`–`SRC-TECH-022` en el [catálogo](../../sources/catalogo.md). Incluyen documentación oficial de los frameworks candidatos y sus prácticas de rendimiento/despliegue. El mapa de evidencias distingue las capacidades documentadas de las inferencias de ajuste al RNC. No se trasladan a este proyecto cifras de benchmark hechas en otro hardware/red.
