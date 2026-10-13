# Estado de la investigación

Estado: CONFIRMADO COMO CONTEXTO DE TRABAJO
Corte: 2026-10-12

## Fase actual

`Fase 0 — conocimiento del negocio, diseño conceptual y validación con el RNC`

La primera reunión formal con el RNC permanece pendiente en la documentación disponible. El conocimiento documental avanzó con la lectura íntegra del Manual de Procedimientos versión VII (2024). Yinet aclaró por escrito el 2026-09-30 grupos de edad y población (`SRC-RNC-005`). Aún se necesitan especialistas para validar vigencia, cerrar los vacíos restantes y convertir acuerdos de diseño en requisitos.

Las aclaraciones del estudiante fijan una web pública para cualquier persona, con consulta de archivos definitivos solamente. Yinet confirmó grupos quinquenales clásicos de 0–4 a 85+ y la creación de agrupaciones adicionales, sin modificar los clásicos. También confirmó población denominadora ONEI para Cuba, provincia y municipio, por sexo y edad simple; el RNC entregará las series. El prototipo administrativo recibe archivos CSV/Excel que un sistema interno ya depuró y declaró definitivos. La muestra `BD PARA DANI.csv` tiene 84 columnas y una fila con datos; Danny confirmó el 12-10-2026 que la estructura y orden de columnas se mantendrán en entregas futuras, aunque tengan miles de filas (ver `05-requisitos/esquema-archivo-recibido.md`). No corrige casos ni deduplica registros: comprueba el contrato técnico y la compatibilidad de denominadores. La conexión a BD queda para otra etapa. Siguen pendientes diccionario, semántica/grano, reglas de integridad, roles, política de divulgación agregada y calendario preciso. La web debe ser atractiva y ligera ante la conectividad cubana; la corrección estadística tiene prioridad sobre la rapidez. Ver `SRC-RNC-006`, REQ-F-010..013, REQ-D-003 y Q-003/004/007/016/017/018.

## Qué ya está cubierto

### Proyecto

El Anexo A y la Propuesta de Trabajo ya fueron cruzados. Se conoce el alcance temporal de Prácticas II y qué actividades quedan para la tesis.

La primera línea base trazable de requisitos/entregables está en `05-requisitos/linea-base-practicas-ii.md`; valida contra el Anexo antes de añadir alcance.

Fuentes: `SRC-RNC-001`, `SRC-RNC-002`.

### Negocio cubano

Ya se documentó el Anuario Estadístico de Salud 2024, literatura histórica y el texto íntegro del Manual RNC 2024. El manual define alcance de casos, codificación, flujo, controles, indicadores de calidad, cuadros estadísticos, confidencialidad y supervisiones. Ver `01-negocio/06-manual-procedimientos-2024.md`.

La revisión del 06-10-2026 añadió el *Anuario Demográfico ONEI 2024*, la Gaceta Oficial con Ley 149/2022 y Resolución 58/2022 y un contraste de las nuevas aclaraciones con las fuentes cubanas. Ver `03-metodologia/03-investigacion-fuentes-cubanas-privacidad-2026-10-06.md`.

Fuentes: `SRC-CUBA-AES-2024`, `SRC-RNC-HIST-001`, `SRC-RNC-003`.

### Benchmark

Ya existen fichas para SEER, GLOBOCAN/Cancer Today, ECIS, USCS, North Carolina, Colorado, Missouri y Cali.

### UX/UI

Ya existe evidencia externa sobre problemas de orientación, controles, feedback, evaluación iterativa, accesibilidad y utilidad de dashboards.

### Calidad

Ya se incorporó el marco IARC de comparabilidad, validez, oportunidad y completitud, junto con indicadores europeos de calidad y documentación CDC sobre incertidumbre, supresión y retrasos.

## Qué todavía falta investigar

### Prioridad 1: negocio estadístico del RNC

- reglas de creación y uso de agrupaciones adicionales con los pesos mundiales Segi/Doll documentados por IARC/CI5;
- entrega, años, edición y regla temporal de las series ONEI por territorio, sexo y edad simple;
- fórmula reproducible de tasas, ajuste directo y método indirecto;
- intervalos de confianza propuestos: nivel, método y ejemplos verificables;
- supresión de celdas pequeñas y riesgo de inferencia;
- contrato del archivo definitivo que entrega el sistema interno, roles de incorporación y trazabilidad sin alterar el contenido;
- regla del RNC sobre publicar conteos pequeños; por el momento no se conoce una regla específica y debe confirmarse cómo se preserva confidencialidad en resultados agregados;
- confirmación de vigencia del manual, calendario, software y formatos de intercambio; cotejo de una tasa RNC con la estándar mundial publicada. La aclaración `SRC-RNC-007` retiró la hipótesis de pesos cubanos alternativos.

### Prioridad 2: publicación y consumo de estadísticas

- cómo se construyen las tablas actuales;
- indicadores mínimos que necesita un investigador;
- qué comparaciones se realizan realmente;
- qué salidas se descargan;
- qué indicadores de calidad (si alguno) deben acompañar una salida pública y qué tareas/preguntas priorizar para los perfiles de público general, comunidad médica y académica.

### Prioridad 3: benchmark de fracaso

Seguir buscando estudios y publicaciones que documenten problemas reales de:

- usabilidad;
- accesibilidad;
- interpretación estadística;
- actualizaciones;
- disponibilidad del servicio;
- mantenimiento;
- sobrecarga visual;
- falta de metodología;
- errores derivados de clasificación o comparabilidad.

### Prioridad 4: evidencia académica

Seguir incorporando tesis y artículos específicamente sobre registros poblacionales de cáncer, visualización epidemiológica y evaluación de herramientas.

## Qué no debe hacerse todavía

No cerrar framework frontend, backend, motor estadístico ni base de datos solo porque aparezcan como opciones en benchmark.

No cambiar la prioridad del proyecto: las medidas de rendimiento deben preservar resultados correctos y reproducibles.

No fijar una política de supresión de pocos casos a partir del estándar de otro país.

No asumir que una clasificación, grupo de edad, población estándar o fórmula extranjera coincide con Cuba.

No presentar proyecciones o estimaciones como si fueran incidencia observada del RNC.

## Siguiente objetivo de investigación

Obtener del RNC ejemplos verificables para cerrar el negocio estadístico que conecte:

`concepto → definición → fórmula/metodología → fuente → ejemplo publicado → riesgo de implementación → pregunta al RNC`.
