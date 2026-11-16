# CLAUDE.md

Entry point for Claude Code on the Malaika Bridge Away Foundation website.
**Internal file — never published** (stripped in `.github/workflows/deploy.yml`).

The non-negotiable project rules live in AGENTS.md and apply to every task:

@AGENTS.md

## Reference docs (read the relevant one before starting a task)

| File | Use it when |
|------|-------------|
| [docs/WEB-BEST-PRACTICES.md](docs/WEB-BEST-PRACTICES.md) | Any content, UX, SEO, accessibility, performance, privacy or safeguarding decision — the NGO-website quality bar |
| [docs/CODE-STANDARDS.md](docs/CODE-STANDARDS.md) | Writing or reviewing HTML / CSS / JS / workflow code — conventions and recipes (new section, new string, new image…) |
| [docs/ROADMAP.md](docs/ROADMAP.md) | Picking up work, checking what is done or blocked, and **logging what you changed** |

## How to work on a task

1. **Check the roadmap first.** If the task is already listed, work from that entry;
   if it is blocked on the owner (e.g. needs a real email address or a Drive folder ID),
   say so instead of guessing.
2. **Plan against the rules.** Trilingual text (EN inline + `en`/`es`/`sw` keys), no
   invented facts, no frameworks/build step, SEO layer kept in sync.
3. **Preview locally over HTTP**, not `file://` (the gallery `fetch('gallery.json')`
   fails on `file://`):
   ```bash
   python3 -m http.server 8000   # then open http://localhost:8000/?lang=en|es|sw
   ```
   Check desktop and ~375 px mobile width, all three languages, keyboard navigation,
   and the browser console (no errors).
4. **Update `docs/ROADMAP.md`**: move the item to *Done* with today's date, or add a
   new *Done* entry for unplanned work. Add follow-ups you discovered to the backlog.
5. **Do not push without the owner's go-ahead.** A push to `main` deploys to production
   within minutes and there is no staging. Commit on a branch or leave changes
   uncommitted and summarize them; after an approved push, run the verification
   checklist in AGENTS.md.

## Commit style

Imperative, specific subject that names the area, matching the history:
`Hero: new intro copy (3 languages)…`, `Gallery: switch media pipeline to Google Drive folders`,
`SEO: meta/OG/Twitter tags, JSON-LD, sitemap…`. One logical change per commit.

## Asking for work — examples the owner can use

- "Add a News section with the first post about the borehole survey" → new section recipe
  in CODE-STANDARDS, 3 languages, nav link, roadmap entry.
- "Update the beneficiary number to X" → only with the confirmed value; update inline EN,
  `i18n.js` (all langs), JSON-LD/meta if referenced.
- "The Drive folders are ready: photos=ID1 videos=ID2" → set the constants, verify embed.
- "Do the next roadmap item" → take the top unblocked item in *Next*.
- "Audit the site" → run the checklists in WEB-BEST-PRACTICES and report, don't fix blindly.
