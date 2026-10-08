# SEO local y descubrimiento en buscadores con IA

## Implementación

- HTML semántico con contenido profesional disponible sin JavaScript, encabezados claros y preguntas frecuentes visibles.
- Nombre, profesión, ICALBA nº 1847, ejercicio desde 1996, dirección en Albacete y email profesional consistentes entre HOME, Schema y guía textual.
- Grafo JSON-LD enlazado: `Person`, `LegalService`, `WebSite` y `WebPage`; sin reseñas, premios, perfiles externos ni resultados inventados.
- Indexación habilitada, canonical `https://amalioabogado.com/`, sitemap de la HOME y robots que permite el contenido público. API y rutas privadas excluidas del rastreo; estas exclusiones no sustituyen controles de acceso.
- `/llms.txt`: guía Markdown opcional con datos públicos, enlaces a secciones y límites del servicio. Se genera únicamente con dominio y publicación aprobados. No incluye NIF, contraseña, remitente SMTP técnico ni información privada de consultas.
- No se añade un endpoint de acciones de IA ni se permite que agentes accedan a consultas privadas. La IA puede descubrir información pública, no administrar el despacho.
- Las rutas `/areas-juridicas`, `/reclamaciones-bancarias`, `/preguntas-frecuentes`, `/contacto`, `/sobre-mi`, etc. siguen siendo secciones de una única HOME con canonical común; no se presentan como páginas nuevas en el sitemap. Las tres rutas abreviadas anteriores tienen redirección 301 y no se enlazan en la navegación ni en llms.

## Qué significa y qué no

La base de visibilidad en Google y sus funciones de IA es el SEO habitual: contenido útil y verificable, acceso de rastreadores, indexación y datos estructurados coherentes. Google indica que no hace falta un archivo de IA ni un Schema especial. `llms.txt` es una ayuda opcional para herramientas que lo utilicen, no un requisito universal ni una señal de posicionamiento garantizada.

El grupo `User-agent: *` permite el contenido público a Googlebot, Bingbot y rastreadores de búsqueda con IA, incluido OAI-SearchBot. No se han creado excepciones del cortafuegos basadas solo en nombres de agentes, porque son falsificables. Las peticiones de prueba con estos nombres comprueban accesibilidad, no prueban que proveedores reales hayan rastreado o indexado el sitio.

OAI-SearchBot se destina a búsqueda; GPTBot se destina a posible entrenamiento. Son controles distintos. La política general de robots existente sigue permitiendo el contenido público y no se ha introducido una política específica de entrenamiento. Cualquier cambio de esa política requiere decisión del titular y revisión por proveedor. `llms.txt` no controla permisos de uso o entrenamiento.

No se garantiza aparición, posición ni citación en ChatGPT, Gemini, Perplexity, Claude u otros servicios. Tampoco se afirma que la HOME esté ya indexada por haber habilitado `index, follow`.

## Seguimiento recomendado

1. Verificar la propiedad en Google Search Console y Bing Webmaster Tools; enviar `https://amalioabogado.com/sitemap.xml`. Requiere cuentas del titular y no se ha hecho desde esta entrega.
2. Crear o actualizar únicamente la ficha real de Google Business Profile y, si procede, Bing Places. Mantener identidad y dirección coherentes; no inventar teléfono, horarios ni reseñas. No se han creado perfiles externos.
3. Comprobar con el proveedor posibles bloqueos por IP/WAF/CDN usando sus registros y rangos oficiales, sin desactivar la seguridad global ni confiar solo en un User-Agent.
4. Revisar consultas reales, datos profesionales y normativa; ampliar contenidos solo con páginas sustanciales y jurídicamente revisadas. No producir páginas repetitivas ni promesas de resultados.

## Pruebas

`npm run check:discovery` comprueba respuesta HTTP 200 de la HOME para nombres declarados de cinco rastreadores, contenido profesional en HTML, canonical, indexación, grafo Schema, robots y `/llms.txt`. No envía correos ni acredita presencia en resultados de búsqueda.

`scripts/check-build.mjs` comprueba generación de llms con el origen configurado y ausencia de datos privados; las compilaciones sin dominio mantienen noindex.

## Fuentes primarias

- Google Search Central: https://developers.google.com/search/docs/appearance/ai-features?hl=es
- Rastreadores OpenAI y diferencia entre búsqueda y entrenamiento: https://platform.openai.com/docs/bots
- Propuesta de formato llms.txt: https://llmstxt.org/

Revisado el 8 de octubre de 2026. La preparación técnica no garantiza indexación o recomendación.
