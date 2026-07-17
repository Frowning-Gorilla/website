# Frowning Gorilla — website

The public website for **Frowning Gorilla Ltd**, a solo indie developer's company. Apps: **Shape n Ship**, **Nearing**.

Plain static site, hosted on **GitHub Pages**, served on a **custom domain** (`www.frowning-gorilla.com`, bound by the `CNAME` file, DNS at Namecheap).

## Deployment — read this first

**Pushing to the default branch deploys to the live site.** There is no staging environment.

- **Never push without explicit approval.** Commits are fine and can be made freely; pushes are releases.
- **The site is already live and public.** "Not promoted" is not "not published" — anything pushed is immediately readable by anyone, including App Review.
- The DNS configuration at Namecheap is already set up correctly. Don't touch it, and don't suggest changes to it.
- **Never modify or delete `CNAME`.** It is the custom domain binding — removing it takes the site off its domain.

## Tech rules

- **Plain HTML and CSS.** No frameworks, no build step, no preprocessors. What is in the repo is what ships.
- **No JavaScript** unless a specific feature genuinely needs it. If it does: minimal, vanilla, and approved before it's written.
- **No external dependencies** — fonts, scripts, trackers, analytics, CDN assets — without explicit approval. The site should load fast and respect visitors' privacy.
- If a change would add a request to a third-party origin, stop and ask first.
- **Images: optimise before committing** (target well under 300 KB each), descriptive filenames.

The site currently makes **zero external requests**. Fonts are self-hosted (`fonts/`), there is no analytics, and there is no form service. That's a claim `site-privacy.html` makes in public — if you add an external request, that page becomes a lie and must change in the same commit.

## Working method

- **Plan first on any multi-file change.** Propose the approach and wait for approval before implementing.
- Small, reviewable changes over sweeping rewrites.
- **After moving or renaming anything, verify links and image paths.** Check every internal `href` and `src` still resolves.
- **Keep this file current in the same commit as the change it describes** — the pages table and Known State below go stale fast and silently.

## Copy conventions

- **British English throughout** (colour, organise, licence as noun, -ise endings).
- **Tone: plain, direct, honest.** No marketing fluff. No invented praise, testimonials, awards, or user numbers. Don't claim anything that isn't true.
- **First person plural — "we".** But **never imply headcount**: no "our team", "the folks at Frowning Gorilla", or similar. Equally, no "solo studio" framing. Just "we".
- **Prices are never hardcoded into copy without a note of where else they'd need updating** — App Store Connect, in-app copy, and any other page carrying the same figure. If you write a price, write the note.
- **The commercial model is enumerated in exactly three places**, and nowhere else: the Shape n Ship **landing page** (pricing section), its **terms** (callout summary and body), and its **support FAQ**. Each states it in its own register but with **identical substance**:
  - **Free** — one project, through concept, development and testing.
  - **Pro** — everything from release prep onward (shipping, submission, promotion), plus **unlimited active projects**. "Active" is load-bearing: the lapse clause turns on active vs archived/read-only, so "unlimited projects" contradicts it.
  - **No other page makes free-tier claims at all.** The privacy page describes **payment handling only** — never tiers, prices, or trials. It was trimmed for exactly this reason: "there is no free trial" is a commercial fact that already changed once, and a privacy page has no business being on the list of things to update when the model moves.
- **Availability lives in one place.** An app is presented as buyable only by the presence of its store badge — never in prose. That keeps publishing a one-line change instead of a hunt through copy. See the badge slots in `index.html`.

## Structure conventions

- Each app gets its own section/pages, including the **support** and **privacy policy** pages Apple requires.
- **App-facing page URLs are load-bearing.** App Store Connect points at them; breaking a URL breaks App Store metadata links.
  - **Never rename or move an existing page URL without flagging it first.**
  - If a URL genuinely must change, that's a conversation — it needs a redirect plan and an App Store Connect metadata update, not just a `git mv`.

### Current pages

| URL | App | Purpose |
|---|---|---|
| `index.html` | — | Company front: intro, app cards, contact |
| `site-privacy.html` | — | Site-level privacy note. Linked from footers |
| `support.html` | Eve Countdown | Support & FAQ — **frozen**, see Known state |
| `privacy-policy.html` | Eve Countdown | Privacy policy — **frozen**, see Known state |
| `nearing-support.html` | Nearing | Support & FAQ |
| `nearing-privacy.html` | Nearing | Privacy policy |
| `shape-n-ship-support.html` | Shape n Ship | Support & FAQ |
| `shape-n-ship-privacy.html` | Shape n Ship | Privacy policy |
| `shape-n-ship-terms.html` | Shape n Ship | Terms of use |

Not built yet: `shape-n-ship.html`, `nearing.html`.

Newer app pages are namespaced by app (`<app>-<purpose>.html`); `support.html` and `privacy-policy.html` are unprefixed for historical reasons and are **Eve Countdown's** pages. Treat that inconsistency as load-bearing until the URLs are deliberately migrated.

### Styling

`styles.css` is the shared stylesheet. Adopt it with a `<link>` **and** `class="fg"` on `<body>`.

Everything except `@font-face` is scoped to `.fg`, so the file cannot reach a page that still carries its own inline CSS. **That scope is load-bearing.** Unscoped, a single `strong` rule reached the frozen Eve pages and reflowed one 148px taller. Pages that haven't migrated link the file for the self-hosted fonts alone and must not add the class.

- **Opted in** (`class="fg"`): `index.html`, `site-privacy.html`, `shape-n-ship-support.html`, `shape-n-ship-privacy.html`, `shape-n-ship-terms.html`.
- **Fonts only** (inline CSS retained): `nearing-support.html`, `nearing-privacy.html`, and both frozen Eve pages.

Accents come in pairs and the distinction matters: `--accent` is brand colour for fills and bullets, `--accent-deep` is for anything a person reads. The brand accents **fail WCAG AA as text** (teal `#19BAB0` is 2.31:1, orange `#E0641C` is 3.35:1). Using `--accent` for text is a bug, not a style choice. Per-app themes: `theme-nearing` (teal), `theme-shape-n-ship` (orange), no class = company indigo `#3E4C7A`.

A page may keep a small local `<style>` block only for rules genuinely unique to it (e.g. the homepage's app cards).

## Known state

Recorded so it isn't rediscovered each time. Not a licence to fix these unprompted.

- **Nearing is the renamed Eve Countdown** — same app. This is deliberately invisible to the public.
- **The Eve pages are frozen deliberately. No succession messaging — do not add any.** Eve purchases don't carry to Nearing, and the rebrand is deliberately not announced to Eve users. The pages stay live at their existing URLs (load-bearing), stay undiscoverable from the homepage, and there is **no public linkage between Eve and Nearing in either direction** — including shared asset URLs, which is why Nearing has its own copies of the shared screenshots.
  - Exception, already used once with approval: something **functionally broken** (not merely stale) may be fixed. The Formspree form was replaced with an email link on that basis, since decommissioning the service would have broken it silently.
  - Consequence, accepted: the Eve pages keep low-contrast teal text (2.31:1). Visual stability beat the accessibility fix.
- **No app is currently on the App Store.** Eve is delisted, Nearing is rejected and under appeal, Shape n Ship hasn't launched. **Do not add a store badge or link until a listing is confirmed live** — a badge pointing at nothing is the same bug as the dead Eve link that used to be on the homepage.
- **Shape n Ship's launch price is worded without a date** — "Launch price — rises to $34.99 shortly after launch." Dateless so nothing broken can ship, bounded so it doesn't read as an evergreen sale. **When the App Store Connect temporary price change is scheduled, that line gets the real end date in the same commit that updates the promo text.**
- Prices are shown in **USD only**, with "(or local equivalent)". The GBP base in App Store Connect and the USD storefront currently share the same numerals — that's a property of Apple's current price matrix, **not a rule**. Never derive one currency from the other; read the US row.
- The git remote is still named `eve-countdown-site`.
