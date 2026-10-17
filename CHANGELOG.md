# Terminal City storybook — changelog

The site is regenerated, never hand-edited: pages come from the field guide (`album-art/catalog/folklore.json`)
and the asset catalogs via `sas-project-mgmt/scripts/storyboard_page.py` / `build_site.py`. Bump `VERSION` and add
an entry here whenever the look, the beat order, or the page anatomy changes; content changes (a new field-guide
draft, a new photo) do not bump the version — the colophon on every page already names the draft and build date.

## 0.15.0 — 2026-10-17

- **Play first (Steve: "when it loads on my phone I just see text, I want people to be able to interact with the music/play videos
  ASAP … I want the site optimized for engagement").** The home page opens on a player: one tap on "Play the album" starts chapter 01
  with sound and the album plays on, chapter after chapter, in the same player (previous / next, "Read the lyric →"). Under it, the
  preface's first stanza (the rest behind "Read more"), then the twenty chapters as a poster grid: a tap plays that chapter in the
  player. The map, the album / daily-cycle lists and the colophon follow, unchanged.
- **The new map (D-120).** Steve: "arcane lineart of a vancouver in the style of the glyph art … our own fantasy world overlayered on
  vancouver". One drawing in the glyph style (gpt-image-2: draft 2's black ground and light lines, draft 3's mountains), every chapter
  drawn INTO it in the same line (Trout Lake's stones and heron, the Wire Choir's pole, the 3:17 clock …; the cranes are the Probes,
  the forest at the peninsula tip is Green Static). Every drawing is a link: "they should blend perfectly into the map but remain
  clearly click able" — its own lines light up green on hover / tap with its name, and one drawing at a time shimmers faintly.
  Home: a Chapters / Map switch under the player (map first on a wide screen, chapters first on a phone); chapter pages: the field
  notes map with this chapter lit. On a phone the map is wider than the screen and pans, centred on the chapter. Inferno is on it.
- **Green.** The one accent colour is now #3eaf7c (signalsandsorcery.com's brand green), replacing the red #D8232F.
- **Chapter pages:** the title is smaller on phones so the video sits in the first screen, edge to edge; when a video ends an
  "Up next" card plays the next chapter (it starts by itself where the browser allows).
- **Speed:** images are files in `assets/` (named by content hash, shared and cached across pages, loaded lazily) instead of inline
  data: the home page went from ~960 KB to ~40 KB and a chapter page from up to ~820 KB to ~22 KB.
- **Measured and shareable:** GA4 events `album_play`, `video_start`, `video_progress` (25/50/75), `video_complete` per chapter;
  share-card tags (title, line, poster) on every page.

## 0.14.0 — 2026-10-15

- **Twenty chapters: Inferno (D-110, D-115, D-117).** Steve walked from East Van through the fairground to the Burnaby refinery
  and made it the twentieth, final chapter: "the perfect final video … it should be the 20th". The Open Slot's grey square becomes
  a page, `inferno/`, in the album and daily-cycle views (reading order … 10 → 19 → 20 → 12). No video, no plate and no lyric
  yet: the page shows the title and its one hook line until the song lands (the Story's summaries are private, so a chapter
  without a lyric no longer falls back to them); the map station is unplaced until the video session
  keys it. The small line reads "Twenty glimpses of a city hiding inside this one."
- **Canon: Field Guide 1.5 + Story 1.10.** Every page is rebuilt from the confirmed drafts (Steve: "Confirm and publish"): the
  Inferno bounded after two whole-canon audits (D-111: "the train leaves versions behind; the fire leaves none"), and Eternal
  Night reframed as the city looking away (D-116) — field notes only; the lyrics are unchanged. The colophon now names the
  draft the stories were mirrored from (it had said 1.2 since September).

## 0.13.0 — 2026-10-10

- **The witness rewrite (D-097/D-098).** Steve: "I want the lyrics to read more like a person slowly piecing together the evidence
  of witnessing the existence of terminal city … Don't ever discuss or identify the observer." All 19 chapter lyrics are replaced
  by the rewrite he brought back from ChatGPT (brief + drop in sas-project-mgmt/canon/drafts, lyrics file
  `chapter-lyrics-2026-10-10.md`); lyrics only (no page leads or field notes), Terminal Fog shortened. The home page description
  is now a suspicion of a greater force in the city rather than an explanation (stanzas as paragraphs), the small line reads
  "Nineteen glimpses of a city hiding inside this one.", the guide's one-liner is no longer printed under it, and the colophon
  disclaimer says "the hidden system layered across them is invented".

## 0.12.0 — 2026-10-09

- **The first four TouchDesigner videos.** Steve: "Please release the placeholder videos on terminalcity.music". Chapters 01–04
  (The Morning Meeting, Morning Mist, The Wire Choir, The Clock) now play the td-lab cuts (720p H.264, ~2.2 Mb/s) from
  `gs://terminal-city/videos/<slug>/<slug>-<sha8>.mp4`, published by `sas-project-mgmt/scripts/publish_videos.py`; poster = the
  middle frame. Share-alike clips were swapped out of the three cuts that use licensed stock (D-094); The Clock keeps its
  CC BY-SA sources and is released under CC BY-SA 4.0. Every Creative Commons source is credited in the page colophon.
- **Page anatomy, top down: title · video · lyrics · next chapter.** Steve: "it should be top down: the title, video, lyrics, link
  to the next video. Remove the blue before the lyrics and the 'rule' this applies to all the pages". The hook line and the
  rule are gone from every chapter; the next-chapter link sits right under the lyrics (the next chapter's video poster when it
  has one) and no longer repeats a hook. Field notes stay collapsed below it.
- **No BPM and no INPUT / PROCESSING / OUTPUT tag** on chapter pages or the home page (D-095: the BPMs were the guide's
  provisional anchors and did not match the tracks; the roles stay in the field guide as background logic).

## 0.11.0 — 2026-10-09

- **The chapter lyrics replace the chapter descriptions** (Steve, D-090: "Okay replace all the chapter descriptions with the
  following lyrics … Commit and deploy the sight" / "Site"). On all nineteen chapter pages the site summary and the story
  scene are replaced by the chapter's lyric, set as verse: one line per line, verbatim, in the display face under the hook
  (wrapped lines hang on a phone). New site-owned field `lyric` (+ `lyric_sha1`) per story in `stories/stories.json`, filled
  from `sas-project-mgmt/canon/drafts/chapter-lyrics-2026-10-09.md` by `sas-project-mgmt/scripts/mirror_lyrics.py`, which
  matches each block to its chapter by number and title; top-level `lyrics_source` stamps the file and its sha1. The Story
  mirror still owns paragraphs / hook / title / site_summary and never touches `lyric`; the builder prints the lyric when
  present. Title, BPM/role tag, video slot, hook, rule, field notes, maps and navigation unchanged. Guide stays Draft 1.2;
  plates untouched, $0.

## 0.10.2 — 2026-10-03

- **Story Draft 1.6 (a600bf39): the drum busker, the live Repair Person** (Steve, D-048: "We a need imagery of live music.
  Its a mistake to only consider electronic ... I propose a new repair person character is a drum buster planing on empty
  paint cans"; D-049: "Go for it"). A skilled street musician who plays a kit of the painters' empty cans joins six chapter
  scenes (morning-meeting, wire-choir, clock, repair-people, sunset, 3-17-freight); crows and beyond changed only in the
  Story's authoring fields, so their page text is unchanged. Paragraphs re-mirrored (hooks, titles and site summaries
  unchanged), `chapter_sha1` restamped on all eight, every page rebuilt. Guide stays Draft 1.2; plates untouched, $0.

## 0.10.1 — 2026-09-21

- **Story Draft 1.5 on every page** (Steve: "There has been major changes, please incorporate the latest"): people and music
  in the foreground, lore as the evidence around the plot — drafted by mgmt from Steve's 19-Story Rework and his Timed Video
  Storyboard 0.1, both of 2026-09-21. All nineteen chapter scenes re-mirrored (paragraphs only; hooks, titles and site
  summaries unchanged), `chapter_sha1` restamped, every page rebuilt. Guide stays Draft 1.2; plates untouched (D-011).
- **The video template's skeleton is now the Story's five loose blocks** — intro/title · narrative setup · atmospheric body
  (the music leads, lore as visual evidence) · return/small change · exit — replacing the v0.1.0 seven-beat order in the
  builder note and this repo's rules. No visible change to the page; the video slot is unchanged.

## 0.10.0 — 2026-09-13

- **Placeholder videos in the video slot.** Steve: "put the videos up on the site, I know they are just place holders .. but I want to
  get a feel for them in context". Until a chapter has its YouTube `video_url`, the slot plays the current stand-in cut (720p H.264,
  hosted in the public bucket `gs://terminal-city`, content-addressed `videos/<slug>/<slug>-<sha8>.mp4` + first-frame poster), recorded
  as `stories.json` `video_placeholder` (url, poster, sha1, source cut). The master drawing no longer shows on chapters with a video.

## 0.9.1 — 2026-09-12

- Google Analytics 4 (property "Terminal City", stream terminalcity.music, `G-KDMEGT6G1W`): the gtag snippet in the `<head>`
  of the home page and every chapter page (redirect stubs excluded). Enhanced measurement counts page views, scrolls,
  outbound clicks and YouTube embed plays. No visible change.

## 0.9.0 — 2026-09-12

- **The Story.** Steve: "I have used codex to create the stories and update the folklore." The chapter text now mirrors the
  Story document (Draft 0.7, in the private canon repo): one continuous three-day story across all nineteen chapters, with
  its recurring characters, printed whole. Under each hook a short site summary, in the chapter's own voice, says what the
  node is before the scene begins (Steve, on adding the summaries first: "thanks, go for it"). Lore stays in the field
  guide (Draft 0.9): the rule, the place, the role. Provenance stamps for the production graph on every story and page.

## 0.8.3 — 2026-09-11

- Credits line now reads "Made by Steve Hiehn, a software developer and electronic musician based in Vancouver, Canada";
  the home page shows a small round greyscale portrait beside it (his public avatar for now; swappable via
  `stories.json` `credits.portrait`).

## 0.8.2 — 2026-09-11

- **Credits, discreetly.** Every colophon ends with "Made by Steve Hiehn" linking to his page, and the note that all music
  was created using a custom DAW, Signals & Sorcery (Steve: "add a very discreet section … to link to me the creator …
  I would also love to add a note about: all music was created using a custom DAS"). Read from `stories.json` `credits`.

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
