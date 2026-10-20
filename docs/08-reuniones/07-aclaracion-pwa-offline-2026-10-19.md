# Aclaración sobre PWA, consulta offline y administración

**Fecha:** 2026-10-19
**Participantes:** Danny Fiallo Muñoz y asistente del proyecto
**Tipo:** dirección de producto comunicada por el estudiante y recomendación técnica; no es una validación institucional del RNC/CUJAE.

## Tema

Posibilidad de instalar el portal en celulares y computadoras y usarlo sin conexión, incluso con conectividad muy inestable. Se consideró inicialmente marcar la aplicación offline tras una hora sin recibir datos y ocultar o retirar información sensible.

## Dirección documentada

- La PWA será exclusivamente para consulta pública. No incluirá funciones/rutas administrativas, sesiones administrativas, microdatos ni respuestas restringidas.
- Offline podrá generar gráficos con datos previamente disponibles solo si corresponden a agregados aprobados para publicación. El paquete deberá mostrar corte, versión y fecha de descarga.
- La administración permanecerá en la web online y requerirá autenticación/autorización del servidor. No se apoyará la protección en detectar la conexión desde el navegador.
- El estado de red se podrá presentar como orientación mediante solicitudes reales con timeout/reintentos. `navigator.onLine` no confirma que el servidor del portal sea alcanzable.
- Una hora podría evaluarse como aviso de conexión reciente, no como control de seguridad, vigencia de estadísticas o eliminación automática. La antigüedad de los datos se muestra desde la versión/fecha de descarga.
- Una copia pública ya descargada no se puede actualizar o revocar mientras el dispositivo esté offline.

## Trazabilidad y límites

`SRC-RNC-012` → `EVD-116..117` → `DEC-013`; ver también `Q-025`. La instalación requiere HTTPS y soporte varía por navegador/plataforma. Las respuestas sensibles deben excluirse explícitamente del Cache API/service worker y administrarse con política HTTP apropiada; el scope del worker debe ser mínimo. Estos puntos siguen requiriendo diseño y validación. La PWA no está implementada.

Fuentes técnicas primarias consultadas: [MDN sobre instalación PWA](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Guides/Making_PWAs_installable), [caché PWA](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Guides/Caching), [`navigator.onLine`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/onLine), [caché HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Caching) y [OWASP HTML5 Security](https://cheatsheetseries.owasp.org/cheatsheets/HTML5_Security_Cheat_Sheet.html).
