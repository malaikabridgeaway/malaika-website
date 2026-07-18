# Malaika Bridge Away Foundation — Website

Official website of the **Malaika Bridge Away Foundation**, a registered Tanzanian NGO
(Reg. No. 00NGO/R/9765) based in Sumve, Kwimba District, Mwanza — working on clean water,
digital learning, educational support and youth talent development.

> Empowering Today — Transforming Tomorrow

## Structure

```
index.html              The whole site (single page, no build step required)
assets/img/             Logo, hero photo, constitution appendix
assets/docs/            Certificate, regional context report, academic proposal (PDFs)
assets/video/           Clean water project video (~80 MB)
```

## Publishing on GitHub Pages

1. Create a new repository on GitHub (e.g. `malaika-website`), **without** adding a README.
2. From this folder, push the existing commit:

   ```bash
   git remote add origin https://github.com/<YOUR-USER>/malaika-website.git
   git branch -M main
   git push -u origin main
   ```

3. On GitHub: **Settings → Pages → Build and deployment**
   - Source: *Deploy from a branch*
   - Branch: `main`, folder `/ (root)` → **Save**
4. After a minute the site is live at `https://<YOUR-USER>.github.io/malaika-website/`.

## Notes

- The video is ~80 MB — under GitHub's 100 MB per-file limit, so it pushes fine, but the
  first push will take a while on a slow connection. If you ever want a faster-loading
  site, re-encode it smaller with:
  `ffmpeg -i assets/video/clean-water-project.mp4 -vf scale=720:-2 -crf 28 -preset slow -c:a aac -b:a 96k out.mp4`
- For nicer social-media link previews, add an `og:image` meta tag in `index.html` with the
  **absolute** URL of the hero image once you know the final site URL, e.g.
  `<meta property="og:image" content="https://<YOUR-USER>.github.io/malaika-website/assets/img/hero.jpg">`
- No build tools, frameworks or servers needed — it is plain HTML/CSS/JS.
