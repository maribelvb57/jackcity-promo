# hotelesparaperrossantiago.cl

Landing page estática (HTML + CSS puro, sin build step) que capta tráfico SEO para la
keyword **"hoteles para perros Santiago"** y lo canaliza a [JackCity](https://jackcity.cl)
con un botón real (`<a href>`), **sin redirect automático** (nada de `meta refresh` ni
`window.location`), para evitar la penalización de Google por *doorway pages*.

## Estructura

```
/
  index.html        Homepage: arte del hero (imagen) + contenido HTML indexable
  styles.css        Estilos
  robots.txt        Indexación abierta + sitemap
  sitemap.xml       Home con lastmod / changefreq / priority
  vercel.json       Cache de assets + headers de seguridad
  home-03.html      Borrador de diseño (noindex + canonical a /). No se enlaza.
  home-03.css
  /assets
    hero-jackcity-santiago.jpg       1222x975  arte del hero (recorte del mockup)
    hero-jackcity-santiago-720.jpg    720x574  versión móvil (srcset)
    og-image.jpg                     1200x630  imagen para redes
    home-03-reference.jpg            1222x1287 mockup original completo
    favicon.svg
```

## Cómo está armado el hero

El hero es el **arte de `home-03`**, recortado justo bajo la curva crema (975 px de alto),
para que los beneficios, el contenido y el footer sean HTML real y no píxeles.

- El titular vive dentro de la imagen; su texto está disponible para buscadores y
  lectores de pantalla en el `alt` y en el bloque `.hero__semantic` (que contiene el `<h1>`).
- El botón "Ir a JackCity" del arte es una **zona activa** (`.hero__cta`) posicionada en
  porcentajes sobre la imagen.

### Si cambias el arte del hero

Hay que recalcular la zona activa. Valores actuales, medidos sobre 1222 × 975 px
(botón amarillo en x 699–1068, y 584–673):

```css
.hero__cta{ top:59.9%; left:57.2%; width:30.3%; height:9.3%; }
```

Para verificarlo: pinta temporalmente `background:rgba(255,0,0,.45)` en `.hero__cta`
y comprueba que cubra exactamente el botón amarillo.

Además, en pantallas ≤760 px se muestra un CTA amarillo de texto bajo el arte
(`.cta-mobile`), porque el botón dibujado queda de ~118×30 px en un teléfono.
Si no lo quieres, elimina ese bloque de `index.html` y su regla en `styles.css`.

## SEO incluido

- `lang="es-CL"`, `<title>`, meta description, `robots`, canonical.
- Un solo `<h1>` (en `.hero__semantic`), `<h2>`/`<h3>` visibles en beneficios, contenido y FAQ.
- Open Graph + Twitter Card apuntando a `/assets/og-image.jpg` (1200×630, ya incluida).
- JSON-LD con `@graph`: `WebSite`, `WebPage`, `Organization`+`LocalBusiness` (JackCity,
  areaServed Santiago / Región Metropolitana) y `FAQPage`.
- `robots.txt` abierto + `sitemap.xml`.
- `home-03.html` queda con `noindex` y canonical a `/` para no competir con la home.

## Deploy en Vercel

1. Vercel → **Add New… → Project** → importar este repo.
2. Framework Preset: **Other**. Build Command: vacío. Output Directory: `.` (raíz).
3. **Settings → Domains** → agregar `hotelesparaperrossantiago.cl` (y `www` redirigido al apex).
4. Apuntar el DNS del dominio a Vercel según indique el panel.

## Post-deploy

- Google Search Console: agregar la propiedad, verificar y enviar
  `https://hotelesparaperrossantiago.cl/sitemap.xml`.
- Revisar FAQ y Organization en el Test de Resultados Enriquecidos.
- Actualizar `<lastmod>` en `sitemap.xml` cuando cambie el contenido.

## Pendiente / mejorable

- El texto del hero es imagen: en móvil se lee pequeño. La alternativa es rehacer ese
  bloque en HTML (existe una versión así en el historial de git, commit `7bc38a9`).
- El hero pesa ~330 KB en JPEG. Convertirlo a WebP/AVIF bajaría a ~120 KB.
