# Mejía & Asociados — Estudio Jurídico

> Sitio web corporativo para bufete de abogados especializado en derecho empresarial y corporativo.

---

## 🎯 PROPÓSITO GENERAL

Este proyecto es un sitio web estático, multipágina y completamente responsivo para el estudio jurídico **Mejía & Asociados**. Su objetivo es proyectar autoridad, confianza y excelencia profesional, presentando al bufete, sus áreas de práctica, equipo legal, casos destacados, metodología de trabajo y un formulario de contacto. No depende de frameworks externos ni de JavaScript, por lo que su mantenimiento es directo y su carga es óptima.

---

## 🚀 TECNOLOGÍAS UTILIZADAS

- **HTML5** — Estructura semántica (`<header>`, `<section>`, `<article>`, `<footer>`, `<nav>`)
- **CSS3 puro** — Sin frameworks (Bootstrap, Tailwind, Bulma, etc.)
  - Variables CSS (`--color-azul`, `--fuente-principal`, etc.)
  - CSS Grid (áreas de práctica, método, contacto, pie de página)
  - Flexbox (encabezado, firma, equipo, clientes)
  - Pseudo-elementos `::before` y `::after`
  - Pseudo-clases `:hover` y `:focus`
  - Media queries para responsividad
  - Transiciones y animaciones CSS
- **Google Fonts** — `Cormorant Garamond` (cuerpo) y `Cormorant SC` (versalitas/etiquetas)
- **HTML5 Video** — Hero con video de fondo (`autoplay`, `muted`, `loop`, `playsinline`)
- **YouTube iframes** — Sección de conferencias

---

## 🛠️ ARQUITECTURA Y FLUJO

```
index.html ──────────────────────────────────────────────────────
│
├── <head>
│     ├── Meta viewport, charset, título
│     └── <link> a estilos.css y Google Fonts
│
├── <body>
│     ├── .encabezado       → Navegación fija (sticky)
│     ├── .inicio           → Hero con video de fondo + contenido
│     ├── .firma            → Sobre nosotros (Flexbox)
│     ├── .areas            → Áreas de práctica (CSS Grid 4 col)
│     ├── .equipo           → Equipo legal (Flexbox)
│     ├── .hitos            → Casos destacados (CSS Grid 4 col)
│     ├── .metodo           → Metodología 4 pasos (CSS Grid 4 col)
│     ├── .clientes         → Logos de empresas asesoradas (Flexbox)
│     ├── .conferencias     → Videos iframes (CSS Grid 3 col)
│     ├── .contacto         → Info + Formulario (CSS Grid 2 col)
│     └── <footer>.pie      → Mapa del sitio (CSS Grid 4 col)
│
estilos.css ─────────────────────────────────────────────────────
│
├── :root                   → Variables CSS (colores, fuentes, espaciado)
├── Reset                   → * { box-sizing, margin, padding: 0 }
├── Base                    → body, img, a
├── Componentes globales    → .etiqueta-seccion, .boton-principal, .boton-secundario
└── Secciones               → encabezado → inicio → firma → áreas → ... → pie
    └── @media queries      → ≤1200px, ≤900px, ≤600px
```

El flujo de carga es lineal: el navegador lee `index.html` de arriba hacia abajo, carga `estilos.css` en el `<head>` (bloqueante pero necesario para evitar FOUC), y renderiza sección por sección. No hay JavaScript de ningún tipo.

---

## 📝 ANÁLISIS DETALLADO DE COMPONENTES Y REGLAS CSS

### Variables CSS (`:root`)

| Variable | Valor | Uso |
|---|---|---|
| `--color-azul` | `#0B1F3A` | Fondo principal oscuro |
| `--color-gris` | `#D9D9D9` | Bordes y separadores |
| `--color-blanco` | `#FFFFFF` | Texto sobre fondos oscuros |
| `--color-dorado` | `#B08D57` | Acentos, números, etiquetas |
| `--fuente-principal` | `Cormorant Garamond` | Tipografía serif de cuerpo |
| `--fuente-versalitas` | `Cormorant SC` | Etiquetas, logos, pequeños títulos |
| `--transicion` | `0.35s ease` | Animaciones interactivas uniformes |

---

### `.encabezado`

- **Técnica:** `display: flex` con `justify-content: space-between` para separar marca y nav.
- **`position: sticky; top: 0; z-index: 100`** — El encabezado se queda fijo al hacer scroll.
- **`::after`** — Traza una línea decorativa dorada degradada en el borde inferior del encabezado. No requiere elemento HTML adicional.
- **Hamburguesa CSS-only:** Un `<input type="checkbox">` oculto actúa como estado. Su `<label>` funciona como botón. Cuando el checkbox está marcado (`#menu-activo:checked ~ .encabezado__nav`), el nav pasa de `display: none` a `display: flex`, logrando el menú desplegable sin JavaScript.

---

### `.enlace-nav`

- **`::after`** — Línea dorada de ancho 0 por defecto. Al hacer `:hover`, `width` pasa a `100%` con transición, creando el efecto de subrayado animado.
- Sin `text-decoration` nativa; el subrayado es completamente CSS custom.

---

### `.inicio` (Hero)

- **`position: relative; overflow: hidden`** — Contiene todos los elementos hijos con `position: absolute`.
- **`.inicio__video-fondo`** — `object-fit: cover` garantiza que el video llene el contenedor sin deformarse, independientemente del ratio de la pantalla.
- **`.inicio__degradado`** — `linear-gradient` diagonal (`105deg`) que va de azul oscuro semitransparente (izquierda) a casi transparente (derecha). Esto asegura legibilidad del texto sobre cualquier fotograma del video.
- **`.inicio__contenido`** — `position: relative; z-index: 2` para aparecer encima del video y el degradado (que tienen `position: absolute`).

---

### `.boton-principal`

- **`::after`** — Capa blanca de ancho 0 sobre el botón. Al `:hover`, `width` se expande a `100%`, simulando un flash de brillo.
- **`overflow: hidden`** en el botón contiene el pseudo-elemento dentro de sus límites.
- **`transform: translateY(-2px)`** en hover da sensación de elevación sin usar `position`.

---

### `.firma` (Sobre Nosotros)

- **`display: flex; align-items: center`** — Coloca texto (55% del ancho) y el ornamento decorativo (40%) en fila horizontal centrada verticalmente.
- **`.firma__ornamento::before`** — Marco interior decorativo usando `border` con `position: absolute` relativo al contenedor padre.
- **`.firma__ornamento::after`** — Las siglas "MjA" gigantes con `opacity: 0.07`, logrando un watermark tipográfico sin imagen adicional.

---

### `.areas__cuadricula` (Áreas de práctica)

- **`display: grid; grid-template-columns: repeat(4, 1fr)`** — Las 8 tarjetas se distribuyen en 4 columnas y 2 filas automáticamente.
- **`gap: 2px`** — Espaciado mínimo que actúa como separador visual tipo "rejilla".
- Las tarjetas tienen `border` dorado muy sutil y en `:hover` aumenta `background-color` y `border-color` además de `transform: translateY(-4px)`.

---

### `.tarjeta-abogado`

- **`.tarjeta-abogado__imagen-contenedor`** — `overflow: hidden` permite que la imagen haga zoom (`scale(1.04)`) sin salirse del recuadro.
- **`.tarjeta-abogado__velo`** — Div vacío con `background-color: rgba(dorado, 0)`. En `:hover` la opacidad sube a `0.15`, creando un tinte dorado sobre la foto.
- **`border-top: 3px solid var(--color-dorado)`** en `.tarjeta-abogado__info` — Línea de acento que separa imagen de texto.

---

### `.info-contacto::before`

- **Pseudo-elemento:** Barra vertical dorada degradada en el borde izquierdo del bloque de información de contacto. Logra énfasis visual sin elemento HTML adicional.
- `height: 60%` y `top: 20%` centran la barra verticalmente.

---

### `.campo__entrada--select`

- **`appearance: none`** — Elimina el selector nativo del sistema operativo.
- **`background-image`** — Inyecta un SVG inline como flecha personalizada dorada, manteniendo el control estilístico completo sobre el elemento.

---

### `.menu-activo` (Hamburguesa sin JS)

| Elemento | Función |
|---|---|
| `<input type="checkbox" id="menu-activo">` | Estado booleano (abierto/cerrado) |
| `<label for="menu-activo">` | Target de clic que activa el checkbox |
| `.menu-activo:checked ~ .encabezado__nav` | Selector CSS que muestra el nav cuando el checkbox está marcado |

- El `<input>` tiene `display: none` (oculto visualmente, pero el `<label>` sigue siendo funcional).
- Funciona en todos los navegadores modernos sin una sola línea de JavaScript.

---

### Media Queries

| Breakpoint | Cambios principales |
|---|---|
| `max-width: 1200px` | Grids de 4 col → 2 col en áreas, hitos y método |
| `max-width: 900px` | Hamburguesa visible, firma en columna, formulario 1 col |
| `max-width: 600px` | Ajuste tipográfico, botones en columna, equipo apilado |

---

## 💻 CÓMO EJECUTARLO

### Requisitos

- Cualquier navegador moderno (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+).
- No requiere Node.js, npm, servidor de backend, ni procesador CSS.

### Pasos

```bash
# 1. Clonar o descargar el repositorio
git clone <url-del-repositorio>
cd mejia-asociados

# 2. Colocar los assets en sus rutas esperadas:
#    video/INTRODUCION.mp4   → video del hero
#    abogado1.jpg            → foto Dr. Roberto Mejía
#    abogada1.jpg            → foto Dra. Elena Valdés
#    abogado2.jpg            → foto Dr. Sergio Arango
#    empresa1.png ... empresa6.png → logos de clientes

# 3. Reemplazar los placeholders de YouTube:
#    En index.html, cambiar VIDEO_1, VIDEO_2, VIDEO_3
#    por los IDs reales de YouTube (ej: dQw4w9WgXcQ)

# 4. Abrir en el navegador
#    Opción A — doble clic en index.html
#    Opción B — servidor local (recomendado para el video):
npx serve .          # Node.js
python -m http.server 8000   # Python 3
```

> **Nota sobre el video:** Algunos navegadores bloquean la reproducción automática de video con audio. El atributo `muted` en el `<video>` garantiza que `autoplay` funcione correctamente en todos los navegadores modernos según las políticas de reproducción automática.

### Estructura de archivos

```
mejia-asociados/
├── index.html
├── estilos.css
├── video/
│   └── INTRODUCION.mp4
├── abogado1.jpg
├── abogada1.jpg
├── abogado2.jpg
├── empresa1.png
├── empresa2.png
├── empresa3.png
├── empresa4.png
├── empresa5.png
└── empresa6.png
```
