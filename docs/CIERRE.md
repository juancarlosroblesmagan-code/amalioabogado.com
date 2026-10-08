# Cierre técnico de la HOME

Fecha: 8 de octubre de 2026. Alcance entregado: HOME de https://amalioabogado.com, sin páginas interiores independientes. El cierre técnico no equivale a certificación legal ni a garantía de posicionamiento o seguridad absoluta.

## Entregado y publicado

- Diseño editorial aprobado, logotipo, navegación, responsive, accesibilidad y textos profesionales con datos confirmados.
- Enlaces limpios a secciones, incluidos `/areas-juridicas`, `/reclamaciones-bancarias`, `/preguntas-frecuentes` y `/contacto`; carga directa, recarga y navegación de historial comprobadas. `/areas`, `/bancario` y `/preguntas` devuelven 301 hacia los nombres nuevos; navegación y llms usan los nuevos.
- Formulario PHP con envío SMTP real y configuración privada en Plesk. Un envío autorizado de prueba fue aceptado por SMTP; recepción en el buzón pendiente de confirmación del titular.
- Seguridad reforzada: cabeceras públicas, HTTPS/HSTS, ModSecurity, antispam y límites por IP/globales, acceso restringido a librerías y archivos sensibles. Pruebas locales y públicas documentadas.
- SEO local: indexación habilitada, canonical, sitemap, robots y entidades Schema consistentes.
- Descubrimiento con IA: contenido HTML legible sin JS, guía pública `/llms.txt` y acceso permitido a contenido público. Pruebas con nombres de Googlebot, bingbot, OAI-SearchBot, PerplexityBot y Claude-SearchBot: HTTP 200. No acredita rastreo real ni citación.
- HTTP y www redirigen al dominio HTTPS sin www.
- Documentación publicada en https://github.com/juancarlosroblesmagan-code/amalioabogado.com. Ese repositorio contiene documentación, no el código fuente ni credenciales.

## Entrega y mantenimiento

- Fuente del proyecto conservada en el entorno local de trabajo.
- `dist/` contiene la compilación pública actual; subir su contenido, nunca archivos privados, `.env`, `reports` o `node_modules`.
- Configuración SMTP y clave antispam residen fuera de `httpdocs`. No se incluyen en GitHub ni en la compilación.
- Copias manuales previas a despliegue/refuerzo fuera de la raíz pública; acordar backups automáticos, separados y probados con el proveedor.
- Guías: `FORMULARIO.md`, `RUTAS.md`, `SEGURIDAD.md`, `SEO-IA.md`, `DOMINIO.md` y `LEGAL.md`.

## Pendientes del titular/proveedor, fuera del cierre técnico

1. Reforzar contraseña del buzón SMTP coordinadamente con el archivo privado; activar doble factor donde esté disponible. No se han rotado credenciales ni configurado MFA automáticamente.
2. Confirmar recepción real del correo de prueba y verificar firma DKIM/alineación SPF-DMARC en sus cabeceras.
3. Verificar cuentas de Search Console y Bing Webmaster Tools, enviar el sitemap y revisar la ficha real de Google Business Profile. No se han creado cuentas ni enviado solicitudes de indexación desde aquí.
4. Completar comprobaciones legales de proveedores, contratos, transferencias, logs y conservación; aprobación final de textos/procedimientos por Amalio. Mantener la advertencia de privacidad mientras corresponda.
5. Confirmar con el proveedor renovación HTTPS, parches, protección DDoS, monitorización y retención/limpieza programada de contadores.

No se promete aparición en Google o asistentes de IA. El mantenimiento posterior y la revisión de estos pendientes son necesarios aunque la HOME esté operativa.
