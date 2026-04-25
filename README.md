# ATLAS — Reportajes long-form

> Plantillas editoriales de larga forma para periodismo económico premium.
> Construidas sobre el design system **SYX**.
> Pensadas y dirigidas por **ATLAS**, el modelo mental editorial.

---

## Qué es esto

Dos plantillas hermanas para reportajes de larga forma sobre figuras y temas del mundo económico. Cada una cubre un registro distinto del periodismo financiero premium:

- **ATELIER** — *Retratos del poder*. Long-form cinematográfico para perfiles humanos (banqueros, magnates, herederos). Identidad ink/bone/brass + Cormorant Garamond.
- **OBSIDIANA** — *Dossier económico*. Long-form forense para investigación (redes de poder, infraestructuras invisibles, datos densos). Identidad obsidian/bone/carmín + Instrument Serif.

Las dos son archivos HTML auto-contenidos: vídeo + imagen + GSAP + Lenis, con `prefers-reduced-motion` cubierto en cada efecto. No requieren build. Se abren en el navegador y se publican como están.

---

## Arquitectura — ATLAS sobre SYX

| Sistema | Rol | Ámbito |
|---|---|---|
| **ATLAS** | **Modelo mental editorial** | Decide qué se cuenta, qué tono tiene, qué identidad exige cada pieza. Define las dos plantillas y sus diferencias narrativas. |
| **SYX** | **Ejecutor técnico** | Provee el sistema de tokens (4 tiers OKLCH), la accesibilidad WCAG, los contratos R01–R08 y la arquitectura de mixins. Garantiza coherencia y rendimiento. |

> *ATLAS sin SYX son intenciones. SYX sin ATLAS son herramientas. Juntos producen las plantillas de este repositorio.*

ATLAS gobierna las decisiones editoriales (paleta brass vs carmín, tipografía Cormorant vs Instrument, ritmo cinematográfico vs forense). SYX gobierna la implementación (tokens semánticos verificados a 4.5:1 mínimo, mixins de transición, BEM estricto, fallbacks de motion).

---

## Las dos plantillas

### 🟤 ATELIER — *Retratos del poder*

Cada capítulo entra como un *cut* de película:

1. Una línea SVG se dibuja a lo ancho de la página (`stroke-dashoffset 1 → 0`).
2. El número del capítulo aterriza desde abajo.
3. El eyebrow lo sigue.
4. El h2 se compone palabra a palabra con un blur que se desvanece (`filter: blur(8px) → 0`).
5. El primer párrafo se levanta del suelo.

Una sola timeline GSAP, 1,8 segundos. Como un crédito de apertura.

**Identidad visual:**
- Paleta: `ink-950` / `bone-50` / `brass-400` (≤ 4 colores · R-COL-01)
- Tipografía: Cormorant Garamond (display) + Inter (body) + DM Mono (data)
- Cursor: brass dot 10px → 72px en hover, `mix-blend-mode: difference`
- Patrones aplicados: character-cascade, pinned horizontal timeline, mask-reveal stagger, magnetic CTA, scramble counter (alfabeto 0-9), pull-quote scroll-coupled rotation, monogram ring draw-in.

**Pieza de demostración:** *"James R. Dimon — el último monarca de Wall Street"*.

---

### ⚫ OBSIDIANA — *Dossier económico*

La estructura es de **expediente forense**. Las imágenes detrás de cada capítulo no aparecen — se *abren* con `clip-path` mientras te acercas con el scroll. Los gráficos animan al ritmo del scroll, no al ritmo del clic. Los datos en pantalla pasan por caracteres aleatorios antes de fijarse — como un terminal de Bloomberg.

**Identidad visual:**
- Paleta: `obsidian-1000` / `bone-50` / `carmine-500` (≤ 4 colores · R-COL-01)
- Tipografía: Instrument Serif (display) + Inter (body) + JetBrains Mono (data)
- Cursor: carmine reticle (crosshair + ring) con etiqueta "enfocar"
- Patrones aplicados: clip-reveal scrubbed, scrub chart con anotaciones flotantes en milestones, network spotlight + scramble on hover, draw-svg-path en chart y red, bibliography stagger draw underlines, coda combinada scramble → typewriter.

**Pieza de demostración:** *"BlackRock — la columna invisible del capital"*.

---

## Lineage de versiones

Las dos plantillas tienen cuatro versiones cada una. Cada salto resuelve un problema concreto:

| Versión | Archivos | Cambio respecto a la anterior |
|---|---|---|
| **v1** | `reportaje-atelier.html` · `reportaje-obsidiana.html` | Estructura mínima sin assets externos. Sirve como referencia cuando se quiere algo rápido o no hay vídeo/imagen disponibles. |
| **v2** | `*-v2.html` | + Imágenes Unsplash, vídeo HTML5, Lenis smooth scroll, cursor follower, magnetic CTA, scramble text, typewriter, clip-reveal (`once: true`), galería editorial asimétrica. |
| **v3** | `*-v3.html` | + Sistema `mol-bg-media`: imágenes a 2.880 px con cascada AVIF/WebP/JPEG, vídeos Pexels con multi-source y **fallback automático JS al poster** si el CDN del vídeo falla en producción. Filtros suaves para nitidez. |
| **v4** | `*-v4.html` | + Orquestación con timelines GSAP. El motion deja de ser eventos sueltos y pasa a ser secuencia coreografiada. Cada capítulo es un *cut* de película. |

**¿Qué versión usar?**

- **v1** si necesitas algo minimal, ligero, o sin dependencias externas de imagen/vídeo.
- **v2** si necesitas la versión rica pero no te preocupa la nitidez perfecta.
- **v3** para producción cuando los activos visuales son críticos (es la más robusta).
- **v4** para piezas que requieren *estado del arte* en storytelling editorial.

---

## El dominio motion del knowledge

La razón por la que v4 funciona como secuencia narrativa y no como acumulación de efectos es un dominio nuevo en el sistema de conocimiento del proyecto:

```
mind-system/knowledges/motion/
├── index.md                                  → entrada del dominio
├── 00-indice/mapa-del-sistema.md
├── 01-fundamentos/
│   ├── modelo-mental.md                      → las cuatro capas: qué cambia, cuándo, qué activa, función narrativa
│   └── vocabulario-base.md                   → tween, timeline, stagger, ease, ScrollTrigger
├── 02-capacidades/index.md                   → catálogo: tween, timeline, stagger, easing, ScrollTrigger, Lenis, plugins
├── 03-patrones/                              → 10 patrones reusables con nombre operativo
│   ├── character-cascade.md
│   ├── parallax.md                           ← incluye Ken Burns
│   ├── pinned-scrub.md
│   ├── horizontal-scroll.md
│   ├── mask-reveal.md
│   ├── magnetic-button.md
│   ├── cursor-follower.md
│   ├── scramble-text.md
│   ├── typewriter.md
│   └── draw-svg-path.md
├── 04-glosario/index.md                      → vocabulario corto para prompts
└── 05-plantillas/plantilla-patron.md         → schema para nuevos patrones
```

Cada patrón documenta: **intención narrativa · definición · sinónimos · control GSAP · parámetros sensibles · casos de uso · prompt accionable · fallback `prefers-reduced-motion`**.

El dominio se carga automáticamente por los modos `[SYX: CREATIVE]:` (siempre) y `[SYX: UI]:`/`[SYX: SKETCH]:` (on-demand). Ver [mind-system/knowledges/index.md](mind-system/knowledges/index.md).

---

## Stack técnico

| Capa | Tecnología | Origen |
|---|---|---|
| Tokens | OKLCH 4 tiers (primitive → semantic → component) | SYX |
| CSS architecture | `@layer` (sin `!important`), BEM, mixins | SYX |
| Motion | GSAP 3.12.5 + ScrollTrigger | CDN jsDelivr |
| Smooth scroll | Lenis 1.1.18 | CDN jsDelivr |
| Imágenes | Unsplash CDN — `<picture>` con AVIF/WebP/JPEG cascade · `w=2880&q=85` para hero/spread · `w=1600&q=85` para galería | Unsplash |
| Vídeos | Pexels CDN — multi-source MP4 con fallback automático al poster | Pexels |
| Tipografía | Google Fonts (Cormorant Garamond, Instrument Serif, Inter, DM Mono, JetBrains Mono) | Google Fonts |

Sin build. Sin npm install. Cada archivo HTML se abre directamente en el navegador.

---

## Cómo abrir las plantillas

```bash
# Desde el navegador
file:///C:/GITHUBS/syx--atlas/reportaje-atelier-v4.html
file:///C:/GITHUBS/syx--atlas/reportaje-obsidiana-v4.html

# O servir la carpeta con cualquier servidor estático
npx serve .
# → http://localhost:3000/reportaje-atelier-v4.html
```

---

## Cómo crear un reportaje nuevo

Para una nueva pieza editorial, el workflow recomendado es:

1. **Decidir registro con ATLAS.** ¿Es un retrato (ATELIER) o un dossier (OBSIDIANA)? Esto determina paleta, tipografía, ritmo y patrones de motion.
2. **Copiar la plantilla v3 o v4** correspondiente y renombrar (`reportaje-{tema}.html`).
3. **Sustituir el contenido editorial:** título, deck, byline, capítulos, citas, datos del scrub chart, network nodes, bibliografía.
4. **Sustituir los assets:** posters Unsplash y vídeos Pexels — mantener los formatos `w=2880&q=85` para hero/spread.
5. **Si añades un efecto nuevo:** documentarlo como un patrón más en `mind-system/knowledges/motion/03-patrones/` siguiendo el schema de `05-plantillas/plantilla-patron.md`.
6. **Verificar contrastes** WCAG 4.5:1 contra los nuevos fondos (los filtros suaves no comprometen el ratio, pero la palabra clave es *verificar*).

Para una **identidad nueva** (otra cabecera distinta a ATELIER/OBSIDIANA), trabajar primero a nivel de tokens en `scss/themes/` siguiendo los modos `[SYX: TOKEN]:` y `[SYX: THEME]:`. Las plantillas de este repositorio son consumidoras del theme — no lo definen.

---

## Accesibilidad y rendimiento

Todas las versiones cumplen:

- **Contrastes WCAG 2.1 AA** verificados en cada par texto/fondo (mayoría AAA, documentado en comentarios SCSS).
- **`prefers-reduced-motion: reduce`** desactiva: Lenis, parallax, character cascade, scramble, typewriter, clip-reveal scrub, mask-reveal stagger, magnetic, cursor follower, animaciones de pulse. Cada efecto tiene su fallback al estado final.
- **Touch devices** ocultan automáticamente el cursor follower (`@media (hover: none)`).
- **Focus visible** con `outline: 2px` + `offset: 4px` en color de marca.
- **Semantic HTML**: `<article>`, `<section aria-labelledby>`, `<blockquote><cite>`, `<dl>`, `<ol>`. SVG con `<title>` + `role="img"` + `aria-label`.

**Rendimiento:**
- Vídeos con `preload="auto"` solo en hero; resto con `preload="metadata"`.
- Detección de fallo de carga con timeout 6s — si Pexels no responde, se libera ancho de banda y queda el poster.
- Imágenes con `decoding="async"` + `loading="lazy"` (excepto el LCP de cada plantilla, con `fetchpriority="high"`).
- `image-rendering: -webkit-optimize-contrast` en posters críticos.
- Sin JS bloqueante: GSAP/Lenis cargados con `defer`.

---

## Mapa de archivos

```
syx--atlas/
├── REPORTAJES.md                              ← este documento
├── README.md                                  ← entrada del design system SYX
│
├── reportaje-atelier.html                     ← v1 ATELIER
├── reportaje-atelier-v2.html                  ← v2 (Unsplash + GSAP avanzado)
├── reportaje-atelier-v3.html                  ← v3 (assets nítidos + vídeo robusto)
├── reportaje-atelier-v4.html                  ← v4 (orquestación storytelling)
│
├── reportaje-obsidiana.html                   ← v1 OBSIDIANA
├── reportaje-obsidiana-v2.html
├── reportaje-obsidiana-v3.html
├── reportaje-obsidiana-v4.html
│
├── articulo-vitrina.html                      ← VITRINA — moda con espíritu económico (artículo standard, no long-form)
├── portada-economista.html                    ← portadas hermanas (no parte de este sistema)
├── portada-economia.html
│
└── mind-system/
    └── knowledges/
        ├── index.md                            ← mapa de dominios
        ├── branding/                           ← reglas de percepción de prestigio
        ├── motion/                             ← dominio GSAP (creado para v4)
        ├── ui/                                 ← motion-principles, color, typography
        ├── ux/                                 ← leyes cognitivas
        ├── front/                              ← arquitectura, a11y
        ├── syx/                                ← tokens, mixins, componentes
        └── vendors/                            ← referentes externos
```

---

## Decisiones notables

Tres decisiones que vale la pena documentar para futuras piezas:

1. **Vídeos con poster Unsplash garantizado.** Cuando un CDN de vídeo falla (Pexels caduca un ID, hay throttling, el cliente está offline), la pieza se ve igualmente nítida porque el `<img>` poster a 2.880 px ya está cargado. El `<video>` con fade-in solo aparece **si confirma carga**. El usuario nunca ve un cuadro negro.
2. **Scramble text con alfabeto contextual.** En OBSIDIANA usa `0-9A-F` (estética de terminal financiero). En ATELIER usa `0-9` (números puros, premium pero no forensic). El alfabeto del scramble es decisión de identidad, no técnica.
3. **Clip-reveal scrubbed en lugar de `once: true`.** En v4 los chapter takeovers de OBSIDIANA atan la apertura del `clip-path` al `progress` del scroll. Te acercas y la escena *se abre* gradualmente. Salir y volver re-cierra/re-abre. Más cinematográfico y mucho más fiel al lenguaje del documental.

---

## Estado y créditos

- **Estado:** v4 es la versión actual recomendada para producción premium. v3 sigue válida cuando se busca registro más contenido. v1/v2 son históricos.
- **Tipografías:** Cormorant Garamond (Catharsis Fonts), Instrument Serif (Instrument Foundry), Inter (Rasmus Andersson), DM Mono / DM Sans (Colophon Foundry), JetBrains Mono (JetBrains).
- **Imágenes:** Unsplash, libres bajo Unsplash License.
- **Vídeos:** Pexels Videos, libres bajo Pexels License.
- **Iconografía:** SVG inline propios.
- **Autoría editorial:** ATLAS / José Luis Pizarro Feo.
- **Sistema técnico:** [SYX](README.md) — design system propio.

---

## Lecturas relacionadas

- [README.md](README.md) — Entrada del design system SYX
- [mind-system/knowledges/motion/index.md](mind-system/knowledges/motion/index.md) — Dominio GSAP completo
- [mind-system/knowledges/branding/perception-of-prestige.rules.md](mind-system/knowledges/branding/perception-of-prestige.rules.md) — Reglas R-TYP / R-SPC / R-COL / R-SYS / R-AUT / R-DET / R-ESC aplicadas a las plantillas
- [mind-system/agents/index.md](mind-system/agents/index.md) — Sistema de modos (`[SYX: CREATIVE]:`, `[SYX: UI]:`, etc.) que carga el dominio motion
