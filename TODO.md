# TODO – SmartOrdi OG Website

A list of everything that's been done and what's still needed on the site, based on the repo's edit history.

## ✅ Done so far

- [x] Redesigned the Hero to be a general company introduction instead of focusing on a single product
- [x] Added a horizontal row of buttons for the programs/products, each opening its own detail page
- [x] Moved all Smart Ordi content (stats, features, pricing, FAQ...) from the home page into its own standalone Smartordi.chat program page
- [x] Moved the contact (Kontakt) form into the Smartordi.chat page, actually wired to Formspree (not a placeholder)
- [x] Added an Impressum page with the company's real legal data (from official documents)
- [x] Corrected the legal address (Steingasse 6a instead of Promenade Steingasse 6a)
- [x] Rewrote the company description to be general (not limited to Austria or to doctors only)
- [x] Unified gold theme across the header/footer/company name/AGB, Datenschutz, and Impressum pages
- [x] Removed light mode entirely — the site is now permanently on dark-mode colors only
- [x] Linked the Smartordi.chat page to 100% real information from the actual product code (name, pricing, free-trial length, supported languages, translation mechanism)
- [x] Applied the real Smartordi.chat visual identity (logo + teal colors) to its page
- [x] Converted the Smartordi.chat page backgrounds to a light theme (white/mint) with dark teal text, instead of the dark theme, matching the real app's UI
- [x] "Get Started" links on the Smartordi.chat page now point to the app's real login page
- [x] Replaced the hand-drawn logo icon with the real app icon (Smartordi.chat)
- [x] **Programm 2 is now SmartAc** (a bookkeeping/financial-tracking app for freelancers and small businesses in Austria), with 100% real data from the actual product code: name, logo, description, features (income/expense tracking, invoicing, UVA tax report, read-only accountant portal, Branchen-Profile for transport and retail, receipt OCR), supported languages (EN/AR with RTL/DE), and its own blue theme matching the app's real visual identity. The pricing section is clearly labeled "Pilot phase / coming soon" since the program is still in a real pilot with no live pricing yet, and the CTA button links to the live demo
- [x] **Programm 3 is now Lamsa (لمستي)** (an AI interior-design app — the user uploads room photos and gets a new AI-generated design), with 100% real data from the actual product code: name, logo (gold shield), description, features (upload up to 5 photos + floor-plan editor, multi-currency budget including Gulf countries, style/color/mood selection, AI result in 15-30 seconds, nearby furniture-store suggestions, Quick Rearrange), supported languages (8 languages: Arabic RTL/English/German/Spanish/Turkish/French/Italian/Russian), and real, live pricing (1 credit/€1, 5/€4, 10/€7 + 1 free credit on signup via Stripe). Used a dark + gold theme matching the app's real identity (already close to the site's general theme). The CTA button links to the real, live login page
- [x] **Sitewide DE/EN language toggle** — a simple text button next to the contact button in the header (and also in each sub-page's header and in the mobile menu), instantly switching all site text between German and English with no page reload, and persisted in the browser (localStorage) so it reopens in whichever language was last chosen. German remains the default language. Covers every page on the site with no exception: the home page, all three legal pages (Impressum, AGB, Datenschutz) with all their legal text, and all three program pages (Smartordi.chat, SmartAc, Lamsa) with all their sections and contact forms
- [x] Removed the duplicate language toggle from the footer — it now only lives in the header (and in each sub-page's header, and in its mobile menu)

## 🔲 Still needed

- [ ] **SmartAc** – once the pilot phase ends and real pricing is set, the pricing section on its page needs to be updated (currently just labeled "coming soon")

### Possible general improvements (not explicitly requested yet, but worth considering)
- [ ] No CI/CD or automated tests on the repo — could be useful if the site grows further
- [ ] The whole site is one HTML file (~250KB+) — as more programs are added this could become harder to maintain, so splitting it up might be worth considering in the future (but that's an architectural decision that needs explicit approval before implementation)
- [ ] No visitor/performance tracking (Analytics) system on the site currently

---

> Note: any item on this list needs explicit confirmation from the project owner before implementation, especially things like splitting the file or major architectural changes.
