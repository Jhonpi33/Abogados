# Mejía & Asociados — Sitio Web
## Proyecto ADSO · SENA Centro Agroturístico

---

## ¿Qué es este proyecto?

Sitio web profesional para el **Estudio Jurídico Mejía & Asociados**, desarrollado como proyecto del brief #7 del programa ADSO. El cliente es el Dr. Roberto Mejía, abogado con 20 años de experiencia. La página transmite **autoridad, experiencia y confianza** a través de una paleta sombría (azul oscuro, dorado, gris y blanco) y tipografía serif clásica.

**Tecnologías usadas:** HTML5 semántico + CSS3 puro. Sin frameworks. Sin JavaScript.

---

## Estructura de archivos

```
/
├── index.html          → Página principal
├── styles.css          → Hoja de estilos principal
├── README.md           → Este archivo
├── img/
│   ├── logomj.png                  → Logo banner del encabezado
│   ├── icono logo.png              → Icono pequeño del hero
│   ├── brief_img/
│   │   ├── roberto_mejia.png       → Foto abogado principal
│   │   ├── elena_valdes.png        → Foto abogada
│   │   ├── sergio_arango.png       → Foto abogado
│   │   └── carolina_pinto.png      → Foto abogada
│   └── Empresas_Asesoradas/
│       ├── capital.png
│       ├── elite.png
│       ├── grupoandino.jpg
│       ├── inversionesnova.png
│       └── sas.jpg
└── video/
    ├── INTRODUCION.mp4             → Video de fondo del hero (Dropbox)
    ├── video audio.mp4             → Conferencia principal (con audio)
    ├── Contratos Comerciales Internacionales.mp4
    ├── Arbitraje Empresarial.mov
    └── Protección Patrimonial.mov
```

---

## Secciones del sitio

### 1. Encabezado (`header.encabezado`)
Barra de navegación fija en la parte superior. Contiene el logo del estudio y el menú de navegación.

**Técnicas usadas:**
- `display: flex` con `justify-content: space-between` para separar logo y nav.
- Menú hamburguesa con **checkbox invisible + label visible** (cero JavaScript). Al marcar el checkbox, el selector `input:checked ~ nav` expande el menú con `max-height`.
- Borde inferior decorativo con `border-image` usando un gradiente dorado.

---

### 2. Hero / Inicio (`section.inicio`)
Sección principal con video de fondo, título, descripción, dos botones de acción y métricas flotantes.

**Técnica clave — Grid de una sola celda:**
Todos los elementos (video, degradado, patrón, contenido, métricas) están en `grid-column: 1 / grid-row: 1`. Esto los apila unos encima de otros **sin usar `position: absolute`**. El orden en el HTML determina cuál queda al frente (los últimos quedan por encima).

```
┌────────────────────────────────┐
│  video-fondo       (capa 1)   │
│  degradado negro   (capa 2)   │
│  patrón de puntos  (capa 3)   │
│  contenido texto   (capa 4)   │
│  métricas          (capa 5)   │
└────────────────────────────────┘
Todos en grid-column: 1 / grid-row: 1
```

**Pseudoelemento usado:** `.inicio__etiqueta::before` agrega una línea dorada horizontal antes del texto "Estudio Jurídico · Fundado en 2004".

---

### 3. Áreas de Práctica (`section.areas`)
Ocho tarjetas (Derecho Laboral, Comercial, Civil, Familia, Asesoría Empresarial, Representación Judicial, Consultoría Corporativa, Elaboración de Contratos).

**Técnicas usadas:**
- `display: grid; grid-template-columns: repeat(4, 1fr)` — 4 columnas iguales.
- El "borde" entre tarjetas se crea con `gap: 1px` y `background-color` en la cuadrícula (no es un borde real, es el fondo que se ve entre tarjetas).
- Hover con `translateY(-3px)` y `border-left-color` dorada para feedback visual.
- La flecha `→` aparece con `opacity: 0` y se revela en hover.

---

### 4. Equipo Legal (`section.equipo`)
Cuatro tarjetas de abogados con foto, nombre, cargo y especialidad.

**Técnica clave — Grid de una sola celda en la imagen:**
El contenedor de imagen usa un grid de una celda para superponer:
1. Texto de fondo `MjA` (vía `::before`)
2. La foto del abogado
3. Un velo dorado translúcido (en hover)
4. El badge de años de experiencia (esquina inferior derecha)

Todo sin `position: absolute`. El badge se ubica con `align-self: end; justify-self: end`.

**Flexbox:** Las cuatro tarjetas usan `display: flex; flex-wrap: wrap` para acomodarse en pantallas de distintos tamaños.

---

### 5. Hitos / Casos Destacados (`section.hitos`)
Cuatro tarjetas sobre casos de éxito del estudio (sin nombres reales, solo el logro).

**Técnicas usadas:**
- `display: grid; grid-template-columns: repeat(4, 1fr)` con separadores dorados (mismo truco de `gap: 1px` + fondo).
- `.tarjeta-hito__ornamento` es un `div` que actúa como línea decorativa: en hover, su `width` pasa de 32px a 60px con transición.

---

### 6. Nuestro Método (`section.metodo`)
Cuatro pasos del proceso jurídico: Consulta Inicial → Diagnóstico → Propuesta → Ejecución.

**Técnicas usadas:**
- `display: grid; grid-template-columns: repeat(4, 1fr)` — sin `gap`, los pasos se separan con `border-right`.
- En móvil (`max-width: 600px`), el `border-right` cambia a `border-bottom` y la grilla pasa a 1 columna.
- Los números grandes (01, 02...) tienen `opacity: 0.12` y se vuelven más visibles en hover.

---

### 7. Empresas Asesoradas (`section.clientes`)
Logos de clientes en tarjetas con efecto hover luminoso.

**Técnicas usadas:**
- `display: flex; flex-wrap: wrap; justify-content: center` — las tarjetas se acomodan automáticamente.
- Fondo con gradiente vertical que va de blanco a azul oscuro, creando transición visual entre la sección método y conferencias.
- Hover con `translateY(-8px) scale(1.05)` y sombra dorada.

---

### 8. Conferencias (`section.conferencias`)
Cuatro videos: uno principal con audio (ocupa 3 columnas) y tres secundarios en silencio y bucle.

**Técnicas usadas:**
- `display: grid; grid-template-columns: repeat(3, 1fr); grid-template-rows: auto auto`.
- `.video-item--principal` usa `grid-column: 1 / 4` para ocupar todo el ancho.
- Los videos secundarios usan `autoplay muted loop playsinline` — atributos HTML nativos, sin JS.
- El badge "Con Audio" usa un contenedor grid de una celda para superponerse sobre el video.

---

### 9. Contacto (`section.contacto`)
Dos columnas: información de contacto (izquierda) y formulario (derecha).

**Técnicas usadas:**
- `display: grid; grid-template-columns: 1fr 1.5fr` — la columna del formulario es 1.5 veces más ancha.
- El formulario interno usa `grid-template-columns: 1fr 1fr` con los campos "completo" usando `grid-column: 1 / -1` (ocupan todo el ancho).
- Inputs con `:focus` y `:focus-visible` para accesibilidad de teclado.
- El select usa `-webkit-appearance: none; appearance: none` para quitar el estilo nativo del navegador.

---

### 10. Pie de Página (`footer.pie`)

**Técnicas usadas:**
- `display: grid; grid-template-columns: 2fr 1fr 1fr 1.5fr` — cuatro columnas de distinto tamaño.
- `footer.pie::before` agrega la línea dorada decorativa en la parte superior del footer (pseudoelemento `::before`).
- Los nav internos del footer usan `display: flex; flex-direction: column` para apilar los enlaces.

---

## Obligaciones técnicas cumplidas

| Obligación | Dónde |
|---|---|
| CSS Grid | Áreas, Hitos, Método, Hero, Conferencias, Contacto, Pie |
| Flexbox | Encabezado, Equipo, Botones, Pie (nav) |
| `::before` o `::after` | `.inicio__etiqueta::before`, `.pie::before`, `.tarjeta-abogado__imagen-contenedor::before` |
| Pseudoclase de interacción | `:hover` en todas las tarjetas, `:focus` y `:focus-visible` en inputs |
| Pseudoclase estructural | `:last-child` en pasos y métricas |
| Variables CSS | Definidas en `:root`, usadas en todo el CSS |
| Responsividad | 5 breakpoints: 1200px, 900px, 600px, 400px, 300px |
| `prefers-reduced-motion` | Al final del CSS |
| Sin JS | Todo funciona con CSS puro |
| Sin frameworks | Solo CSS nativo |
| Sin `float` | No se usa en ningún lugar |
| Sin `position` (casi) | Solo `position: relative` implícito en transformaciones |

---

## Paleta de colores

| Variable | Valor | Uso |
|---|---|---|
| `--color-azul` | `#0B1F3A` | Fondo principal oscuro |
| `--color-azul-medio` | `#112847` | Fondos secundarios oscuros |
| `--color-dorado` | `#B08D57` | Acento principal, bordes, íconos |
| `--color-dorado-claro` | `#C9A96E` | Acento suave |
| `--color-dorado-oscuro` | `#8A6B3A` | Hover de botón principal |
| `--color-gris` | `#D9D9D9` | Bordes claros |
| `--color-gris-suave` | `#F2F2F2` | Fondos de secciones claras |
| `--color-blanco` | `#FFFFFF` | Texto sobre fondos oscuros |
| `--color-texto` | `#1a1a1a` | Texto principal |
| `--color-texto-suave` | `#555555` | Texto secundario |

---

## Tipografía

| Variable | Fuente | Uso |
|---|---|---|
| `--fuente-principal` | Cormorant Garamond | Cuerpo de texto, títulos |
| `--fuente-versalitas` | Cormorant SC | Etiquetas, botones, versalitas |

Ambas son fuentes serif clásicas de Google Fonts. Se importan en el `<head>` del HTML.

---

## Responsividad — Breakpoints

| Breakpoint | Cambios principales |
|---|---|
| `≤ 1200px` | Grillas pasan a 2 columnas, padding lateral se reduce |
| `≤ 900px` | Menú hamburguesa activo, métricas del hero ocultas |
| `≤ 600px` | Todo a 1 columna, tarjetas de abogados al centro |
| `≤ 400px` | Fuentes más pequeñas, logo más pequeño, botones a ancho completo |
| `≤ 300px` | Escala mínima para pantallas muy pequeñas |

---

*Proyecto desarrollado por Jhon Alexander Pimiento Bueno — ADSO · SENA Centro Agroturístico · 2025*
