# Tharunkumar A.R — Portfolio site

Personal portfolio for Tharunkumar A.R (aerospace engineering, Stanford). A single static page, `index.html`, hosted on GitHub Pages.

- **Live:** https://tharunkumar-ar.github.io/
- **Repo:** `Tharunkumar-AR/Tharunkumar-AR.github.io` (public). Pages serves the `main` branch from `/`, and every push redeploys in about a minute.
- **Deploy:** edit, `git commit`, `git push`. There is no build step.

## Files

| Path | What it is | In git? |
|---|---|---|
| `index.html` | **The site.** Inline CSS + JS + data. This is the only file to edit. | yes |
| `assets/img/<project-slug>/*.webp` | Project images referenced by relative path | yes |
| `CLAUDE.md` | This file | yes |
| `Tharunkumar A.R — Portfolio.html` | Original single-file export, a **stale backup**. Don't edit it. | no |
| `Resources/` | Source material, e.g. FTC engineering portfolio PDFs | no (gitignored) |
| `Projects/` | Source material for new projects, added by the owner over time | no (gitignored) |

The source folders are gitignored because they're large and contain teammate, outreach and team information that shouldn't be public. Only content curated into `index.html` and `assets/` gets published.

## How updates work (standing process)

The owner drops material for a project into `Projects/<name>/` or `Resources/` and asks for the portfolio to be updated. Then:

1. Read and extract the material. Use subagents in parallel, one per source document. Render the PDF pages and look at them, then pull text, stats and images.
2. Curate: write in the site voice (below), pick 5–8 strong images, and convert them to WebP (quality ~80, long edge ≤1600 px) in `assets/img/<slug>/`.
3. Add or update the entry in `PROJECTS` in `index.html`. Follow the schema below, decide `featured` and array position, and update `MILESTONES`/`HONORS`/`EXPERIENCE` if relevant.
4. Verify: JS syntax check (`node --check` on the extracted `<script>`), all image paths exist, and the page renders in light and dark mode.
5. **Update this file:** add the project to the content log, record any new schema fields, and record any design change (see Theme history).
6. Commit and push. Confirm the live site updates.

### Content rules
- **FTC Team 4545 (Ouroboros) robots: hardware only.** The owner was hardware lead and project manager. Source mechanisms, CAD, iterations, materials, stats, design challenges and hardware images. Don't feature the teams' software/autonomy code or outreach/marketing/business content, even though the owner did marketing work.
- Never invent facts. Quote numbers exactly as the source states them. If sources conflict, keep the site's value and flag it to the owner.
- No teammate or mentor names, and no quotes from portfolios.
- Restricted work (SpaceX) stays at "Details restricted under ITAR, export control and NDA".

## Design system — MUST be preserved

**Current theme: "Drafting Paper" (v1, in use since the site's first publish, Nov 2026).** The motif is an engineering drawing on graph paper: warm off-white paper, near-black ink, a single crimson accent, wide heavy uppercase display type, and hairline-ruled lists. Mostly square corners, no shadows except on the Poise screenshots.

If the theme ever changes, **don't delete this section**. Move it to *Theme history* below with its dates, then document the new theme here.

### Color tokens (`:root`)
| Token | Light | Dark | Use |
|---|---|---|---|
| `--bg` | `#FFFFFA` | `#080705` | page/header background |
| `--surface` | `#F6F4EE` | `#111114` | `.facts` box |
| `--plate` | `#EFECE4` | `#2C2E36` | image plates (tiles, hero, gallery) |
| `--ink` | `#080705` | `#FFFFFA` | text, 2px rules, `.btn` bg |
| `--muted` | `#5F626C` | `#9799A3` | secondary text, labels, nav |
| `--line` | `#E0DDD4` | `#26272D` | 1px hairlines, chip borders |
| `--grid` | `rgba(8,7,5,0.05)` | `rgba(255,255,250,0.04)` | graph-paper lines |
| `--orange` (a **crimson** accent, despite the name) | `#912F40` | `#D06A7C` | "A.R", active nav, hovers, focus ring |
| `--orange-deep` | `#702632` | `#B8505F` | `.btn.orange` bg (text `#FFFFFA`) |
| `--panel` | `#080705` | `#40434E` | SpaceX feature band |
| `--panel-ink` / `--panel-muted` | `#FFFFFA` / `#A9ABB3` | `#FFFFFA` / `#D0D2D8` | panel text |
| `--panel-line` / `--panel-accent` | `#2A2B31` / `#D9798A` | `#5A5D6B` / `#F2AAB6` | panel rules / accent |

**Discipline colors:** `--aero` `#912F40`/`#D06A7C` (same as the accent), `--sw` `#134074`/`#7FA3D6` (navy), `--hw` `#5E8B62`/`#8DBE90` (green) and `--el` `#A6873F`/`#D2B46A` (ochre). Each is shown as a 0.55rem dot.

**Theming:** light by default. Dark mode comes from `@media (prefers-color-scheme: dark) { :root:not([data-theme="light"]) }`, and `:root[data-theme="dark"]` forces it. The dark block is **duplicated verbatim**, so edit both. There is no toggle UI.

### Typography
- **Archivo variable** from Google Fonts: `family=Archivo:ital,wdth,wght@0,62..125,100..900;1,100,400`. Stack: `"Archivo", "Helvetica Neue", Arial, sans-serif`.
- **Width is the main lever.** Display type is weight 800 at `font-stretch: 125%`, usually uppercase with tight tracking (-0.02em). Body is 17px (1.0625rem), 400 weight, 100% width, line-height 1.6.
- Hero name: `fitName()` sizes "Tharunkumar" to fill the width (max 150px), with "A.R" on its own line in the accent color and a staggered per-letter animation.
- Page titles `clamp(2.6rem, 8vw, 6rem)`. Project h1 `clamp(2.1rem, 5vw, 3.6rem)`, not uppercase. Section heads 1.35rem uppercase with a 2px ink top rule that draws in. Stats 2.1rem 800/125%, tabular numerals, count-up on reveal.
- Prose measure ~62ch. Captions/labels 0.78–0.95rem muted. No uppercase eyebrows.

### Layout & motifs
- `.wrap` max 76rem, padding `0 1.5rem`. Breakpoints: 38rem, 40rem, 46rem, 52rem, 56rem (two-column layouts).
- Graph-paper backgrounds are two 1px `--grid` linear-gradients: 32px cells in the hero, 28px on the project hero, 24px on tile plates.
- Rules: 1px `--line` hairlines, 2px `--ink` structural rules, 1.5px `--ink` "drawing" boxes (`.titleblock` is an engineering title block: Project/Discipline/Year/Role/Context).
- Home has the milestone **trajectory** SVG (a curve rising through `MILESTONES`, with a dashed accent segment to the `next` one), the SpaceX dark panel, the Poise feature, then Selected work tiles.
- Motion: easing `cubic-bezier(.2,.7,.2,1)`. IntersectionObserver reveals (`data-reveal` → `.in`), staggered entrances. `prefers-reduced-motion` disables all of it in both CSS and JS. Keep that working for anything new.
- Images sit on `--plate` with contained fit. Transparent CAD renders need that plate so they read in dark mode.

### Voice & copy
- First person, humble, learning-focused, concrete numbers, no hype. Short declarative sentences. **No Oxford comma.**
- Curly apostrophes `’`. Spaced em dash ` — ` for asides. Unspaced en dash for seasons/ranges (`2024–25`), spaced for open ranges (`2026 – present`). `·` between org and location. Space before units (`7.5 s`, `2.5 mm`, `~3 ft`). `×` for multipliers. `&` in roles.
- `learned` ("What I learned") is one reflective paragraph of 1–3 sentences. Summaries are one sentence. Captions are short noun phrases with no period.

## Code map (`index.html`)
Everything is inline. In order: `<head>` + fonts → `<style>` (tokens, components, motion, reduced-motion) → markup with one `<section id="v-…">` per view → `<script>` (data constants → helpers → render functions → hash router → boot).

- **Routing:** hash-based. The views are `home, work, experience, about, photography, contact`. A project page is `#p-<slug>`.
- **Data constants:**
  - `AREAS`, `CFD_URL`, `DEMO_URL`, `PRIVACY_URL`, `POISE`
  - `MILESTONES` `{yr, t, s, next?}`, where exactly one `next` is allowed and it must be last
  - `PROJECTS`
  - `EXPERIENCE`, `SKILLS`, `LEADERSHIP`, `HONORS`
- **Hard-coded HTML:** the About bio and facts, the SpaceX panel and the Poise feature copy are written into the markup, not stored as data.
- **Escaping:** all text goes through `esc()`. Image `src` values are inserted raw.
- **Images:** older ones are inline base64 WebP data URIs. **New images go in `assets/img/<slug>/` as relative paths** to keep `index.html` small. Both forms work.

### `PROJECTS` schema
The array order is the display order everywhere, including prev/next; nothing is sorted. `featured: true` puts a project in home "Selected work".

| Field | Required? | Shape | Renders as |
|---|---|---|---|
| `slug` | yes | string | `#p-<slug>` |
| `featured` | no | bool | home tile |
| `title` | yes | string | tile, h1, titleblock, doc title |
| `season` | yes | string, e.g. `"2024–25"` | tile meta, titleblock Year |
| `areas` | yes | `["hw","sw","aero","el"]` subset | first = dot color, filters |
| `context` | yes | string | titleblock (prints "undefined" if missing) |
| `summary` | yes | string | tile text |
| `intro` | yes | string | detail intro |
| `image` / `thumb` / `alt` | no | src / src / string | hero; `thumb` is tile-only |
| `hook` | **yes if no `image`** | `[value, caption]` | text plate |
| `stats` | no | `[[value, label], …]` | shown only if ≥ 2 |
| `subsystems` | one of these two | `[[name, text], …]` | "How it works" |
| `body` | **yes if no `subsystems`** | `string[]` | "Overview" |
| `iteration` | no | string | only shown with `subsystems` |
| `learned` | no (all projects have it) | string | "What I learned" |
| `role` | yes | string | titleblock |
| `tools` | **yes**; the page crashes without it | `string[]` | aside |
| `recognition` | no | `string[]` | aside |
| `links` | no | `[[label, url], …]` | crimson buttons, new tab |
| `shots` | no; takes precedence over `gallery` | `[[src, caption, isPhone?], …]` | Poise-style screenshots |
| `gallery` | no | `[[src, caption], …]` | square plates + captions |

<!-- NEW-FIELDS: fields added after v1 are documented here -->
**Added Nov 2026 (all optional):**
| Field | Shape | Renders as |
|---|---|---|
| `challenges` | `[[title, problem, whatWeChanged], …]` | "Design challenges" section below Iteration; `ul.subsys.chal` with muted "Problem" / "What we changed" labels (`.chal small`) |
| `progression` | `{ steps: [[label, value], …], note }` | "Scoring progression": `ol.prog[data-reveal]` — 1.5px ink rule with a dot per step (last dot accent, echoes the trajectory), big 800/125% count-up values, muted labels, `.prog-note` below |
| `gallery` 3rd element | `[src, caption, alt?]` | alt text; falls back to caption |

**Gallery dark-mode backing:** `.gallery2` plates use the literal light plate `#EFECE4` in dark mode (in **both** dark blocks), and images use `mix-blend-mode: multiply` (plate has `isolation: isolate`). This keeps dark-grey/white-backed CAD renders legible.

## Content log
<!-- Keep this current. One line per project: slug — season — status/notes. -->
Projects in `PROJECTS`, in array order: `poise`, `into-the-deep`, `nacelle-cfd`, `centerstage`, `robot-autonomy`, `arcade-game`, `focus-rover`, `powerplay`, `freight-frenzy`, `two-hour-build`. Featured: into-the-deep, nacelle-cfd, centerstage.

- **into-the-deep**, 2024–25. Enriched from `Resources/Engineering Portfolio 2024-2025.pdf` (hardware pp. 7–12): 8 images in `assets/img/into-the-deep/`, challenges, progression (30 → 158 pts, hardware-only) and an intake-time fix to 1.1 s.
- **centerstage**, 2023–24. Enriched from `Resources/Engineering Portfolio 2023-2024.pdf` (hardware pp. 7–12): 8 images, challenges, iteration, progression (14 → 86; includes one software step, labelled as such).
- **powerplay**, 2022–23. Enriched from `Resources/RG Engineering Portfolio 2022-2023.pdf` (hardware pp. 7–12): 7 images, challenges, iteration, progression (34 → 113). The arm text is clarified: only V3 is machined aluminum.
- **nacelle-cfd**: framed as a self-directed **research project**, not a "paper". Link label is "Read the project write-up"; the contact row says "CFD research project".
- **EXPERIENCE** (Nov 2026):
  - SpaceX 2026 bullets come from the owner's own résumé text: high-pressure systems, dynamic fixtures, seals, novel metals process, furnace commissioning/SOPs, Python tooling, top 5% + return offer.
  - SpaceX panel stats: 18+ projects / 2 summers / Top 5% of interns.
  - **Never link TPS with alloy development.** Mention them as separate items ("TPS R&D, alloy and process development"), never as "TPS alloy development".
  - Suzuki bullets were also rewritten from the owner's text.
  - The UT Austin title is "Student Researcher (summer program)". The site uses US spelling, so "program", not "programme".
- Recognition lists for all three robots are **not** in the PDFs. They came from the original site and haven't been verified against these sources.

## Known issues / open questions
- The About-page `.sec-head`s lack `data-reveal`, so their 2px top rule never draws except under reduced motion.
- Dead CSS: `.devices .mac/.phone/.screen/.wordmark`, `.x`, `.c` and `.brand svg`.
- **Open questions for the owner:**
  - Power Play "35 pt autonomous": the PDF says 24-pt (pg. 06), 34 in the plan and 25 for the current path.
  - Into the Deep ground clearance: the PDF says 2.5 mm on p7 but 2.3 mm on p11; the site uses 2.5 mm.

## Theme history
<!-- When the design changes, move the old "Design system" section here verbatim with its date range. Never delete old themes. -->
- **v1 "Drafting Paper"**: Nov 2026 – present (current, documented above).
