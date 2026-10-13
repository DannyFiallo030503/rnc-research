# Auditoría documental y de referencias — 2026-10-04

Estado: REVISIÓN DOCUMENTAL. Este archivo registra qué material se cotejó, qué se corrigió y qué requiere datos o validación del RNC. `rnc-research` es la base viva; los originales externos al repositorio conservan su carácter de fuente o antecedente.

## Cobertura del material recibido

| Material | Archivos revisados | Resultado |
|---|---|---|
| Proyecto y planificación | `ANEXO_A_Danny_Fiallo_Munoz.docx`, copia `(1)`, `Propuesta de Trabajo pag web RNC.pdf` y transcripción `.md`, `Resumen_Practicas_II_y_Tesis_RNC_Danny_Fiallo.docx`, `Investigacion_Negocio_Benchmark_RNC_2026.docx`, presentación inicial `.pptx` | Los dos Anexos tienen el mismo texto extraído. La propuesta y el Anexo delimitan el alcance; el resumen, la investigación y la presentación son síntesis/antecedentes que pueden contener decisiones anteriores al 30-09-2026. |
| Procedimiento y publicación cubana | `Man Proc Reg Nac Cáncer 16,5 x 23,5 cm Color.pdf` y transcripción `.md`; Anuario Estadístico de Salud 2024 publicado oficialmente en 2025 | Manual v. VII (2024) como referencia documental RNC; vigencia operativa y ejemplos de cálculo pendientes de confirmar. El Anuario etiqueta la incidencia 2022 como preliminar; eso no autoriza publicarla en la nueva web. |
| Escritura académica | `Buenas_prácticas_Escritura_Defensa_Trabajo_de_Diploma_Abril_2026.docx` | Guía de calidad, actualidad y datos bibliográficos, incorporada en `00-criterio-investigacion.md`. |
| Preguntas y reuniones previas | `Preguntas.md`, `Preguntas_Reunion_RNC.md`, `00-preparacion-primera-reunion.md`, `01-guia-reunion-primer-reunion.md` | Borradores históricos. El mapa vigente es `05-requisitos/mapa-de-preguntas.md`. |
| Material de otra investigación | `ANEXO_A_4to_Manuel_David_Montero_Crespo.docx` | Trata otro proyecto (geocodificación); no fundamenta requisitos del RNC. |
| Repositorio central | Todos los archivos Markdown de `rnc-research`, el DOCX de preguntas derivado y el catálogo de fuentes | Se cotejaron afirmaciones, enlaces, edades, población, naturaleza del dato, alcance y trazabilidad. |
| Copias archivadas | `rnc-research.tar.gz`, `rnc-research (1).tar.gz`, `rnc-research-v3.tar.gz` | Respaldos anteriores; la comparación de nombres no halló Markdown exclusivos de los archivos comprimidos. No se usan como versión vigente. |

La imagen `ANEXO_A_Danny_Fiallo_Munoz.jpg` es un recurso gráfico, no una fuente textual de requisitos. El archivo temporal `.tmp` no tiene valor documental identificado.

## Contraste de referencias y cambios hechos

| Tema | Hallazgo verificado | Rectificación en la base viva |
|---|---|---|
| Grupos de edad y población | Yinet confirmó el 30-09-2026 grupos quinquenales clásicos 0–4 a 85+, agrupaciones nuevas y población oficial ONEI para Cuba, provincia y municipio por sexo y edad simple (`SRC-RNC-005`). | Ya incorporado en reunión, preguntas, requisitos y contexto. Se conserva como pendiente la regla exacta de agrupación y la recepción de series. La población ONEI denominadora se distingue de la estándar para ajuste. |
| Publicación | La dirección del proyecto exige mostrar solo datos definitivos; la incidencia 2022 del Anuario 2024 figura como preliminar (`SRC-RNC-004`, `SRC-CUBA-AES-2024`). | Separados el carácter del Anuario y la política de la futura web. Pendiente el flujo de aprobación de cortes. |
| Entrada de datos | El proyecto indicó carga inicial Excel/CSV por una persona y conexión directa a BD para etapa posterior (`SRC-RNC-004`). | Corregidas referencias que sugerían BD como entrada inicial. El formato real del archivo y las validaciones siguen abiertos. |
| Manual | La ficha editorial indica 80 páginas bibliográficas; el archivo digital local contiene 95 páginas, incluidas cubiertas y preliminares (`SRC-RNC-003`). | Explicada la diferencia. No hay prueba documental de una edición posterior al manual VII de 2024. |
| Enlaces IARC | Dos enlaces directos del catálogo antiguo devolvían 404. | Sustituidos por el PDF funcional de Villa Clara (histórico) y la página editorial del capítulo de calidad (`SRC-IARC-CUBA-001`, `SRC-IARC-QC-001`). |
| IARC actual | CI5 volumen XII (2024) incluye capítulos de calidad/comparabilidad y ajuste por edad; la estrategia 2026–2030 anuncia evolución de CanReg y clasificaciones. | Se añadió `SRC-IARC-CI5XII-2024` y vigilancia `SRC-IARC-2026-ROADMAP`; la obra de calidad de 1994 quedó histórica. No se reemplazó automáticamente CIE-O-3/ICCC-3 documentadas en el manual cubano. |
| Portales actuales | GCO indica versión GLOBOCAN 2024 de 08-07-2026; SEER*Explorer muestra actualización 2026; ECIS separa observado y estimado; USCS muestra incidencia hasta 2023 y mortalidad hasta 2024 (`SRC-IARC-001`, `SRC-SEER-002`, `SRC-ECIS-001`, `SRC-CDC-002`). | Fechas y naturaleza de las series precisadas en fichas. Una estimación o un dato preliminar de otro portal no se equipara a incidencia definitiva del RNC. |
| Estudios de dashboards | El estudio de 210 paneles incluía 58 federales y 152 estatales, no 210 estatales (`SRC-DASH-US-2025`). La revisión exploratoria incluyó 89 publicaciones; 42 paneles eran accesibles y 26 artículos reportaron evaluación de usabilidad (`SRC-DASH-SCOPING-2025`). | Corregida la muestra y creada ficha con límites de interpretación. |
| Intervalos y supresión | CDC describe IC del 95 % con gamma modificado bajo variabilidad Poisson; la supresión complementaria procede de las notas de la base de uso público, no de la página técnica del visualizador (`SRC-CDC-CI-2026`, `SRC-CDC-PUBLIC-CAUTION-2026`). | Corregida la atribución. El umbral CDC de menos de 16 casos sigue siendo evidencia externa, no regla cubana. |
| Accesibilidad | W3C mantiene WCAG 2.2 como recomendación consultada; Colorado estudió WCAG 2.1 en su trabajo previo (`SRC-WCAG-001`, `SRC-CO-002`). | Separado el estándar actual del usado en el caso histórico. Nivel RNC por definir. |
| Ejemplos de registro | CaRDO cuenta con artículo y manual 2025; SWInCaRe es un estudio de 2019 (`SRC-CARDO-2025`, `SRC-CARDO-HANDBOOK-2025`, `SRC-SWINCARE-001`). | CaRDO se documentó como candidato de comparación especializado y SWInCaRe como antecedente histórico. |
| Bibliografía de la tesis | La guía universitaria pide fuentes actuales, completas, homogéneas, mayoritariamente de los últimos cinco años y presencia significativa de inglés (`SRC-UNI-001`). | Se agregó un criterio de revisión que distingue fecha de contenido de fecha de consulta. El catálogo de trabajo aún no equivale a una bibliografía final normalizada. |

## Inconsistencias de los borradores externos

- `Preguntas.md` y `01-guia-reunion-primer-reunion.md` llamaban originalmente «denominador del sistema de casos» a lo definido por la inclusión de casos; ya se corrigió esa frase. En una tasa de incidencia, los casos elegibles forman el **numerador** y la población en riesgo, el denominador.
- Esos borradores preguntan como si fueran desconocidos los grupos oficiales, la fuente de población y si se admitirán agrupaciones nuevas. Esas respuestas constan en `SRC-RNC-005`; solo quedan abiertas sus reglas detalladas.
- El resumen y la presentación inicial tratan opciones de stack, edades y flujo de datos como hipótesis previas. Para trabajo posterior se aplican `PROJECT_CONTEXT.md`, la línea base y el mapa de preguntas vigentes.
- La propuesta y el Anexo tienen una diferencia de calendario para la migración histórica: el Anexo la ubica en 2027. Se mantiene como asunto de planificación para validar con tutor; no se adelantó al alcance de Prácticas II.

## Pendientes que ninguna referencia externa puede cerrar

1. Confirmar vigencia operativa del Manual RNC VII y recibir esquema/ejemplo anonimizado de casos, archivos Excel/CSV y series ONEI prometidas, con años, edición, territorio, sexo, edad y regla temporal.
2. Obtener pesos de la población estándar, fórmulas y ejemplos oficiales de ajuste directo/indirecto e intervalos; validar tratamiento de cero y grupos personalizados.
3. Definir quién aprueba un corte definitivo, cómo se corrige/versiona, y la política cubana de conteos pequeños y confidencialidad.
4. Precisar perfiles, tareas prioritarias, nivel WCAG, conectividad de prueba y criterios de aceptación.
5. Preparar para el informe una bibliografía normalizada por tipo de fuente, con fecha de publicación/actualización y fecha de consulta; revisar versiones de portales y librerías antes de seleccionarlas.

## Regla de mantenimiento

En cada actualización registrar fecha de revisión del contenido, año de los datos, versión del portal/estándar y URL primaria. Etiquetar expresamente material histórico, propuesta o regla cubana confirmada. El catálogo `../sources/catalogo.md` y `evidence-map.md` deben actualizarse con cualquier nueva afirmación relevante.
