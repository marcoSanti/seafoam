# Sample deck — Dracula Waves Light

A self-contained deck demonstrating the `seafoam` theme with
Marp. No external assets required.

## Render

```bash
# zero-dependency (uses the global marp CLI)
npx @marp-team/marp-cli deck.md --theme ../seafoam.css --output deck.html

# or via package scripts (npm install first for the local CLI)
npm run html   # -> deck.html
npm run pdf    # -> deck.pdf (needs Chrome/Chromium)
```

Open `deck.html` in a browser. The front matter is the canonical starting
point for any deck using this theme.

## What it shows

`lead` and `title` slides, `institution-logos` headers, `section` dividers,
highlighted code, a table with `metric` cards, a two-column `grid`, `timeline`
with markers, `fast-stats`, `flow`, `callout`/`warning`, `architecture`,
`reference-range`, figure helpers, text utilities (`eyebrow`, `accent`,
`badges`, `mark`, …), an `invert` slide, and a `closing` slide.

The logos under `assets/` are self-authored sample marks so the deck is
copyright-free — swap in any permissively-licensed logo (Python's PSF mark,
Marp's MIT mark, …).
