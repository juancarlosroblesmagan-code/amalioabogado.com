# Dominio confirmado

El usuario ha confirmado el 8 de octubre de 2026 la solicitud del dominio **amalioabogado.com**.

- Origen principal configurado: `https://amalioabogado.com`, sin `www`.
- `.env.production` establece `VITE_SITE_URL` para canonical, Open Graph y los identificadores y URLs del grafo Schema.
- Indexación autorizada expresamente por el usuario: `PUBLICATION_APPROVED=true`. La compilación incluye robots permisivo y sitemap de la HOME; las verificaciones legales siguen pendientes.
- El correo profesional sigue siendo `amalioabogado@icalba.com`; el dominio nuevo no implica un cambio de buzón.

## Pendiente en Zafiro Telcom

1. Confirmar que el registro del dominio está completado y configurar los registros DNS indicados por el hosting.
2. Instalar y verificar el certificado HTTPS.
3. Redirigir HTTP a HTTPS y, si se configura `www`, redirigirlo al dominio principal sin `www`.
4. Publicar únicamente `dist/` y verificar cabeceras, cookies, caché y contacto en el servidor real.
5. Completar las comprobaciones de privacidad recogidas en `docs/LEGAL.md`.
6. Subir la compilación actual y comprobar robots, canonical, sitemap y Schema públicos; entonces solicitar indexación en Search Console. La versión remota revisada todavía tenía noindex y robots bloqueado.

El dominio ya responde por HTTPS con la HOME. HTTP redirige a HTTPS; www todavía no redirige al dominio principal. No se ha accedido al panel ni se han cambiado DNS. Se entrega `.htaccess` para Apache; si Nginx sirve directamente los archivos, configurar sus equivalentes en Plesk y comprobar las cabeceras reales.
