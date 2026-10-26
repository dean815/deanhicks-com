# deanhicks.com

Source for my personal front page: who I am, a line on what I do, my CV, and
the places to find me. It replaces a Linktree.

One HTML file, one stylesheet, one font file, one photo, one PDF. No framework,
no build step, no package manager. The only external request is the Cloudflare
Web Analytics beacon; everything else the page needs is served from this
repository.

## Files

| | |
|---|---|
| `index.html` | The entire site: content, the CV overlay, its script, and `Person` structured data |
| `styles.css` | Design tokens, layout, light and dark palettes |
| `fonts/` | Bricolage Grotesque, subset to Latin, plus its OFL license |
| `headshot.jpg` | The photo, 1086×1448 |
| `resume.pdf` | The CV, opened in an overlay on desktop and directly on phones |
| `CNAME` | Binds the custom domain for GitHub Pages |

## Design

Two halves on a wide screen: text on the left, the photo bleeding to the right
edge. On a phone the photo sits on top and the text stacks under it. One face,
Bricolage Grotesque, does everything, from the heavy name down to the small
"Writing" label.

Colour and spacing are CSS custom properties defined once in `:root`, with a
`prefers-color-scheme: dark` block redefining the colour tokens. The palette is
near-neutral: white paper with near-black ink, inverted in dark mode, and the
ink itself is the only accent, so the CV button is the one solid block on the
page. Every text/background pair in both palettes clears the WCAG AA 4.5:1
floor; the lowest is 5.3:1 in light and 7.3:1 in dark.

## The CV overlay

The CV button is a plain link to `resume.pdf`. On a desktop browser with an
inline PDF viewer, a small script upgrades it to a native `<dialog>` that embeds
the PDF: `showModal()` makes the rest of the page inert and handles Esc, a
keydown handler keeps Tab inside the dialog, and focus returns to the button on
close. The PDF frame is kept out of the Tab order because browser PDF viewers
swallow keystrokes once focused, Esc included; the "Open the PDF" link in the
dialog's bar is the keyboard route to the full viewer. Phones, tablets and
browsers without an inline viewer never see the dialog and just get the PDF.

## Font

Bricolage Grotesque is self-hosted as a single variable `.woff2` (weight and
optical size axes, Latin subset, about 75 KB) rather than loaded from a CDN,
which is what keeps the external-request count at one. It is licensed under the
SIL Open Font License; the license text ships alongside it in `fonts/` as that
requires.

## Deployment

GitHub Pages serves the repository root from `main`. DNS is at Cloudflare with
the proxy disabled, so GitHub can issue and renew its own certificate. Web
Analytics runs in JS Snippet mode for the same reason: with the proxy off,
Cloudflare cannot inject the beacon itself.

## Updating

A new CV is a new `resume.pdf` at the same path; nothing else changes. The
page's own text is edited in `index.html` by hand. There is deliberately no
generator.
