# ChrisGordon-DS

Design tokens: Safiro typeface, brand orange scale, spacing.

## Structure

```
fonts/            Safiro webfonts (woff2/woff), regular/medium/semibold/bold + italics
css/
  fonts.css       @font-face declarations
  colors.css      --color-orange-* / --color-neutral-* custom properties
  typography.css  --font-family-base / --font-weight-* custom properties
  spacing.css     --space-{xs,s,m,l,xl} custom properties
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

## Fonts

Sourced from the Font Squirrel "Safiro Complete Webfont" kit. Only woff2/woff
are included (no eot/ttf — add them back from the original kit if you need
IE or non-browser support). `fonts/LICENSE.pdf` is the original license —
check it before distributing or embedding these files outside your own
projects.
