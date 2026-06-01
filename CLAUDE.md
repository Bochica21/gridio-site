# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

This is the marketing website for **gridio**, a Brazilian digital product agency. It is a single self-contained file: `index.html` at the repo root. There is no build system, no package manager, no framework — everything (HTML structure, CSS, JavaScript) lives inline in that one file.

## Running the site

Open `index.html` directly in a browser. No server or build step is required. For a local dev server you can use any static file server, e.g.:

```
npx serve .
# or
python -m http.server
```

## Architecture

Everything is in `index.html`:

- **CSS** (`<style>` block, lines ~16–1729): all styling inline. Uses CSS custom properties (`--bg`, `--blue`, `--display`, etc.) defined in `:root`. No external stylesheet.
- **HTML** (lines ~1731–2456): semantic sections — `nav`, `hero`, `problem-section`, `tiers-section`, `process-section`, `#cases`, `#showcase`, `#faq-section`, `#contato`, `footer`.
- **JavaScript** (`<script>` block, lines ~2457–2858): vanilla JS, no libraries. Key subsystems:
  - **Scroll square** (`#scroll-square`): a blue square that travels along the grid following section titles via `requestAnimationFrame` + lerp. Snaps to the "Gridio" accent text in the CTA section and triggers a CSS flash animation on collision.
  - **Reveal on scroll**: `IntersectionObserver` adds `.in-view` to `.reveal` elements.
  - **Contact form**: client-side validation → opens native email client via `mailto:` with pre-filled subject and body. No backend — form data never hits a server.
  - **Copy to clipboard**: `navigator.clipboard` with `execCommand` fallback.

## Image assets

Images are referenced in the HTML as `./assets/cases/puma/puma-*.jpg` (relative to the repo root, where `index.html` lives), so they live at `assets/cases/puma/`.

## Design system

All colors and fonts are CSS custom properties in `:root`. Fonts are loaded from Google Fonts (Bricolage Grotesque for display, Geist for body, Geist Mono for code/labels). The grid background is a `fixed` `div.global-grid` using `background-image` with two perpendicular linear gradients at 56px intervals.

## Language

All copy is Brazilian Portuguese. Keep all user-facing text in pt-BR.

## Contact

Form submissions go to `sougridio@gmail.com` via `mailto:`. To change the recipient, search for `sougridio@gmail.com` (appears 4 times).
