# Manual de procedimientos del RNC de Cuba (2024): hallazgos

Estado: FUENTE OFICIAL CUBANA REVISADA; reglas según alcance del manual  
Cotejo inicial: 2026-09-30; revisión íntegra PDF y anexos gráficos: 2026-10-13  
Fuente: `SRC-RNC-003`  
Original: [Manual PDF](../../../Man%20Proc%20Reg%20Nac%20C%C3%A1ncer%2016%2C5%20x%2023%2C5%20cm%20Color.pdf)  
Texto consultable: [Markdown convertido](../../../Man%20Proc%20Reg%20Nac%20C%C3%A1ncer%2016%2C5%20x%2023%2C5%20cm%20Color.md)

## Alcance y lectura

Es la versión VII del Manual de Procedimientos del Registro Nacional de Cáncer de Cuba, publicada por MINSAP / Editorial Ciencias Médicas en 2024 (80 páginas bibliográficas; el PDF local tiene 95 páginas contando cubierta y preliminares). Sustituye al manual de 2010. Describe organización, captación, procesamiento, validación, estadísticas, confidencialidad y supervisión del registro. Es la fuente cubana principal de esta investigación para los procedimientos que documenta; su vigencia operativa actual debe confirmarse con el RNC.

Las referencias de página que siguen son las páginas impresas del manual. El Markdown es una conversión con errores puntuales de OCR y contenido de formularios que aparece como imagen; ante dudas sobre códigos, fórmulas o texto legal debe cotejarse el PDF. La existencia de una regla en el manual no confirma por sí misma una decisión nueva de interfaz o arquitectura.

### Cotejo íntegro PDF/Markdown — 13-10-2026

Se recorrieron las 95 páginas físicas del PDF con extracción textual página a página y se cotejaron los apartados de procedimiento y los anexos. Las páginas de formulario que no se extraen como texto se inspeccionaron visualmente: Anexo 2.1 (pp. 73–74), Anexos 2.2–2.3 (p. 75), Anexo 3.2 (p. 77), Anexo 4 (p. 78) y las guías de supervisión (pp. 80–83). Las páginas preliminares y anexos gráficos no aportan un diccionario del CSV del proyecto. En caso de discrepancia prevalece la imagen/PDF legible.

Hallazgos que afinan la lectura del esquema y el alcance del trabajo:

- El formulario de caso separa explícitamente **dirección/residencia habitual**, sus componentes de dirección, **localidad**, **municipio** y **provincia**. El instructivo define municipio como municipio de residencia y provincia según carné de identidad; la provincia informante aparece en otra sección. La codificación DPA 2011 se declara para provincias (p. 17), pero el manual no dice qué encabezado del CSV recibido equivale a esos campos ni da su código municipal. Por tanto, no se puede concluir que `LOC` y `LUGAR` sean equivalentes o que alguno sea el municipio solo por su nombre.
- En el mismo formulario, **localización (topografía)** es el sitio anatómico del tumor primario, con el mayor detalle/subsitio posible; **tipo histológico (morfología)** es el diagnóstico histológico completo. Son variables distintas. El manual describe CIE-O-3 para topografía/morfología desde 2007 en personas de 20 años o más y la clasificación infantil citada para menores de 20 (pp. 16–17).
- Para neoplasias hematológicas, el reporte incluye campos específicos de transformación y clasificación. La imagen del Anexo 2.1 muestra para linfomas el esquema Ann Arbor; se trata de estadio y debe mantenerse separado de la morfología que identifica el tipo histológico. Para analizar Hodgkin (o subtipos de linfoma) no basta la localización anatómica: hay que disponer de la variable/código histológico y, si la consulta trata extensión/estadio, del campo Ann Arbor. El manual no detalla aquí una regla nueva de agrupación para la plataforma.
- Los cuadros estadísticos incluyen incidencia total por **municipio de residencia** para provincias, con casos y tasas, así como cuadros por localización, morfología, sexo, grupo de edad, año, etapa clínica y unidad informante (pp. 36–38). Esto documenta dimensiones que el RNC usa en sus salidas; no aprueba automáticamente su publicación pública ni resuelve la política de celdas pequeñas.
- El Anexo 3.1 especifica el circuito de envío de cierres al RNC: último viernes cada dos meses según calendario, registros nuevos introducidos/validados/enviados por primera vez, ficheros por año de diagnóstico, sin pendientes ni variables obligatorias vacías, exportación desde el sistema, compactación y sin manipulación con otro software (p. 76). El Anexo 3.2 (p. 77) acompaña el cierre con territorio, fecha, responsable, reportes por año de diagnóstico, acumulado, observaciones y listado de números de reportes eliminados de la base. Este proceso interno no prueba que el CSV de muestra recibido por el proyecto sea ese paquete ni autoriza convertirlo; su origen y uso requieren aclaración.
- Los formularios de anexo confirman que el registro opera con documentos nominales/confidenciales, y que los formularios electrónicos/de transferencia y cierre son parte de un flujo controlado. La vista pública prevista debe seguir separada de esos microdatos; el manual no define supresión estadística de celdas ni controla la inferencia por combinación de filtros.

## Hallazgos por tema

### Propósito, cobertura y organización — pp. 1–9

- El RNC, creado en 1964, es un registro poblacional de alcance nacional. Su propósito incluye describir la epidemiología del cáncer, apoyar prevención, diagnóstico, tratamiento y planificación de recursos, e impulsar investigación.
- Su cobertura comprende las 15 provincias y el municipio especial Isla de la Juventud. Incluye a residentes permanentes de Cuba; el manual cita población media de ONEI para denominadores poblacionales.
- La red tiene niveles nacional, provincial y unidades informantes. El RNC central dirige técnicamente el sistema, controla procedimientos y calidad, asesora metodológicamente y emite estadísticas. Los departamentos territoriales revisan datos y coordinan las unidades informantes.
- El RNC central cuenta con grupos de control de calidad, análisis de datos e informatización, y procesamiento/edición. La Comisión Técnica Asesora aprueba cambios a procedimientos administrativos y técnicos.

### Definición de caso registrable — pp. 9–11

- Se reportan tumores primarios diagnosticados desde enero de 1964: invasivos, in situ, metástasis sin primario conocido diagnosticadas por primera vez, y tumores del sistema nervioso central benignos, de comportamiento incierto o malignos. También se incluyen NIC III desde 2007 en las topografías indicadas por el manual.
- Son registrables las personas cubanas con residencia permanente en el país. Se confecciona un reporte por cada tumor que cumpla la definición; metástasis de un tumor ya reportado no generan por sí solas un nuevo primario.
- La definición exige información mínima: nombre y primer apellido, fecha de nacimiento o edad, sexo, provincia de residencia, localización, morfología, comportamiento y año de incidencia.
- Si un fallecido no se reportó al diagnóstico, primero se busca información clínica. Si no se encuentra, se clasifica SCD (solo por certificado de defunción), se usa la fecha de fallecimiento como fecha de diagnóstico y se asigna incidencia al año del fallecimiento.
- El formulario incluye identificadores personales y datos clínicos. Es un registro individual confidencial, no un conjunto concebido para publicación con identificadores.

### Codificación, edad y variables — pp. 10–17

- Para topografía y morfología de personas de 20 años o más, diagnosticadas desde 1-1-2007, se usa CIE-O, tercera edición (CIE-O-3). En menores de 20 se usa la Clasificación Internacional de Tumores en la Infancia, tercera edición (ICCC-3; edición identificada en la referencia bibliográfica 6).
- Provincias se codifican según la división político-administrativa vigente desde 2011; unidades informantes usan los códigos de MINSAP listados en el Anexo 1.
- Edad es la edad cumplida al diagnóstico. Para estadísticas pediátricas el umbral es menor de 20 años. El manual enumera estratos publicados (20–29, 30–44, 45–59 y 60+, además de menor de 20), pero no especifica una tabla completa de bandas etarias finas ni los pesos de edad de la población mundial.
- El formulario de caso incluye identidad, nombre, sexo, color de piel, residencia, provincia/municipio, embarazo y trimestre, VIH, historia clínica, fecha de diagnóstico, topografía, lateralidad, morfología, TNM, tumor primario/metástasis, base más válida de diagnóstico, extensión y etapa clínica, grado, transformación hematológica, síntomas, fuentes, unidad/provincia informante y datos del médico. No todos estos campos son dimensiones de publicación.
- El manual define población residente media como semisuma de la población al inicio y al final del año, y cita un total nacional ONEI para 2023 (p. 4). No incorpora series de población por grupos de edad, sexo, provincia y año requeridas para reproducir todos los denominadores.

### Captación y flujo de datos — pp. 8–9, 15–25

- La captación es mixta: reporte pasivo por médicos y búsqueda activa en anatomía patológica, laboratorios clínicos/hematología, egresos, certificados de defunción e historias clínicas.
- La unidad informante crea el reporte, registra casos en el sistema automatizado vigente y mantiene controles locales. Las provincias revisan reportes y bases, reclaman reparos y envían cierres al RNC. El RNC central valida los cierres, conserva originales por provincia/año/cierre, detecta duplicados, contrasta mortalidad e incorpora a la base general solo casos validados.
- Las unidades hospitalarias reciben reportes diariamente, revisan fuentes semanalmente, verifican casos pendientes mensualmente y reportan mensualmente al territorio; los casos sin diagnósticos en el mes se notifican como cero. Territorios remiten al RNC con el calendario estadístico anual. Las unidades nacionales remiten cada dos meses según ese calendario.
- Los reparos se responden en 15 días; los casos CDI remitidos para búsqueda clínica se devuelven con información, o se señalan como no encontrados, dentro de plazos descritos (un mes o dos meses según el nivel/procedimiento).
- El Anexo 3.1 precisa para cada dos meses el último viernes como cierre de envío al RNC; pide casos nuevos introducidos, validados y enviados por primera vez, separados por año de diagnóstico, sin pendientes ni variables obligatorias vacías, sin duplicados idénticos ni manipulación externa al software. Esto debe conservarse junto a los procedimientos mensuales locales, no reducirse a una única frecuencia de carga.
- Los anexos incluyen el directorio de unidades informantes (anexo 1), formularios de reporte/control (anexo 2), requisitos y cierre de envíos (anexo 3), compromiso de confidencialidad (anexo 4), solicitud de datos/servicio (anexo 5) y guías de supervisión (anexo 6). Algunos formularios son imágenes y su texto no se extrae íntegro en el Markdown.
- El RNC distribuye en marzo las bases del último año procesado con cifras definitivas y envía antes del 1 de marzo los resultados anuales (provisionales o definitivos) para el Anuario. Se conservan bases por año con las cifras emitidas. El manual no define criterios técnicos completos ni un historial de cambios para pasar de provisional a definitivo.
- Se menciona un sistema automatizado único nacional, cuyo cambio requiere aprobación del RNC. El manual no identifica el nombre ni versión del software, formato técnico del intercambio, API o arquitectura.

### Duplicados, múltiples primarios y CDI/SCD — pp. 25–29

- Duplicado: mismo individuo repetido por el mismo diagnóstico; un segundo tumor primario distinto no es duplicado y debe conservarse como otro caso.
- La oficina central ejecuta pareamiento probabilístico en la base nacional. Compara identidad/tarjeta del menor, nombres y apellidos, fecha de nacimiento, sexo, topografía y morfología. Revisa identidades exactas y parecidas, incluidos errores de dígitos y variaciones de nombres.
- Para múltiples primarios aplica reglas IARC mediante IARC Tools / Multiple Primaries. Para duplicados reales consolida datos: con fechas de diagnóstico a no más de tres meses, usa como referencia la institución de mayor nivel y completa campos con otros reportes; con diferencia superior, prioriza la fecha más antigua. Discrepancias clínicas requieren buscar historias y elegir el código más completo o el de mayor nivel institucional.
- CDI significa inicialmente detectado por certificado de defunción, pendiente de recuperar historia clínica; si se obtiene, se asigna al año de diagnóstico. SCD queda solo con la evidencia del certificado y se atribuye al año de fallecimiento. SCD inferior al 10 % es el comportamiento esperado según el manual.

### Calidad y validaciones — pp. 29–35, 45–47

El manual define procedimientos operativos e indicadores, por tanto responde en buena medida qué calidad mide el RNC:

- Exhaustividad: conciliación de reportes físicos y base; volumen trimestral esperado 25/50/75/100 %; comparación anual con años previos; búsqueda activa y CDI/SCD. CDI/SCD normal por debajo de 10 %; se evalúa subregistro mediante inspección.
- Completitud de variables esenciales: edad, sexo, residencia/geografía y topografía desconocidas por debajo de 2 %; se solicita completar y, si no se recupera en 72 horas, se acude a la unidad.
- Verificación histológica/citológica: se calcula sobre todos los casos, incluidos SCD; valor aceptable superior a 80 %. Morfología desconocida por encima de 20 % indica mala calidad.
- Estadio desconocido/TNM, sitio primario desconocido, topografía/morfología mal definida (SAI), subsitio anatómico SAI, base más válida de diagnóstico y promedio de fuentes por caso (en unidades informantes).
- Validez/consistencia: datos faltantes, incompatibilidades, morfología/base diagnóstica, lateralidad, nacimiento/edad/fecha de incidencia, topografía/morfología, sexo/topografía e histología, comportamiento/topografía/histología, grado/histología y otras validaciones IARC Check. El manual da un rango de 80–100 % para los indicadores de consistencia indicados.
- Comportamiento del sistema: casos por mes/unidad, porcentaje por base diagnóstica y quinto dígito morfológico; estabilidad temporal de tasas, patrón por edad, cáncer infantil y cociente mortalidad/incidencia (M:I = muertes por cáncer del año / casos nuevos de cáncer del año). M:I superior a 1 se interpreta como posible subregistro, considerando localización y otras señales.
- Frecuencias e indicadores se desglosan por país, provincia, unidad, localización y año; varias evaluaciones son trimestrales, semestrales o anuales según el indicador.

El manual no prescribe que estos indicadores deban mostrarse al público en la nueva plataforma. Hay que separar controles internos del registro y metadatos publicables.

### Estadísticas publicadas y metodología — pp. 3–4, 36–38

- El objetivo incluye frecuencias; tasas específicas por edad y sexo; tasas crudas; tasas ajustadas a población estándar mundial; por topografía, grupos diagnósticos y edad, Cuba y provincias.
- Los cuadros incluyen casos, tasas crudas, específicas y ajustadas a población mundial; desgloses por sexo, provincia/municipio, localización/aparato, edad, año, morfología, etapa clínica, unidad informante y base válida de diagnóstico. Incluyen listados de primeras localizaciones y tablas de calidad.
- Población de cobertura se define con población residente y el manual identifica población media como semisuma de población al inicio y final del año.
- **El manual no da fórmula reproducible de tasa cruda, tasa específica, ajuste directo, ajuste indirecto, pesos/versión exacta de la población estándar ni intervalos de confianza.** Solo confirma tasas ajustadas a la población estándar mundial como salida. No documenta método indirecto ni intervalos Poisson/normal.
- No fija celdas pequeñas, umbral de supresión, supresión complementaria ni protección frente a inferencia por filtros. Confidencialidad sí está regulada para microdatos e intercambio.

### Confidencialidad, seguridad y uso de datos — pp. 39–45, anexos 4–5

- Los datos identificables y los fallecidos están sometidos a confidencialidad. El acceso se limita a personal del RNC por tareas y autorización; los formularios se custodian en lugares restringidos y se requiere compromiso firmado.
- Los sistemas deben tener claves y niveles de acceso; los datos de identificación deben codificarse/cifrarse cuando proceda. Acceso restringido con usuario/clave, credenciales protegidas y cambio periódico. Copia diaria de la base a dispositivo externo; copias bajo llave y copia extra en ubicación segura.
- Transferencias identificables se protegen y vinculan mediante número; correo con bases compactadas conforme anexos. Desarrolladores que accedan por soporte firman confidencialidad y solo usan datos para esa tarea.
- No se entregan datos personales identificables a terceros, incluso de fallecidos. Las entregas para investigación/uso institucional son anónimas/disociadas, con justificación de bien público, formulario y acuerdo; las aprueba el jefe del RNC y pueden revocarse por incumplimiento.
- Esto establece principios y controles generales, pero no especifica roles detallados de una plataforma nueva, auditoría digital, seguridad de infraestructura web, cifrado concreto, estándar técnico de anonimización ni controles de divulgación estadística.

### Supervisiones — pp. 45–47, anexo 6

Hay supervisión territorial semestral y del RNC anual, con cronograma, inspección de fuentes, revisión de formularios/calidad, informe a directivos y visitas para recuperar subregistro. Los instrumentos comprueban personal, manuales, codificación, uso del sistema, fuentes, controles, reportes y seguimiento de dificultades.

## Resultado del cotejo con las preguntas existentes

Ver el estado por ID en `../05-requisitos/mapa-de-preguntas.md`. El manual cierra las reglas de inclusión, codificación por grupo de edad, duplicados y varios indicadores de calidad. Responde parcialmente grupos de edad, población estándar, cadencia y estados de publicación, así como el proceso/software actual. Deja sin responder los métodos estadísticos reproducibles, política de celdas pequeñas, necesidades de usuarios y nivel WCAG.

## Implicaciones para Prácticas II

1. Actualizar el modelo conceptual con personas, tumores/reportes separados, múltiples primarios, residencia/territorio, fuente, fecha de diagnóstico, fecha de reporte, base diagnóstica, estado de validación, CDI/SCD y metadatos de cierre. Evitar modelar “paciente” y “caso/tumor” como una sola entidad.
2. La dirección del proyecto (`SRC-RNC-004`) confirma web pública y suministro inicial por archivos Excel/CSV; la conexión directa a una base de datos queda para una etapa posterior. Respetar la confidencialidad del manual: publicar resultados agregados y no convertir el portal público en el sistema de registro ni replicar flujos nominales sin autorización explícita.
3. Solicitar al RNC tablas de ejemplo, las series ONEI prometidas por año/territorio/edad simple/sexo (`SRC-RNC-005`), pesos de población estándar, cálculos de referencia, intervalos de confianza, política de publicación agregada, calendarios vigentes y especificación del sistema automatizado.
4. Usar los umbrales internos del manual como contexto de control de calidad, sin trasladarlos automáticamente a mensajes públicos o criterios de supresión.
5. Mantener en la reunión la validación de vigencia y alcance de la versión VII, la interpretación de la pauta de datos anónimos y las reglas estadísticas que el manual no formula.
