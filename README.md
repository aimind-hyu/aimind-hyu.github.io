# AiMIND Lab website

A multi-page redesign of the AiMIND Lab site (originally on Google Sites), mirroring the original's structure. Built with plain HTML/CSS — no build step, no framework, no dependencies beyond Google Fonts (Noto Sans KR, used for both Latin and Hangul).

## Files

- `index.html` — Home (hero with the lab description folded in, research summary, news, open positions)
- `team.html` — Professor, Ph.D. students, undergraduate researchers, former members
- `publications.html` — Publications hub: one card per channel, linking to the four detail pages
- `publications-journal.html` / `publications-conference.html` — full lists, each entry with its key figure from `images/pub/`
- `publications-domestic.html` / `publications-patent.html` — full lists (no figures available for these)
- `research.html` — The four research areas (AI4AD, AI4Mobility, AI4Sensing, AI4BMS). Each is a `.research-area` block: tag chip + title + one-line lede, then the illustration (175px column) beside grouped topic lists, then any supporting figures from `images/research/`. A 2px `#CFD4DA` rule separates the four areas — `--paper-line` is too faint for a divider at that scale
- `projects.html` — On-going and completed funded projects
- `gallery.html` — Photos and captions from lab events, one photo at a time in an arrow-navigated carousel
- `courses.html` — Undergraduate and graduate courses taught
- `contact.html` — Email, office address, embedded map
- `style.css` — shared styling for every page
- `images/` — logo, banner photo, and the four research-area illustrations (used locally, must stay next to the HTML files)
- `images/gallery/` — event photos used by `gallery.html`
- `images/pub/` — publication figures, named by publication id (`J1`–`J9`, `C1`–`C9`), plus `J9-cover.jpg` (the Advanced Science issue cover). Any `<id>-cover.jpg` is picked up automatically and shown *beside* that entry's figure with a "Cover paper" badge — the two sit in a row inside a 250px column (cover fixed at 84px, figure takes the rest), because stacking them made that one row twice as tall as every other.
- `images/research/` — supporting figures for the research areas, prefixed by area (`ai4m-*`, `ai4sensing-*`)
- `images/selected/` — team portraits (square, circle-cropped PNGs). Originals are kept in `images/selected/_originals/`; the served copies are downscaled to 400×400 since they render at 150px.

## Preview locally

Just open `index.html` in a browser, or run a tiny local server:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Deploy on GitHub Pages

The site is published from a GitHub **organization** rather than a personal
account, so the lab owns the URL independently of any one person's login and
can hand it over without moving the repo.

1. Create an organization named `aimind-hyu` (github.com/organizations/new,
   Free plan), then a **public** repo inside it named `aimind-hyu.github.io`.
   The repo name must match the org name exactly -- that is what puts the site
   at the bare `https://aimind-hyu.github.io` instead of a `/subpath/`.
   Leave "Add a README" unchecked; this directory already has one.
2. Push these files to the repo's default branch (`main`):
   ```bash
   git init
   git add .
   git commit -m "Initial site"
   git branch -M main
   git remote add origin https://github.com/aimind-hyu/aimind-hyu.github.io.git
   git push -u origin main
   ```
   `git add .` stages the whole directory; `.gitignore` keeps the working
   originals (`images/figure/`, the `_originals/` portraits, `*.pptx`) out,
   which is what holds the repo near 11 MB instead of 78 MB. Those files
   remain on disk -- they are simply not published.
3. On GitHub, go to **Settings → Pages**.
4. Under **Build and deployment → Source**, choose **Deploy from a branch**.
5. Set **Branch** to `main` and folder to `/ (root)`, then **Save**.
6. Wait 1–2 minutes; GitHub will show the live URL at the top of the Pages settings.

## Next steps / things to customize

- **Student photos**: `team.html` shows portraits from `images/selected/`, matched to each person by filename. All current members and the one former member have one.
- **Former members**: Sungbin Lim is listed under `Former members` with the period `2025 – 2026`. Correct the end year if it is wrong, and move future alumni into that section the same way.
- **Gallery photos**: all photos are local, in `images/gallery/` (resized to 1600px wide). Events were matched to photos using the epoch-millisecond filenames of the originals (e.g. `1768019278842.jpg` → 2026-01-10 → Campus Lab Start-up Bridge). `2026 그룹 단체 회식` still has only 1 photo and `2025 AI 라이프 챌린지` only the ceremony shot plus a poster — add more to `images/gallery/` and extra `<img>` tags if you have them.
- **Originals are kept**: files in `images/` and `images/figure/` that no page references are the full-size sources for the resized copies under `images/gallery/`, `images/pub/` and `images/research/`. Safe to keep or prune.
- **Date to double-check**: the `2026 Hanyang AI-dea Challenge` entry is dated 2026.02.21, but the banner in its photos reads `일시 | 2026. 4. 6.(월) 10:00` — the award ceremony date. Confirm which date the entry should show.
- **Fonts**: Noto Sans KR for everything — Latin and Hangul both come from one family, so a sentence mixing the two never switches typeface mid-line. Set once in `--font-display` / `--font-body`; changing it means editing the `<link>` in all 12 pages plus the two variables. Roboto (the original) had no Hangul at all, so Korean text fell back to whatever the OS supplied and rendered differently per platform.
- **Hero title size**: 38px, not 40px — Noto Sans KR's Latin runs wider than Inter's, and at 40px the title needed 826px inside the 820px `.hero-photo .hero-text` column and wrapped to two lines.
- **Research figures**: the supporting figures under each area are the ones the original Google Sites research page carries, verified by downloading its images and pixel-matching them against the local files. AI4Mobility has exactly those two (`ai4m-assistance-scenarios.png` = `figure/2025.png`, `ai4m-invehicle-dashboard.jpg` = `figure/길동이.jpg`); four figures picked from `images/figure/` were dropped. The originals stay in `images/figure/` if you want any back. Note the original AD section has one figure this site does not.
- **Patent titles**: `publications-patent.html` shows the Korean title with the English title underneath (`.pub-title-en`), transcribed from the original Google Sites publications page. Two things came across from the original that look like errors there and are worth fixing: P8/P9 read `MTHOD` (missing E), and P6 (장애물 회피 경로를 생성하는 방법 및 장치) carries P5's English title `METHOD AND APPARATUS FOR POST-PROCESSING DATASET` instead of its own. P2 is a US patent, so it has no separate English line. Filing and publication dates for P1 and P3 were also picked up from the original.
- **Subpage titles**: `.page-hero h1` is `clamp(34px, 4vw, 46px)` at weight 400 in `#494D52` — bigger and lighter than the original 32px/500/`--ink`. 400 is the lightest weight loaded from Noto Sans KR, and `#494D52` still gives 8.1:1 contrast on the `--bg-tint` band (large text needs 3:1). Applies to all 11 subpages; `index.html` uses `.hero-photo` instead.
- **Nav dropdown**: the Publications menu sits 14px below its trigger, and `.nav-item-dropdown::after` is an invisible 16px bridge across that gap — without it the pointer leaves the container on the way down, `:hover` drops, and the menu closes before it can be clicked.
- **Gallery carousel**: `gallery.html` is the only page with JavaScript (a ~40-line inline script at the bottom). The viewport is a CSS scroll-snap strip, so photos stay swipeable and scrollable if the script does not run — the arrows and the `n / total` counter are the only things that need it. Entries with one photo hide both automatically.
- **Home hero photo**: the banner image is the hero's own background (`.hero-photo` on `index.html`), with the text sitting on top the way the original Google Sites header did, plus a short gold rule under the title. Two stacked layers do the work: `::before` holds the photo (inset by 16px so `filter: blur(2px)` cannot fade the edges; `background-image: inherit` picks up the inline URL) and `::after` is a left-to-right white scrim, strong where the text is and fading past ~70% so the building stays visible. `.hero-photo .hero-text` is capped at 820px to keep text off the building. The source photo is only 256px tall, so `min-height` is capped at 470px — raising it further just upscales and softens the image.
- **News**: all 21 items from the original Google Sites news list are in `index.html`, each tagged with a category (`data-cat`): `funding`, `people`, `paper`, `award`, `talk`, `lab`. To add an entry, copy a `.timeline-item` block to the top of `#news-list`, set `data-cat` and the matching `.news-tag-*` class, and bump the count in that category's filter chip (and in the `All` chip). Filter chips and the "Show all" button are driven by a small inline script; without JS every item is visible and both are hidden. The Jun 2025 item carries the one external link the original news list had (`http://hy-erica.com/vol110/post23.html` — the webzine serves HTTP only, so keep the `http://` scheme).
- Custom domain: if the lab has its own domain, add a `CNAME` file with the domain name and configure DNS per GitHub's custom domain docs.
- Each page currently repeats the same `<header>`/`<footer>` markup (a limitation of plain HTML with no build step). If you add many more pages, consider a static site generator (e.g. Eleventy, Jekyll — which GitHub Pages supports natively) so the nav only needs to be edited once.
