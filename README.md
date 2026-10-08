# Amalio Sánchez Martínez · Documentación web

Documentación técnica de la HOME de [amalioabogado.com](https://amalioabogado.com), actualizada el 8 de octubre de 2026.

Este repositorio recoge la documentación solicitada. No incluye el código fuente, la entrega compilada, datos de consultas ni credenciales del hosting o SMTP.

## Guías

- [Envío directo del formulario](docs/FORMULARIO.md): requisitos PHP/SMTP, instalación privada y verificación real de recepción.
- [Enlaces sin #](docs/RUTAS.md): rutas como `/contacto`, navegación de secciones, historial y configuración del servidor.
- [Dominio y publicación](docs/DOMINIO.md): canonical, robots, sitemap y comprobaciones pendientes.
- [Textos legales y verificaciones pendientes](docs/LEGAL.md): alcance y proveedores que deben confirmarse; no certifica cumplimiento legal.

## Estado

La entrega local `dist/` está preparada con indexación habilitada, enlaces limpios y formulario PHP con SMTP autenticado, validación y antispam. Debe subirse **su contenido** a la raíz pública de Plesk y configurar el SMTP **fuera de ella**.

El frontend pasó las pruebas locales de responsive (320–2560 px), accesibilidad automática e interacciones, incluidas carga directa, recarga e historial de `/contacto`. El backend pasó pruebas con un SMTP TLS local. Posteriormente se instaló la entrega en Plesk y se activó el SMTP privado: un único envío de prueba real obtuvo aceptación SMTP y HTTP 200. Falta confirmar recepción en el buzón destinatario; aceptación SMTP no equivale a llegada a bandeja de entrada.

No compartir contraseñas aquí, en issues ni en archivos versionados. La aceptación SMTP no garantiza llegada a bandeja de entrada. Las comprobaciones legales y del alojamiento real siguen pendientes.
