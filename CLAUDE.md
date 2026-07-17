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
- **Each app's commercial model has its own rule. They are different models — don't merge them.**
- **Shape n Ship's model is enumerated in exactly three places**, and nowhere else: the **landing page** (pricing section), its **terms** (callout summary and body), and its **support FAQ**. Each states it in its own register but with **identical substance**:
  - **Free** — one project, through concept, development and testing.
  - **Pro** — everything from release prep onward (shipping, submission, promotion), plus **unlimited active projects**. "Active" is load-bearing: the lapse clause turns on active vs archived/read-only, so "unlimited projects" contradicts it.
  - **No other page makes free-tier claims at all.** The privacy page describes **payment handling only** — never tiers, prices, or trials. It was trimmed for exactly this reason: "there is no free trial" is a commercial fact that already changed once, and a privacy page has no business being on the list of things to update when the model moves.
- **Nearing's model lives canonically in `nearing-support.html`** ("What do I get with Nearing Premium?"): free gives three simultaneous countdowns, teal only, standard widget size, fully opaque; Premium is a **one-time purchase** unlocking unlimited countdowns, all eleven background colours, rainbow and single-colour rings, the compact size, adjustable opacity, and no upgrade prompts. One purchase covers Mac, iPhone and iPad, and Family Sharing works. Spoken announcements, large-text mode, always-on-top and the completion animation are free for everyone.
  - `nearing.html` carries a deliberate **subset**, not a parallel copy: *"Free for your first three countdowns. Premium unlocks the rest, once."* A subset can't drift into contradiction the way a second full copy can. **Don't expand it** into a feature breakdown — link to the FAQ instead.
  - **Nearing names no price anywhere on the site.** Adding one makes that page the first thing to keep in sync with App Store Connect.
- **Availability lives in one place.** An app is presented as buyable only by the presence of its store badge — never in prose. That keeps publishing a one-line change instead of a hunt through copy. See the badge slots in `index.html` and `shape-n-ship.html`.
  - A **pre-launch status line** may sit directly under a badge slot ("Launching soon on the App Store."). It must be **deleted in the same commit that adds the badge** — the two must never both appear. It lives next to the slot so the swap stays a single, atomic edit.
- **Heading levels must not skip.** On most pages the app name in the header is the `h1`, the hero is `h2`, sections are `h3`. On a landing page the hero headline takes the `h1` (the app name uses `.brand`), so sections are `h2` and cards `h3`. `styles.css` gives `.fg main h2` and `.fg h3` the same treatment for exactly this reason.

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
| `nearing.html` | Nearing | Landing page. Pricing line is a subset of the FAQ |
| `nearing-support.html` | Nearing | Support & FAQ. Canonical Nearing model |
| `nearing-privacy.html` | Nearing | Privacy policy |
| `shape-n-ship.html` | Shape n Ship | Landing page. Third place stating the model |
| `shape-n-ship-support.html` | Shape n Ship | Support & FAQ |
| `shape-n-ship-privacy.html` | Shape n Ship | Privacy policy |
| `shape-n-ship-terms.html` | Shape n Ship | Terms of use |


Newer app pages are namespaced by app (`<app>-<purpose>.html`); `support.html` and `privacy-policy.html` are unprefixed for historical reasons and are **Eve Countdown's** pages. Treat that inconsistency as load-bearing until the URLs are deliberately migrated.

### Styling

`styles.css` is the shared stylesheet. Adopt it with a `<link>` **and** `class="fg"` on `<body>`.

Everything except `@font-face` is scoped to `.fg`, so the file cannot reach a page that still carries its own inline CSS. **That scope is load-bearing.** Unscoped, a single `strong` rule reached the frozen Eve pages and reflowed one 148px taller. Pages that haven't migrated link the file for the self-hosted fonts alone and must not add the class.

- **Opted in** (`class="fg"`): every page except the two frozen Eve pages.
- **Fonts only** (inline CSS retained): `support.html` and `privacy-policy.html` — the frozen Eve pages. They link the file for the self-hosted fonts alone and must never gain the class.

Accents come in pairs and the distinction matters: `--accent` is brand colour for fills and bullets, `--accent-deep` is for anything a person reads. The brand accents **fail WCAG AA as text** (teal `#19BAB0` is 2.31:1, orange `#E0641C` is 3.35:1). Using `--accent` for text is a bug, not a style choice. Per-app themes: `theme-nearing` (teal), `theme-shape-n-ship` (orange), no class = company indigo `#3E4C7A`.

**Links in body text and cards are underlined at rest. Do not remove the underlines as a design cleanup.** WCAG 1.4.1: a link identified by colour alone must contrast ≥3:1 with the surrounding text, and ours don't — measured against body copy the company indigo is **1.06:1**, teal and orange **1.41:1**. Strip the colour and the link vanishes into the sentence. (All three still clear 4.5:1 against the *background* — that's a separate question, and passing it is not a substitute.) Nav and footer link lists are exempt: a link that is the whole line is identifiable by position. Underlines use `text-underline-offset: 2px` and `text-decoration-thickness: 1px`; hover thickens to 2px rather than adding a line.

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
- **Nearing has no terms page, deliberately** — the standard Apple EULA suffices for its one-time in-app purchase, which is not an auto-renewable subscription. The asymmetry with Shape n Ship (which has one) is intentional, not an oversight.
- The git remote is still named `eve-countdown-site`.
