# deanhicks.com

Source for my personal resume site.

One HTML file and one stylesheet. No framework, no build step, no package
manager, and no external requests — the page loads `index.html` and
`styles.css`, and nothing else. The type is a system font stack rather than a
webfont, which is what keeps that true.

## Files

| | |
|---|---|
| `index.html` | The entire site — content, semantics, and `Person` structured data |
| `styles.css` | Design tokens, layout, dark mode, print |
| `resume.pdf` | Downloadable CV, linked from the header |
| `CNAME` | Binds the custom domain for GitHub Pages |

## Design

Colour, type scale, and spacing are CSS custom properties defined once in
`:root`, with a `prefers-color-scheme: dark` block overriding six colour tokens.
Restyling is a token change rather than a rewrite.

Every text/background pair was checked against the WCAG AA 4.5:1 contrast floor.

## Print

`@media print` redefines those tokens for paper — black on white, flattened
lists, external URLs revealed after their link text — and fits the page onto two
sheets. Cmd-P produces a usable document rather than a screenshot of a web page.

## Deployment

GitHub Pages serves the repository root from `main`. DNS is at Cloudflare with
the proxy disabled, so GitHub can issue and renew its own certificate.

## Updating

The CV is maintained outside this repo; changes are mirrored into `index.html`
by hand. There is deliberately no generator — a CV that changes a few times a
year does not need a build pipeline.
