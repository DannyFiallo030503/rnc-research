# CI5 XII: estandarización por edad y lectura de referencias

Estado: síntesis metodológica externa contrastada con el capítulo oficial y las imágenes recibidas.

Fecha de revisión: 2026-10-12. Archivo de transcripción: [`MasDatos.txt`](../../../MasDatos.txt). Imágenes de las páginas 148–150: [`2.jpg`](../../../2.jpg), [`3.jpg`](../../../3.jpg), [`4.jpg`](../../../4.jpg). Fuente bibliográfica íntegra: capítulo 7 de *Cancer Incidence in Five Continents*, volumen XII (IARC, 2024), `SRC-IARC-CI5XII-2024`.

## Aportes principales

1. **Inspeccionar primero las tasas específicas por edad.** CI5 recomienda revisar su patrón antes de resumirlo: puede revelar anomalías del dato y explicar diferencias que una tasa global ocultaría. Para el portal esto respalda mostrar tasas específicas por edad como salida analítica junto a la ajustada, sin afirmar que el patrón por sí solo identifica causas.
2. **Separar tasa cruda de tasa ajustada.** La tasa cruda describe la incidencia observada de la población y su estructura de edad. No elimina el efecto de diferencias etarias, por lo que no debe usarse sola para comparar territorios/poblaciones con estructuras distintas.
3. **La tasa ajustada directa es una medida resumen hipotética.** Aplica las tasas específicas observadas a una distribución estándar. Se comparan tasas ajustadas solo si comparten estándar, grupos de edad, periodo, definiciones y unidad. No es la tasa cruda observada de la población ni una probabilidad individual.
4. **La estándar Segi–Doll se mantiene en CI5 XII (2024).** El capítulo explica su continuidad práctica e histórica. Las 18 ponderaciones de 0–4 a 85+ coinciden con los grupos clásicos informados para el RNC. Es una referencia internacional sólida para el cálculo piloto, sujeta al cotejo numérico pendiente con el RNC; no convierte automáticamente cada detalle de CI5 en regla cubana.
5. **El ajuste directo y su error estándar tienen una base reproducible bajo Poisson.** La fórmula de CI5 puede implementarse en una prueba técnica; el nivel y el método para convertir el error estándar en intervalos que se publiquen deben acordarse aparte.
6. **Edades desconocidas y grupos abiertos afectan el resultado.** CI5 corrige las medidas resumen por la proporción total/conocida de casos de la misma combinación de sexo y tipo de cáncer, bajo el supuesto de que desconocer la edad es independiente de la edad real. El propio capítulo advierte que este supuesto puede fallar, por ejemplo, si la edad se omite más entre personas mayores. También indica que limitar los datos de edades altas a 75+ u 80+ puede cambiar la tasa ajustada. Son temas de calidad y reglas por confirmar con el RNC.
7. **Tasa acumulada/riesgo acumulado son conceptos útiles, pero no están en el alcance confirmado.** La tasa acumulada requiere declarar el rango de edad; CI5 XII usa 0–64 y 0–74. El riesgo acumulado se obtiene como `1 − exp(−tasa acumulada)` y aproxima la probabilidad en ausencia de otras causas de muerte; para riesgos menores de 10% la aproximación tasa/riesgo es estrecha. Registrar como posible métrica futura, no añadir al alcance sin tutor/RNC.

## Fórmulas de referencia

Sea `dᵢ` el número de casos, `yᵢ` los persona-años en riesgo y `wᵢ` el peso Segi–Doll del grupo `i`. La tabla de CI5 usa pesos absolutos cuya suma es `W = 100 000`.

**Tasa cruda anual por 100 000:**

```text
100 000 × (Σ dᵢ / Σ yᵢ)
```

**Tasa específica anual del grupo `i` por 100 000:**

```text
rᵢ = 100 000 × dᵢ / yᵢ
```

**Tasa ajustada directa (ASR) por 100 000:** ambas expresiones son equivalentes cuando `Σwᵢ = 100 000`:

```text
Σ (wᵢ × dᵢ / yᵢ)
Σ ((wᵢ / 100 000) × rᵢ)
```

Si se usan pesos proporcionales que suman 1 en vez de los pesos absolutos CI5, hay que aplicar la tasa `rᵢ` en las unidades publicadas. Evitar mezclar normalizaciones o multiplicar por 100 000 dos veces.

**Varianza y error estándar del ASR bajo Poisson:**

```text
Var(ASR) = Σ [dᵢ × (wᵢ / yᵢ)²]
SE(ASR) = √Var(ASR)
```

El error estándar no es por sí mismo un intervalo de confianza. Por ejemplo, `ASR ± z × SE` sería una aproximación normal cuya aceptabilidad para conteos bajos, ceros y límites debe evaluarse; CI5 XII presenta el error estándar y no fija la política de IC del RNC. `Q-009` sigue abierta.

**Corrección CI5 descrita para edades desconocidas:** multiplicar el ASR y su error estándar calculados con edad conocida por `T/K`, donde `T` son todos los casos del mismo tipo de cáncer y sexo, y `K` los casos con edad conocida. Depende del supuesto de distribución aleatoria de edades desconocidas; no implementar como política RNC hasta validarlo (`Q-021`), además de confirmar la disponibilidad de campos y cifras.

**Tasa acumulada hasta una edad definida:** para bandas quinquenales, suponiendo tasa constante dentro de cada banda:

```text
CR = 5 × Σ (dᵢ / yᵢ)
Riesgo acumulado = 1 − exp(−CR)
```

`CR` está en escala de proporción; multiplicar por 100 para expresarlo en porcentaje. Si se parte de tasas `rᵢ` expresadas por 100 000, `CR = 5 × Σ(rᵢ / 100 000)`. Especificar explícitamente el intervalo (por ejemplo 0–64 o 0–74). No confundir esta medida con la tasa anual por 100 000.

## Corrección necesaria a `MasDatos.txt`

`MasDatos.txt` es una transcripción, no la fuente que debe usarse para programar. Las fotos `2.jpg` y `3.jpg` confirman los datos del libro impreso y el PDF oficial de IARC permite comprobarlos con mejor legibilidad. La transcripción altera cifras de la tabla 7.1 y omite factores/unidades en fórmulas. Entre las diferencias verificadas:

- La tabla oficial da tasa cruda **55,5 por 100 000** y ASR **44,7 por 100 000**; la transcripción dice 4,47 y una diferencia de 55,5%, mientras la página del libro dice que el ASR es 19% menor que la tasa cruda.
- La tasa acumulada 0–74 del ejemplo oficial es **0,050 (5,0%)** y el riesgo acumulado es **4,9%**, aproximadamente 5,0%; la transcripción contiene 10,7 y 10,1%.
- Para los grupos de cinco años, la fórmula de tasa acumulada incluye el factor `5`; la fórmula de error estándar publicada para la tasa acumulada porcentual también incorpora `500`.
- El error estándar ajustado se deriva de la varianza de Poisson ponderada por `wᵢ/yᵢ`, como se muestra arriba; las expresiones de la transcripción no son fiables.
- La referencia de Bray tiene DOI `10.1023/A:1014344519276`; el DOI que aparece en la transcripción tiene dígitos incorrectos. La referencia de Esteve corresponde al registro IARC `/283`, y Jensen et al. al `/238` (no `/123` ni `/228`).

No copiar estas cifras del ejemplo de Bucaramanga como casos de prueba. Para validar el motor del RNC se necesita un ejemplo RNC aprobado; datos sintéticos para vistas/pruebas se crearán en otra etapa.

## Qué aportan las referencias de la fuente

Esta evaluación resume el enfoque del capítulo y la descripción bibliográfica de los editores/publicadores. Salvo el artículo de Bray y las páginas consultadas, no constituye una relectura íntegra de cada libro/capítulo citado.

| Referencia | Aporte al proyecto | Prioridad/uso |
|---|---|---|
| Armitage y Doll (1954), teoría multietapa y distribución por edad del cáncer | Fundamento histórico de que la incidencia varía con edad y tipo de cáncer; justifica examinar tasas específicas. No prescribe la visualización ni la fórmula del portal. | Contexto teórico; usar con literatura actual si se discuten mecanismos biológicos. |
| Bray et al. (2002), imposición de una nueva estándar mundial | Compara estándares Segi y OMS: concluye que los cocientes de tasas estandarizadas con Segi aproximan el riesgo relativo con precisión semejante y argumenta razones prácticas para conservarlo. Apoya comparabilidad relativa, pero los valores absolutos cambian con la estándar y solo se comparan usando la misma. CI5 XII confirma continuidad de Segi–Doll en 2024. | Alta: fundamentar por qué fijar/etiquetar la versión de la estándar. DOI corregido en la referencia. |
| Day (1992), tasa y riesgo acumulados | Explica el vínculo entre una suma de tasas por edad y una probabilidad aproximada; el rango de edad y la ausencia de riesgos competitivos son esenciales. | Secundaria: solo si se propone una futura estadística de riesgo de vida. |
| Doll, Payne y Waterhouse (1966); Segi (1960) | Antecedentes de la estándar mundial Segi modificada por Doll que CI5 sigue usando. | Histórico: documentar procedencia, mientras CI5 2024 sirve de referencia operativa actual. |
| dos Santos Silva (1999), *Cancer Epidemiology: Principles and Methods* | Manual general de epidemiología del cáncer: ocurrencia, tasas, diseños, azar, confusión, registros y análisis de datos rutinarios. | Complemento didáctico en español/inglés; es antiguo, no sustituye normas actuales. |
| Estève, Benhamou y Raymond (1994), *Statistical Methods in Cancer Research IV: Descriptive Epidemiology* | Desarrollo teórico de epidemiología descriptiva y variaciones espaciotemporales; recurso para comprender las decisiones estadísticas. | Consulta profunda; antecedente metodológico, no norma cubana vigente. |
| Jensen et al. (1991), *Cancer Registration: Principles and Methods* | Referencia amplia sobre colecta, almacenamiento, análisis e interpretación en registros poblacionales. | Complementaria para conceptos del negocio; el Manual RNC más reciente prevalece para el proceso cubano. |
| Kirkwood y Sterne (2003), *Essential Medical Statistics* | Estadística médica general, incluidos error estándar, Poisson, tasas, comparación y estandarización. | Apoyo pedagógico para cálculos/pruebas; validar procedimientos con fuentes especializadas y actuales. |
| Smith (1992), comparación entre registros por tasas estandarizadas | Discute interpretación/comparación entre registros y el papel del método de ajuste. | Alta para el marco comparativo; capítulo histórico de CI5 VI, complementar con CI5 XII y el ejemplo RNC. |

## Referencias bibliográficas cotejadas

Se conservan los metadatos de la bibliografía visible en `4.jpg`; los identificadores/enlaces corregidos se cotejaron con PubMed y el catálogo editorial de IARC cuando están disponibles.

1. Armitage P, Doll R (1954). The age distribution of cancer and a multi-stage theory of carcinogenesis. *British Journal of Cancer*. 8(1):1–12. https://doi.org/10.1038/bjc.1954.1
2. Bray F, Guilloux A, Sankila R, Parkin DM (2002). Practical implications of imposing a new world standard population. *Cancer Causes & Control*. 13(2):175–182. https://doi.org/10.1023/A:1014344519276
3. Day NE (1992). Cumulative rate and cumulative risk. In: Parkin DM, Muir CS, Whelan SL, Gao YT, Ferlay J, Powell J, editors. *Cancer Incidence in Five Continents*. Vol. VI. IARC Scientific Publication No. 120. Lyon: IARC. pp. 862–864.
4. Doll R, Payne P, Waterhouse J, editors (1966). *Cancer Incidence in Five Continents: A Technical Report*. Berlin: Springer-Verlag (for UICC).
5. dos Santos Silva I (1999). *Cancer Epidemiology: Principles and Methods*. IARC Non-Series Publication. Lyon: IARC. https://publications.iarc.who.int/421
6. Estève J, Benhamou E, Raymond L (1994). *Statistical Methods in Cancer Research. Vol. IV: Descriptive Epidemiology*. IARC Scientific Publication No. 128. Lyon: IARC. https://publications.iarc.who.int/283
7. Jensen OM, Parkin DM, MacLennan R, Muir CS, Skeet RG, editors (1991). *Cancer Registration: Principles and Methods*. IARC Scientific Publication No. 95. Lyon: IARC. https://publications.iarc.who.int/238
8. Kirkwood BR, Sterne JAC (2003). *Essential Medical Statistics*. 2nd ed. Oxford: Blackwell Science.
9. Segi M (1960). *Cancer Mortality for Selected Sites in 24 Countries (1950–57)*. Sendai, Japan: Department of Public Health, Tohoku University School of Medicine.
10. Smith PG (1992). Comparison between registries: age-standardized rates. In: Parkin DM, Muir CS, Whelan SL, Gao YT, Ferlay J, Powell J, editors. *Cancer Incidence in Five Continents*. Vol. VI. IARC Scientific Publication No. 120. Lyon: IARC. pp. 865–870.

## Estado para requisitos RNC

- `Q-004`: Segi–Doll queda respaldada como referencia de trabajo por CI5 XII 2024; aún se coteja la salida numérica con un ejemplo RNC.
- `Q-005`: CI5 XII aporta fórmulas reproducibles de tasa cruda, tasas específicas y ASR directo; siguen pendientes validación RNC de unidad/agrupaciones, edades desconocidas y redondeo.
- `Q-009`: CI5 XII aporta un error estándar basado en Poisson, no un IC o una regla para publicar intervalos. Conservar la decisión pendiente.
- `Q-021`: confirmar si el RNC corrige tasas resumen por edad desconocida y si acepta el supuesto CI5.
- `Q-003`/`Q-016`: los 18 grupos estándar implican comprobar los grupos y población de edades altas, además de las correspondencias de edades personalizadas.
- Métricas de tasa/riesgo acumulados: documentadas para aprendizaje, fuera del alcance aprobado por ahora.
