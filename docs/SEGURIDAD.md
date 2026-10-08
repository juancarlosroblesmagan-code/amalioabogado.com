# Seguridad: medidas verificadas y pendientes

Revisión del 8 de octubre de 2026. No es una auditoría de penetración independiente ni una garantía de seguridad absoluta.

## Activo y comprobado

- HOME estática sin WordPress, plugins de CMS, base de datos, uploads de visitantes, analítica o scripts externos.
- HTTPS operativo. HSTS inicial de 86400 segundos, sin `includeSubDomains` ni preload, para no afectar correo u otros servicios no auditados. Ampliar progresivamente tras verificar estabilidad y renovación del certificado.
- CSP sin `unsafe-inline` ni `unsafe-eval`: recursos propios, JSON-LD autorizado por hash, objetos y marcos externos bloqueados. `X-Frame-Options: DENY`, `nosniff`, política de referencia y permisos restringidos, COOP/CORP `same-origin`.
- Corregido en Plesk el procesamiento estático inteligente de Nginx que omitía las cabeceras de Apache en la HOME. El proxy Nginx permanece; Apache aplica ahora las reglas de la web a los recursos estáticos. No se han modificado otras suscripciones.
- Cuerpo máximo de petición del dominio: 64 KiB en Nginx y Apache; formulario: 16 KiB adicionales en PHP. No afecta a cargas del administrador en el panel separado de Plesk.
- ModSecurity **On**, reglas Atomic Standard en Apache. Ya estaba activo; no se han deshabilitado reglas.
- PHP 8.3.35, OpenSSL habilitado, errores no mostrados al visitante.
- SMTP autenticado con certificado validado; remitente fijo y usuario visitante exclusivamente en Reply-To. Mensajes de texto plano, sin adjuntos ni destinatarios arbitrarios.
- Validación servidor de UTF-8, longitud, controles, email y área; formato JSON estricto. Origen y Fetch Metadata restringidos. Esto limita ataques desde navegadores ajenos, no sustituye el antispam: un bot puede falsificar cabeceras.
- Tokens HMAC de un solo uso, ligados a IP, caducidad de 15 minutos y espera mínima; honeypot. Sin cookies de sesión.
- Límites por IP: 30 tokens/5 minutos y 8 intentos de envío/15 minutos. Techos globales: 300 tokens/5 minutos, 60 intentos/15 minutos y 200 solicitudes de envío validadas/24 horas; una conexión SMTP simultánea. Pueden requerir ajuste si crece el tráfico legítimo. No constituyen protección DDoS completa.
- Credenciales fuera de `httpdocs`, configuración con permisos 600 y carpeta privada 700. Contadores privados sin contenido de consultas ni IP en claro; identificadores seudonimizados, no anónimos.
- Acceso HTTP a `.env`, `.git/config` y archivos de librería PHP devuelve 403; ruta pública al archivo privado devuelve 404. Directorios sin listado y archivos de respaldo bloqueados por Apache.
- Registros DNS publicados: SPF con `-all`, clave DKIM en selector `default` y DMARC `p=quarantine` con alineación estricta. Publicación de registros no demuestra por sí sola la firma y alineación de cada mensaje: comprobar cabeceras del correo recibido.
- `npm audit` y Composer audit: sin avisos conocidos en la fecha de revisión. Esto no descarta vulnerabilidades desconocidas.
- Pruebas del backend reforzado con SMTP TLS local, sin correos externos. Frontend probado en producción: responsive 320–2560 px, axe e interacciones, sin errores en la ejecución final; el SMTP del frontend se simula en esas pruebas. Un intento inicial tuvo un error transitorio de decodificación de imagen; la verificación posterior de las imágenes y la repetición completa pasaron.

## Prioridad: cuenta y buzón

Los hallazgos específicos sobre credenciales se comunican al titular por separado, no se publican. Utilizar una contraseña aleatoria exclusiva de al menos 20 caracteres mediante un gestor, actualizar el buzón y la configuración privada coordinadamente, y verificar SMTP después. Cambiar solo el archivo de la web no cambia la contraseña del servidor de correo. No se han rotado credenciales automáticamente.

Activar doble factor en Plesk/GitHub y, si el proveedor lo permite, en el correo. Guardar códigos de recuperación fuera del servidor. Estas medidas requieren intervención del titular; no se han activado ni probado. Preferir SFTP/FTPS a FTP sin cifrar y cerrar sesiones del panel cuando termine el trabajo.

## Dependencias del proveedor y mantenimiento

1. Parches periódicos de sistema, Plesk, PHP/OpenSSL y reglas WAF; confirmar renovación automática del certificado y alertas.
2. Protección DDoS/rate limiting en red y proxy, IP real correctamente configurada y monitorización de errores y abuso. Los límites PHP no detienen inundaciones que saturan el servidor antes de ejecutar PHP.
3. Copias automáticas cifradas, separadas del hosting y pruebas de restauración. Hay copias manuales de `httpdocs` previas a despliegue/refuerzo, fuera de raíz pública; no se ha probado su restauración ni configurado una política automática.
4. Limpieza programada de contadores caducados y retención acordada de logs/backups/correo. La recolección actual es probabilística con tráfico y no garantiza un plazo máximo estricto sin cron.
5. Revisión periódica de dependencias (`npm audit`, `composer audit`) y mínimo privilegio para usuarios del panel y repositorio.
6. Confirmar SPF/DKIM/DMARC en mensajes reales antes de endurecer DMARC a reject; no se han cambiado DNS.
7. Nginx aún identifica Plesk en algunas cabeceras y sus respuestas de error propias no incorporan todas las cabeceras de Apache. Pedir al proveedor configuración equivalente si se necesita uniformidad también en errores. Ocultar la firma no sustituye mantener el servidor actualizado.
8. El correo no es cifrado de extremo a extremo. No enviar documentación jurídica sensible mediante el formulario; usar un canal seguro acordado con el despacho. Mantener revisión de privacidad y contratos de proveedores.

## Comprobación reproducible

`npm run check:security` comprueba cabeceras públicas, denegación de rutas sensibles y rechazo de origen ajeno con peticiones acotadas. No envía correos ni prueba DDoS. Resultados privados en `reports/security-check.json`. `npm run check:backend` verifica las defensas de la aplicación con servidor local.
