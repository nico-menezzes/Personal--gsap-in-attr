<div align="center">

# GSAP in Attributes

**Declarative GSAP animations for Webflow — no code, just `data-` attributes.**

[![Version](https://img.shields.io/badge/version-1.2.0-7cf6b0?style=flat-square)](https://github.com/nico-menezzes/personal--gsap-in-attr/tags)
[![License: MIT](https://img.shields.io/badge/license-MIT-89b4ff?style=flat-square)](LICENSE)
[![GSAP](https://img.shields.io/badge/GSAP-3.13%2B-88CE02?style=flat-square)](https://gsap.com)
[![jsDelivr](https://img.shields.io/badge/CDN-jsDelivr-e84d3d?style=flat-square)](https://www.jsdelivr.com/package/gh/nico-menezzes/personal--gsap-in-attr)

[Live demo & playground](https://claude.ai/code/artifact/2a3ea2fa-5c38-40f5-abee-2cf5688671d7) · [Quick start](#quick-start) · [Attribute reference](#attribute-reference) · [Presets](#presets)

</div>

---

Paste **one script tag** into your site. Then animate any element by adding
`data-gsap` and a few optional `data-gsap-*` attributes directly in the
Webflow Designer — no custom code, no exported animations to maintain.

```html
<h1 data-gsap="text-up">My headline</h1>

<div data-gsap="fade-up"
     data-gsap-duration="1.2"
     data-gsap-ease="snappy"
     data-gsap-delay="0.2"></div>
```

## Why

| | |
|---|---|
| ⚡ **Zero JS for the end user** | Everything is driven by `data-*` attributes set in the Webflow Designer. |
| 📦 **Self-loading** | Auto-fetches GSAP + ScrollTrigger + SplitText + CustomEase from jsDelivr if they aren't already on the page. |
| ✂️ **Free split text** | Lines, words, or characters (GSAP 3.13+ SplitText, no license needed). |
| 🎚️ **Strong easing, built in** | Four hand-picked curves (`smooth`, `snappy`, `swift`, `soft`), or bring your own `cubic-bezier`. |
| 🪄 **No flash of unanimated content** | Elements stay hidden until the library is ready, then reveal in place. |
| ♿ **Accessible by default** | Respects `prefers-reduced-motion` — motion is skipped, content still appears. |
| 🧩 **Scales to real sites** | One DOM scan, a public API to re-run it after CMS loads, page transitions, or tab switches. |

---

## Quick start

**1. Host the library.** This repo already builds `dist/gsap-attributes.min.js`,
served live via jsDelivr — see the URL in step 2.

**2. Paste the script** in Webflow → **Project Settings → Custom Code → Footer Code**
(site-wide), or on a single page's Footer Code:

```html
<script src="https://cdn.jsdelivr.net/gh/nico-menezzes/personal--gsap-in-attr@1/dist/gsap-attributes.min.js"></script>
```

> `@1` always resolves to the latest `1.x.x` release. Pin an exact version with `@1.2.0` if you want full control over when you upgrade.

**3. Publish**, then select any element in the Designer → **Settings (D) → Custom
attributes** → add `data-gsap` with a preset name, e.g. `fade-up`. Publish again.
Done — if GSAP is already on the page, the library reuses it instead of loading
a second copy.

---

## Presets

| Category | Presets |
|---|---|
| **Fade / move** | `fade` · `fade-up` · `fade-down` · `fade-left` · `fade-right` · `slide-up` · `slide-down` · `slide-left` · `slide-right` |
| **Scale / rotate** | `scale-in` · `zoom-in` · `rotate-in` · `flip-up` · `flip-down` · `blur-in` · `skew-in` |
| **Reveal (clip-path)** | `reveal-up` · `reveal-down` · `reveal-left` · `reveal-right` |
| **Text (SplitText)** | `text-up` (masked lines) · `text-lines` · `text-words` · `text-chars` · `text-fade` · `text-flip` · `text-fill` (scroll-linked reading fill) |
| **Blank canvas** | `custom` (fades by default) · `none` (no default motion) — build an entrance entirely from the [customization attributes](#customize-the-motion) below |

---

## Attribute reference

Everything is optional except `data-gsap`. Every attribute is prefixed
`data-gsap-`, e.g. `data-gsap-duration`.

### Core

| Attribute | Values | Default | What it does |
|---|---|---|---|
| `data-gsap` | preset name (see [Presets](#presets)) | — | **Required.** Which animation to run. |
| `data-gsap-duration` | seconds | `0.8` | How long the animation runs. |
| `data-gsap-delay` | seconds | `0` | Wait before it starts. |
| `data-gsap-ease` | named curve · GSAP ease · `cubic(...)` | `smooth` | The easing curve. See [Easing](#easing). |

### Trigger (scroll vs. load)

| Attribute | Values | Default | What it does |
|---|---|---|---|
| `data-gsap-trigger` | `scroll` · `load` | `scroll` | Fire on scroll-into-view, or immediately on page load. |
| `data-gsap-start` | ScrollTrigger start | `top 85%` | When it fires on scroll — `[element edge] [viewport position]`. |
| `data-gsap-end` | ScrollTrigger end | — | End point (used with `scrub`, or a custom `toggle`). |
| `data-gsap-once` | `true` · `false` | `true` | Play once, or replay every time the element re-enters. |
| `data-gsap-scrub` | `true` · number | `false` | Tie progress directly to the scrollbar instead of playing once. |
| `data-gsap-trigger-element` | CSS selector | self | Animate this element, but fire when *another* one (e.g. the parent section) enters. |
| `data-gsap-scroller` | CSS selector | window | Use a custom scrollable container instead of the page. |
| `data-gsap-toggle` | ScrollTrigger `toggleActions` | auto | Full manual control, e.g. `play pause resume reverse`. |
| `data-gsap-markers` | `true` | `false` | Show ScrollTrigger's debug markers (start/end lines) while you tune things. **Remove before publishing.** |

### Customize the motion

Override any preset's starting values, or build a motion from scratch with
`data-gsap="custom"` / `data-gsap="none"`.

| Attribute | Values | What it does |
|---|---|---|
| `data-gsap-distance` | px | Travel distance used by the fade/slide presets. |
| `data-gsap-y` | px or `%` | Starting vertical offset. |
| `data-gsap-x` | px or `%` | Starting horizontal offset. |
| `data-gsap-opacity` | `0`–`1` | Starting opacity. |
| `data-gsap-scale` | number | Starting scale. |
| `data-gsap-rotate` | degrees | Starting rotation. |
| `data-gsap-blur` | px | Starting blur (animates to sharp). |
| `data-gsap-rotation` | degrees | Initial rotation for `rotate-in` / flip presets specifically. |

### Stagger (lists, grids, split text)

| Attribute | Values | Default | What it does |
|---|---|---|---|
| `data-gsap-stagger` | seconds | `0.06` | Gap between items when animating a group of children. |
| `data-gsap-stagger-from` | `start` · `center` · `end` · `edges` · `random` | `start` | Where the stagger cascade begins. |
| `data-gsap-target` | CSS selector | direct children | Which descendants to stagger (see [Staggering](#staggering-lists--grids)). |
| `data-gsap-split` | `lines` · `words` · `chars` | preset default | Override how a `text-*` preset splits its content. |

---

## Easing

Four strong, intentional curves ship built in. Reference them by name:

| Name | Feel | Curve |
|---|---|---|
| `smooth` *(default)* | Strong ease-out — great for entrances | `cubic-bezier(0.23, 1, 0.32, 1)` |
| `snappy` | iOS drawer feel, crisp settle | `cubic-bezier(0.32, 0.72, 0, 1)` |
| `swift` | Strong ease-in-out, for things moving across the screen | `cubic-bezier(0.77, 0, 0.175, 1)` |
| `soft` | Gentle, understated ease-out | `cubic-bezier(0.25, 1, 0.5, 1)` |

```html
<div data-gsap="fade-up" data-gsap-ease="snappy"></div>
```

Or pass your own cubic-bezier — it's registered as a GSAP `CustomEase` automatically:

```html
<div data-gsap="fade-up" data-gsap-ease="cubic(0.16, 1, 0.3, 1)"></div>
```

Or use any named GSAP ease directly: `power1` … `power4`, `back.out(1.7)`,
`elastic.out(1, 0.4)`, `expo.out`, `circ.out`, `sine.inOut`, etc.

---

## Scroll fill — `text-fill`

Text starts dim and brightens progressively as the reader scrolls, tied to
the scrollbar — the "reading highlight" effect. Choose the unit with
`data-gsap-split` and the starting dimness with `data-gsap-opacity`:

```html
<p data-gsap="text-fill"
   data-gsap-split="words"      <!-- words | chars | lines -->
   data-gsap-opacity="0.15"     <!-- how dim it starts -->
   data-gsap-start="top 75%"
   data-gsap-end="bottom 55%">Your paragraph…</p>
```

It's **scrubbed by default** (progress follows the scrollbar, not a timer), so
`data-gsap-duration` and `data-gsap-ease` behave a little differently here:

- **Speed of the fill** → controlled by `data-gsap-start` / `data-gsap-end`, not `duration`. A wider range fills more slowly.
- **Sharpness of the read boundary** → `data-gsap-duration` + `data-gsap-stagger` control overlap between words:
  - Crisp, one-at-a-time: `duration="0.2"` `stagger="0.15"`
  - Soft gradient, several brightening together: `duration="0.8"` `stagger="0.05"`
- **`data-gsap-ease`** maps against scroll position — leave it on the default (`none`, linear) for natural reading; anything else makes the fill accelerate/decelerate as you scroll.

Prefer it to run once, on a timer, instead of tied to scroll? Set
`data-gsap-scrub="false"` — `duration` and `ease` then behave exactly like
every other preset (seconds, real easing curve).

---

## Staggering lists & grids

Put the attribute on the **container**, add `data-gsap-stagger` — its
children animate in sequence:

```html
<div class="cards" data-gsap="fade-up" data-gsap-stagger="0.08">
  <div class="card">...</div>
  <div class="card">...</div>
  <div class="card">...</div>
</div>
```

Only want specific descendants (not every direct child)?
Use `data-gsap-target=".card"`.

Want a real section entrance — animate a grid, but fire when its parent
*section* scrolls in, not the grid itself?

```html
<section class="hero">
  <div class="cards"
       data-gsap="fade-up"
       data-gsap-stagger="0.1"
       data-gsap-target=".card"
       data-gsap-trigger-element=".hero"
       data-gsap-start="top 75%"></div>
</section>
```

---

## Global config

Set project-wide defaults before the library script loads:

```html
<script>
  window.GSAPAttr = {
    defaults: { ease: 'snappy', duration: 0.9, start: 'top 80%' },
    gsapVersion: '3.13.0',
    autoload: true,          // fetch GSAP from jsDelivr if missing
    hideUntilReady: true,    // prevent flash of unanimated content
    respectReducedMotion: true
  };
</script>
<script src="https://cdn.jsdelivr.net/gh/nico-menezzes/personal--gsap-in-attr@1/dist/gsap-attributes.min.js"></script>
```

## Public API

```js
GSAPAttr.refresh(root)         // re-scan the DOM (after CMS load, Barba transition, tab switch)
GSAPAttr.register(name, fn)    // register a custom preset at runtime
GSAPAttr.init()                // re-initialize everything
GSAPAttr.eases                 // the built-in named curves (smooth/snappy/swift/soft)
```

Register your own preset:

```js
GSAPAttr.register('drop-in', function (o) {
  return { opacity: 0, y: -o.distance, scale: 1.1 };
});
```

```html
<div data-gsap="drop-in"></div>
```

---

## Project structure

```
GSAP in Attributes/
├── src/gsap-attributes.js        ← source (read this to understand the internals)
├── dist/gsap-attributes.js       ← readable build (same content, pre-build step)
├── dist/gsap-attributes.min.js   ← minified build — this is what jsDelivr serves
├── demo/index.html               ← docs, playground, and live simulators
├── demo/standalone.html          ← single-file version of the demo (no server needed)
├── build-standalone.js           ← regenerates demo/standalone.html from demo/ + src/
└── README.md
```

Open `demo/index.html` (or `demo/standalone.html` directly) in a browser to
try every preset live, including a load-intro simulator and a scoped
scroll-trigger simulator.

---

## Changelog

### v1.2.0
- **`text-fill`** — scroll-linked "reading" fill (dim → bright), split by words/letters/lines, adjustable starting opacity.

### v1.1.0
- `data-gsap-trigger="scroll|load"` clearly separates the two entrance kinds.
- Per-property overrides: `-y` `-x` `-opacity` `-scale` `-rotate` `-blur` — fine-tune any preset, or build one from scratch with `data-gsap="custom"` / `"none"`.
- `-trigger-element` fires when a parent section enters; `-toggle` for full `toggleActions` control; `-stagger-from` for cascade origin; `-scroller` for custom scroll containers.

### v1.0.0
- Initial release: fade/slide/scale/rotate/reveal presets, SplitText-based text presets, named easing curves, FOUC guard, reduced-motion support.

---

## Roadmap

- [ ] Attribute-chained timelines (`data-gsap-timeline`) to sequence multiple elements as one animation.
- [ ] Dedicated parallax helpers.
- [ ] Hover / click triggers (beyond scroll and load).
- [ ] Exit presets for page transitions.

---

## License

[MIT](LICENSE) · built by [Nico Menezes](https://github.com/nico-menezzes)
