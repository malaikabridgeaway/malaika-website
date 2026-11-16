# Malaika Bridge Away Foundation — Website

Official website of the **Malaika Bridge Away Foundation**, a registered Tanzanian NGO
(Reg. No. 00NGO/R/9765) based in Sumve, Kwimba District, Mwanza — working on clean water,
digital learning, educational support and youth talent development.

> Empowering Today — Transforming Tomorrow

**Live site: https://malaikabridgeaway.org** (GitHub Pages, custom domain via Namecheap DNS)

## Structure

```
index.html              The whole site (single page, no build step required)
404.html                Not-found page served by GitHub Pages
robots.txt, sitemap.xml SEO crawler files
assets/js/i18n.js       Translations (English / Spanish / Swahili) + language switcher
assets/img/             Logo, hero photo, social-share image, favicons, constitution appendix
assets/gallery/         Photo gallery — drop images here (see UPLOAD-GUIDE.md)
assets/docs/            Certificate, regional context report, academic proposal (PDFs)
assets/video/           Clean water project video (720p, ~6 MB)
```

## Languages

The site is trilingual — **English, Spanish and Swahili** — switchable with the
EN / ES / SW buttons in the navigation bar. The choice is remembered between visits,
and first-time visitors get the language their browser is set to. You can also link
directly to a language: `...?lang=es` or `...?lang=sw`. All translations live in
`assets/js/i18n.js`; edit the strings there to adjust wording.

## Deployment

The site is served by **GitHub Pages**, deployed by the GitHub Actions workflow
`.github/workflows/deploy.yml` (Pages build type "workflow", not branch/Jekyll), with the
custom domain `malaikabridgeaway.org` (the `CNAME` file) pointed at GitHub via Namecheap
DNS and HTTPS enforced. **Every push to `main` redeploys the live site automatically**
within a few minutes. The workflow also rebuilds `gallery.json` from `assets/gallery/`
and strips internal files (`AGENTS.md`, `CLAUDE.md`, `README.md`, `UPLOAD-GUIDE.md`,
`docs/`, `.claude/`) before publishing — there is no staging environment.

Visitor analytics: [GoatCounter](https://malaikabridgeaway.goatcounter.com) (snippet at
the bottom of `index.html`).

## Notes

- Keep videos small: re-encode before committing (this is how the current ~6 MB file
  was made from the 80 MB original), and bump the `?v=` in the `<source>` URL in
  `index.html` when replacing a file under the same name:
  `ffmpeg -i in.mp4 -vf scale=720:-2 -c:v libx264 -crf 28 -preset slow -pix_fmt yuv420p -c:a aac -b:a 96k -movflags +faststart out.mp4`
- No build tools, frameworks or servers needed — it is plain HTML/CSS/JS.
