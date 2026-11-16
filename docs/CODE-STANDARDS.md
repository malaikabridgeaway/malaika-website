# Code standards — plain HTML / CSS / vanilla JS on GitHub Pages

How code is written in this repo. Match the existing code; when in doubt, copy the
nearest similar pattern in `index.html`. Internal file — not published.

## Stack (and what not to add)

| Layer | What we use | Do not add |
|-------|-------------|------------|
| Markup | Single `index.html` (+ `404.html`) | Templating engines, SSGs, Jekyll |
| Styles | One inline `<style>` block in `<head>`, CSS custom properties | Tailwind, Bootstrap, Sass, extra fonts |
| Scripts | Inline `<script>` at end of body + `assets/js/i18n.js` | jQuery, React/Vue, bundlers, npm deps |
| Hosting | GitHub Pages via `.github/workflows/deploy.yml` | Branch/Jekyll Pages builds, servers |

If a feature genuinely seems to need a framework or build step, stop and propose it to
the owner with trade-offs instead of adding it.

## HTML

- Two-space indentation; lowercase tags and attributes; double quotes.
- Semantic elements first (`section`, `nav`, `header`, `footer`, `ul`, `dl`, `button`).
- Every top-level section follows this skeleton:
  ```html
  <!-- Section name -->
  <section id="kebab-id" class="kebab-id">
    <div class="wrap">
      <div class="section-head reveal">
        <span class="kicker" data-i18n="key.kicker">Kicker</span>
        <h2 data-i18n="key.title">Title</h2>
        <p class="lead" data-i18n="key.lead">Lead sentence.</p>
        <div class="rule"></div>
      </div>
      <!-- content; add class="reveal" to blocks that fade in -->
    </div>
  </section>
  ```
- Alternate backgrounds: sections with a white band use `background:#fff` + top/bottom
  `--line` borders; the dark band pattern is `.transparency`.
- Escape `&` as `&amp;` in HTML **and** in i18n strings that contain it.
- External links: `target="_blank" rel="noopener"`. PDFs: say "(PDF)" in the label.
- Images: `alt`, `width`/`height` (or CSS `aspect-ratio`), `loading="lazy"` unless
  above the fold.
- IDs are kebab-case and double as nav anchors (`#water-project`).

## Translations (i18n) — mandatory for every visible string

Mechanism (`assets/js/i18n.js`): `applyLang()` finds `[data-i18n]` elements and replaces
their content with `I18N[lang][key]`; strings containing `<` are set as `innerHTML`,
others as text. `[data-i18n-aria]` translates `aria-label`.

Adding or changing a string:
1. Write the English inline in `index.html` with `data-i18n="section.name"`.
2. Add the same key, in the same position, to the `en`, `es` **and** `sw` objects in
   `i18n.js`. The English value must equal the inline text.
3. Keys are `section.element` (`water.f1`, `doc3.open`, `legal.date.v` for values).
4. Allowed inline markup in strings: `<strong>`, `<em>`, `<b>`, `<br>` only.
5. Do not add `data-i18n` to proper nouns that never change (names, reg. number,
   address) or to the motto.
6. Verify each key exists in all three languages:
   ```bash
   grep -o 'data-i18n\(-aria\)\?="[^"]*"' index.html | sed 's/.*="\(.*\)"/\1/' | sort -u > /tmp/keys
   for k in $(cat /tmp/keys); do c=$(grep -c "\"$k\":" assets/js/i18n.js); [ "$c" -ne 3 ] && echo "$k: $c"; done
   ```
   (no output = every key is present in en/es/sw)

## CSS

- Use the tokens in `:root` (`--terra`, `--ink-2`, `--line`, `--radius`, `--shadow`,
  `--font-display`…). No new hard-coded colours unless you add a token.
- Group rules under the existing `/* ── Section ── */` comments; put new section styles
  in their own commented block before `/* Reveal on scroll */`.
- Class names are short, lowercase, hyphenated (`.p-card`, `.stat-row`, `.doc-card`).
- Layout with CSS Grid / Flexbox; fluid type with `clamp()`.
- Responsive: add rules to the existing breakpoints (`1380px` nav collapse, `960px`,
  `520px`) — don't invent new ones without reason. Mobile must be checked at 360–400 px.
- Motion: transitions ≤ .3s for hover, wrap anything animated so
  `prefers-reduced-motion` disables it.

## JavaScript

- Vanilla ES2017+, no dependencies; `const`/`let`, arrow functions, 2-space indent,
  single quotes in `index.html` script (i18n.js uses double quotes — follow the file).
- Keep scripts small and at the end of `<body>`; external files use `defer`.
- Progressive enhancement: the page must be readable with JS off (English inline).
- Build DOM with `createElement` + properties/`textContent` (see gallery code);
  never inject untrusted strings via `innerHTML`.
- Guard optional features (`if (DRIVE_PHOTOS_FOLDER) …`) and fail silently with
  `.catch(() => {})` for non-critical fetches.
- Wrap `localStorage` in `try/catch` (private mode).
- Configuration constants are UPPER_SNAKE_CASE at the top of the relevant block with a
  comment explaining what to paste there.
- The GoatCounter `<script>` stays last. No other trackers.

## Assets

- Paths: `assets/img/` (site images), `assets/gallery/` (`YYYY-MM-DD-description.jpg`),
  `assets/docs/` (PDFs — do not rename), `assets/video/`.
- File names: lowercase, hyphens, no spaces or accents.
- Optimise before committing: images resized + compressed, EXIF stripped; nothing
  > 50 MB. Useful commands (if installed):
  ```bash
  magick in.jpg -resize '1600x1600>' -strip -quality 78 out.jpg
  ffmpeg -i in.mp4 -vf scale=720:-2 -crf 28 -preset slow -c:a aac -b:a 96k out.mp4
  ```
- Replacing an image under the same name → bump `?v=N` wherever it is referenced.

## Deploy workflow (`.github/workflows/deploy.yml`)

- Keep `permissions` minimal and `concurrency.cancel-in-progress: false`.
- The "Strip internal files" step must list every internal file/folder
  (`AGENTS.md CLAUDE.md README.md UPLOAD-GUIDE.md docs .claude …`). Adding an internal
  file without updating this line publishes it.
- `gallery.json` is generated in CI — don't hand-edit it.

## Recipes

**New section:** skeleton above → styles block → nav link in `nav.links` with
`data-i18n="nav.x"` → keys in 3 languages (`nav.x` + section keys) → check nav still fits
(desktop nav shows only above 1380 px) → update sitemap `lastmod` → ROADMAP.

**New document:** PDF into `assets/docs/` (lowercase-hyphen name) → new `.doc-card` in
`#documents` (if a 5th card, check `.cards-4` grid) → 3-language keys → ROADMAP.

**New contact/social:** only with owner-confirmed data → contact card or `.handles` link
→ add URL to JSON-LD `sameAs` for social profiles.

**Fact change:** confirmed value only → search every occurrence
(`grep -rn "old value" index.html assets/js/i18n.js 404.html`) including JSON-LD and
meta tags → update all languages.
