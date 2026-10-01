# Seafoam

A standalone [Marp](https://marp.app/) / Marpit theme (`seafoam.css`, 1280x720):
a light, low-contrast variant of the classic Dracula palette, dressed with soft
wave motifs for title slides and section dividers. It ships with a
ready-to-render sample deck in [`sample/`](sample/).

**Seafoam** takes its color system and typography from the
[Dracula Marp theme](https://github.com/dracula/marp), and its wave
backgrounds, rounded code blocks, and two-column layout from the
[Wave Marp theme](https://github.com/JuliusWiedemann/MarpThemeWave) — then
remaps everything to a light scheme and layers on structural slide classes
(`lead`, `section`, `title`, `closing`), layout utilities, and figure helpers.

![Seafoam title slide](screenshots/slide-01.png)

---

## What it borrows, and from where

**Seafoam** is a deliberate mashup of two established Marp themes.

- **Palette and typography** come from the
  [Dracula Marp theme](https://github.com/dracula/marp): the full Dracula
  color set as CSS variables, the Highlight.js token colors, the
  header/footer/pagination boxes, table styling, and the `h1`–`h6` color
  hierarchy — all re-tinted for a light background.
- **Waves and code/columns** come from the
  [Wave Marp theme](https://github.com/JuliusWiedemann/MarpThemeWave): the
  wave footer band, rounded code blocks, and two-column layout (its
  `.columns` becomes `grid`/`cols-*` here).

The light palette is the theme's own contribution — each Dracula hue is
desaturated and darkened for readability on a `#f8fafc` background while
keeping its semantic role (see [Palette](#palette)). The wave SVGs are
inlined `data:` URIs rather than remote images, so the theme is
self-contained and works offline.

---

## Requirements

- [Marp CLI](https://github.com/marp-team/marp-cli) (v4+, includes Marpit)
  or the Marp for VS Code extension.
- `html: true` in front matter — the layout components use raw HTML.

## Install / use

Drop `seafoam.css` anywhere and point Marp at it. In a deck's front matter set
the theme and enable HTML:

```yaml
---
marp: true
theme: seafoam
html: true
paginate: true
---
```

Render from the command line, passing the stylesheet explicitly:

```bash
marp deck.md --theme path/to/seafoam.css --output deck.html
```

Marp resolves `theme: seafoam` by the `@theme` name in the CSS; the `--theme`
flag points at the file itself. HTML must be enabled when using the layout
components below.

## Syntax highlighting

Fenced code blocks use Marp's built-in Highlight.js parser and the theme's
token colors. Add a language after the opening fence:

````markdown
```python
def greet(name):
    return f"Hello, {name}"
```
````

Common language identifiers include `python`, `javascript`, `typescript`,
`bash`, `json`, `yaml`, and `cpp`. Blocks without a language remain
unhighlighted.

## Slide classes

Use Marp's local class directive before a slide:

```markdown
<!-- _class: lead -->
```

| Class | Purpose |
|---|---|
| `lead` | Title slide with wave footer and gradient heading |
| `section` | Centered section-divider slide with wave background |
| `invert` | Dark-background variant (flips light/dark emphasis) |
| `title` | Title slide with large top logo |
| `closing` | Closing slide with contact grid |
| `compact` | Smaller type for dense content |
| `sources` | Smaller type for references |

`lead`, `section`, `title`, and `closing` are the main structural variants.
`compact` and `sources` are text-density tweaks.

## Headers and footers

Marp renders header/footer text and the page counter through Marpit's own
`section::after`; this theme only styles their boxes. Use normal Marp
directives:

```markdown
<!--
header: Section title
footer: Deck footer
-->
```

The footer and page counter sit on a solid wave backdrop. You can place
institution logos in the header with an HTML layout:

```html
<header>
  <div class="institution-logos">
    <img class="institution-logo unito-logo" src="assets/unito.png">
    <img class="institution-logo" src="assets/partner.png">
  </div>
</header>
```

`institution-logo` keeps the logo at a fixed height; `unito-logo` gives a
slightly taller variant. On `lead` slides the logo block moves to the bottom
of the slide; on `title` slides it sits larger at the top; on `closing` slides
it stays at the top.

## Grid and cards

`cols-2` and `cols-3` create equal-width columns. `cols-4` creates a 2x2 grid.

```html
<div class="grid cols-3">
  <div class="card"><h3>First</h3><p>Short description.</p></div>
  <div class="card"><h3>Second</h3><p>Short description.</p></div>
  <div class="card"><h3>Third</h3><p>Short description.</p></div>
</div>
```

Use `metric` for a large value inside a card:

```html
<div class="card">
  <div class="metric">120M</div>
  <p>parameters</p>
</div>
```

## Figures

Use `paper-figure` inside a fixed-height `figure-box` to keep plots within the
slide while preserving their aspect ratio. Add `short` or `tall` to select a
245px or 400px container; the default is 360px.

```html
<div class="figure-box tall">
  <img class="paper-figure" src="assets/results.png">
</div>
```

Use `visual-split` for a large figure beside explanatory text. The first child
is the figure panel and the second is the text panel. Add `narrow-image` when
the figure should stay at a fixed 550px column.

```html
<div class="visual-split">
  <div><img class="paper-figure" src="assets/results.png"></div>
  <div>
    <h3>Main result</h3>
    <p>Short explanation of the figure.</p>
  </div>
</div>
```

The optional spacing classes `tight-grid`, `tight-flow`, and `tight-callout`
reduce vertical gaps on dense slides. These utilities and all figure layouts
are opt-in, so they do not alter existing slides unless explicitly used.

## Timeline

The timeline supports five equally spaced stages. Add `timeline-4` for four
stages:

```html
<div class="timeline">
  <div class="timeline-item"><div class="timeline-marker">1</div><h3>Collect</h3><p>Input data</p></div>
  <div class="timeline-item"><div class="timeline-marker">2</div><h3>Process</h3><p>Prepare data</p></div>
  <div class="timeline-item"><div class="timeline-marker">3</div><h3>Analyze</h3><p>Find structure</p></div>
  <div class="timeline-item"><div class="timeline-marker">4</div><h3>Validate</h3><p>Measure errors</p></div>
  <div class="timeline-item"><div class="timeline-marker">5</div><h3>Present</h3><p>Show results</p></div>
</div>
```

```html
<div class="timeline timeline-4">
  <!-- Four timeline-item elements -->
</div>
```

## Flow and callouts

Use `flow`, `step`, and `arrow` for short sequential processes:

```html
<div class="flow">
  <div class="step"><strong>Input</strong></div>
  <div class="arrow">→</div>
  <div class="step"><strong>Output</strong></div>
</div>
```

Use `callout` for a conclusion and add `warning` for cautionary text:

```html
<div class="callout">Main conclusion.</div>
<div class="callout warning">Important limitation.</div>
```

## Closing slide

`closing` lays out contact info and a QR code. Use the `closing-grid` /
`closing-grid-4` layout with `closing-contact` entries, and `qr-code` /
`qr-block` for a QR panel:

```html
<!-- _class: closing -->
# Thanks

<div class="closing-grid closing-grid-4">
  <div class="closing-contact"><h3>Email</h3><p>name@example.com</p></div>
  <!-- ... -->
</div>
```

```html
<div class="qr-corner">
  <div class="qr-block"><img class="qr-code" src="assets/qr.png">Scan for slides</div>
</div>
```

`dare-center` centers a block horizontally near the bottom of the slide (top
on `title`/`closing` slides). `dare-logo` renders a white-padded logo. The
`qr-code` image is forced pixelated and sits on a white rounded panel so it
scans cleanly.

## Architecture diagram

Use `architecture` with `.box` nodes and `.connector` arrows for a horizontal
pipeline:

```html
<div class="architecture">
  <div class="box"><strong>Ingest</strong>Load data</div>
  <div class="connector">→</div>
  <div class="box"><strong>Process</strong>Clean data</div>
  <div class="connector">→</div>
  <div class="box"><strong>Serve</strong>Expose API</div>
</div>
```

## Reference range diagram

`reference-range` draws a low/normal/high band with a marker showing the
current value:

```html
<div class="reference-range">
  <div class="range-track">
    <span class="range-zone range-low"></span>
    <span class="range-zone range-normal"></span>
    <span class="range-zone range-high"></span>
    <span class="range-marker"></span>
  </div>
  <div class="range-labels"><span>Low</span><span>Normal</span><span>High</span></div>
</div>
```

The marker is positioned by its `left` percentage (61% by default); edit that
value in the CSS or inline to move it.

## Text utilities

| Class | Effect |
|---|---|
| `subtitle` | Wide subtitle on lead slides |
| `eyebrow` | Uppercase label on lead slides |
| `muted` | Secondary text color |
| `accent` | Cyan text |
| `green` | Green text |
| `orange` | Orange text |
| `small` | 76% font size |
| `tiny` | 62% font size |

`citation` renders a centered quoted source in a bordered box, with an optional
`citation-label`:

```html
<div class="citation"><span class="citation-label">Source:</span> <code>paper.pdf</code></div>
```

`fast-stats` renders a large green value over a small caption:

```html
<div class="fast-stats">
  <p><strong>120M</strong><span>parameters</span></p>
  <p><strong>0.2ms</strong><span>latency</span></p>
</div>
```

Keep each slide focused on one point. Prefer open layouts and short text over
adding more containers.

---

## Sample project

[`sample/`](sample/) is a self-contained deck that exercises the theme end to
end — title slide, section dividers, highlighted code, tables, grids,
timeline, flow, an invert slide, and a closing slide — with no external assets
required.

```bash
cd sample
npm install        # not required — marp is used directly via npx
npm run html       # -> sample/deck.html
npm run pdf        # -> sample/deck.pdf  (requires a Chrome/Chromium)
```

The `html` script is the zero-dependency path:

```bash
cd sample
npx @marp-team/marp-cli deck.md --theme ../seafoam.css --output deck.html
```

Open `deck.html` in a browser (or `deck.pdf` in a viewer) to see the theme in
action. The sample's front matter is the canonical starting point for any deck
using this theme.

## Screenshots

Rendered from `sample/deck.md` with Seafoam:

![Title (lead)](screenshots/slide-01.png)

*Title (`lead`)*

![Section divider](screenshots/slide-03.png)

*Section divider*

![Highlighted code](screenshots/slide-05.png)

*Highlighted code*

![Two-column grid](screenshots/slide-07.png)

*Two-column grid*

![Closing](screenshots/slide-11.png)

*Closing*

## Palette

The light variant keeps Dracula's hue-to-role mapping but re-tunes each color
for a `#f8fafc` background:

| Role | Dracula (dark) | Seafoam |
|---|---|---|
| background | `#282a36` | `#f8fafc` |
| background alt | `#21222c` | `#eef2f7` |
| current line | `#44475a` | `#cbd5e1` |
| foreground | `#f8f8f2` | `#0f172a` |
| comment | `#6272a4` | `#475569` |
| cyan | `#8be9fd` | `#006b73` |
| green | `#50fa7b` | `#166534` |
| orange | `#ffb86c` | `#92400e` |
| pink | `#ff79c6` | `#8f3657` |
| purple | `#bd93f9` | `#1e4f7a` |
| red | `#ff5555` | `#b42318` |
| yellow | `#f1fa8c` | `#654d00` |

---

## Credits

- Dracula palette and theme conventions: [Dracula Marp theme](https://github.com/dracula/marp) by Daniel Gisolfi.
- Wave motifs and code/column styling: [Wave Marp theme](https://github.com/JuliusWiedemann/MarpThemeWave) by Julius Wiedemann.
- Built on [Marp](https://marp.app/) / [Marpit](https://github.com/marp-team/marpit).

## License

MIT. Use it freely in decks and presentations.
