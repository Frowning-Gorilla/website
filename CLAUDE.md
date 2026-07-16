# Frowning Gorilla — website

The public website for **Frowning Gorilla Ltd**, a solo indie developer's company. Apps: **Shape n Ship**, **Nearing**.

Plain static site, hosted on **GitHub Pages**, served on a **custom domain** (`www.frowning-gorilla.com`, bound by the `CNAME` file, DNS at Namecheap).

## Deployment — read this first

**Pushing to the default branch deploys to the live site.** There is no staging environment.

- **Never push without explicit approval.** Commits are fine and can be made freely; pushes are releases.
- The DNS configuration at Namecheap is already set up correctly. Don't touch it, and don't suggest changes to it.
- **Never modify or delete `CNAME`.** It is the custom domain binding — removing it takes the site off its domain.

## Tech rules

- **Plain HTML and CSS.** No frameworks, no build step, no preprocessors. What is in the repo is what ships.
- **No JavaScript** unless a specific feature genuinely needs it. If it does: minimal, vanilla, and approved before it's written.
- **No external dependencies** — fonts, scripts, trackers, analytics, CDN assets — without explicit approval. The site should load fast and respect visitors' privacy.
- If a change would add a request to a third-party origin, stop and ask first.
- **Images: optimise before committing** (target well under 300 KB each), descriptive filenames.

## Working method

- **Plan first on any multi-file change.** Propose the approach and wait for approval before implementing.
- Small, reviewable changes over sweeping rewrites.
- **After moving or renaming anything, verify links and image paths.** Check every internal `href` and `src` still resolves.

## Copy conventions

- **British English throughout** (colour, organise, licence as noun, -ise endings).
- **Tone: plain, direct, honest.** No marketing fluff. No invented praise, testimonials, awards, or user numbers. Don't claim anything that isn't true.
- **Prices are never hardcoded into copy without a note of where else they'd need updating** — App Store Connect, in-app copy, and any other page carrying the same figure. If you write a price, write the note.

## Structure conventions

- Each app gets its own section/pages, including the **support** and **privacy policy** pages Apple requires.
- **App-facing page URLs are load-bearing.** App Store Connect points at them; breaking a URL breaks App Store metadata links.
  - **Never rename or move an existing page URL without flagging it first.**
  - If a URL genuinely must change, that's a conversation — it needs a redirect plan and an App Store Connect metadata update, not just a `git mv`.

### Current pages

| URL | App | Purpose |
|---|---|---|
| `index.html` | — | Homepage |
| `support.html` | Eve Countdown | Support & FAQ (has a Formspree contact form) |
| `privacy-policy.html` | Eve Countdown | Privacy policy |
| `nearing-support.html` | Nearing | Support & FAQ |
| `nearing-privacy.html` | Nearing | Privacy policy |
| `shape-n-ship-privacy.html` | Shape n Ship | Privacy policy |
| `shape-n-ship-terms.html` | Shape n Ship | Terms of use |

Newer app pages are namespaced by app (`<app>-<purpose>.html`); `support.html` and `privacy-policy.html` are unprefixed for historical reasons and are **Eve Countdown's** pages. Treat that inconsistency as load-bearing until the URLs are deliberately migrated.

### Styling

Every page is self-contained: its CSS lives in a `<style>` block in its own `<head>`. There is no shared stylesheet. Two design systems currently coexist:

- **`index.html`** — dark theme (navy `#0d1117` / teal `#3ecfb2`), Syne + DM Sans.
- **All sub-pages** — light theme (`#fafafa` / ink `#1a1f2e`), DM Sans + DM Serif Display, with a per-app accent: teal `#19BAB0` (Eve, Nearing), orange `#E0641C` (Shape n Ship).

Match the page you are editing. Changing a design system across pages is a multi-file change — plan and get approval first.

## Known state

Recorded so it isn't rediscovered each time. Not a licence to fix these unprompted.

- **Pending decision:** Google Fonts (all pages) and Formspree (support form) predate the no-external-dependencies rule; a decision on each is owed during the restructure.
- The homepage is **entirely Eve Countdown** and mentions neither Shape n Ship nor Nearing.
- **Shape n Ship has no support page**, though Apple requires a support URL.
- All app pages except the homepage are **orphaned** — nothing links to them from `index.html`.
- The git remote is still named `eve-countdown-site`.
- `index.html` line ~616: the Apple logo SVG `path` data contains the literal word `blurb`, which corrupts it.
- `nearing-support.html` references its images by **absolute** `https://www.frowning-gorilla.com/` URL; every other page uses relative paths.
- Screenshots in the repo are unoptimised (four ~1.7 MB PNGs) with camera-roll filenames (`IMG_6091.PNG`).
