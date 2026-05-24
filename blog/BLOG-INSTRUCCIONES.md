# 📝 Cómo publicar un nuevo artículo en el blog

Sistema sin frameworks ni backend. Solo HTML estático + JSON + JS ligero.

## Cómo funciona el blog

- `blog/index.html` — Índice del blog. Renderiza las tarjetas **leyendo dinámicamente** `posts.json`.
- `blog/posts.json` — **Fuente única de datos**. Lista de artículos publicados.
- `blog/plantilla-articulo.html` — Template para duplicar al crear un artículo nuevo.
- `blog/<slug>.html` — Cada artículo es un archivo individual.

Para añadir un artículo solo tocas **dos archivos**: la nueva página HTML y el `posts.json`. No hay que editar `index.html` ni código JavaScript.

---

## Paso a paso para publicar un artículo nuevo

### 1. Crea el archivo del artículo

1. Duplica `blog/plantilla-articulo.html`.
2. Renombra el duplicado con tu slug (sin acentos, sin espacios, sin mayúsculas):
   ```
   blog/decisiones-postergadas.html
   ```
3. Abre el archivo y rellena cada marcador `[[ ALGO ]]`. La lista completa de marcadores está al inicio del propio archivo de plantilla, con ejemplos.

> **Importante**: el nombre del archivo (sin `.html`) tiene que coincidir exactamente con el campo `slug` que pondrás en `posts.json`.

### 2. Añade la entrada al `posts.json`

Abre `blog/posts.json` y añade un objeto nuevo al final del array `posts`. Ejemplo:

```json
{
  "slug": "decisiones-postergadas",
  "title": "Decisiones postergadas: por qué llevas meses sin decidir",
  "excerpt": "Resumen breve que se ve en la tarjeta del blog. 1-2 frases.",
  "category": "Coaching humanista",
  "date": "2026-06-15",
  "dateDisplay": "15 de junio de 2026",
  "readTime": "6 min",
  "icon": "→",
  "featured": false,
  "published": true
}
```

**Campos**:

| Campo         | Para qué sirve                                                  |
|---------------|-----------------------------------------------------------------|
| `slug`        | Nombre del archivo HTML sin extensión.                          |
| `title`       | Título completo del artículo.                                   |
| `excerpt`     | Texto del párrafo que aparece en la tarjeta del blog.           |
| `category`    | Etiqueta superior de la tarjeta. Ej: "Coaching humanista", "Recursos". |
| `date`        | Fecha en formato `YYYY-MM-DD` (se usa para ordenar).            |
| `dateDisplay` | Fecha que se ve en la tarjeta. Ej: `15 de junio de 2026`.       |
| `readTime`    | `"6 min"` o `"7 min de lectura"`.                               |
| `icon`        | Carácter o símbolo que aparece en la imagen decorativa. Ej: `∞`, `↑`, `⇄`, `→`. |
| `featured`    | `true` para destacar el artículo en grande (solo uno cada vez). |
| `published`   | `false` para ocultarlo aunque siga en el JSON.                  |

### 3. Actualiza `sitemap.xml`

Añade el bloque de la nueva URL al `sitemap.xml` de la raíz:

```xml
<url>
  <loc>https://guillermorepresa.com/blog/decisiones-postergadas.html</loc>
  <lastmod>2026-06-15</lastmod>
  <changefreq>monthly</changefreq>
  <priority>0.8</priority>
</url>
```

### 4. Sube los cambios

```bash
git add blog/decisiones-postergadas.html blog/posts.json sitemap.xml
git commit -m "Nuevo artículo: Decisiones postergadas"
git push
```

Vercel desplegará automáticamente.

---

## Operaciones habituales

### Ocultar un artículo sin borrarlo

En `posts.json`, cambia `"published": true` por `"published": false`. La tarjeta deja de aparecer en el listado, pero la URL del artículo sigue funcionando.

### Cambiar el artículo destacado

Pon `"featured": true` solo en el que quieras destacar. Si hay varios marcados como `featured`, todos aparecen como destacados (no es recomendable). Lo habitual es: el más reciente o el más estratégico.

### Reordenar artículos

El orden se calcula automáticamente: los `featured` primero, después los demás por fecha descendente. No hace falta reordenar manualmente.

### Borrar un artículo

1. Quita el objeto del `posts.json`.
2. Borra el archivo `blog/<slug>.html`.
3. Quita la entrada del `sitemap.xml`.
4. (Opcional pero recomendado) configura una redirección 301 en Vercel hacia el blog index para no romper enlaces externos antiguos.

---

## Errores frecuentes

- **El artículo no aparece en el listado.** Revisa que `"published": true`, que el JSON sea válido (sin comas finales, comillas dobles), y que el archivo HTML exista en `blog/`.
- **El enlace de la tarjeta lleva a 404.** El `slug` del JSON no coincide con el nombre del archivo HTML.
- **El JSON da error al guardar.** Usa un validador online (jsonlint.com) o un editor con resaltado. Causas habituales: coma sobrante al final del último objeto, comillas simples en vez de dobles, caracteres especiales sin escapar.
- **Cambios no se ven en producción.** Vercel necesita ~30 seg para desplegar tras el push. Refresca con Ctrl+Shift+R (sin caché).
