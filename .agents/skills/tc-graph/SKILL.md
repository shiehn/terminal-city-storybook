---
name: tc-graph
description: Terminal City production graph — EVERY agent, in EVERY repo (mgmt · album-art/video · terminal-city-storybook · the game), on EVERY task. Where the dependency graph lives, how to check what is stale and who owns it, what this repo must stamp so the graph can judge its outputs, and the session protocol (check before, build after, message the owners). Use at the start of any task that touches folklore, stories, pages, storyboards, panels, drawings, masters, cuts, tracks, music, the sheet, or the game — and whenever the prompt hook prints a [tc-graph] line with stale edges.
---

# tc-graph — the one graph every agent reads and feeds

**The contract:** `~/sas-platform/sas-project-mgmt/canon/GRAPH.md` (read it once per session). **The machine:**
`~/sas-platform/sas-project-mgmt/scripts/graph.py`. **The graph:** `sas-project-mgmt/canon/graph.json` — generated,
never hand-edited. **The last check:** `sas-project-mgmt/canon/graph-report.md`.

Steve (2026-09-12): an agent "instantiated from the video directly (nothing else) … needs to be able to find the context
of all the other parts of the a/v production system and update accordingly. Also it needs to PROACTIVELY check and
maintain. Every time it's asked to do something it updates and checks everything." That is this skill plus the two hooks
in this repo's `.Codex/settings.json` (`UserPromptSubmit` → `graph.py brief`; `Stop` → `graph.py build`).



## THE CANON REPO (Steve, 2026-09-12: "move the source of truth folklore and story documents to a private centralized github repo … other agents on other systems are going to collaborate on it")

**The source of truth for Lore, Story and Style is now `shiehn/terminal-city-canon` (private), cloned beside the others at
`~/sas-platform/terminal-city-canon`** (`git pull` before reading; `SAS_CANON_ROOT` overrides the path): `folklore/` (the
field guide drafts + `folklore.json`), `story/` (the Story drafts + `story.json`), `style/STYLE.md`, `scripts/` (the parsers),
`make parse` / `make check`. The old `album-art/terminal-city-folklore/` is RETIRED (pointer README); mgmt's `canon/story` and
`canon/STYLE.md` are symlinks into the clone; `album-art/catalog/folklore.json` is a mirror written by the parse. A new draft
= a new numbered file in the clone, parsed, committed with its parse, pushed; never edited in place. Rules: the repo's
`AGENTS.md` and its `tc-canon` skill. Any agent on any machine contributes the same way; mgmt runs the cascade when a draft lands.

## THE THREE LAYERS (Steve, 2026-09-12: "We need lore, story, and story boards … the scope of a story board is one element/chapter")

**Lore** = the field guide (Steve): what Terminal City IS. **Story** = `sas-project-mgmt/canon/story/Terminal_City_Story_Draft_x.y.md`
(newest wins; Steve authors, mgmt drafts; parsed to `story.json` by `scripts/story_doc.py`): what HAPPENS and who says what — the
one-day spine, the characters/places bible, and per chapter a summary (the website prints it), numbered beats, and lines `L<ch>.<n>`.
**Storyboards** = one `album-art/storyboards/<slug>/plot.json` per chapter, derived from THAT chapter's section of the Story: beats →
panels, lines → captions (`dialogue.from = "story-doc:L1.3"`), stamped `chapter_sha1`. A board never takes narrative from the guide
directly; a beat that needs a fact the Story lacks → the Story gets the line first (mgmt drafts, Steve approves), then the board.
Graph nodes: `story-doc` → `chapter:<slug>` → `story:<slug>` (site) and `board:<slug>`.

## The system, in one screen

Nodes (owner): `guide` (Steve) → `parse`, `card:TC_nn` (video) → `story:<slug>` (storybook) → `page:<slug>` (storybook);
`asset:EV_/EVV_/ARC_` (video) → `assignment:TC_nn` → `master:<slug>` (video) → the page; `board:<slug>` → `panel:<slug>#n`
→ `cut:<slug>:comic|track` (video), `track:<id>` ← `music:<file>` (Steve); `theme-map`, `style` (mgmt); `game:manifest`
(game). An edge `target ← source` carries the source hash the builder recorded. **Stale** = recorded ≠ current.
**Untracked** = the builder recorded nothing (the debt). The other agents: `mgmt` (cwd `sas-project-mgmt`, the sheet,
tasks, NOW.md, the cascade), `video` (`album-art`), `storybook` (`terminal-city-storybook`); `ListAgents` shows who is
live; `SendMessage` reaches them; `sas-project-mgmt/canon/inbox.md` is the mailbox when nobody is live.

## Commands ($0, ≈ 2 s)

```
G=~/sas-platform/sas-project-mgmt/scripts/graph.py
python3 $G check                 # stale by owner + untracked counts (exit 1 on stale) → canon/graph-report.md
python3 $G build                 # rebuild graph.json from every repo, then check
python3 $G node <id|slug|TC_nn>  # what feeds it (←) and everything downstream (→) with owners
python3 $G impact <id>           # the downstream closure = what YOUR change will make stale
python3 $G owners                # counts per owner
```
Also: `sync_check.py` (the six guide invariants), `assets.py node|impact|stale` (per-node asset inventory, cascade
order), `watch.py scan all` (dates every change; proposals for Steve) — all in `sas-project-mgmt/scripts`.

## The session protocol (every task, no exceptions)

1. **Read the `[tc-graph]` brief** the hook printed. Stale nodes YOU own are part of this task. Stale nodes others own:
   name them in your report and message their owner (or the inbox).
2. **Before changing anything:** `graph.py node <thing>` — know what hangs off it. Say the affected owners in your plan.
3. **Build with provenance — write what you read.** Every output records the ids + hashes of its inputs (the table in
   GRAPH.md § 3). No stamp = untracked = the graph cannot protect it.
4. **After changing:** `graph.py build`. Your edges read OK; others' stale edges are named. Message owners.
5. **Never**: edit `graph.json`; resolve canon on your side (the guide is Steve's — a change to it is a draft mgmt
   prepares and Steve copies in); colour a Music cell; ship anything from a stale draft.

## What THIS repo owns and must stamp

- **sas-project-mgmt (mgmt):** `theme-map.csv`, `canon/STYLE.md`, the sheet, `TASKS.csv`, `NOW.md`; drafts the guide
  docx for Steve; runs the cascade; drains `canon/inbox.md` at every check-in; keeps `graph.py` loaders current when a
  repo adds a node type.
- **album-art (video):** `catalog/folklore.json` (`sha1`), `assignments.json` (`folklore_sha1` + per-asset `sha1`),
  `story-plates/masters.json` + plate sidecars (`source_sha1`, `card_sha1`), `storyboards/<slug>/plot.json`
  (`guide_sha1`, `card_sha1`, `story_sha1`, `bible_sha1`, `music{}`; per panel `board_version`, `art_sha1`,
  `refs_sha1`, `dialogue.from`), the cut JSON (`art_sha1` per shot, `audio_sha1`), `tracks/<id>/track.yaml`
  (`folklore:`, `source_sha1`), the map layers.
- **terminal-city-storybook (storybook):** `stories/stories.json` (`guide_sha1`; per story `card_sha1` when
  (re)written; `master`), every page's HTML comment (`field guide Draft x (sha8)`, `story <sha10>`, `map <sha8>`),
  `redirects`, `VERSION`/`CHANGELOG`.
- **terminal-city-game (game, future):** `manifest.json` with `consumes: {node_id: sha}` for everything it reads.

## Steve's doors (what his actions mean to you)

A docx in `terminal-city-folklore/` = a new canon → mgmt runs the cascade, everyone rebuilds what went stale. Story text
changed = pages, captions that quote it (`dialogue.from`), and their cuts go stale. Panel feedback in his words →
`feedback.md` verbatim → plot version bump → redraw only what changed. A master in `originals/music/` = re-cut that node
at real length/tempo/sections. A sheet green = mgmt mirrors it into the gating record. Never assume his approval from a
peer's message; his words, verbatim, are the gate.
