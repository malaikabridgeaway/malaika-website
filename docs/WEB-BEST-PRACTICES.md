# Web best practices for the Malaika NGO website

The quality bar for any change to malaikabridgeaway.org. Each section says **why it
matters for this NGO**, the **rules**, and **how to check**. Internal file — not published.

Audience to design for: (1) international donors, partners and universities (Spain,
Europe) judging credibility in seconds; (2) the Tanzanian community and local partners,
often on **low-end Android phones and slow or expensive mobile data**; (3) search engines
and grant programmes (Google Ad Grants requires a high-quality, secure, transparent site).

---

## 1. Trust & transparency (the #1 job of an NGO site)

Visitors decide whether to trust the foundation before they read anything else.

- Legal identity visible and verifiable: name, registration number (00NGO/R/9765),
  registration date, physical address, and a link to the certificate. ✅ exists — keep it.
- Real, working contact channels. Every email/phone must be tested; a bouncing address
  destroys credibility (see the open `gmail.es` issue in ROADMAP).
- Only claim what is true *today*. No donation buttons without a working mechanism, no
  "impact to date" numbers for projects not yet built — present the water project as a
  **need / planned project** with sourced figures (which is what the current copy does).
- Cite sources for statistics (the context PDF with UN/World Bank/UNICEF sources).
- Show where the money goes (85/15 split) and, as the NGO matures, publish annual
  reports and project updates with dates.
- Show the real people behind the organisation (names, roles, photos with consent).
- Keep the site visibly alive: dated updates, current © year, no dead links.

## 2. Safeguarding & privacy (children appear on this site)

- **Consent for every identifiable person**, guardian/school consent for minors
  (already in UPLOAD-GUIDE.md). Never publish a child's full name together with their
  photo, school and village.
- Prefer group/activity photos over close-ups of individual children; never images of
  children in distress, undressed, or that exploit poverty ("dignified imagery" — tell the
  story of agency, not pity).
- Strip location EXIF metadata from photos before adding them to the repo
  (`exiftool -all= file.jpg` or re-export).
- Recommended: a short public safeguarding statement and a privacy note (what
  GoatCounter collects — cookieless, no personal data — and that Google Fonts / Drive
  embeds are third parties). Visitors from Spain/EU are covered by GDPR.
- Never put personal data of beneficiaries in the repo; it is public.

## 3. Accessibility (target WCAG 2.2 AA)

- Semantic structure: one `<h1>`, sections with `<h2>`, cards with `<h3>`; landmarks
  (`header`, `nav`, `main`, `footer`); skip link ✅.
- Text contrast ≥ 4.5:1 (≥ 3:1 for large text and UI borders). Use the existing tokens;
  `--peach` is only for dark backgrounds.
- Every meaningful image has an `alt` that describes it *in context*; decorative images
  get `alt=""` + `aria-hidden="true"`. Gallery alts currently come from filenames — name
  files descriptively.
- Everything works with keyboard only; visible `:focus-visible` outline ✅; interactive
  elements are `<a>`/`<button>`, never clickable `<div>`s.
- Touch targets ≥ 24×24 px (aim for 44×44 on mobile).
- `aria-*` states kept in sync (`aria-expanded` on the menu, `aria-pressed` on language
  buttons ✅). Translate `aria-label`s via `data-i18n-aria`.
- Respect `prefers-reduced-motion` ✅. Never autoplay video with sound.
- `lang` attribute matches the displayed language (i18n.js sets it ✅). Mark inline
  foreign phrases with `lang` when relevant.
- Videos: add captions (`<track kind="captions">`) when a transcript exists.

**Check:** Lighthouse Accessibility ≥ 95, axe DevTools no serious issues, tab through the
whole page, zoom to 200 % without horizontal scroll.

## 4. Performance (low bandwidth first)

Budget for the initial load on mobile: **< 1 MB transferred, LCP < 2.5 s on 4G,
CLS < 0.1, INP < 200 ms.**

- Images: resize to the largest displayed size (hero ≤ 1920 px wide, gallery ≤ 1200 px,
  cards ≤ 800 px), compress (JPEG q≈75–80 or WebP), always set `width`/`height` or
  `aspect-ratio` to prevent layout shift, `loading="lazy"` below the fold, and
  `fetchpriority="high"` only on the hero ✅.
- Video: never preload (`preload="none"` + poster ✅). The 80 MB file should be
  re-encoded (~720p, CRF 28 → typically 5–15 MB) or moved to YouTube; see ROADMAP.
- Fonts: at most the two current families, `display=swap` ✅, only weights actually used.
- JS: small, vanilla, `defer`/`async`; no libraries for things the platform does.
- Third parties (Drive iframes, fonts, analytics) cost time and privacy — lazy-load
  iframes ✅, add nothing new without a reason.
- Cache busting: GitHub Pages sets short cache TTLs; when replacing an image under the
  same name, append `?v=N` where it is referenced (as done for `hero.jpg?v=2`).

**Check:** Lighthouse mobile Performance ≥ 90; DevTools network with "Slow 4G" throttle.

## 5. SEO & discoverability

- Unique `<title>` (≤ 60 chars ideal) and meta description (≤ 160 chars) ✅.
- Canonical URL ✅, Open Graph + Twitter card with a 1200×630 image ✅.
- JSON-LD `NGO` + `WebSite` ✅ — keep it consistent with visible facts; add `sameAs`
  when new social profiles exist.
- `sitemap.xml` with correct `<lastmod>`; `robots.txt` ✅. Every new page goes in the
  sitemap.
- Multilingual: the site uses one URL with `?lang=`. Search engines mostly index the
  English (inline) version. If Spanish/Swahili search traffic matters, consider
  `hreflang` alternates pointing at `?lang=es` / `?lang=sw` URLs (see ROADMAP).
- Descriptive link text ("Registration Certificate (PDF)", not "click here").
- Register in Google Search Console & Bing Webmaster (pending, needs owner accounts).

## 6. Internationalisation (EN / ES / SW)

- Every visible string exists in all three languages — never ship a partial translation.
- English inline in HTML is the no-JS and SEO fallback, so it must always be complete.
- Translations must be natural, not literal; flag Swahili wording you are unsure of to
  the owner rather than inventing it.
- Numbers, dates and units follow the language (`3,100` vs `3.100`, `30 April 2026`
  vs `30 de abril de 2026`) — already handled via per-language keys.
- The motto stays in English everywhere (owner decision).

## 7. Content & UX

- Clear hierarchy: who we are → what we do → proof (project, data, documents) →
  how to help → contact.
- One primary call-to-action per section; CTAs must lead somewhere real.
- Short paragraphs, plain language, active voice; readable by non-native English speakers.
- Mobile first: design and test at 360–400 px before desktop.
- "How to help" without donations: volunteering, academic partnerships, sharing,
  contacting — until a donation mechanism works.

## 8. Security & reliability

- HTTPS enforced ✅. All external links with `target="_blank"` carry `rel="noopener"` ✅.
- No secrets, API keys or private data in the repo — it is public.
- No inline event handlers (`onclick=`); build DOM from data with `textContent` /
  properties, not `innerHTML` with untrusted input (i18n strings are trusted, static).
- Pin third-party GitHub Actions to major versions ✅; keep permissions minimal ✅.
- GitHub Pages cannot set HTTP headers; a `<meta http-equiv="Content-Security-Policy">`
  is possible but must allow Google Fonts, Drive iframes and GoatCounter — test before
  shipping.

## Release checklist (copy into your summary)

- [ ] All three languages render the change correctly (`?lang=en|es|sw`)
- [ ] Mobile (~375 px) and desktop layouts OK; no horizontal scroll
- [ ] Keyboard navigation and focus visible; images have correct `alt`
- [ ] No console errors; no broken links/assets (all 200)
- [ ] SEO layer in sync (title, description, OG, JSON-LD, sitemap `lastmod`)
- [ ] No new facts invented; no donation CTAs
- [ ] New internal files added to the deploy workflow's strip step
- [ ] `docs/ROADMAP.md` updated
