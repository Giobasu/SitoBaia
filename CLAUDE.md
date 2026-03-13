# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static single-page website for **La Baia di Popeye**, an Italian lakeside resort/restaurant at Lago di Castreccioni (Marche, Italy). The site was originally generated from WordPress (WPBakery Page Builder) and exported as standalone static HTML.

## Development

No build system. Edit files directly and preview by opening `index.html` in a browser. There are no dependencies to install, no tests, and no build steps.

To serve locally:
```bash
python3 -m http.server 8080
```

## Architecture

The entire site is a **single HTML page** (`index.html`, ~1950 lines). All content, inline `<style>` blocks, and inline `<script>` blocks live in that one file.

### File Layout

- `index.html` — the entire site; contains all page HTML, many `<style>` blocks, and two inline `<script>` blocks at the bottom
- `css/cssbaia.css` — main stylesheet (Font Awesome Pro 5.1.0 + all custom/theme CSS)
- `js/jsbaia.js` — main JS bundle (~1172 lines): jQuery Migrate, Slider Revolution, FlexSlider, and custom scroll/interaction logic
- `js/jquery.min.js`, `js/hooks.min.js`, `js/i18n.min.js`, `js/lazysizes.min.js` — third-party libraries
- `fonts/` — all Google Fonts and icon fonts served locally (Lobster Two, Oswald, Raleway, Roboto, Satisfy, Futura variants, Flaticon, Font Awesome)
- `images/` — photos (with responsive variants: `-768x`, `-1023x`, `-1536x`), SVG icons, logos, favicon
- `files/Menu-Baia-di-Popeye.pdf` — downloadable restaurant menu

### Bilingual (IT/EN)

Language switching is implemented entirely in the inline `<script>` at the bottom of `index.html`:

- `currentLang` variable (starts as `'it'`)
- `translations` object with keys `'it'` and `'en'`
- HTML elements carry `data-i18n="key"` attributes; `toggleLanguage()` swaps their `textContent` on click
- The `<html>` element's `lang` attribute is updated accordingly

### Service Modals

The `serviceModalData` object (inline script, bottom of `index.html`) holds content for the detail modals:
- Keys: `calice`, `spiaggia`, `natanti`, `cane`, `museo`, `territorio`, `servizi`
- Each entry has `images[]`, `title: {it, en}`, and `text: {it, en}`
- `openServiceModal(serviceId)` / `closeServiceModal(event, force)` control visibility

### CSS Conventions

- CSS class names follow WPBakery/Red theme patterns: `.red-*`, `.vc_*`, `.wpb_*`
- Page-specific overrides are written as additional `<style>` blocks inside `index.html`, not in `cssbaia.css`
- Primary brand color: `#156f73` (teal)
- Mobile breakpoint: `680px`

### Images

Responsive images follow the naming convention: `imagename.jpg`, `imagename-768x<h>.jpg`, `imagename-1023x<h>.jpg`, `imagename-1536x<h>.jpg`. Custom SVG icons live directly in `images/`.
