# SmartOrdi OG – Marketing Website

The official marketing website of **SmartOrdi OG** (an IT company based in Linz, Austria), live at [www.smartordiog.eu](https://www.smartordiog.eu).

## Project nature

The site is a **single file**: `index.html`. There's no build step and no framework — everything (HTML + CSS + JavaScript) lives in that one file, so it's easy to deploy and edit directly.

Deployment happens automatically via **Netlify**, connected to the `main` branch of the repo — any push to `main` triggers an automatic deploy of the live site.

## Page structure

The page is built around an "overlay pages" pattern: every page exists as a `<div>` alongside the others in the same file, and one is shown while the rest are hidden via JavaScript (`display:none` / `block`), instead of real navigation between separate pages.

Current pages:

| Page | Description |
|---|---|
| **Home (Hero)** | General company introduction + a row of buttons for the different programs/products + a Kontakt (contact) section + Footer |
| **Smartordi.chat** (`#programm-smartordi-page`) | Detailed page about the Smartordi.chat product (a practice management system and patient portal) — stats, features, supported languages, onboarding steps, pricing, FAQ, contact form |
| **SmartAc** (`#programm-2-page`) | Detailed page about SmartAc, a bookkeeping/accounting app for freelancers and small businesses in Austria — features, supported languages, industry profiles, contact form. Pricing is marked "Pilot phase / coming soon" since it's still in a real pilot with no live pricing yet |
| **Lamsa (لمستي)** (`#programm-3-page`) | Detailed page about Lamsa, an AI interior-design app — features, supported languages (8 languages, including Arabic RTL), live Stripe-based credit pricing, contact form |
| **AGB** (`#agb-page`) | Terms and conditions |
| **Datenschutz** (`#datenschutz-page`) | Privacy policy |
| **Impressum** (`#impressum-page`) | Legal company data (per § 5 ECG and § 25 MedienG) |

## Language toggle (DE / EN)

The whole site — home page, all three legal pages, and all three program pages — supports a DE/EN language toggle. It's a simple "DE / EN" text button that lives in the header nav, in each page's own sticky header, and in the mobile nav dropdown. Switching languages updates all text instantly (no page reload) via `data-de`/`data-en` (and `-html`/`-placeholder`/`-aria` variant) attributes read by a small `applyLang()` function, and the choice is persisted in `localStorage`. German is the default language.

## Themes (colors)

- **The site in general** (header, footer, hero, company name, AGB/Datenschutz/Impressum pages): a **gold** theme taken from the company logo.
- **The Smartordi.chat page specifically**: its own **light teal** theme, matching the real visual identity of the app itself (same colors and logo as [smartordi-chat-app](https://github.com/SmartOrdi-OG/smartordi-chat-app)), with light backgrounds (white/mint) and dark teal text.
- **The SmartAc page specifically**: its own **blue** theme (`#1a7fd4`), matching the real product's UI.
- **The Lamsa page specifically**: its own **dark + gold** theme, matching the real product's branding (close to the site's general theme already).
- **Dark mode is permanent** across the whole site — light mode has been fully removed and there is no theme-toggle button.

⚠️ **Important note when editing**: CSS variables like `--navy`, `--muted`, `--sky`, `--text`, `--frost`, `--cream`, `--warm` used to have different values between light and dark mode — and since dark mode is now always on, using any of these as a background on an element must first be checked against its dark-mode value, or colors will look wrong. Only `--gold` (`#5EC9C2`) is stable across both.

## Real content policy

All facts on the program pages (pricing, free-trial length, supported languages, features) are taken from the actual product codebases — [smartordi-chat-app](https://github.com/SmartOrdi-OG/smartordi-chat-app), `smartac`, and `Lamsa` — so nothing is invented or guessed.

## Local development

No build tools required — just open `index.html` directly in a browser, or run a simple server:

```bash
python3 -m http.server 8000
```

then open `http://localhost:8000`.

## Deployment

- Hosting: **Netlify**
- Domain: `www.smartordiog.eu`
- Any `push` to `main` triggers an immediate automatic deploy.
