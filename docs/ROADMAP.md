# Roadmap & change log

Single place to track what has been done, what is blocked, and what is next.
Internal file — not published.

**How to maintain (humans and Claude):**
- When you finish something, move it to **Done** with the date (YYYY-MM-DD) and the
  commit hash if known. Newest first.
- Unplanned work still gets a Done entry.
- Things waiting on the owner or an external account go in **Blocked**, with what is
  needed to unblock.
- Ideas and improvements go in **Backlog** with a priority: P1 (credibility/broken),
  P2 (quality/impact), P3 (nice to have).

---

## Blocked — waiting on the owner

| Item | Needed to unblock |
|------|-------------------|
| Fix Irene Muñoz's email (`Irenemunoz11@gmail.es` bounces — no MX) | The confirmed correct address |
| Facebook link in the socials row (currently plain text) | The Facebook page URL |
| Google Drive photo/video gallery (`DRIVE_PHOTOS_FOLDER` / `DRIVE_VIDEOS_FOLDER` empty) | Create the two Drive folders in the foundation account, share "Anyone with the link – Viewer", send the folder IDs |
| Google Search Console + Bing Webmaster verification | Access to the foundation's Google/Microsoft accounts |
| Google Ad Grants application | Foundation's Google for Nonprofits account (site quality items below help) |
| Donation section | A working, verified donation mechanism (see AGENTS.md — do not re-add before) |
| `info@malaikabridgeaway.org` (Namecheap forward → `malaika.bridgeaway@gmail.com` + Gmail "Send mail as") | Owner sets it up and confirms send/receive works; then switch the site's contact email + JSON-LD `email` to it (3 languages) |
| Google for Nonprofits application (Goodstack verification, Tanzania NGO 00NGO/R/9765 — no US EIN needed) | Apply with `info@` once it works; wait for approval |
| Google Workspace for Nonprofits on `malaikabridgeaway.org` + shared drives for the media upload workflow | Nonprofits approval; domain TXT verification in Namecheap; then create "Website – Inbox" / "Website – Published" shared drives and send folder IDs |

## Next — ready to do

1. **P1 · Re-encode the 80 MB video** (~720p, CRF 28) or move it to YouTube — biggest
   cost for mobile visitors and the reason deploys take ~8 min.
2. **P1 · Fix outdated README deployment note** — README says Pages serves from the
   `main` branch root; it is actually the GitHub Actions workflow.
3. **P2 · Image optimisation pass** — add `width`/`height` to images missing them,
   compress `appendix-a.jpg` (~500 KB), consider WebP.
4. **P2 · Privacy & safeguarding note** — short trilingual footer section/page:
   GoatCounter is cookieless, third parties used (Google Fonts, Drive), consent policy for
   photos of minors. Text must be approved by the owner.
5. **P2 · `og:locale:alternate` for Swahili** is `sw_KE`; the NGO is Tanzanian →
   `sw_TZ`.
6. **P2 · Sitemap `lastmod`** still `2026-08-06` although content changed on 2026-08-18
   — keep it in sync on each content deploy.

## Backlog

- **P2 · "How you can help" section** without donations: volunteering, academic
  partnerships (engineering faculties), sharing on social media, contact.
- **P2 · News / project updates** section with dated posts (borehole progress, Talent
  Club events) — shows the NGO is active.
- **P2 · Team / board section** with names, roles and photos (consent) to build trust.
- **P2 · Trilingual 404 page** (currently English only).
- **P2 · Video captions** (`<track>`) once a transcript exists.
- **P2 · `hreflang` alternates** for `?lang=es` / `?lang=sw` if non-English search
  traffic matters.
- **P3 · Self-host Fraunces + Inter** (privacy/GDPR, one less third party) — same fonts,
  needs owner OK.
- **P3 · Lightweight CI checks** in the deploy workflow: HTML validation, broken-link
  check, i18n key parity (en/es/sw) — without committing a package manager.
- **P3 · Content-Security-Policy meta tag** allowing Fonts, Drive and GoatCounter.
- **P3 · Annual report / financial statements** in Documents once available.
- **P3 · Desktop nav collapses below 1380 px** — revisit so laptops (1280–1366 px) show
  the full menu.

---

## Done

### 2026-09-22
- Added `CLAUDE.md`, `docs/WEB-BEST-PRACTICES.md`, `docs/CODE-STANDARDS.md`, this
  roadmap and `.claude/settings.json`; deploy workflow now strips `CLAUDE.md`, `docs/`
  and `.claude/` from the published site.

### 2026-08-18
- Removed donations UI (nav button + #donate section) until a working donation
  mechanism exists — `22a0a42`.

### 2026-08-06
- Deploy workflow: queue deploys instead of cancelling, 30-min deployment timeout;
  several redeploys to recover from stuck Pages queue / hourly limit —
  `6ab4ad1`, `311323f`, `8cbb0de`, `da25801`.
- Nav: renamed Gallery → "Photos & Videos" in 3 languages; fixed nav overflow — `73c63fb`.
- Gallery: media pipeline switched to Google Drive folder embeds, repo grid kept as
  fallback — `d892834`.
- Added Photos & Videos section with self-updating photo pipeline (`gallery.json` built
  in CI) — `e887de2`.
- Hero: cleaned photo (painted branding removed), crisp circular logo overlay, cache-bust
  `hero.jpg?v=2` — `87aca83`, `18cf8c7`.
- Hero: new intro copy in 3 languages; motto kept in English by owner decision — `c6d0e83`.
- Switched to GitHub Actions deploy; internal files stripped from the published site —
  `57e5aa0`.
- Added `AGENTS.md` with AI agent rules — `75440a3`.

### 2026-07-19
- SEO: meta description, Open Graph/Twitter tags, JSON-LD (NGO + WebSite), sitemap,
  robots.txt, 404 page, performance fixes — `3f969ac`.

### 2026-07-18
- Fixed Instagram handle → `@malaikabridgeawayfoundation` — `c1f0c01`.
- Added GoatCounter analytics — `bc89daf`.
- Custom domain `malaikabridgeaway.org` via `CNAME` — `0b712a2`.
- Language selector with SVG flags — `11a6cd3`.
- Trilingual support (English, Spanish, Swahili) with language switcher — `c55341b`.
- Removed Juan Menor contact card; contact grid rebalanced to two columns — `a0c8df7`.
- Initial website launched — `44062a8`.
