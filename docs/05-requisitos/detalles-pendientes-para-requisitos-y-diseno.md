# Decisiones pendientes para requisitos y diseño de la plataforma del RNC

**Actualizado:** 6 de octubre de 2026, tras la aclaración `SRC-RNC-007`. Documento breve para conversación con el RNC; estado de cada cuestión en el [mapa de preguntas](mapa-de-preguntas.md). Fundamento y fuentes en la [investigación cubana](../03-metodologia/03-investigacion-fuentes-cubanas-privacidad-2026-10-06.md).

## Información ya aclarada

- Las tablas clásicas usan grupos quinquenales de 0–4 hasta 85+. Debe poderse crear una agrupación nueva sin alterar esas tablas.
- La población denominadora proviene de ONEI; el RNC facilitará desgloses por Cuba, provincia, municipio, sexo y edad simple. El *Anuario Demográfico 2024* ofrece parte de esos datos, pero aún falta el archivo exacto que se usará en el sistema.
- Para el ajuste por edad del cáncer se toma como referencia la **estándar mundial** documentada por IARC/CI5 y citada en Manual VII y Anuario de Salud 2024. La población cubana ONEI es el denominador de las tasas, no una tabla de pesos alternativos.
- Los archivos proceden de un sistema interno que ya depura y entrega datos definitivos. La nueva plataforma no corrige los registros definitivos.
- La consulta será pública y la entrada inicial usará archivos Excel/CSV. La conexión directa a la base interna pertenece a una etapa posterior.
- El RNC no incorpora actualmente intervalos de confianza en este producto; se pueden proponer como nueva función.
- La confidencialidad específica de las salidas agregadas y los perfiles de usuario todavía deben conversarse. La actualización se prevé con una cadencia habitual de registro, sin calendario exacto confirmado.

## Preguntas prioritarias que sí requieren respuesta o archivo

### 1. Población estándar y tasas ajustadas

La aclaración posterior del estudiante resuelve la ambigüedad: se usan normas internacionales de cáncer y población cubana para denominadores. La tabla de pesos mundial Segi/Doll está documentada por [IARC/CI5](https://ci5.iarc.who.int/ci5-xii/about/) para 18 grupos quinquenales. Pedimos **una tasa directa publicada y sus datos de entrada** para comprobar la edición, el redondeo y las reglas de edades faltantes. Para el ajuste indirecto: ¿qué medida y tasas de referencia se esperan? (`Q-004` a `Q-006`).

### 2. Series ONEI y correspondencia de datos

¿Pueden facilitarse los archivos de población por **año × territorio × sexo × edad simple**, su edición, fuente y códigos territoriales? ¿Corresponden a población media anual, efectiva u otra serie? ¿Qué regla se aplica cuando falta una combinación? La cifra de población de una tasa debe corresponder al mismo período y estrato que los casos (`Q-016`).

### 3. Definición de frecuencia relativa

El denominador de un porcentaje de casos es un **total de casos**, distinto de la población ONEI que denomina una tasa. ¿Cuál es el universo de casos para cada porcentaje publicado y cómo se manejan categorías desconocidas y redondeo? Solicitamos una tabla o cálculo de ejemplo (`Q-018`).

### 4. Contrato de los archivos definitivos

Ya se dispone de `BD PARA DANI.csv` como ejemplo de estructura y Danny confirmó que futuras entregas conservarán los mismos 84 encabezados y orden, aunque varíe la cantidad de filas (ver `esquema-archivo-recibido.md`). ¿Puede facilitarse el diccionario autorizado de columnas, tipos, formatos, codificación, catálogos, años y metadatos? ¿Cada fila representa un tumor/caso, persona, reporte u otra entidad? ¿Qué identificador y señal del sistema interno acreditan origen y estado definitivo? ¿Cómo debe comunicarse un **rechazo técnico** por formato, integridad o cobertura sin modificar el archivo definitivo? (`Q-017`, `Q-008`).

### 5. Agrupaciones de edad nuevas

¿Quién puede definir una agrupación nueva; se guarda o solo vive durante la consulta? ¿Debe cubrir todas las edades sin huecos ni solapamientos? ¿Puede usarse para tasas ajustadas o solo para tablas y tasas específicas? ¿Cómo se enlaza cada grupo con edades simples y pesos del estándar? (`Q-003`).

### 6. Intervalos de confianza como propuesta

¿Se acepta mostrarlos como función nueva? De ser así, ¿nivel (por ejemplo 95 %), método para conteos y tasas, tratamiento de cero y conteos pequeños, y ejemplos de resultados esperados? La elección del método se propondrá y validará antes de implementarse (`Q-009`).

### 7. Confidencialidad de consultas y exportaciones

La Constitución, la Ley 149/2022 y la Resolución 58/2022 protegen datos personales y sensibles; no establecen por sí solas un número universal de casos para ocultar una celda. Proponemos publicar solo agregados autorizados, evaluar combinaciones de filtros que permitan inferencias, controlar descargas con la misma política y documentar supresión/redondeo cuando proceda. ¿Quién aprueba la política institucional, quién revisa resultados con pocos casos y qué datos nunca deben salir? (`Q-007`).

### 8. Responsabilidades del panel y publicación

¿Qué tareas exactas harán el doctor encargado y el personal de mantenimiento? ¿Quién incorpora archivos definitivos, ve incidencias técnicas, autoriza las salidas agregadas y administra series ONEI? ¿Qué acciones requieren registro de acceso o auditoría? Estas preguntas no suponen una nueva aprobación de la definitividad del archivo (`Q-017`).

### 9. Actualización y trazabilidad

¿Qué calendario aproximado de nuevos archivos definitivos se espera? ¿Qué año diagnóstico, fecha de recepción, fuente, identificador o huella y versión deben mostrarse al público? ¿Qué procedimiento excepcional seguiría la plataforma ante un error de transferencia, sin corregir casos en ella? Las cifras preliminares del Anuario de Salud 2024 y los archivos definitivos entrantes se tratarán como series diferentes mientras no se demuestre su relación (`Q-008`, `Q-010`).

### 10. Validación y experiencia de uso

Proponemos tareas representativas para público general, profesionales e investigadores; salida tabular accesible junto a gráficos; navegación por teclado; criterios WCAG 2.2 nivel AA; páginas ligeras para conectividad cubana; y pruebas de cálculos contra ejemplos aprobados. ¿Qué perfiles pueden participar en la revisión y qué condiciones de infraestructura, navegadores, tiempo de respuesta y descarga deben tomarse como metas? (`Q-014`, `Q-015`, `Q-019`).

## Material más útil para la siguiente reunión

1. Un archivo de datos definitivo autorizado y su diccionario.
2. La serie ONEI exacta que corresponderá a esos datos.
3. Dos o tres ejemplos de tasas RNC ya calculadas, con casos y denominadores usados, para contrastar la tabla mundial IARC y el redondeo.
4. Un ejemplo de tabla con frecuencia relativa y la definición de su total.
5. Un responsable que pueda revisar la política de divulgación y las funciones del panel.
