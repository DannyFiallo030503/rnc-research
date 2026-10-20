# DEC-016 — Descargas públicas, auditoría y logs

**Estado:** recomendación de diseño para validar; no política institucional aprobada.
**Fecha:** 2026-10-20
**Trazabilidad:** `SRC-PRJ-006` → `EVD-129..131` → `Q-028`; relacionada con `DEC-007`, `DEC-011`, `DEC-015`, `Q-007` y `Q-027`.

## Recomendación

No exigir registro para consultar o descargar estadísticas públicas aprobadas. Una cuenta permitiría asociar una descarga a una identidad, pero no impediría que el archivo se copie o circule después. Sí crearía credenciales que mantener y un historial capaz de revelar qué contenidos o filtros de cáncer interesaron a una persona. Que esa combinación constituya dato de salud personal en cada caso requiere análisis institucional; como riesgo de diseño debe tratarse con cuidado.

Mientras se determina la finalidad de los logs, no añadir historial individual ni analítica pública persistente. Se mantiene el acceso público sin cuenta y se conserva únicamente la auditoría administrativa que ya existe para parte de las operaciones. Es una salvaguarda provisional de diseño, no una política legal aprobada.

Si el objetivo es conocer qué partes del portal se usan, registrar métricas agregadas sin identidad: por ejemplo, recuento de apertura de gráficos por tipo y descargas por formato/corte en periodos amplios. No guardar por defecto nombre, email, IP, cookie/identificador persistente, sesión, consultas exactas ni combinaciones detalladas de filtros. No convertir los contadores públicos en un historial por usuario. Los límites temporales contra abuso son un control operativo separado y no una razón para conservar el historial de navegación.

Una cuenta pública podría evaluarse más adelante para una función que requiera personalización elegida por el propio usuario (p. ej., guardar favoritos), o para una descarga no pública/autorizada que realmente necesite atribución. En ambos casos se necesitarían finalidad concreta, campos mínimos, aviso claro, consentimiento/base aplicable, acceso y retención aprobados; validar especialmente si un usuario menor de edad podría acceder.

## Cuatro registros con finalidades distintas

1. **Auditoría administrativa atribuible:** actor, fecha/hora, acción, objeto/corte/cuenta, resultado y motivo cuando aplique. Incluir altas/bajas y cambios de roles, cargas, revisiones, publicación y revocación. No copiar filas, códigos clínicos de pacientes, secretos o contenido completo de archivos.
2. **Logs técnicos y de seguridad:** inicios de sesión exitosos/fallidos, rechazos de autorización, señales de abuso, errores operacionales y cambios de configuración. Minimizar IP/identificadores y contenido de solicitudes; definir acceso restringido y plazo corto/justificado para campos que identifiquen dispositivos.
3. **Métricas públicas de uso:** contadores anónimos/agregados de vistas y exportaciones por función y formato, sin usuario ni búsqueda detallada. Sirven para priorizar interfaz, no para vigilancia individual.
4. **Historial visible al usuario:** función distinta que solo tendría sentido si se habilita una cuenta pública y el usuario pide conservar sus propias acciones. No es necesario para publicar o usar estadísticas abiertas.

OWASP distingue los registros de auditoría/operación de los logs de seguridad y advierte que los logs pueden contener datos personales; define los campos según propósito, protege integridad/acceso y establece retención. La Ley cubana 149/2022 exige finalidad informada, recogida necesaria y conservación limitada; sus artículos 15–16 incluyen salud entre los datos sensibles. La aplicación concreta a eventos de navegación debe revisarla el RNC/asesoría institucional, no se presume aquí.

## Estado de `rnc-web`

Existe `AuditEvent` con `actor`, `action`, `target`, `reason` y `created_at`, y hay llamadas para algunas acciones de cuentas, cargas, publicación y revocación. Es un historial de aplicación parcial, guardado en la BD ordinaria; no es un registro resistente a manipulación ni cubre toda actividad administrativa o eventos de seguridad. La descarga pública de exportaciones no crea un evento duradero y no hay historial público por persona (`EVD-129`). El rate limit temporal de renderizado no equivale a auditoría de quién exportó.

La consulta y descarga pública no exigen cuenta. Las respuestas del explorador llevan `Cache-Control: no-store` y `Referrer-Policy: no-referrer`; esto reduce almacenamiento en cachés del navegador y filtración de filtros mediante `Referer`, pero no elimina URLs del historial local ni configura access logs de proxy/servidor/CDN. La configuración de esos componentes debe revisarse antes de desplegar. No se han añadido contadores agregados: primero hay que acordar su finalidad, granularidad y retención.

La mejora recomendada es cerrar primero el inventario de eventos administrativos, campos, cobertura y controles de integridad/retención; luego definir logs técnicos con la institución. Si se desea analítica pública, añadir contadores anónimos y agregados después de acordar finalidad, granularidad, aviso/política y retención. No crear una cuenta obligatoria de descarga como atajo de auditoría.

## Decisiones pendientes

Resolver `Q-028` con el RNC/CUJAE: finalidad y fundamento de cada registro, qué campos hacen falta, quién puede consultarlos, conservación/eliminación, integridad, respuesta a incidentes, aviso al usuario y si hay una necesidad concreta de cuentas públicas. Mantener descargas estadísticas públicas sin registro mientras esa necesidad no exista y no haya validación.
