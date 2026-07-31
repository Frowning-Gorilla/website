# Fonts

Self-hosted so the site makes no request to Google Fonts. Do not replace these with a
`fonts.googleapis.com` link — see CLAUDE.md, "no external dependencies".

## What's here

| File | Family | Covers |
|---|---|---|
| `dm-sans-latin.woff2` | DM Sans | Latin (`U+0000-00FF` + common punctuation) |
| `dm-sans-latin-ext.woff2` | DM Sans | Latin Extended |
| `dm-serif-display-latin.woff2` | DM Serif Display | Latin |
| `dm-serif-display-latin-ext.woff2` | DM Serif Display | Latin Extended |

Both families are **variable** fonts as served: the single DM Sans file covers the whole
300–600 weight range the site uses, so there is no file-per-weight. The `@font-face` rules
and their `unicode-range` declarations live in `styles.css`.

**No italic face is shipped.** The site never loaded one, so `<em>` renders as a synthesised
oblique. Adding a real italic would change how existing pages render — including the frozen
Eve Countdown pages. Don't add one without checking that.

## Provenance

Google Fonts, DM Sans **v17** and DM Serif Display **v17**, fetched from `fonts.gstatic.com`.
The exact URLs are the woff2 sources named in the `css2` response for:

```
https://fonts.googleapis.com/css2?family=DM+Sans:wght@300;400;500;600&family=DM+Serif+Display&display=swap
```

Request that URL with a current Chrome user-agent to get woff2 (an older UA returns TTF).

## Licence

Both are SIL Open Font License 1.1. The licences are **not** interchangeable and both must
stay in place:

- `OFL-DM-Sans.txt` — Copyright 2014 The DM Sans Project Authors.
- `OFL-DM-Serif-Display.txt` — Adobe (2014–2018) and Google LLC (2019), **with Reserved Font
  Name 'Source'**. The reserved name restricts redistribution under that name; it does not
  restrict using the font as-is, which is all this site does.


## Required for the Shape n Ship landing page

Two faces are referenced by `styles.css` but not yet in this folder. Until they
are added the landing page falls back to Helvetica/Arial for headlines and the
system monospace for labels — it stays readable, but the typography is not the
design.

| File | Family | Source |
|---|---|---|
| `archivo-latin.woff2` | Archivo, variable, wght 400–900 | Google Fonts (OFL) |
| `jetbrains-mono-latin.woff2` | JetBrains Mono, variable, wght 400–700 | Google Fonts (OFL) |

Latin subset only — the site is en-GB, and the `unicode-range` in `styles.css`
matches the DM faces' latin range. Keep both well under 100 KB.

Licences are included: `OFL-Archivo.txt` and `OFL-JetBrains-Mono.txt`, taken
from `google/fonts` (`ofl/archivo/`, `ofl/jetbrainsmono/`).

Fetch the two woff2 files from the repo root — Fontsource publishes the latin
subset with the weight axis intact, which is exactly what the `unicode-range`
above expects:

```
curl -L -o fonts/archivo-latin.woff2 \
  https://cdn.jsdelivr.net/fontsource/fonts/archivo:vf@latest/latin-wght-normal.woff2

curl -L -o fonts/jetbrains-mono-latin.woff2 \
  https://cdn.jsdelivr.net/fontsource/fonts/jetbrains-mono:vf@latest/latin-wght-normal.woff2
```

A one-off download into the repo, not a runtime dependency: the files are
committed and served from our own domain, so the site keeps making zero external
requests.

**Do not add a `fonts.googleapis.com` link instead.** The site makes zero
external requests, and `site-privacy.html` says so in public.
