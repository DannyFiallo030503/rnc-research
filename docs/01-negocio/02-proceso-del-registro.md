# Proceso del registro y calidad de datos

Estado: CONFIRMADO POR MANUAL RNC 2024 + EVIDENCIA HISTÓRICA

## Evidencia disponible

El Manual de Procedimientos del RNC, versión VII (2024), define el proceso vigente documentado: captación pasiva y activa desde hospitales, anatomía patológica, laboratorios, egresos e información de mortalidad; llenado/codificación de reportes; revisión provincial; cierres periódicos; validación central; detección de duplicados y múltiples primarios; pareamiento con mortalidad; incorporación de casos validados y emisión anual de cifras. Ver desglose y páginas en [`06-manual-procedimientos-2024.md`](06-manual-procedimientos-2024.md).

La documentación histórica de IARC describe prácticas anteriores y queda como corroboración histórica, no como fuente principal frente al manual de 2024.

## Flujo documentado en la versión VII

La secuencia siguiente resume las responsabilidades del proceso existente; no es el flujo de la plataforma pública propuesta (Manual, pp. 8–9, 15–25):

1. **Captación en unidad informante.** Los médicos llenan un Reporte de Cáncer por tumor elegible. El registrador combina la notificación pasiva con búsqueda activa en anatomía patológica, hematología/laboratorio, egresos, defunciones e historias clínicas.
2. **Control y entrada local.** La unidad crea/actualiza su tarjetero de control, codifica topografía y morfología según el catálogo aplicable e introduce reportes completos en el sistema automatizado nacional. Contrasta listas de fuentes para detectar casos faltantes y nuevos primarios.
3. **Revisión territorial.** La provincia concilia formularios físicos con la base, comprueba variables/códigos, reclama reparos y recibe informes mensuales de cada unidad (con notificación de cero casos si corresponde).
4. **Cierre y remisión al RNC.** Según el Anexo 3.1, el envío territorial a la oficina central se realiza el último viernes cada dos meses conforme al calendario anual. Se exportan casos nuevos validados, por año de diagnóstico, acompañados por el informe de cierre y formularios correspondientes; el paquete se compacta y no se manipula externamente.
5. **Validación central y consolidación.** El RNC verifica consistencia entre archivos, reportes, completitud/codificación y cierres; ejecuta pareamiento probabilístico para diferenciar duplicados reales de tumores múltiples; compara con mortalidad y solicita aclaraciones. Solo incorpora al acumulado los casos validados.
6. **CDI/SCD y emisión estadística.** El RNC busca casos detectados inicialmente por certificado de defunción; si recupera información clínica los asigna al año de diagnóstico, y si no la recupera los clasifica SCD con incidencia en el año de fallecimiento. Conserva cierres/bases y emite los resultados del último año procesado; distribuye bases definitivas a provincias en marzo y remite los resultados anuales para el Anuario antes del 1 de marzo.

La periodicidad no es uniforme: algunas revisiones locales son diarias, semanales, mensuales o trimestrales, mientras el envío territorial al RNC es bimestral y la distribución anual de cifras ocurre en marzo. Confirmar el calendario actualmente vigente con el RNC.

El formulario del Manual distingue territorio de residencia (dirección, localidad, municipio y provincia) de unidad/provincia informante; para el tumor separa topografía y morfología. El CSV de prácticas no está mapeado a esos conceptos y no debe suponerse que `LOC`/`LUGAR` coinciden con municipio/localidad. En el formulario se registra además Ann Arbor para linfomas; es estadio, no morfología histológica. Véase [el cotejo íntegro del Manual](06-manual-procedimientos-2024.md) y Q-002/Q-017.

Fuentes: `SRC-RNC-003` (principal), `SRC-IARC-CUBA-001` (histórica).

## Implicación para el sistema

La plataforma de Prácticas II debe tratarse como capa de consulta/difusión de datos validados. El manual describe procesamiento en el sistema nacional vigente, pero no identifica su nombre o versión ni define una interfaz de integración. No modelar el portal público como sistema de captura nominal sin nueva autorización y requisitos explícitos.

## Preguntas a resolver

Preguntas parcialmente abiertas: identificar software y formatos de intercambio; obtener calendario estadístico anual; confirmar que la versión VII sigue vigente; distinguir el cierre interno validado de la publicación y sus estados. Ver Q-008, Q-010 y Q-013.
