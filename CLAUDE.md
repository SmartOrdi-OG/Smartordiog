# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository overview

This repo is the marketing website for **SmartOrdi OG**, an Austrian company building digital
tools for medical practices ("Ordinationen"). The entire site is a single static file:

- `index.html` — everything: markup, `<style>` CSS, and vanilla JS `<script>` blocks. There is no
  build system, no package.json, no bundler, and no test suite. The file is deployed as-is.

There is no local dev server config in the repo. To preview changes, open `index.html` directly in
a browser (e.g. `open index.html` / a "Live Server"-style extension), or serve the directory with
any static file server (e.g. `python3 -m http.server`). There is no lint/build/test command to run
— validate changes by opening the page and exercising the interaction manually.

The site content and UI copy are in German (`lang="de"`), targeting Austrian medical practices.
Keep new user-facing copy in German and consistent in tone with existing sections unless told
otherwise.

## Architecture: single-page "overlay pages" pattern

There is no router and no separate HTML files per page. Instead, the whole site is one DOM tree
with several full-page sections that are shown/hidden via plain `display` toggles:

- `#main-content` — the real landing page (nav, hero, product, pricing, FAQ, contact, footer, all
  built from `<section>`s with anchor ids like `#das-produkt`, `#vorteile`, `#angebot`, `#preise`,
  `#faq`, `#kontakt`, `#testen`).
- Overlay "pages", each a sibling `<div>` normally `display:none`, listed in the `OVERLAY_PAGES`
  array near the bottom `<script>`:
  - `#programm-smartordi-page`, `#programm-2-page`, `#programm-3-page` — per-product detail pages
    reached from the hero's "Unsere Programme" button row (`showProgramSmartordi()`, etc). Programs
    2 and 3 are intentionally unbuilt placeholders ("Demnächst" / in development).
  - `#agb-page`, `#datenschutz-page` — legal pages (Terms, Privacy).

Navigation between `#main-content` and an overlay is done entirely with JS, not real routing:
`showX()`/`hideX()` functions call the shared `_pageSwitch(hideId, showId)` helper, which fades the
current page out, sets `display:none`/`display:block`, scrolls to top, and fades the new one in.
`_hideOtherOverlays(exceptId)` ensures only one overlay is visible at a time. When adding a new
overlay page, add its id to `OVERLAY_PAGES` and add matching `showX()`/`hideX()` functions following
the existing naming convention.

Everything lives in three `<script>` blocks right before `</body>` (in this order): cookie banner +
scroll-to-top, page-switch/overlay logic + contact form + counters + theme + mobile nav + scroll
reveal + FAQ accordion. Keep new script logic in the appropriate block rather than adding new
`<script>` tags.

## Styling conventions

- All CSS lives in one `<style>` block in `<head>`. Theme colors are CSS custom properties on
  `:root` (`--navy`, `--blue`, `--sky`, `--frost`, `--cream`, `--warm`, `--gold`, `--text`,
  `--muted`) — always use these variables instead of hardcoding colors so dark mode keeps working.
- Dark mode is a `body.dark` class toggled by `toggleTheme()`, persisted via
  `localStorage.getItem('theme')`. `body.dark` redefines the same CSS variables plus a handful of
  `!important` overrides for cards/inputs/footers that don't purely rely on the variables. When
  adding a new card-like component with a hardcoded light background, add a corresponding
  `body.dark .your-class { ... !important }` rule near the existing dark-mode overrides at the top
  of the `<style>` block.
- Fonts are Google Fonts `Inter` (body) and `Manrope` (headings), loaded via `<link>` in `<head>`.
- Reusable visual patterns to follow: `.hero-card` / `.agb-card` for white content cards,
  `.section` + `.section-label`/`.section-title`/`.section-desc` for section headers,
  `.scroll-reveal` (paired with the `IntersectionObserver` in the JS) for fade/slide-in-on-scroll
  animations, `.pricing-card` (with `.featured` for the highlighted plan).

## Key interactive behaviors (in the final `<script>` blocks)

- **Cookie banner**: `#dsgvo-banner`, gated by `localStorage['dsgvo']`. The site sets **no**
  tracking/analytics cookies — "Ablehnen" (decline) has the same technical effect as "Verstanden"
  (accept); the banner is purely an informational DSGVO notice, not a consent-gate for scripts.
  Don't wire real tracking scripts to the accept/decline handlers without revisiting this design.
- **Contact form** (`submitContactForm()`): client-side validates required fields, email format,
  and the privacy-policy checkbox, then POSTs JSON to a Formspree endpoint
  (`https://formspree.io/f/xqenvrev`). On success it swaps `#contact-form` for `#contact-success`;
  on failure/network error it alerts the user and points them to `team@smartordi.eu`.
- **Stat counters**: `.counter[data-target][data-suffix]` elements are animated by
  `animateCounter()` once `.stats-row` scrolls into view (via `IntersectionObserver`).
- **FAQ / AGB accordions**: `toggleFaq()` and `toggleAgb()` both use the same
  max-height-collapse pattern; only one answer stays open at a time within its group.
- **Mobile nav**: hamburger toggle (`toggleMobileNav()`), closes on outside click or link click.

## Pricing model (kept in sync across the pricing section and program pages)

Three tiers, single one-time setup fee, monthly plans:
- Basic: 60€/mo — booking + dashboard only, no anamnesis/translation.
- Professional (recommended/featured): 120€/mo — adds anamnesis, DE/AR/EN UI, auto-translation,
  patient history/document upload.
- Premium: 150€/mo — adds visit-reason selection, PDF export, daily/monthly reports.
- All tiers: 1.500€ one-time setup fee, unlimited users (doctor + front desk) at no extra cost.

If pricing or feature lists change, update both `#preise` and the corresponding `programm-*-page`
copy so they don't drift out of sync.

## SEO / meta conventions

`<head>` carries a full set of German-locale SEO/social meta tags (description, keywords, Open
Graph, Twitter Card, geo tags for Linz/Austria) plus a `canonical` link to `https://www.smartordi.eu`.
When editing headline copy or the value proposition, update these meta tags to match so search/social
previews stay accurate.
