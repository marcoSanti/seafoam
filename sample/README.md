# Seafoam sample deck

An anonymous 25-slide technical presentation demonstrating every public
component in the [`seafoam`](../seafoam.css) Marp theme.

![Sample title slide](../screenshots/slide-01.png)

## Build

Install the local Marp CLI and render both formats:

```bash
npm install
npm run html   # deck.html
npm run pdf    # deck.pdf; requires Chrome/Chromium
```

To render without installing the local dependency first:

```bash
npx @marp-team/marp-cli deck.md \
  --theme ../seafoam.css \
  --allow-local-files \
  --output deck.html
```

Local asset access is required because the deck uses SVGs from [`assets/`](assets/).

## Content

The deck follows a conference-style technical narrative:

1. Problem framing
2. Proposed approach
3. Synthetic evidence
4. Delivery and operational guidance
5. Sources and closing contacts

All organizations, people, links, metrics, and results are fictional. Example
URLs use the reserved `.invalid` domain.

## Component coverage

| Area | Components demonstrated |
|---|---|
| Slide variants | `lead`, `title`, `section`, `compact`, `invert`, `sources`, `closing` |
| Branding | `institution-logos`, `institution-logo`, `unito-logo`, `center-logo` |
| Layouts | `grid`, `cols-2`, `cols-3`, `cols-4`, `visual-split`, `figure-box` |
| Process | `flow`, `timeline`, `architecture`, `reference-range` |
| Content | `card`, `metric`, `callout`, `warning`, `citation`, `badges`, `fast-stats` |
| Closing | `closing-grid`, `closing-contact`, `qr-corner`, `qr-block`, `qr-code` |
| Utilities | Text colors/sizes, tight spacing, tables, code, blockquotes, `<mark>`, `<hr>` |

The SVG assets are self-authored placeholders and may be replaced with your
own logos, figures, badges, and QR code.

## Files

| Path | Purpose |
|---|---|
| [`deck.md`](deck.md) | Canonical sample source |
| `deck.html` | Generated browser presentation |
| `deck.pdf` | Generated PDF presentation |
| [`assets/`](assets/) | Local anonymous SVG assets |
| [`package.json`](package.json) | Reproducible Marp commands |

For the complete component API and copyable snippets, see the
[main Seafoam documentation](../README.md).
