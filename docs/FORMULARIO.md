# Activar el envío directo en Plesk

## Entrega pública

Subir **el contenido de `dist/`** a `httpdocs` o `public_html`, incluidos `.htaccess`, `api/` y `api/lib/`. No subir el proyecto entero. Usar PHP 8.2 o posterior con OpenSSL habilitado. No servir PHP como texto ni mediante un hosting exclusivamente estático.

PHPMailer queda incluido al compilar; para una instalación nueva del proyecto ejecutar `composer install --no-dev --working-dir=backend` antes de `npm run build`. Las credenciales no se incluyen en `dist`.

## Configuración privada

### Datos SMTP facilitados por el usuario

| Parámetro | Valor |
| --- | --- |
| Servidor saliente | `amalioabogado.com` |
| Puerto SMTP | `465` |
| Seguridad | TLS implícito (`smtp_security => 'ssl'` en PHPMailer) |
| Autenticación | Obligatoria |
| Usuario previsto | `amalioabogado@amalioabogado.com` (confirmar que el proveedor usa la dirección completa) |
| Remitente | `amalioabogado@amalioabogado.com` |
| Destinatario actual | `amalioabogado@icalba.com` |

La contraseña no se ha recibido ni se debe versionar. La configuración de ejemplo ya incluye estos datos sin secretos y mantiene `enabled => false`. Falta configurar la contraseña y la clave antispam en el archivo privado, confirmar PHP/OpenSSL, conectividad saliente y certificado TLS válido para `amalioabogado.com`, y probar recepción real. No deshabilitar la validación TLS si aparece un error: pedir al proveedor el hostname correcto del certificado.

Los puertos entrantes POP3 995 e IMAP 993 no intervienen en el envío del formulario. El nuevo buzón se utiliza como remitente técnico; no se ha cambiado el email profesional visible ni el destinatario sin una petición expresa.

### Datos que debe facilitar el proveedor

- Confirmación de PHP 8.2+ y OpenSSL en Plesk.
- Host SMTP, puerto 587 con STARTTLS o 465 con TLS implícito, usuario y contraseña.
- Dirección remitente autorizada (puede ser un buzón del dominio nuevo; el destinatario seguirá siendo `amalioabogado@icalba.com`). No es necesario conocer la contraseña del buzón destinatario si se utiliza otro SMTP autorizado.
- Permiso de conexión saliente al SMTP, SPF/DKIM/DMARC y ruta privada accesible por PHP.

No enviar credenciales por chat ni subirlas a GitHub. Configurarlas directamente en el archivo privado del servidor. No basta con subir el HTML: también se necesitan `api/`, PHPMailer y configuración privada. Las capturas con «Preparar consulta por email» muestran la versión anterior, no el envío directo nuevo.

1. Fuera de la raíz pública, crear `private/` como directorio hermano de `httpdocs`.
2. Copiar `backend/contact-config.example.php` como `private/amalio-contact.php`.
3. Utilizar los datos SMTP facilitados arriba y configurar la contraseña del buzón directamente en el servidor. Confirmar con el proveedor cualquier discrepancia de usuario o certificado. No compartir contraseñas en el chat. Mantener destinatario `amalioabogado@icalba.com`.
4. Rellenar la configuración y generar una clave con `php -r "echo bin2hex(random_bytes(32));"`. Restringir los permisos a la cuenta PHP; el directorio de contadores debe ser escribible por PHP y no accesible desde la web.
5. Comprobar SPF, DKIM y DMARC del remitente. El visitante se usa como Reply-To, nunca como From.
6. Cambiar `enabled` a `true` solo después de configurar todo. Si la estructura de carpetas es distinta, configurar la variable privada `AMALIO_CONTACT_CONFIG` con la ruta absoluta del archivo. Revisar restricciones `open_basedir` de Plesk.

La ruta automática es `../private/amalio-contact.php` respecto de la raíz pública. Los contadores contienen cantidades y caducidad, no mensajes ni IP en claro. Sus identificadores derivados siguen siendo datos seudonimizados, no datos anónimos. Los archivos caducados se recogen probabilísticamente con tráfico; acordar con el hosting una limpieza periódica si se necesita un plazo máximo estricto de eliminación.

## Verificación de producción

### Instalación realizada en Plesk (8 de octubre de 2026)

- Creada copia de seguridad de la HOME anterior fuera de la raíz pública.
- Subida la compilación actual con `api/`, PHPMailer, rutas de secciones e indexación habilitada. Verificados 34 archivos estáticos remotos contra la entrega local, sin diferencias.
- Creado `private/amalio-contact.php` fuera de `httpdocs`, con configuración SMTP y clave antispam generada. Permisos del directorio 700 y del archivo 600.
- Confirmado PHP 8.3.35 (FPM servido por Apache), OpenSSL habilitado y `open_basedir` compatible con el directorio privado.
- La ruta privada consultada desde la web devuelve 404. El titular introdujo la contraseña directamente en Plesk, sin compartirla en chat o GitHub. Después se activó `enabled => true`, conservando la contraseña del buzón y el destinatario.
- Prueba real autorizada: token HTTP 200 y un único envío de prueba aceptado por SMTP, con respuesta HTTP 200 y `ok: true`. Destinatario: `amalioabogado@icalba.com`; asunto: «Consulta jurídica · Otra consulta». El mensaje está identificado como prueba técnica, no consulta jurídica. Pendiente de que el titular confirme recepción en bandeja de entrada o spam; no se ha accedido al buzón destinatario.
- Nginx todavía añade barra en la carga directa de `/contacto`; JavaScript normaliza la URL. Algunas respuestas estáticas de Nginx no incorporan las cabeceras de `.htaccess`; queda revisar su equivalente en Plesk.

La extracción mostró un aviso por separadores de Windows en el ZIP; los archivos estáticos se comprobaron después byte a byte. La prueba SMTP posterior pasó y cargó las dependencias PHP necesarias. No se han incluido contraseñas ni claves privadas en esta documentación.

- Confirmar que `/api/contact.php?action=token` responde JSON, nunca código PHP, y sin caché. Sin configuración debe responder 503.
- Probar un envío autorizado y verificar la recepción real en el buzón y la respuesta al visitante. Una aceptación SMTP no garantiza la llegada a bandeja de entrada.
- Verificar errores sin perder datos, validación, ausencia de cookies inesperadas y protección de la carpeta privada.
- Revisar `.htaccess`, redirección de www y cabeceras en el hosting real. Nginx puede requerir configuración equivalente en Plesk; `_headers` no configura Plesk.
- Mantener las verificaciones legales de `docs/LEGAL.md`, incluidos alojamiento y proveedor SMTP.

## Pruebas locales

`npm run check:backend` requiere PHP y OpenSSL en PATH (o variables `PHP_BIN`, `PHP_EXTENSION_DIR` y `OPENSSL_BIN`). Usa un SMTP TLS local y **no envía correos externos**. Genera fixtures privados en `reports/`, que no deben publicarse.

`scripts/check.mjs` prueba el frontend con respuestas simuladas, no la recepción de correo en producción. En desarrollo Vite reenvía `/api` al servidor PHP local en `127.0.0.1:8080`; la vista previa estática no ejecuta PHP.
