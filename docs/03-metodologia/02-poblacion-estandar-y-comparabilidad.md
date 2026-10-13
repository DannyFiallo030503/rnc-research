# Población estándar y comparabilidad de tasas

Estado: REFERENCIA INTERNACIONAL DE TRABAJO + DENOMINADORES CUBANOS PENDIENTES DE ARCHIVO
Corte: 2026-10-12

## Por qué importa

Una tasa ajustada por edad depende de una población estándar. Dos tasas calculadas con poblaciones estándar diferentes no son directamente comparables como si fueran el mismo indicador.

CDC advierte explícitamente que tasas ajustadas usando diferentes poblaciones estándar no deben compararse sin considerar esa diferencia.

Fuente: `SRC-CDC-INTERP-2026`.

## Evidencia cubana disponible

El Anuario Estadístico de Salud 2024 publica tasas ajustadas por edad a la **población estándar mundial** por 100 000 habitantes. El Manual de Procedimientos RNC VII (2024) también menciona la estándar mundial. El estudiante aclaró después que la expresión «población estándar de Cuba» se refería al uso de **datos poblacionales cubanos** y que para cáncer se seguirá la metodología internacional (`SRC-RNC-007`). La hipótesis de una tabla cubana alternativa de pesos queda retirada del diseño base.

Fuente: `SRC-CUBA-AES-2024`.

Yinet confirmó que los denominadores de población del proyecto provienen de ONEI por edades simples, sexo y territorio (`SRC-RNC-005`). Esta serie denominadora no es la población estándar usada para ajustar tasas; su edición y regla temporal siguen pendientes (`Q-016`). El Anuario Demográfico ONEI 2024 distingue población media y efectiva: para calcular tasas hay que identificar la serie exacta que corresponda al numerador y al período. Las tablas públicas verificadas no aportan por sí solas una matriz completa municipio × edad simple × sexo × año; el RNC ofreció entregar los datos detallados.

## Estándar mundial de referencia

[IARC/CI5](https://ci5.iarc.who.int/ci5-xii/about/) documenta la población estándar mundial de **Segi modificada por Doll** que utiliza en su aplicación. Suma 100 000 unidades y coincide en forma con los 18 quinquenios clásicos de 0–4 a 85+ indicados por Yinet. Esta es la tabla de referencia de trabajo para ASR(W), sujeta a comprobar que reproduce las salidas cubanas con un ejemplo real del RNC.

| Edad | Peso | Edad | Peso | Edad | Peso |
|---|---:|---|---:|---|---:|
| 0–4 | 12 000 | 5–9 | 10 000 | 10–14 | 9 000 |
| 15–19 | 9 000 | 20–24 | 8 000 | 25–29 | 8 000 |
| 30–34 | 6 000 | 35–39 | 6 000 | 40–44 | 6 000 |
| 45–49 | 6 000 | 50–54 | 5 000 | 55–59 | 4 000 |
| 60–64 | 4 000 | 65–69 | 3 000 | 70–74 | 2 000 |
| 75–79 | 1 000 | 80–84 | 500 | 85+ | 500 |

Para aplicar ajuste directo, calcular tasas específicas cubanas con casos RNC y población ONEI compatible, multiplicar cada tasa por el peso mundial del mismo grupo y dividir la suma de productos entre la suma de pesos. El resultado se expresa por 100 000 si las tasas específicas están en esa unidad. Para una agrupación nueva, solo se pueden sumar pesos de quinquenios completos compatibles; una división de un quinquenio requiere una regla de ponderación adicional y no se inventará a partir de edades simples cubanas. Mantener la estándar mundial y la población ONEI como entidades distintas.

El capítulo 7 de CI5 XII (2024), revisado en octubre de 2026, concreta el cálculo y sus límites: con pesos `wᵢ` de suma 100 000 y `dᵢ/yᵢ` casos por persona-año, `ASR = Σ(wᵢ dᵢ/yᵢ)`; equivalentemente, ponderar las tasas por 100 000 por `wᵢ/100 000`. Bajo Poisson, `Var(ASR) = Σ[dᵢ(wᵢ/yᵢ)²]` y `SE = √Var`. El error estándar no determina por sí solo el intervalo de confianza. Ver síntesis, corrección de la transcripción y discusión de edades desconocidas/altas en [`04-ci5-xii-estandarizacion-edad.md`](04-ci5-xii-estandarizacion-edad.md).

CI5 recomienda inspeccionar primero la tasa específica por edad. También señala que los casos de edad desconocida requieren un supuesto explícito si se corrigen las medidas resumen: CI5 multiplica por `T/K` (casos totales/casos con edad conocida del mismo sexo y cáncer), suponiendo que la ausencia de edad no depende de la edad real. El texto reconoce que este supuesto puede fallar. La disponibilidad de población para 75+, 80+ o 85+ puede modificar el ASR. Estas son advertencias metodológicas internacionales, no decisiones ya aprobadas para el RNC.

## Evidencia SEER

SEER documenta el uso habitual de la población estándar estadounidense de 2000 y también distribuye varias tablas internacionales, incluidas «World (Segi 1960)» y «World (WHO 2000–2025)». Por eso «norma internacional» no significa que todos los portales usen **los mismos pesos**; aquí se escoge la tabla concreta de IARC/CI5 coherente con el Manual y Anuario cubanos. SEER mantiene además una definición explícita de grupos de edad.

Fuente: `SRC-SEER-STDPOP-2026`, `SRC-SEER-MANUAL-2026`.

La lección no es elegir la población de SEER, sino documentar siempre cuál población estándar y qué agrupación etaria se utilizaron.

## Regla propuesta para el futuro sistema

Toda tasa ajustada debería poder asociarse de manera trazable con:

- población estándar;
- versión o referencia de esa población;
- grupos de edad;
- pesos utilizados;
- método de ajuste;
- unidad de la tasa.

Estado: `PROPUESTA`.

## Preguntas que el RNC debe cerrar

`Q-004`: referencia mundial identificada; verificar con el RNC que su ejemplo reproduce la tabla de IARC/CI5 y registrar la versión empleada.

`Q-003`: grupos clásicos quinquenales 0–4 a 85+ ya confirmados; faltan reglas para crear y calcular con agrupaciones nuevas.

`Q-005`: definición operativa y fórmula exacta del ajuste directo.

`Q-006`: definición y fórmula exacta del ajuste indirecto.

La posible publicación de tasa/riesgo acumulados es una métrica adicional explicada en CI5 XII, fuera del alcance confirmado actualmente. No incorporarla sin validación de tutoría/RNC.

## Riesgo

El riesgo restante es usar una edición de población ONEI que no corresponda al año o estrato de los casos, o combinar la estándar mundial con grupos de edad incompatibles. La tabla internacional permite adelantar la lógica y sus pruebas; los resultados cubanos finales requieren archivo ONEI y ejemplo RNC.
