# AGENTS.md — rules for AI agents working on this repository

Internal instructions for any AI agent (Claude Code, Copilot, Cursor, etc.) editing this
repo. This file is **not published** on the website — it is excluded in `_config.yml`,
together with `README.md`. Keep it that way.

## What this repository is

The official website of the **Malaika Bridge Away Foundation**, a registered Tanzanian
NGO (Reg. No. 00NGO/R/9765) in Sumve, Kwimba District, Mwanza. Live at
**https://malaikabridgeaway.org**.

- Hosting: **GitHub Pages** from the `main` branch root, custom domain via the `CNAME`
  file, HTTPS enforced. DNS lives in **Namecheap** (4 apex A records to GitHub Pages +
  `www` CNAME to `malaikabridgeaway.github.io`).
- **Every push to `main` deploys to production in ~1 minute.** There is no staging.
  Verify changes locally (open `index.html` in a browser) before pushing.
- Plain HTML/CSS/JS. No build step, no frameworks, no package manager. Do not introduce
  them.

## Hard rules

1. **Never invent or alter facts.** Registration number, registration date (30 April
   2026), address, phone numbers, emails, beneficiary statistics, the 85/15 fund split —
   these are legal/factual claims by a real NGO. Change them only when the user provides
   confirmed new values.
2. **Every user-visible text change must be made in all three languages.** English lives
   inline in `index.html` (it is the no-JS fallback) AND as the `en` keys in
   `assets/js/i18n.js`; Spanish (`es`) and Swahili (`sw`) live in `i18n.js` only. A new
   visible string needs: inline English + `data-i18n` attribute + `en`/`es`/`sw` keys.
3. **Do not delete or rename these files** — external things depend on them:
   `CNAME` (custom domain breaks), `robots.txt`, `sitemap.xml`, `assets/docs/*` and
   `assets/img/appendix-a.jpg` (linked as official documents), `assets/js/i18n.js`.
4. **Keep the GoatCounter snippet** (last `<script>` in `index.html`) — it is the site's
   only analytics (dashboard: https://malaikabridgeaway.goatcounter.com).
5. **No files over 50 MB** (GitHub warns; 100 MB is a hard block). The existing 80 MB
   video is a known grandfathered exception.
6. **Internal docs must not reach the published site.** GitHub Pages publishes every
   file in the repo unless excluded in `_config.yml` → `exclude:`. Add any new internal
   file (notes, plans, this file) to that list, and verify it 404s after deploy.
7. When you change page content, keep the SEO layer in sync: `<title>`, meta
   description, Open Graph/Twitter tags, the JSON-LD block (NGO + WebSite schema in
   `<head>`), and `sitemap.xml` `<lastmod>`.

## Design system

Match the existing style — do not import CSS or fonts beyond the current Google Fonts
(Fraunces + Inter). Design tokens are CSS variables in `:root` (`--terra`, `--peach`,
`--cream`, `--ink`…). Body text must keep ≥4.5:1 contrast. Respect
`prefers-reduced-motion` (see `.reveal`). Icons are emoji by design.

## Verification checklist after deploy

Wait ~60 s after pushing, then:

```bash
curl -s -o /dev/null -w '%{http_code}\n' https://malaikabridgeaway.org/          # 200
curl -s https://malaikabridgeaway.org/ | grep -c 'og:image'                      # ≥1
curl -s -o /dev/null -w '%{http_code}\n' https://malaikabridgeaway.org/AGENTS.md # 404
```

Plus: the language switcher (EN/ES/SW) still works, and any asset you added returns 200.

## Known issues / open items

- **`Irenemunoz11@gmail.es` (Contact section) is a dead address** — `gmail.es` has no
  MX records, so mail bounces. Waiting for the user to confirm the real address
  (probably `@gmail.com`). Do not "fix" it by guessing.
- Facebook in the socials row is plain text — no page URL provided yet.
- Google Search Console / Bing Webmaster verification and the Google Ad Grants
  application are pending — they require the foundation's own accounts.

## Accounts connected to this project

| What | Where |
|------|-------|
| Repo / hosting | github.com/malaikabridgeaway/malaika-website (GitHub Pages) |
| DNS | Namecheap, domain `malaikabridgeaway.org` |
| Analytics | GoatCounter — `malaikabridgeaway.goatcounter.com` |
| Instagram | `@malaikabridgeawayfoundation` |
| TikTok | `@malaikabridgeawayfnd` |
| Contact email | `malaika.bridgeaway@gmail.com` |
