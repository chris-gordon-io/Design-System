# ChrisGordon-DS

Design tokens: Safiro typeface, brand orange scale, spacing.

## Structure

```
fonts/            Safiro webfonts (woff2/woff), regular/medium/semibold/bold + italics
css/
  fonts.css       @font-face declarations
  colors.css      --color-orange-* / --color-neutral-* custom properties
  typography.css  --font-family-base / --font-weight-* custom properties, .heading-1/.heading-2
  spacing.css     --space-{xs,s,m,l,xl} custom properties
  radius.css      --radius-{sm,md,lg,xl,full} custom properties
  buttons.css     .btn component — skins + sizes
  index.css       imports all of the above
tokens/
  tokens.json     source of truth, plain data
  tokens.js       JS/TS import of tokens.json
```

## Usage

CSS:
```css
@import 'css/index.css';

body {
  font-family: var(--font-family-base);
  color: var(--color-orange-100);
}
```

JS/TS:
```js
import { color, font } from './tokens/tokens.js';

color.orange['100']; // '#da441b'
```

## Colour scales

`--color-orange-{step}` is a linear mix of the base colour (`100`, `#da441b`)
toward white, where the step number is the mix percentage. Steps
`100/90/80/60/40/20` came from Figma; `70/50/30/10/5` were derived with the
same formula to fill the ramp.

`--color-neutral-{step}` (`100`→`10`) came from Figma directly. It follows
the same base-mixed-toward-white formula as orange down to `30`, but `20`
and `10` were hand-adjusted off that line (kept as sourced, not normalized).

## Spacing

`--space-{xs,s,m,l,xl}` → `4 / 8 / 16 / 40 / 80` (px). Doubles through the
small end, then jumps for the spacious end; every value sits on a 4px grid.
Not sourced from Figma — pick your own steps if these don't fit.

## Type styles

`.heading-1` (38px / bold / -1.5px tracking / 1.0 line-height) and
`.heading-2` (28px / bold / -0.4px / 1.3). Both use Safiro and
`--color-neutral-100`, with `margin: 0`; override colour on dark surfaces.

```html
<h1 class="heading-1">Benchmark</h1>
<p class="heading-2">Topline</p>
```

## Buttons

`.btn` is the base class; combine with a skin and a size. Sourced from
Figma node `3275:9290` ("Buttons") — text is Safiro Medium 16/20 at every
size, so only padding (and therefore height) changes between sizes.

Skins:
- `.btn--primary` — solid dark fill (`#272737`), white text.
- `.btn--primary-reversed` — solid white fill, dark text. For use on dark
  backgrounds.
- `.btn--secondary` — transparent, 1px dark outline/text, tints on hover.

All three use `#272737` ("dark-100" in Figma), which is a distinct value
from the neutral scale's `--color-neutral-100` (`#23233b`) — don't conflate
the two.

Sizes: `.btn--sm` (36px tall), `.btn--md` (44px tall) — both match the
Figma spec exactly. `.btn--lg` (52px) extrapolates beyond it for contexts
needing a bigger tap target. An optional leading/trailing `.btn-icon` (an
inline `<svg>`) is 16px by default.

**States**: hover and active darken (`--primary`) or dim (`--primary-reversed`)
the fill via `color-mix()` rather than opacity, so contrast only improves,
never degrades, at every step — checked against WCAG AA (base fills are
~14.7:1 against their text). `--secondary` tints its background instead,
on the same logic. Every skin also gets a `:focus-visible` ring in
`--color-orange-100`, which holds ≥3:1 against all three fills (white,
transparent-on-page-bg, `#272737`) — meets 2.4.7 Focus Visible / 1.4.11
Non-text Contrast without needing a different ring colour per skin.

```html
<a href="/" class="btn btn--primary btn--md">Get in touch</a>
<a href="/" class="btn btn--secondary btn--md">
  <svg class="btn-icon" viewBox="0 0 16 16">…</svg>
  Back to all work
</a>
```

## Fonts

Sourced from the Font Squirrel "Safiro Complete Webfont" kit. Only woff2/woff
are included (no eot/ttf — add them back from the original kit if you need
IE or non-browser support). `fonts/LICENSE.pdf` is the original license —
check it before distributing or embedding these files outside your own
projects.
