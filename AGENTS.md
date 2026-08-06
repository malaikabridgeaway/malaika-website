# AGENTS.md — rules for AI agents working on this repository

Internal instructions for any AI agent (Claude Code, Copilot, Cursor, etc.) editing this
repo. This file is **not published** on the website — the deploy workflow
(`.github/workflows/deploy.yml`) deletes it, together with `README.md` and
`UPLOAD-GUIDE.md`, before uploading the site. Keep it that way.

## What this repository is

The official website of the **Malaika Bridge Away Foundation**, a registered Tanzanian
NGO (Reg. No. 00NGO/R/9765) in Sumve, Kwimba District, Mwanza. Live at
**https://malaikabridgeaway.org**.

- Hosting: **GitHub Pages**, deployed by the GitHub Actions workflow
  `.github/workflows/deploy.yml` on every push to `main` (Pages build type is
  "workflow", NOT branch/Jekyll). Custom domain `malaikabridgeaway.org` with HTTPS
  enforced. DNS lives in **Namecheap** (4 apex A records to GitHub Pages + `www` CNAME
  to `malaikabridgeaway.github.io`).
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
   **Exception (owner decision):** the hero motto "Empowering Today — Transforming
   Tomorrow." (`.hero .motto`) has no `data-i18n` on purpose — it must always appear in
   English in every language. Do not translate it or add a translation key.
3. **Do not delete or rename these files** — external things depend on them:
   `CNAME` (custom domain breaks), `robots.txt`, `sitemap.xml`, `assets/docs/*` and
   `assets/img/appendix-a.jpg` (linked as official documents), `assets/js/i18n.js`.
4. **Keep the GoatCounter snippet** (last `<script>` in `index.html`) — it is the site's
   only analytics (dashboard: https://malaikabridgeaway.goatcounter.com).
5. **No files over 50 MB** (GitHub warns; 100 MB is a hard block). The existing 80 MB
   video is a known grandfathered exception.
6. **Internal docs must not reach the published site.** The deploy workflow publishes
   every file in the repo except those deleted in its "Strip internal files" step
   (`.github/workflows/deploy.yml`). Add any new internal file (notes, plans, this
   file) to that `rm` line, and verify it 404s after deploy. Note: Jekyll
   `_config.yml` excludes do NOT work — GitHub deploys this repo without Jekyll.
7. When you change page content, keep the SEO layer in sync: `<title>`, meta
   description, Open Graph/Twitter tags, the JSON-LD block (NGO + WebSite schema in
   `<head>`), and `sitemap.xml` `<lastmod>`.

## Photo & video gallery (#gallery section)

- **Primary mechanism — Google Drive**: the NGO team uploads media to two Drive
  folders in the foundation's account (malaika.bridgeaway@gmail.com), shared as
  "Anyone with the link – Viewer" (uploaders are added per-Gmail as Editor). The page
  embeds each folder via `https://drive.google.com/embeddedfolderview?id=<ID>#grid`.
  The folder IDs go in the `DRIVE_PHOTOS_FOLDER` / `DRIVE_VIDEOS_FOLDER` constants in
  `index.html`'s inline script. While an ID is empty, that block is hidden (videos) or
  falls back to the repo grid (photos). As of August 2026 the folders do not exist
  yet — waiting for the owner to create and share them.
- **Fallback photo grid**: files in `assets/gallery/` named `YYYY-MM-DD-description.jpg`;
  the deploy workflow regenerates `gallery.json` from that folder on every deploy
  (committed `gallery.json` is only a local-preview seed; do not hand-edit it). This
  path becomes dead code once `DRIVE_PHOTOS_FOLDER` is set — keep it until then.
- Uploader instructions live in `UPLOAD-GUIDE.md` (internal, not published; the owner
  shares it via the GitHub blob URL).
- Caveat to remember: Drive files under heavy traffic can hit Google's download quota
  and temporarily fail to render; if the site outgrows Drive, videos should move to a
  YouTube channel (embed the uploads playlist) — there is no `YT_PLAYLIST` constant
  anymore, it was replaced by the Drive design.

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
