# Penn MEDIATED — Grants

The Grants page for the [Center on Media, Technology and Democracy](https://infodem.upenn.edu). Static HTML/CSS, no build step. Mirrors the content at https://infodem.upenn.edu/grants/.

Same conventions as the [`about`](https://github.com/PennMEDIATED/about) and [`home`](https://github.com/PennMEDIATED/home) repos — shared spacing tokens, brand colors, fonts, and footer. This page intentionally has no top nav bar; the footer (copied from `about`) is the only site-wide navigation.

- `index.html` — page markup
- `styles.css` — all styling (design tokens live at the top in `:root`)
- `assets/` — logos, shared with `about`/`home`

See the [`about` repo's README](https://github.com/PennMEDIATED/about#style-guide-shared-across-about-and-home) for the full shared style guide (spacing scale, color tokens, type, layout conventions). Pull values from there rather than guessing new ones.
