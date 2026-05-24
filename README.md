# Guillermo Represa · Coach Personal Humanista

Web oficial de Guillermo Represa, coach personal humanista certificado por ASESCO.

🌐 **Producción:** https://guillermorepresacoachpersonal.vercel.app

## Stack

Web 100% estática, sin frameworks ni backend:
- HTML, CSS y JavaScript ligero (vanilla).
- Tipografía: Fraunces + Inter (Google Fonts).
- Despliegue automático en Vercel desde este repositorio.

## Estructura

```
.
├── index.html                  Home
├── servicio.html               Página de servicio
├── gracias.html                Confirmación post-reserva
├── aviso-legal.html            Aviso legal (LSSI-CE)
├── politica-privacidad.html    Política de privacidad (RGPD/LOPDGDD)
├── sitemap.xml                 Sitemap (Google + crawlers de IA)
├── robots.txt                  Robots con permisos explícitos para crawlers IA
├── logo-coaching.svg           Logo (SVG escalable)
├── og-image.png / .svg         Imagen para redes sociales (1200×630)
├── equilibrio.jpg              Imagen de fondo en sección Para Quién
├── guillermo-represa-coach.jpg Foto principal
├── guillermo-natural.jpg       Foto secundaria
└── blog/
    ├── index.html              Índice del blog (renderiza desde posts.json)
    ├── posts.json              Fuente única de datos del blog
    ├── plantilla-articulo.html Plantilla para nuevos artículos
    ├── BLOG-INSTRUCCIONES.md   Guía rápida para publicar
    └── <slug>.html             Cada artículo individual
```

## Cómo añadir un nuevo artículo

Consulta **`blog/BLOG-INSTRUCCIONES.md`**. Resumen:

1. Duplica `blog/plantilla-articulo.html` → `blog/tu-slug.html` y rellena los marcadores `[[ ... ]]`.
2. Añade una entrada al array `posts` en `blog/posts.json`.
3. Añade la URL en `sitemap.xml`.
4. `git push`. Vercel despliega solo.

El índice del blog (`blog/index.html`) detecta el nuevo post automáticamente — no hay que editarlo.

## SEO / AEO

- Schema.org enriquecido: `Person`, `ProfessionalService`, `FAQPage`, `Article`, `BreadcrumbList`, `Blog`.
- `AggregateRating` con testimonios verificados.
- `robots.txt` con permisos explícitos para crawlers de IA (GPTBot, ClaudeBot, PerplexityBot, etc.).
- Open Graph y Twitter Cards en todas las páginas.
- `hreflang` preparado para futuras versiones en otros idiomas.

## Despliegue

Vercel observa la rama `main`. Cada push despliega automáticamente. URL canónica: `https://guillermorepresa.com` (cuando se conecte el dominio).

## Datos de contacto

- WhatsApp: +34 625 19 28 90
- Email: guillermorepresacoachpersonal@gmail.com
- Instagram: https://www.instagram.com/guillermorepresacoachpersonal/
- LinkedIn: https://www.linkedin.com/in/guillermo-represa-coach-personal-4b681b350/
- Certificación: ASESCO CPS 10326

## Licencia

Contenido editorial © Guillermo Represa. Código bajo dominio del propietario del repositorio. No reutilizar sin permiso.
