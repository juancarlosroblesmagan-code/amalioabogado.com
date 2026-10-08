# Dominio confirmado

El usuario ha confirmado el 8 de octubre de 2026 la solicitud del dominio **amalioabogado.com**.

- Origen principal configurado: `https://amalioabogado.com`, sin `www`.
- `.env.production` establece `VITE_SITE_URL` para canonical, Open Graph y los identificadores y URLs del grafo Schema.
- Indexación autorizada expresamente por el usuario: `PUBLICATION_APPROVED=true`. La compilación incluye robots permisivo y sitemap de la HOME; las verificaciones legales siguen pendientes.
- El correo profesional sigue siendo `amalioabogado@icalba.com`; el dominio nuevo no implica un cambio de buzón.

## Estado verificado y seguimiento

1. Dominio operativo y HOME publicada. No se han modificado DNS desde este proyecto.
2. HTTPS verificado; confirmar con el proveedor renovación automática y alertas.
3. Comprobado el 8 de octubre de 2026: HTTP y `https://www.amalioabogado.com/` redirigen a `https://amalioabogado.com/`. Verificar periódicamente, especialmente tras cambios del proxy.
4. Publicado el contenido de `dist/` en `httpdocs`; configuración SMTP fuera de la raíz pública. Seguridad reforzada y pruebas documentadas en `SEGURIDAD.md`.
5. Completar las comprobaciones de privacidad recogidas en `docs/LEGAL.md`.
6. Robots permisivo, canonical, sitemap y Schema públicos comprobados. La configuración de indexación está habilitada; falta verificar cuentas y enviar el sitemap en Search Console/Bing. Esto no acredita indexación real ni presencia en respuestas de IA; ver `SEO-IA.md`.

Se ha accedido a Plesk con la sesión del titular para desplegar y reforzar la web; no se han cambiado DNS ni contraseñas del buzón. El proxy Nginx permanece y Apache aplica las cabeceras del proyecto a los recursos públicos. Los cambios futuros del servidor requieren volver a verificar esas cabeceras.
