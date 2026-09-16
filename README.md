# Finca Papirucho

Sitio web de una sola página para Finca Papirucho, un sitio de ecoturismo frente al río Sonador en Yásica, Puerto Plata, República Dominicana. Reservas por WhatsApp.

**Live:** [fincapapirucho.site](https://fincapapirucho.site/)

## Qué es

Un sitio estático hecho con HTML, CSS y JavaScript puros — sin frameworks, sin build system, sin dependencias npm. Todo vive en `index.html` (~6300 líneas).

### Servicios que presenta

- Camping y glamping
- Excursiones por el río Sonador
- Fourwheel tours
- Áreas recreativas y balneario

### Funcionalidades

| Feature | Implementación |
|---------|---------------|
| Selector de idioma (ES/EN/FR) | JS inline con `DICT`, traduce texto visible + `aria-label` |
| Galería de imágenes | Viewer fullscreen con pan/zoom (`panzoom.min.js`), hotspots para tours |
| Carruseles por servicio | Autoplay 4s, play/pause, drag/swipe, dots de progreso |
| Imágenes progresivas | 4 resoluciones por foto (`_low`, `_med`, `_web`, original) + base64 placeholders |
| FAQ accordion | `<details>`/`<summary>` con CSS custom |
| Reservas WhatsApp | Links con mensaje prellenado por servicio (`wa.me/18492077092`) |
| Quicknav | Barra lateral sticky que marca la sección visible vía scroll-spy |
| Responsive | Mobile-first; bottom sheet en mobile, grid en desktop |

## Estructura

```
finca-papirucho/
├── index.html              ← El sitio completo (HTML + CSS + JS inline)
├── assets/
│   ├── progressive/        ← Imágenes en 4 resoluciones + base64 placeholders
│   ├── js/panzoom.min.js   ← Única dependencia externa (pan/zoom de galería)
│   ├── logo.jpg            ← Favicon
│   ├── background.mp4      ← Video hero
│   └── bank-banreservas.png, bank-bhd.png  ← Logos de bancos
├── LICENSE                 ← Apache 2.0
└── README.md
```

## Desarrollo

No hay paso de build. Abrí `index.html` directamente en el navegador o usá un servidor local:

```bash
# Cualquier servidor estático sirve
python -m http.server 8080
# o
npx serve .
```

Para ver la versión en producción, push a `main` — GitHub Pages despliega automáticamente.

## Deploy

El sitio estático se sirve vía GitHub Pages y Cloudflare Workers:

- **GitHub Pages:** `https://fincapapirucho.site/` (dominio principal)
- **Cloudflare Workers:** `https://finca-papirucho.kevinjooo59.workers.dev/` (preview)

Push a `main` = deploy automático.

## Notas técnicas

- **CSS:** colores con CSS custom properties (`--forest`, `--muted`, etc.), responsive con media queries en `759px`/`760px` (mobile bottom sheet vs desktop grid)
- **JS:** vanilla, sin módulos, todo inline en `<script>` al final del `<body>`
- **Imágenes:** hashes en nombres (`02c3367f_web.jpg`), `loading="lazy"` en imágenes below-the-fold
- **SEO:** schema.org `TouristAttraction`, Open Graph, Twitter cards, meta description
- **Accesibilidad:** `role="tablist"`, `aria-label` en controles interactivos, skip-link, `prefers-reduced-motion`

## Licencia

Apache License 2.0 — ver [LICENSE](LICENSE).
