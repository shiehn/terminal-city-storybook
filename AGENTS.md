# AGENTS.md — terminal-city-storybook (the static storybook website)



## THE CANON REPO (2026-09-12)
The source of truth for the field guide (lore), the Story and the style guide is the private repo `shiehn/terminal-city-canon`,
cloned at `~/sas-platform/terminal-city-canon` (`git pull` first). `album-art/terminal-city-folklore/` is retired; the parse
mirrors into `album-art/catalog/folklore.json`. Drafts are added there as new numbered files, never edited in place — see its
`AGENTS.md` and the `tc-canon` skill; the `tc-graph` skill carries the same paragraph.

## The production graph (Steve, 2026-09-12) — READ THE `tc-graph` SKILL FIRST, EVERY TASK
Every file this repo makes is a node in `sas-project-mgmt/canon/graph.json` with an owner and a hash; every edge records the
source hash the builder read. `.Codex/settings.json` here runs `graph.py brief` on every prompt and `graph.py build` on every
stop, so an agent started in this folder alone sees the whole system's state. Contract: `sas-project-mgmt/canon/GRAPH.md`.
Rule: write what you read — stamp your inputs' hashes in your outputs; fix or flag the stale nodes you own before finishing.

## The authority on Terminal City (READ FIRST)

**All text on these pages comes from the field guide in `../album-art/terminal-city-folklore/` — the NEWEST
draft there wins** (today, 2026-09-09: `Terminal_City_Field_Guide_Draft_0.7.docx`, Draft 0.7, Steve's own — 20 nodes in
his list order, dossiers JOB · OPERATING LOGIC · CONNECTIONS · VISIBLE EVIDENCE · RULE · OPEN, one primary role each;
the 0.5 stories/plates are now written from an older draft — T64). Steve authors
it; never edit or move it. Pages are generated from its parsed copy `../album-art/catalog/folklore.json`; if that
file's `sha1` no longer matches the newest docx, re-parse first (`cd ../album-art && .venv/bin/python
scripts/field_guide.py`). **Never hand-edit card text in a page** — fix the guide, re-parse, rebuild.

**Three layers (Steve, 2026-09-12): LORE = the field guide (what is true: rule, place, role, the card facts) · STORY = the
Story document `../sas-project-mgmt/canon/story/Terminal_City_Story_Draft_x.md` (newest draft wins; Steve authors, mgmt drafts;
parsed to `canon/story/story.json`) · STORYBOARDS (video, one per chapter).** The chapter text on every page (paragraphs,
hook, title) is a MIRROR of the Story: `../sas-project-mgmt/scripts/mirror_story.py` copies story.json → `stories/stories.json`
and stamps `chapter_sha1`; then `stamp_stories.py`; then rebuild. **Never edit paragraphs or hooks in stories.json** — a wording
change goes to the Story document (mgmt drafts, Steve approves) and mirrors down. stories.json keeps what is the site's own:
master, source_photo, motifs, image_prompt, video_url, final_audio, redirects, credits, preface.

**Historically, the story on each page was a RETELLING of its card** (Steve, 2026-09-08: preteen/teen reading level, a few
paragraphs, its own title, a generated image). Source: `stories/stories.json` (keyed by slug; stamps the guide draft +
sha1 it was written from). The retelling may add warmth and explanation but must never contradict the card, and the
sensitivity lines bind it. When a new draft lands: re-parse → re-read every story against its card → update
`stories.json` (bump its `guide_sha1`) → rebuild; until then the pages flag the story as written from an older draft.

## What this site is

One of the delivery formats of the album: **a static, beautiful storybook — one chapter per NAMED node (19 since Draft 0.7 — the Open Slot is a
placeholder and gets no page; ids renumber between drafts, pages key on the slug) — an ALBUM, not a wiki (site review 2026-09-10).** Chapter anatomy
(v0.5.0): chapter · BPM · a small cold role tag (INPUT / PROCESSING / OUTPUT, never the job text) → the video slot (the
YouTube embed when `stories.json` has a `video_url`, the master drawing until then) → a one-line `hook` → the story → the
rule → field notes, COLLAPSED (where + the map with every station a link, a photograph, "Known associations" as names
only) → next chapter (hook + thumb) → prev / map / next → colophon = version + the disclaimer + the discreet credits line (`stories.json` `credits`). Home page: album order (default) + a "Daily cycle" view from
the guide's `cycle_order` / `off_clock`; the preface ends with the guide's `one_line`. Maps (v0.8.0, Steve: "each element
glows red when mouse over or click .. and stays red when in focus"): no numbered chips — every drawn element is a link
(`station_links()`), its mask red-tinted as the glow on hover / focus / press / current; ONE tap navigates on touch (no tap-to-light). **No scaffolding on the
public page**: no filenames, hashes, draft stamps (they live in an HTML comment for `sync_check.py`), production notes,
job text, status words or connection sentences — the builder enforces it, never hand-edit. The video template keeps the
seven-beat storyboard skeleton (`../sas-project-mgmt/world-design.md`).

## Invariants

- Pages live at `<theme-slug>/index.html` (slug = the card's `slug`, e.g. `morning-meeting/`); a renamed slug keeps a
  redirect page at the old dir via `stories.json` `redirects` (written by the builder); the home page
  (`index.html`) is the map with every station linked (the builders count pages from the guide). One page: `../sas-project-mgmt/scripts/storyboard_page.py
  TC_nn`; the whole site: `build_site.py [--only TC_01,…]`. **Generated files are never hand-edited** — change
  the source (guide, assets, builder) and regenerate. Missing assets become labelled empty frames — never fake an image.
- **A new field-guide draft makes every page stale (Steve, 2026-09-08).** Ids, order, prev/next, the station marks
  (`renders/terminal_map/layout.json`) and the colophon all come from the guide; after a new docx the site must be
  regenerated (`build_site.py`, on Steve's say-so, after the map layout is re-keyed by the `video` session). The full
  cascade (CSVs → sheet → video → storybook) is the `pm-folklore` skill in `sas-project-mgmt`'s monorepo skills.
- **Provenance stamps (tc-graph, T114):** every story carries `card_sha1` (run `sas-project-mgmt/scripts/stamp_stories.py`
  after writing or rewriting a story); every page's HTML comment carries the guide sha, `story <sha10>` and `map <sha8>`
  (the builder writes them). The graph (`graph.py check`) judges pages and stories by these — never strip them.
- **The site evolves (Steve, 2026-09-07) — nothing here is law except the authority and the sensitivity lines.**
  The look and the beat order are the CURRENT version: `VERSION` (0.8.3) + `CHANGELOG.md` in this folder; every
  page's colophon stamps the site version, build date and field-guide draft it was built from. Change the look
  by changing the builder, bumping `VERSION`, adding a changelog line and a dated entry in
  `../sas-project-mgmt/world-design.md` — then regenerate. Shipped look since 0.4.0 (Steve 2026-09-10 "darkness better"): the DARK ground — page `#0B0C0D`, type `#EDEFF1`,
  graphite `#A9B1B8`, hairlines `#2A2F34`, masters native white-on-black, map = `renders/terminal_map/map_ink.png`;
  `build_site.py --theme paper` keeps the version-1 look (ink on cold paper `#EDEFF1`, ink `#101214`, photographs as
  charcoal plates); one colour per page (the map station's red `#D8232F`); Young Serif ·
  Newsreader · IBM Plex Mono; single theme. Assets embedded (data URIs) so a page is self-contained.
- Assets come from `../album-art` only: `assets/story-plates/<slug>.png` (the chapter illustration = the promoted MASTER
  drawing, made by `../album-art/scripts/plates.py` (the one generator shared with the videos) via
  `../sas-project-mgmt/scripts/story_plates.py` from the node's photographs + the arcane archive under
  `../sas-project-mgmt/canon/STYLE.md`; promotion + contact sheets: `promote_masters.py`; generation spends image credits —
  only on Steve's say-so), `assets/landmarks/TC_nn.png`,
  `prepared/photos/monochrome/EV_*.jpg` (photos tagged to the theme via `catalog/folklore-gaps.json`),
  `renders/terminal_map/map_ink.png` (the dark map, ARCANE landmark set) + `renders/terminal_map/stations_arcane/`
  (its per-station masks; the paper theme uses `map_storybook_ink.png` + `stations/`, the INK set — the two renders carry
  different drawings, so a mask set only fits its own map). The video session's `station_layers.py --set ink|arcane`
  MUST be re-run for both sets after any map re-render or the glows drift.
- The field guide's sensitivity lines are law on every page: no claim to historical, Indigenous or religious
  tradition; DTES imagery must not exploit vulnerable people; the Far Shore lights never spell anything; real
  festivals are echoed, never named. The colophon carries the disclaimer verbatim.
- Music on a page = the track's web export; video = the YouTube embed by URL only (no local video copies).
- Status is tracked on the sheet's **Storybook** tab (Text · Images · Track audio · YouTube · Page); the
  `storybook` watch source notices page changes.
- **Hosting (Steve, 2026-09-08): this folder is its own PUBLIC git repo** `shiehn/terminal-city-storybook` (ignored by the
  monorepo, same pattern as sas-inference), served by GitHub Pages from `main:/` at
  https://shiehn.github.io/terminal-city-storybook/ (no custom domain yet). Publish = rebuild → `git add -A && git commit
  && git push` inside this folder, only on Steve's say-so (it is public). `AGENTS.md` is gitignored there; `.nojekyll` stays.
