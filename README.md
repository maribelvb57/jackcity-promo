# hotelesparaperrossantiago.cl

Landing page estática (HTML + CSS puro, sin build step) que capta tráfico SEO para la
keyword **"hoteles para perros Santiago"** y lo canaliza a [JackCity](https://jackcity.cl)
mediante un botón real (`<a href>`), **sin redirect automático** (nada de `meta refresh`
ni `window.location`), para evitar la penalización de Google por *doorway pages*.

## Estructura

```
/
  index.html          Página completa (HTML semántico + JSON-LD)
  styles.css          Estilos (mobile-first, sin frameworks)
  robots.txt          Indexación abierta + sitemap
  sitemap.xml         Home con lastmod / changefreq / priority
  vercel.json         Cache de assets + headers de seguridad
  /assets
    hero-placeholder.svg   <-- PLACEHOLDER del hero (reemplazar)
    favicon.svg
```

## Reemplazar la imagen del hero

1. Deja la foto final en `assets/` (recomendado: `hero.webp` ~1600×1200, < 300 KB;
   opcionalmente `hero.jpg` como respaldo).
2. En `index.html`, cambia el `src` del hero:

   ```html
   <img class="hero__bg" src="/assets/hero.webp" alt="..." ...>
   ```

3. Encuadre: el CSS usa `object-fit: cover`. Si el perro queda mal recortado, ajusta
   `object-position` en `styles.css` (`.hero__bg` para móvil, y el bloque
   `@media (min-width:900px)` para escritorio).

## Imagen para redes (Open Graph)

Falta `assets/og-image.jpg` (**1200×630**). Las metaetiquetas ya apuntan a
`https://hotelesparaperrossantiago.cl/assets/og-image.jpg`; basta con subir el archivo.

## Deploy en Vercel

1. Vercel → **Add New… → Project** → importar este repo.
2. Framework Preset: **Other**. Build Command: vacío. Output Directory: `.` (raíz).
3. **Settings → Domains** → agregar `hotelesparaperrossantiago.cl` y `www.` (redirigido al apex).
4. Apuntar el DNS del dominio a Vercel (registro A `76.76.21.21` o CNAME según indique el panel).

## Post-deploy (SEO)

- Google Search Console: agregar la propiedad de dominio, verificar y enviar
  `https://hotelesparaperrossantiago.cl/sitemap.xml`.
- Revisar el rich result de FAQ y Organization en el Test de Resultados Enriquecidos.
- Actualizar `<lastmod>` en `sitemap.xml` cuando cambie el contenido.

## Notas

- El CTA abre JackCity en una pestaña nueva (`target="_blank" rel="noopener"`).
  Para abrirlo en la misma pestaña, elimina `target="_blank"`.
- Los enlaces a jackcity.cl son `follow` a propósito: transfieren autoridad al sitio principal.
