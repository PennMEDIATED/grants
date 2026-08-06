# Penn MEDIATED — Grants

The Grants page for the [Center on Media, Technology and Democracy](https://infodem.upenn.edu). Static HTML/CSS, no build step. Mirrors the content at https://infodem.upenn.edu/grants/. Live at https://pennmediated.github.io/grants/

Same conventions as the [`about`](https://github.com/PennMEDIATED/about) and [`home`](https://github.com/PennMEDIATED/home) repos — shared spacing tokens, brand colors, fonts, and the newsletter/supporters block. This page intentionally has no top nav bar; the newsletter and supporters sections at the bottom (identical to `about`/`home`) are the only site-wide touchpoint.

- `index.html` — page markup
- `styles.css` — all styling (design tokens live at the top in `:root`)
- `assets/` — logos (school crests, funder logos, wordmark), shared with `about`/`home` where applicable

## Style guide (shared across `about`, `home`, and `grants`)

All three repos are static HTML/CSS built off the same design system. If you're adding or editing anything, pull values from here rather than guessing new ones — that's what keeps the sites looking like one brand instead of drifting apart.

### Design tokens (`:root` in `styles.css`)

**Spacing** — Atlassian's 8px scale. Always use the variable, never a raw pixel value:

```
--space-025: 2px   --space-100: 8px   --space-300: 24px  --space-600: 48px
--space-050: 4px   --space-150: 12px  --space-400: 32px  --space-800: 64px
--space-075: 6px   --space-200: 16px  --space-500: 40px  --space-1000: 80px
--space-250: 20px
```

**Color:**

| Token | Hex | Use |
|---|---|---|
| `--c-dark` | `#0d0d0c` | Primary text, dark backgrounds |
| `--c-accent` | `#5533ee` | Brand purple |
| `--c-red` | `#f03d1f` | Brand red/orange — links, tags, and this repo's numbering system |
| `--c-gray` | `#888680` | Secondary/muted text |
| `--c-gray-dark` | `#54534f` | ~8:1 contrast on white — `about`/`home`'s default for paragraph copy; this repo uses `--c-dark` for body copy instead (see below) |
| `--c-light-bg` | `#f8f7f4` | Placeholder/image background, neutral card backgrounds |
| `--c-pale-orange` | `#fce4dc` | `--c-red` tinted ~12% onto white — introduced in `grants` for callout boxes (status banner, Important Dates, Secondary Goals cards, eligible-schools grid). Backport to `about`/`home` if they add similar callouts. |
| `--c-white` | `#ffffff` | — |

**Brand gradient** — used on every purple-to-red surface (the about page's orbital section, all three repos' newsletter/supporters block, the home hero): `linear-gradient(150deg, #5533ee 0%, #df3611 81%)` via `--c-gradient`. Never write this gradient out by hand or approximate it with different stops — reference the variable so a future palette tweak only has to happen in one place per repo.

**Type:**
- `--f-serif`: `'EB Garamond', Georgia, 'Times New Roman', serif` — headlines, quotes, the "MEDIATED" wordmark
- `--f-sans`: `'DM Sans', system-ui, -apple-system, sans-serif` — everything else, including small meta labels (see below)
- `--f-mono`: `'Courier New', Courier, monospace` — declared for parity with `about`/`home`'s token set, but not actively used on this page. Small labels here (date labels, tags, spec headings) use `--f-sans` with letter-spacing instead, matching `about`'s quote-attribution treatment (e.g. "Amy Gutmann · Penn President Emerita...") rather than a monospace face.

**Layout:** `--max-w: 1440px` page cap, `--pad-x: var(--space-1000)` (80px) side padding on the shared `*__inner` containers, scaling down responsively to `--space-400` (32px) under 900px and `--space-250` (20px) under 480px — same breakpoints as `home`. Body-copy blocks have no `max-width` of their own; they fill the padded container at every viewport width rather than freezing at a fixed cap, so resizing the window always visibly reflows the text.

### Layout conventions

- Every section's content wrapper is named `.<section>__inner` and shares one rule (`width:100%; max-width:var(--max-w); margin-inline:auto; padding-inline:var(--pad-x);`). Add new sections to that shared selector list instead of writing a one-off inner container.
- Section-to-section vertical rhythm uses `--space-1000` (80px top and bottom) for genuine color/background transitions (white ↔ purple ↔ dark). Between subsections that share the same background (e.g. this page's RFP criteria → Secondary Goals → Guidelines flow), use the tighter, uniform **64px heading margin-top + 64px preceding content's margin-bottom = 128px** rhythm instead — full page-level padding on every internal heading reads as accidental, not deliberate.
- A heading immediately followed by body copy uses a flat `--space-300` (24px) gap, consistently, everywhere on the page.
- BEM-ish naming: `.block__element`, modifiers as `.block--variant` or `.block__element--variant` (e.g. `.school-block__logo--seas`, `.tag--closed`).

### Shared components

- **Newsletter CTA ("Subscribe Here")**: a white rectangle button. On hover, the label is knocked out via `background-clip:text` filled with `--c-gradient`, so the brand gradient appears to show through the letterforms — background stays solid white, only the text goes transparent. This exact effect lives in all three repos' `.newsletter__cta:hover .newsletter__cta-label` — if you touch one, touch the others.
- **Supporters row**: `.supporters__label` 24px/weight 700/uppercase, Knight Foundation logo at `height:65px`, Penn logo at `height:120px`, both `width:auto`. Logos use `assets/knight-foundation-logo.png` and `assets/upenn-logo-full.png` — same files, copied between repos; don't re-crop or re-export one without the other.
- **Numbering system**: every ordinal label (grant list `01`–`12`, criteria `01`–`03`, proposal requirements `01`–`05`) uses the same treatment — `--f-sans`, weight 800, `--c-red`, sized close to its adjacent text (18px next to 20px body copy, 15px next to card titles) and baseline-aligned (`align-items: baseline` on the flex row) rather than a fixed-position badge. Keep any new numbered list on this exact pattern.
- **Pale-orange callout boxes**: status banners, the Important Dates box, the Secondary Goals cards, and the eligible-schools grid all share `background: var(--c-pale-orange)`. One consistent tint for "supplementary info" boxes, distinct from `--c-light-bg`'s neutral gray (used for plain content backgrounds, not callouts).
- **Purple block + white cards**: sections that need to stand out (e.g. "All Center-Funded Grants") use `background: var(--c-accent)` with white `.card`-style boxes inside — same surface language as `about`'s `.related-centers`, just with boxed content instead of a plain list.
- **Logo/crest grids**: the eligible-schools grid (`.school-grid`) is a 4-column (2-col tablet, 1-col mobile) grid of bordered white tiles, each centering a school's official crest image. Logos are sized by `height` (not `width`), since lockup aspect ratios vary a lot school to school — check a new logo against its neighbors and add a `--modifier` height override if it reads noticeably smaller or larger at the shared height (see `.school-block__logo--seas`).
- **Responsive grids**: never let a multi-column grid just shrink its columns as the viewport narrows — text becomes unreadably vertical. Reflow to fewer columns at defined breakpoints instead (see `.school-grid`, `.grant-list__grid`, and `.secondary-goals__grid`'s media queries).

### Keeping the repos in sync

`about`, `home`, and `grants` are separate repos with duplicated CSS, not a shared stylesheet — so consistency is a discipline, not something enforced automatically. When you change a shared token or component in one repo, check whether the same change belongs in the others before considering the task done.
