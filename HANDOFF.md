# HANDOFF — 100Daysz marketing/legal website

This file is a self-contained briefing for continuing work on this project from a
context that has **no access to the repo, terminal, or git** (e.g. Claude chat
instead of Claude Code). Paste this whole file in, plus the specific page's HTML
if you need it edited, and the new session should have everything it needs.

## What this is

A static marketing + legal website for **100Daysz** ("100sDays" is the informal
app name; **100Daysz** is the brand/legal spelling used consistently across the
whole site and all legal documents — do not switch to "100sDays" anywhere).

- **App**: Flutter habit/100-day-challenge tracker for iPhone (App Store) and
  Android (Google Play). Both platforms are **"coming soon"** — not yet published
  as of this handoff.
- **Core features**: daily challenge/streak tracking, offline-first local storage,
  local reminder notifications, guided workout circuits, narrated breathing
  sessions, a 3D guide character.
- **Legal entity**: 100Daysz LLC, California, USA. (This supersedes an earlier,
  informal framing of the developer as an individual in India — the actual
  Privacy Policy/Terms PDFs the owner supplied name 100Daysz LLC as the
  contracting party, and that's what's used everywhere on the site now.)
- **Monetization**: in-app purchases/subscriptions via **RevenueCat**. App is
  **ad-free**. No personal data is sold.
- **Minimum age**: 18+ (hard requirement, stated in both Privacy Policy and
  Terms).
- **Site purpose**: satisfies Apple App Store Connect and Google Play Console
  submission requirements (Privacy Policy URL, Support URL, Marketing URL,
  account-deletion URL), plus a basic landing page.

## Site owner's accounts/contacts (for reference, don't invent others)

- Support email (general): **support@100daysz.com**
- Privacy/legal/account-deletion email: **admin@100daysz.com**
- GitHub repo: **https://github.com/nabaliri/100sdays** (public)
- Live site right now: **https://nabaliri.github.io/100sdays/**
- Intended future custom domain: **100daysz.com** (owned by the site owner, but
  **DNS is not yet pointed at GitHub Pages** — see "Open items" below)

## Current store-submission URLs (safe to use today)

| Field | URL |
|---|---|
| Privacy Policy | `https://nabaliri.github.io/100sdays/privacy.html` |
| Support URL | `https://nabaliri.github.io/100sdays/support.html` |
| Marketing URL | `https://nabaliri.github.io/100sdays/` |
| Account deletion (Play Data Safety) | `https://nabaliri.github.io/100sdays/delete-account.html` |

These will switch to the `100daysz.com` equivalents once DNS is migrated (all
canonical/OG tags and `sitemap.xml` already hardcode `100daysz.com`, in
anticipation of that move).

## Repo structure (everything lives at repo root, not in a subfolder)

```
100sdays/  (repo root)
├── index.html              landing page
├── privacy.html             Privacy Policy (36 numbered sections + 28A)
├── terms.html                Terms of Use (29 numbered sections + 4A, 14A, 14B + User Acknowledgment)
├── support.html              contact + troubleshooting + FAQ
├── delete-account.html       account/data deletion instructions
├── styles.css                shared stylesheet (all pages use this)
├── nav.js                    shared mobile-nav-toggle script
├── favicon.svg                also used as the inline logo mark in headers/footers
├── robots.txt
├── sitemap.xml
├── googlea405f12902df0f8c.html   Google Search Console verification file — do not delete
├── README.md                  just a stub ("# 100sdays"), not meaningful
└── .gitignore                 excludes documents/ and .DS_Store
```

**`documents/` (privacy_policy.pdf, terms_and_conditions.pdf) is intentionally
NOT in the repo.** The site owner has the original legal PDFs locally; they were
the source text for `privacy.html`/`terms.html` but were explicitly excluded from
GitHub (they contain nothing secret, the owner just didn't want source files
published alongside the rendered HTML).

## Design system (match this exactly for any new content)

- **Palette**: forest green primary, cream background, mint accent. CSS custom
  properties in `styles.css` (`--color-forest`, `--color-bg`, `--color-mint`,
  etc.), with a full dark-mode variant via `prefers-color-scheme` plus manual
  `[data-theme="dark"]` / `[data-theme="light"]` overrides.
- **Font**: Plus Jakarta Sans (Google Fonts), system sans-serif fallback.
- **Every page** has the same header (`<header class="site-header">` with logo
  SVG + nav links + mobile hamburger) and footer (`<footer class="site-footer">`
  with brand/App/Legal columns), copy-pasted identically across all 5 HTML
  files. `nav.js` is the shared mobile-menu-toggle script, loaded via
  `<script src="nav.js"></script>` at the end of `<body>`.
- **Legal pages** (`privacy.html`, `terms.html`) share a specific layout:
  - `.legal-wrap` → two-column grid: `.legal-toc` (sticky left sidebar, a `<nav>`
    with an `<ol>` of anchor links) + `.legal-body` (right column).
  - Each numbered clause is `<section id="kebab-case-id"><h2>N. Title</h2>...</section>`.
  - **Lettered sub-sections** (e.g. `4A`, `14A`, `14B`, `28A`) are the established
    pattern for inserting new content **without renumbering the existing
    sequence** — always follow this convention rather than renumbering.
  - `<div class="callout">` = neutral important-info box. `<div class="callout
    warning">` = amber-tinted box for user-facing warnings. Both are defined in
    `styles.css`.
- **Support/delete-account pages** additionally use `.contact-card` (email CTA
  box), `.troubleshoot-card` (icon + numbered `<ol>` fix steps), and
  `.ordered-steps` (circular-numbered step list, used in `delete-account.html`).
- Store badges on `index.html` are **placeholder inline SVGs** styled as
  "Coming soon" (not clickable) — there are HTML comments right above them
  linking to the official Apple/Google badge-asset pages, to be swapped in once
  the app is actually live.

## Content additions beyond the original source PDFs (flag for legal review)

The owner's Privacy Policy/Terms PDFs did not anticipate some of what's now on
the site. These were added deliberately but should be confirmed by whoever
drafted the original PDFs / counsel before relying on them:

1. **Terms §4A "Health & Fitness Disclaimer"** — not medical advice, consult a
   doctor before exercising; added because the app has guided workouts/breathing
   sessions the original PDF didn't cover.
2. **Privacy §28A "India — Digital Personal Data Protection Act, 2023"** — the
   original PDF covers CCPA/GDPR/UK but not India's DPDP Act; added since the
   developer is India-based. Has an inline note flagging it for counsel review.
3. **Terms §14A "How to Cancel Your Subscription"** and **§14B "How to Restore
   Your Subscription"** — step-by-step instructions (iPhone/Android cancel paths,
   24-hour-before-renewal warning, no-refunds policy with links to Apple's
   `reportaproblem.apple.com` and Google Play's refund-policy page; restore
   purchases flow, cross-platform non-transferability, troubleshooting steps).
   Added in the most recent session; not in the original PDF either.

## Open items / TODOs (search the HTML for literal "TODO" comments too)

1. **`delete-account.html`**: the in-app deletion menu path ("Profile/Settings →
   Account → Delete Account") is a **generic placeholder** — must be checked
   against the actual app UI before submission.
2. **`delete-account.html`**: the **30-day deletion timeframe** is a placeholder
   — confirm against the real backend process, and make sure the same number is
   used in Google Play's Data Safety form.
3. **`index.html`**: no Open Graph social-preview image yet (`og:image` tag is
   commented out with a TODO) — needs a real 1200×630 image.
4. **`privacy.html` §14/§32**: analytics/crash-reporting SDK language is
   deliberately vague ("specific providers may change") — if Firebase, Sentry,
   etc. are actually integrated, name them explicitly here **and** make sure
   Apple's App Privacy labels + Google Play's Data Safety form say the same
   thing. Mismatches between this page and the store forms are a common
   rejection reason.
5. **`privacy.html` §23 table**: Geolocation row says "only if a feature
   specifically requires it" — confirm the app doesn't currently request
   location; update if it does.
6. **Store badges on `index.html`**: swap placeholder SVGs for the official
   Apple/Google badge assets once each store listing is actually live, and
   update the href/URLs.

## DNS / custom domain status (important — read before touching DNS or CNAME)

- `100daysz.com` **currently resolves to Squarespace** (a "Coming Soon"
  placeholder page), **not to GitHub Pages**. The domain is owned by the site
  owner but DNS hasn't been migrated yet.
- A `CNAME` file (containing `100daysz.com`) was added to the repo once, which
  made GitHub Pages auto-redirect `nabaliri.github.io/100sdays/` →
  `100daysz.com` — but since DNS wasn't pointed at GitHub yet, this **broke the
  only working URL** (it redirected to the Squarespace placeholder instead of
  the real site). The `CNAME` file was **removed** to restore the working
  `github.io` URL. **Do not re-add a `CNAME` file until DNS has actually been
  updated** (see next steps below), or the same breakage will happen again.
- To cut over for real: add 4 **A records** for the apex domain pointing to
  `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`,
  plus a **CNAME record** for `www` → `nabaliri.github.io`, at whatever
  registrar/DNS host controls `100daysz.com`. Then re-add the `CNAME` file to
  the repo root (content: `100daysz.com`), wait for GitHub Pages to pick it up,
  and enable "Enforce HTTPS" in the repo's Settings → Pages. After that, update
  all store-submission URLs and the Search Console property from the
  `github.io` URL to `https://100daysz.com/...`.

## Google Search Console status

- A verification file, `googlea405f12902df0f8c.html`, is live at the repo root
  (**do not delete it** — removing it un-verifies the property).
- The owner initially tried to verify the wrong property
  (`https://nabaliri.github.io/100sdays/privacy.html/` — a single page, which
  doesn't work since it's a file, not a directory). They were advised to
  delete that property attempt and instead add
  `https://nabaliri.github.io/100sdays/` (the site root) as a URL-prefix
  property. **Whether this retry was completed and the property successfully
  verified was not confirmed before this handoff was written** — check
  Search Console directly, and if not verified yet, redo the "Add property"
  flow with the root URL, not a page URL.
- Once verified, submit `sitemap.xml` (`https://nabaliri.github.io/100sdays/sitemap.xml`
  for now, or the `100daysz.com` equivalent after the domain migration).
- Note: `sitemap.xml` and every page's `<link rel="canonical">`/OG tags already
  hardcode `https://100daysz.com/...`, not the current `github.io` URL — this
  is intentional (future-proofing for the domain migration) but means Search
  Console may flag a host mismatch if you verify the `github.io` property
  before migrating DNS. That's expected and will resolve itself once the
  domain migration happens.

## Working with this project from a no-repo-access session

If you're a fresh Claude chat session reading this with no file/terminal
access: you cannot read or edit the live files directly. To make further
changes, ask the user to paste the current content of whichever file needs
editing (or the specific `<section>` you need to see), then give back either
a full replacement file or precisely-scoped find/replace instructions they can
apply by hand (e.g. via GitHub's web editor, or locally then `git add/commit/push`).
Always match the existing structure/classes/tone described above rather than
introducing new patterns.
