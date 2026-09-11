# Terminal City storybook — changelog

The site is regenerated, never hand-edited: pages come from the field guide (`album-art/catalog/folklore.json`)
and the asset catalogs via `sas-project-mgmt/scripts/storyboard_page.py` / `build_site.py`. Bump `VERSION` and add
an entry here whenever the look, the beat order, or the page anatomy changes; content changes (a new field-guide
draft, a new photo) do not bump the version — the colophon on every page already names the draft and build date.

## 0.8.1 — 2026-09-11

- **One tap on touch.** Steve, on a Galaxy S25 in Chrome: "it requires two clicks .. the first turns the hyperlink image red,
  and the second performs the navigation .. this is bad .. on mobile it should just be one click". The tap-to-light step is
  gone; a tap navigates, with the red glow flashing on press. Hover, keyboard focus and the current-station state are unchanged.
- The Crows landmark redrawn without lettering (video session), and the station masks are now cut per map render: the
  dark map's set for the dark site, the ink map's set for the paper look, so every glow sits on its own drawing.

## 0.8.0 — 2026-09-10

- **The drawn elements are the map.** Steve: "the map looks great. But I think the hyperlink numbers are lazy. what I want
  is the same map, but each element glows red when mouse over or click .. and stays red when in focus" — then, on the
  preview, "go live". The numbered chips are gone from the home map and the chapter maps; each drawn element is the link,
  glowing red on hover and keyboard focus, and the current chapter's element stays red on its own map. Touch: tap to
  light, tap again to open. Built on per-station masks cut from the map (`album-art/renders/terminal_map/stations/`); the
  station anchors now come from the ink layout (a layout mix-up with the video map was fixed on the way). Same map image.
  No image credits spent.

## 0.7.0 — 2026-09-10

- **Node 04 is The Clock.** Steve: "We have decided that element Skytrain needs to be renamed and re-written to [his
  text] please update all assets accordingly" — his text, verbatim, is the chapter
  (`sas-project-mgmt/canon/drafts/the-clock-2026-09-10.md`; Field Guide Draft 0.9). Hook "Every city needs a clock.
  Vancouver rides inside its."; rule "If the SkyTrain chime lands exactly on the beat, don't check the time. The Clock
  already has it." The page lives at `clock/`; `skytrain/` redirects there. The drawing is unchanged (the SkyTrain is
  the real thing; only the node is renamed). No image credits spent.

## 0.6.0 — 2026-09-10

- **The daily cycle as a second ordering.** The home page has an "Album order / Daily cycle" switch: album order stays
  the default and the page order; the cycle view lists the fifteen timed nodes in the guide's order with the time of day
  beside each, then "Off the clock" (Green Static, the Endless Stair, the Beyond, Far Shore). In the cycle view only, each
  map station carries a small monochrome position mark. Chapter field notes open with the node's place in the day.
- **SkyTrain** everywhere, from Field Guide Draft 0.8 and the re-rendered map; the map cartouche carries no draft number.
- **About copy**: the preface ends with the guide's line "Maintenance is not the point of the city. Maintenance exists so
  people can eventually stop working."
- **Re-drawn masters** for Eternal Night (raw 62bddb8675), the 3:17 Freight (a2c09dd9bf), Far Shore (e60ec3f7db, now
  drawn from a North Shore photograph) and the Nocturnals (216763e69b), promoted by the video side on Draft 0.8 evidence.
- **Audio and video gates**: a player appears on a chapter only when its track audio is final and the web export exists
  (title and BPM only); the video embed only when a URL exists. No chapter is final yet.
- Steve: "please make sure all this feedback is addressed and implemented" (the site review,
  `sas-project-mgmt/feedback/2026-09-10-site-review.md`), the approved plan, then on the preview: "push". Built on Draft
  0.8; no image credits spent by the storybook.

## 0.5.0 — 2026-09-10

- **An album, not a wiki.** From the site review Steve collected (`sas-project-mgmt/feedback/2026-09-10-site-review.md`;
  Steve: "please address all of it" · "We should update the field guide accordingly" · on the preview: "copy it, and push").
  Built on Field Guide Draft 0.8; masters unchanged; no image credits spent. Chapter anatomy: chapter ·
  BPM · a small cold role tag → the video slot (the YouTube embed when a video exists, the master plate until then) →
  a one-line hook → the story → the rule → field notes, collapsed (where + the map, a photograph, known associations)
  → next chapter (hook + plate) → prev / map / next. The 19-station map leaves the page body for the field notes.
- **Scaffolding off the public page**: track filenames, "master not yet cut", draft hashes, photo-anchor and disturbance
  notes, map symbols, the cards' job text, status words, connection sentences. Colophon = version + the disclaimer;
  the guide draft + sha1 live in an HTML comment for the sync check.
- **Stories**: an editing pass on all 19 with a hook each — less explanation, more subtext; Eternal Night and Far Shore
  retold on the review's line, now canon in Draft 0.8; the Nocturnals' rule is in-world; 3:17 arrives with the train;
  "SkyTrain" as the public spelling.

## 0.4.1 — 2026-09-10

- **Navigation** (Steve: "it should be easier to get back to the home page… the maps should always be clickable… highlight
  the current location but add a hyperlink/rollover everywhere"). The "Terminal City" title on every chapter links to the
  map; every station on every map (chapter pages and the home page) is a link with a rollover chapter name; the current
  chapter's station stays highlighted in red; the map caption links to all chapters.

## 0.4.0 — 2026-09-10

- **The dark ground.** Steve on the paper version of 0.3.0: "I don't love the new washed out storybook art… it's not the
  images but I don't like the mostly white look"; on the dark mock: "yep, darkness better". The page ground is now the
  drawings' own black (`#0B0C0D`), type off-white (`#EDEFF1`), captions and hairlines in graphite (`#A9B1B8` / `#2A2F34`),
  the one red accent unchanged. The masters are unchanged and shown native: white line on black, no inversion, no curve,
  no blend. The map is the video side's white-line layer (`renders/terminal_map/map_ink.png`), so book and videos share
  one map; landmark thumbnails are ink-inverted to off-white. Builder: `build_site.py --theme dark|paper`, dark default.
  No image credits spent.

## 0.3.0 — 2026-09-10

- **Masters under the style guide.** Every chapter's illustration is now a hybrid drawing made from the node's own
  photographs plus the arcane engraving archive (`sas-project-mgmt/canon/STYLE.md`, approved by Steve 2026-09-10 with
  the Repair People plate as the reference specimen): one source photograph per master, geometry locked to it, drawn in
  the archive's white-line engraving language and shown here inverted to ink on cold paper. Three takes were made per
  node; the promoted take is recorded in `stories/stories.json` (`master`), the contact sheets live under
  `album-art/assets/story-plates/sheets/` for later swaps. The earlier pencil-illustration plates are retired.
- Chants retired (0.2.3). Field notes carry the card's rule only.

## 0.2.3 — 2026-09-10

- **Chants retired** (Steve, T62: "1, gone"). Field notes now carry only the card's rule; the 0.5 chants stay in
  `folklore.json` under `legacy` as provenance and are not printed.

## 0.2.2 — 2026-09-09

- **Field guide Draft 0.7.** 19 chapters in the guide's list order (not tempo order), the 3:17 Freight new; all
  19 stories retold from the 0.7 dossiers (JOB · OPERATING LOGIC · CONNECTIONS · VISIBLE EVIDENCE · RULE); four plates
  regenerated where the scene changed (the Morning Meeting is one Repair Person feeding reporting crows, the
  Nocturnals are tracks and shadows rather than a cast of animals, the Eternal Night is forgotten built space, the
  Freight is new). The map page gains a short preface and the guide's north star. Card fields the draft leaves
  empty (phase, BPM off the ten anchors) no longer print.

## 0.2.1 — 2026-09-09

- **Placeholder slots get no chapter.** The Open Slot is a placeholder in the guide (role "placeholder", place
  "Unassigned"), not an element; its page is gone and the book is 18 chapters, Terminal Fog looping back to the
  Morning Meeting. The builder skips any card the guide marks that way.

## 0.2.0 — 2026-09-08

- **The page is now a short story** (Steve: "turn it into a short story — each of the 19 elements its own title,
  a few paragraphs and a generated image", preteen/teen reading level). Chapter anatomy: title · the illustration ·
  the story · field notes (the card's rule + chant) · the map (station marked) · a photograph if one is tagged ·
  connections · next chapter · listen / watch · cycle nav · colophon. The seven-beat storyboard order stays the
  video template's; the storyboard timing labels are gone from the page.
- **Story source**: `stories/stories.json` — one retelling per card, keyed by slug, stamped with the guide draft +
  sha1 it was written from. The guide stays canon; a page whose story was written from an older draft is flagged
  in red until the retelling is re-checked. Never hand-edit the story in a page — edit `stories.json`, rebuild.
- **Illustrations**: `album-art/assets/story-plates/<slug>.png`, one pen-and-ink plate per chapter generated by
  `sas-project-mgmt/scripts/story_plates.py` (gpt-image-2, the map landmarks' ink language, greyscale; prompt cached
  in `raw/`). Missing plate → the map landmark stands in, labelled; no landmark → a labelled empty frame.
- Rebuilt for field guide **Draft 0.5** (19 chapters; the Open Slot has a page: "An empty slot is not a missing
  one"). Colophon carries the Draft 0.5 disclaimer verbatim and now stamps the stories' draft too. Home page:
  stations not yet placed on the map are hidden from the map layer but stay in the chapter list.

## 0.1.0 — 2026-09-07

- First page: The Morning Meeting (TC_01), as the seven-beat storyboard — the map (station marked) · picture ·
  the element · picture · connections graph · the story · prelude to the next phase — then listen / watch, the
  cycle navigation, the colophon.
- Visual world v1: ink on cold paper, photographs as charcoal plates, one colour (the map station's red).
  Young Serif · Newsreader · IBM Plex Mono. Single theme.
- Steve: "decent start". Open: paper or dark; the typefaces; landmark or photograph first.
