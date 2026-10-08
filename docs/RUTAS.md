# Enlaces sin almohadilla

Los enlaces visibles usan rutas como `https://amalioabogado.com/contacto`, sin `#`. Siguen siendo secciones de la misma HOME, no nuevas páginas interiores.

## Alias disponibles

`/areas-juridicas`, `/sobre-mi`, `/segunda-oportunidad`, `/reclamaciones-bancarias`, `/preguntas-frecuentes`, `/contacto`, `/forma-de-trabajar`, `/penal`, `/faq-segunda` y `/contenido` (salto accesible al contenido). El logotipo y «Volver arriba» usan `/`.

Las rutas anteriores `/areas`, `/bancario` y `/preguntas` redirigen permanentemente con 301 a sus nombres nuevos en Apache. El navegador también normaliza las rutas antiguas si se utiliza un servidor estático sin esas reglas. Los enlaces de navegación y `/llms.txt` usan solo los nombres nuevos.

`src/routes.js` centraliza el mapa y el comportamiento. El plugin de Vite transforma las anclas semánticas del HTML fuente en enlaces limpios en desarrollo y compilación. El navegador cambia la URL mediante History API y desplaza/focaliza la sección. Se respeta movimiento reducido, selección de área y apertura de FAQ. Atrás/adelante restauran la sección; los enlaces antiguos `/#contacto` siguen funcionando y se normalizan.

## Carga directa y servidor

`dist` incluye un `index.html` en cada directorio de alias, con recursos de rutas absolutas. Así recargar o compartir `/contacto` no depende únicamente de JavaScript ni devuelve una página vacía. Sin JavaScript se ve la HOME completa; el desplazamiento automático a la sección requiere JavaScript.

En Apache, `.htaccess` resuelve los alias hacia la HOME antes de añadir una barra al directorio. En Nginx estático, un directorio puede redirigir primero a `/contacto/`; el navegador normaliza después la URL a `/contacto`. Para evitar ese salto, el administrador puede configurar en el bloque del dominio (sin tocar `/api`):

```nginx
location ~ ^/(contenido|areas-juridicas|sobre-mi|segunda-oportunidad|reclamaciones-bancarias|preguntas-frecuentes|contacto|forma-de-trabajar|penal|faq-segunda)/?$ {
    try_files /index.html =404;
}
```

Aplicar a través de la configuración adecuada de Plesk y validar con el proveedor. No sustituir las reglas PHP existentes ni configurar un fallback global que oculte errores de `/api`.
En un hosting exclusivamente Nginx, añadir también redirecciones de las tres rutas antiguas a las nuevas. El alojamiento actual usa Nginx como proxy y Apache para aplicar las reglas del proyecto.

## SEO y pruebas

Los alias mantienen canonical hacia `https://amalioabogado.com/`. El sitemap incluye solo la HOME: no presenta estas rutas como páginas con contenido independiente. Los `#` de identificadores de Schema (`@id`) son internos, no enlaces de navegación, y se conservan.

Pruebas locales superadas: enlaces sin hash, selección de consulta, apertura de FAQ, carga directa de `/contacto`, recarga, historial y compatibilidad con `/#contacto`; responsive y axe entre 320 y 2560 px. Falta comprobar las reglas y redirecciones en el alojamiento real tras subir el contenido actualizado de `dist`.
