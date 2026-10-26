# deanhicks.com

Source for my personal resume site.

One HTML file, one stylesheet, two font files. No framework, no build step, no
package manager. The only external request is the Cloudflare Web Analytics
beacon; everything else the page needs is served from this repository.

## Files

| | |
|---|---|
| `index.html` | The entire site — content, semantics, and `Person` structured data |
| `styles.css` | Design tokens, layout, light and dark palettes, print |
| `fonts/` | JetBrains Mono and Newsreader, subset to Latin, plus their OFL licenses |
| `resume.pdf` | Downloadable CV, linked from the header |
| `CNAME` | Binds the custom domain for GitHub Pages |

## Design

Monospace carries the structure — name, section labels, dates, skill chips —
and a reading serif carries the prose. The split is the point: the mono says
what the work is, the serif keeps five roles of bullets comfortable to read.

Colour, type scale, and spacing are CSS custom properties defined once in
`:root`, with a `prefers-color-scheme: dark` block redefining seven colour
tokens. Restyling is a token change rather than a rewrite.

The dark palette is the primary design and the light one is its pairing, not an
inversion — a flipped dark palette goes muddy, and the accent in particular is
re-derived rather than reused. Every text/background pair in both was computed
against the WCAG AA 4.5:1 floor; the lowest is 4.97:1.

## Fonts

Both faces are self-hosted `.woff2` rather than loaded from a CDN, which is what
keeps the no-external-requests claim above true. They are variable fonts subset
to Latin, about 88 KB for the pair. Both are licensed under the SIL Open Font
License; the license text ships alongside them in `fonts/` as that requires.

## Print

`@media print` drops the slate entirely — black on white, flattened skill lists,
external URLs revealed after their link text — and fits the page onto two
sheets. The screen design still shows through in the type. Anything marked
`.site-only` is omitted, so the printed document matches the CV rather than the
website. Cmd-P produces a usable résumé rather than a screenshot of a web page.

## Deployment

GitHub Pages serves the repository root from `main`. DNS is at Cloudflare with
the proxy disabled, so GitHub can issue and renew its own certificate.

## Updating

The CV is maintained outside this repo; changes are mirrored into `index.html`
by hand. There is deliberately no generator — a CV that changes a few times a
year does not need a build pipeline.
