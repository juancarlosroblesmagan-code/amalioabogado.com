# Arquitectura SEO para siguientes fases

| URL prevista | Intención y condición de creación |
| --- | --- |
| `/` | Entidad personal, confianza y visión general. Única página canónica actual. |
| `/abogado-albacete/` | Trayectoria y atención local. Crear solo con contenido propio; si duplica HOME, mantener sección Sobre mí y no crear URL. |
| `/derecho-penal/` | Defensa penal, alcance confirmado, consulta prudente. |
| `/derecho-civil/` | Procedimientos civiles; concretar servicios con Amalio. |
| `/segunda-oportunidad/` | Requisitos y alternativas, revisión normativa y fecha editorial. Sin cancelación garantizada. |
| `/reclamaciones-bancarias/` | Página general de defensa financiera, enlazando contenidos específicos. |
| `/tarjetas-revolving/` | Explicación diferenciada del producto, análisis contractual y circunstancias. |
| `/gastos-hipotecarios/` | Contenido específico revisado y actualizado, no copiar página bancaria general. |
| `/derecho-laboral/` | Servicios laborales previamente confirmados. |
| `/divorcios/` | Divorcios y Familia: delimitar alcance real. |
| `/preguntas-frecuentes/` | Crear solo si aporta un recurso distinto y suficiente respecto de FAQ de HOME. |
| `/contacto/` | Datos confirmados, canales reales y tratamiento de datos validado. |

Los enlaces actuales son rutas limpias que llevan a secciones de la misma HOME (ver `RUTAS.md`). No existen páginas interiores vacías. Cada nueva página deberá tener title/description propios, canonical confirmado, breadcrumbs reales, HTML semántico y enlaces contextuales. Sitemap incluirá únicamente páginas publicadas con contenido propio. Si se convierte un alias existente en página independiente, actualizar mapa de rutas, enlaces y canonical.

## Entidades

`Person` representa a Amalio, `LegalService` su actividad, `WebSite` el sitio y `WebPage` la HOME. `worksFor`, `founder`, `publisher`, `about` e identificadores comunes enlazan el grafo. Se usa LegalService y no el tipo Attorney obsoleto. Colegiación representada como credencial profesional; no como título académico inventado. No hay `Review`, `AggregateRating`, `sameAs`, precios o premios.

No se generan AboutPage/ContactPage/BreadcrumbList para documentos que aún no existen. FAQPage puede valorarse cuando corresponda, sin asumir elegibilidad para resultados enriquecidos de Google.

## SEO local y generativo

Mantener nombre, email, dirección y colegiación consistentes. Crear o revisar la ficha real de Google Business solo con autorización y datos confirmados. No se han inventado horarios, teléfono o perfiles sociales. Contenido claro y verificable, autor real, respuestas directas, lenguaje sin promesas y revisión jurídica previa. Ninguna técnica garantiza aparición o posicionamiento en respuestas generativas.
Implementación y seguimiento de descubrimiento con IA en `SEO-IA.md`, incluida guía pública `/llms.txt`.
