# DEC-013 — PWA exclusivamente pública y consulta offline

Fecha: 2026-10-19. Estado: dirección de producto acordada para documentar; propuesta de implementación pendiente de diseño y validación técnica/institucional.

Trazabilidad: `SRC-RNC-012` → `EVD-116..117`; `SRC-TECH-026`; `Q-025`; relacionada con `DEC-011`.

## Decisión de diseño

Preparar una PWA instalable para el portal público, sin funciones administrativas. La experiencia offline podrá generar gráficos únicamente con un paquete local de agregados ya aprobados para publicación. El paquete debe identificar el corte, versión y fecha de descarga. No incluirá microdatos, sesiones/tokens administrativos, pantallas autenticadas ni respuestas restringidas. El panel administrativo continuará en la aplicación web online con autorización en el servidor.

## Seguridad y conectividad

No usar la detección de conectividad del navegador ni una hora de desconexión para autorizar o proteger acciones. La aplicación puede mostrar conexión intermitente mediante fallos/timeouts de solicitudes reales y reintentos prudentes. La hora podría evaluarse solo como señal de conexión reciente, separada de la fecha/version del paquete. En offline, las acciones administrativas fallan al no llegar al servidor; la PWA sirve exclusivamente el paquete público.

El service worker tendrá scope mínimo, precacheará recursos públicos y excluirá explícitamente rutas y respuestas autenticadas/sensibles de Cache API. Si PWA y panel comparten origen, se verificará que el worker no intercepte rutas administrativas; se prefiere aislar el origen. Se usarán directivas HTTP `no-store` donde correspondan, además de la exclusión del service worker. Un paquete previamente descargado no puede actualizarse ni revocarse mientras el dispositivo no reconecte.

## Pendientes

Definir si el paquete abarca un corte nacional o selecciones, granularidad y volumen; cálculo local reproducible; política de divulgación y compatibilidad de versiones; aviso de antigüedad y actualización; comportamiento tras revocación; soporte por navegador/dispositivo; HTTPS y despliegue; alcance de evaluación de privacidad/seguridad. Ningún archivo público actual del prototipo se convierte automáticamente en contenido apto para offline.

La decisión no declara la PWA implementada ni validada por RNC/CUJAE. Ver también la [arquitectura evolutiva](../06-arquitectura/arquitectura-evolutiva-rnc.md) y la [arquitectura objetivo/operación](../../../rnc-web/docs/ARQUITECTURA-OBJETIVO-OPERACION.md).
