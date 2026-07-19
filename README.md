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
assets/docs/            Certificate, regional context report, academic proposal (PDFs)
assets/video/           Clean water project video (~80 MB)
```

## Languages

The site is trilingual — **English, Spanish and Swahili** — switchable with the
EN / ES / SW buttons in the navigation bar. The choice is remembered between visits,
and first-time visitors get the language their browser is set to. You can also link
directly to a language: `...?lang=es` or `...?lang=sw`. All translations live in
`assets/js/i18n.js`; edit the strings there to adjust wording.

## Deployment

The site is served by **GitHub Pages** from the `main` branch root, with the custom
domain `malaikabridgeaway.org` (the `CNAME` file) pointed at GitHub via Namecheap DNS
and HTTPS enforced. **Every push to `main` redeploys the live site automatically**
within about a minute — there are no other deployment steps.

Visitor analytics: [GoatCounter](https://malaikabridgeaway.goatcounter.com) (snippet at
the bottom of `index.html`).

## Notes

- The video is ~80 MB — under GitHub's 100 MB per-file limit, so it pushes fine, but the
  first push will take a while on a slow connection. If you ever want a faster-loading
  site, re-encode it smaller with:
  `ffmpeg -i assets/video/clean-water-project.mp4 -vf scale=720:-2 -crf 28 -preset slow -c:a aac -b:a 96k out.mp4`
- No build tools, frameworks or servers needed — it is plain HTML/CSS/JS.
