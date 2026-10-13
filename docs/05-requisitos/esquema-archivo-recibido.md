# Estructura observada del archivo recibido

Estado: estructura observada y estabilidad confirmada por Danny; diccionario y grano pendientes.

Fecha de inspección del archivo: 2026-10-12. Cotejo semántico con el Manual RNC: 2026-10-13. Archivo: `BD PARA DANI.csv`, ubicado en la raíz del espacio de trabajo.

## Contrato estructural conocido

- CSV en UTF-8, campos separados por coma.
- 84 encabezados, en el orden enumerado abajo.
- Danny confirmó el 2026-10-12 que los archivos que recibirá el proyecto conservarán esa misma estructura aunque el volumen futuro sea de miles de filas.
- La muestra actual contiene una sola fila no vacía; las 327 líneas restantes después del encabezado están vacías y no son registros de ejemplo.
- 50 de las 84 columnas tienen algún valor en esa fila de muestra. Una columna vacía en la muestra no debe eliminarse ni asumirse opcional.

## Encabezados en orden

```text
NOHOSP, PROVINFO, UNIDIDAD, NOMMEDI, FECHAR, TUMOURIDSOURCETABLE, SOURCERECORDID, FUENTEINF1, FUENTEINF2, FUENTEINF3, FUENTEINF4, VERIF, ESTADO, MODIF, FCHAINTO, EDAD, FECHAD, TOPO, BILATERAL, CODIPM, PMSEQ, PMTOT, MORF, COMP, T, N, M, S, CLINPATO, BASE, EXTEN, ETAPA, DIF, TUMOR, C10, CICN, FECHA1, TRANSHEMAT, LEU, LEUCRIN, LEUAGUDA, LEUMIEC, MIELMULT, CLASMIEL, LINFO, NING, OBSOLETEFLAGTUMOURTABLE, TUMOURID, PATIENTIDTUMOURTABLE, PATIENTRECORDIDTUMOURTABLE, TUMOURUPDATEDBY, TUMOURUNDUPLICATIONSTATUS, CIRUG, RADIO, QUIM, HORMON, IMMUN, OTRA, DESCON, MET, NOCASO, BUSCAR, NOMBRES, PRIMA, SEGA, SEXO, COLOR, NOID, FECHAN, DIREC, LOC, LUGAR, PROV, EMBARAZADA, VIH, ESTADOV, FECHAUC, CAUSA, OBSOLETEFLAGPATIENTTABLE, PATIENTRECORDID, PATIENTUPDATEDBY, PATIENTUPDATEDATE, PATIENTRECORDSTATUS, PATIENTCHECKSTATUS
```

## Qué falta para especificar el importador

La estabilidad del encabezado permite fijar el contrato estructural, pero no basta para definir validaciones o cálculos. Se debe obtener un diccionario autorizado que describa nombre/propósito, tipo, formato, dominio/códigos, nulabilidad y relaciones entre columnas. También falta confirmar si cada fila representa un tumor, una persona, un reporte u otra entidad; la muestra de una fila no responde ese grano. Determinar qué columnas deben ser obligatorias o pueden estar vacías y cómo se identifican cortes/años/cobertura. No inferir significado únicamente de los nombres abreviados.

No copiar a documentación, logs, capturas o ejemplos los valores de la fila real: contiene información sensible de salud y puede contener identificadores directos o indirectos. Las pruebas de volumen y de gráficos se prepararán más adelante con datos ficticios que respeten los 84 encabezados y sus dominios autorizados; no se reciclarán valores del registro de muestra.

## Contraste preliminar con las necesidades de consulta

Esta lectura contrasta los requisitos de filtros e indicadores con los **nombres de encabezado solamente**. No confirma el significado, las unidades, los códigos ni la adecuación epidemiológica de ningún campo; esa validación requiere el diccionario del RNC.

| Necesidad de la plataforma | Encabezados que podrían relacionarse | Resultado de la revisión |
|---|---|---|
| Edad / grupo de edad | `EDAD` | Hay un candidato nominal. Falta formato, unidad, codificación, fechas de referencia, tratamiento de edades desconocidas y si es edad al diagnóstico. |
| Sexo | `SEXO` | Hay un candidato nominal. Falta catálogo de códigos y regla de categorías desconocidas. |
| Clasificación/localización tumoral | `TOPO`, `MORF`; también aparece `C10` | El Manual define por separado localización/topografía (sitio anatómico y subsitio) y tipo histológico/morfología (diagnóstico histológico completo); el sistema usa CIE-O-3 en personas de 20 años o más y la clasificación infantil indicada para menores de 20. Para linfomas, la morfología identifica el tipo histológico y el formulario recoge aparte la clasificación Ann Arbor, que representa estadio; esta última no sustituye a la morfología. Las categorías analíticas deben usar el código/catálogo autorizado y su versión. `C10` permanece sin identificar. (Manual, pp. 11–17; formulario, pp. 73–74). |
| Territorio / posible ubicación más detallada | `PROV`, `LOC`, `LUGAR`, `DIREC`, `PROVINFO` | El Manual diferencia en el formulario dirección/residencia habitual, localidad, municipio y provincia; define municipio y provincia como residencia, y separa la provincia informante. El recuerdo de que `LOC` y `LUGAR` podrían ser equivalentes no permite fusionarlos: el Manual no asigna esos encabezados del CSV a sus campos. `DIREC` podría relacionarse con dirección, pero solo el diccionario puede establecerlo. Confirmar cuáles columnas corresponden a localidad, municipio/provincia de residencia, dirección y provincia informante; el Manual explicita codificación DPA para provincias, no la codificación municipal del archivo recibido. (Manual, pp. 11, 16–17; formulario e instructivo, pp. 73–74). |
| Año de incidencia | `FECHAR`, `FECHAD`, `FECHA1`, `FECHAN`, `FECHAUC`, `PATIENTUPDATEDATE` | Hay campos con apariencia de fecha, pero no un encabezado inequívoco de año de diagnóstico/incidencia. No seleccionar uno hasta conocer sus definiciones. |
| Frecuencias absolutas | Grano de las filas; posibles identificadores de tumor/persona | No se encontró un encabezado inequívoco de conteo agregado. Si cada fila es un tumor/caso contable, podría contarse tras validar el grano y las reglas; si el archivo está agregado, hace falta identificar la columna de conteo. |
| Corte definitivo, periodo/cobertura y procedencia | No se identifica un encabezado inequívoco en la lista | El estado definitivo, año(s) cubiertos, versión/código del corte y fecha de extracción podrían venir en metadatos externos o tener nombres no evidentes. Deben formar parte del contrato de entrega, aunque no necesariamente sean filtros del visitante. |
| Denominadores ONEI | No se identifica un encabezado de población por territorio/sexo/edad/año | La serie ONEI debe entregarse como insumo aparte o paquete complementario; es necesaria para tasas, no para conteos. Confirmar la estructura de esa serie. |
| Pesos de población estándar | No se identifica un encabezado de peso estándar | La tabla/versionado Segi–Doll es un insumo metodológico separado; no se debe buscar ni deducir de la fila de casos. |

### Lectura funcional inicial

Para filtros y gráficos se espera necesitar como mínimo año de incidencia, territorio de residencia al nivel de publicación aprobado, sexo, edad o grupo de edad, categoría tumoral y un numerador contable. Los encabezados muestran candidatos para edad, sexo, topografía, morfología y varias granularidades geográficas; **no permiten confirmar todavía el año, la jerarquía geográfica correcta ni el numerador**. El Manual confirma que municipio de residencia es una dimensión estadística usada en cuadros del RNC, pero el mapeo a `LOC`/`LUGAR` y los códigos del CSV siguen pendientes. Geografía y localización anatómica del tumor (`TOPO`) son conceptos diferentes; `MORF` describe el eje histológico. Para linfomas deben distinguirse histología y estadio Ann Arbor, si ambos se incluyen en la consulta. Las categorías visibles deben seguir los códigos y agrupaciones autorizados, no un campo supuesto. La necesidad no es que aparezcan literalmente columnas llamadas `AÑO` o `CONTEO`: esos datos pueden derivarse válidamente si el RNC confirma la semántica y el grano.

El archivo completo de 84 columnas puede seguir siendo el contrato estructural de recepción aunque la plataforma derive una vista analítica mínima. No se deben eliminar columnas del original ni guardarlas/reproducirlas en la zona pública por iniciativa del importador. La selección de campos derivados debe aprobarse tras el diccionario y el análisis de riesgo; identificadores, nombres, direcciones exactas, fuentes clínicas, tratamientos y otras variables que no sean necesarias para el cálculo no deben propagarse a la capa analítica pública. Si el RNC autoriza consulta municipal, debe publicarse el código/nombre municipal aprobado y excluir la dirección exacta. Conservar o eliminar temporalmente el original queda sujeto a la política institucional de acceso y retención.

El Anexo 3.1 del Manual describe el envío institucional de cierres desde las provincias y unidades al RNC: frecuencia bimestral según calendario, exportación desde el sistema automatizado, casos nuevos por año de diagnóstico, solo registros introducidos, validados y enviados por primera vez, sin pendientes ni variables obligatorias vacías, compactados y acompañados por el informe de cierre. También indica que esas bases no deben manipularse con otro software. Esto describe el circuito interno del RNC; **no demuestra que el CSV de muestra recibido por el proyecto sea el archivo de ese intercambio ni autoriza a procesarlo como tal**. Confirmar con el RNC el origen, autorización, transformación y propósito del CSV de prácticas antes de definir el importador (Manual, pp. 24–25 y Anexo 3.1, p. 76).

### Preguntas concretas para cerrar el mapeo

1. ¿Qué campo identifica la fecha/año de diagnóstico que se usa para incidencia, y qué significan las demás fechas?
2. ¿Qué campos representan provincia/municipio de residencia del caso y qué códigos/catálogo oficial usan? ¿Cuáles se refieren al hospital o a la fuente?
3. ¿Cada fila es un tumor, una persona, un reporte o una fila de otra granularidad? Si el archivo ya es agregado, ¿qué campo contiene el conteo y cuál es su unidad?
4. ¿Qué campos del archivo corresponden a localidad, municipio y provincia de residencia, y qué códigos usan? ¿Cómo se construirán las categorías públicas tumorales desde topografía y morfología; y, para linfomas, cómo se distinguirán histología y estadio Ann Arbor y qué versión/catálogo aplica?
5. ¿Cómo se identifican el corte definitivo, sus años, fecha de cierre/extracción y procedencia: dentro del CSV o en metadatos de entrega?
6. ¿Qué archivo complementario de población ONEI se usará y cómo se alinea con territorio, sexo, edad y año del numerador?
