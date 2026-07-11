# team-and-tasks (tnt)

## What this is

A single-file, no-install team planning tool: a Notion-style Gantt chart for tracking who is
doing what and by when. Everything — markup, styles, and logic — lives in one `.html` file with
no build step. Open it in any browser and it works.

## The name

tnt is the small charge that gets a stuck project moving — the dynamite that turns a pile of
tasks and a loose team into something that actually ships. That's the whole pitch: a plan you
can open in one click, edit in place, and hand to someone else as a single file.

## Why it exists

Built originally for coordinating a small event-setup team (an NYU ITP / Creative Equity
Initiative screening event) across a handful of workstreams — venue, program, guests,
marketing — where a shared doc or spreadsheet got unwieldy fast, but a full project-management
tool was overkill. The single-file constraint is deliberate: easy to share, easy to fork, easy
to keep forever, no account or server required to use it.

## Repo

https://github.com/brianjbishop/team-and-tasks

Public, MIT licensed. GitHub Pages is enabled on `main` / root, so the live tool is also
served at https://brianjbishop.github.io/team-and-tasks/.

## Files

- `tnt.html` — the real, current tool. This is what most work should happen in.
- `index.html` — a tiny static redirect stub to `tnt.html`, so GitHub Pages (which only serves
  `index.html` at the site root) keeps working at the existing public URL. Not the app itself —
  don't add logic here.
- `README.md` — public-facing description (features, why, dev history).
- `LICENSE` — MIT.

The two earlier prototype stages (`v1-prototype.html`, `v2-hierarchy.html`) have been removed
from the working tree — the evolution is still browsable through the commit history on `main`,
just not as standalone files anymore.

## Current feature set (in `tnt.html`)

- Task → subtask hierarchy with collapsible groups.
- Draggable timeline pills — drag an edge to resize, the middle to move, or the date labels
  themselves.
- Multi-person assignment per subtask, rolled up to the task level.
- Per-task and per-person color coding (two separate palettes), with a hover-triggered color
  picker.
- A dedicated Team section: each person expands into a rollup of everything they're
  responsible for, with an inline status dropdown.
- Status tracking (to-do / in progress / done) that cycles from a click on the timeline pill's
  icon, feeding a live "% complete" stat.
- Drag-and-drop reordering for both subtasks and team members.
- Save — downloads the current state as a standalone `.html` snapshot with the data baked into
  a small `<script type="application/json" id="initial-data">` tag, so sharing a plan is just
  sending that one file and opening it reloads exactly where you left off. There is
  intentionally no separate "Load" button — the saved file *is* the loaded state.
- Copy plan as plain text, or export cards to PNG bundled into a `{title}-tnt.zip`. Each card
  mirrors its live counterpart rather than a generic gantt row: task cards keep the timeline
  pill/track with assignee avatars on the right of each subtask line; team/person cards drop
  the timeline entirely and instead look like the live Team rollup — light task-colored rows,
  no dates, status text on the right, and an initials avatar next to the person's name. Files
  are named `task-{label}.png` / `team-{name}.png` inside the zip.

## Working conventions

- Keep it a single file. No bundler, no npm dependencies beyond the two CDN scripts already in
  `<head>`/`<body>` (`html2canvas`, `JSZip`). Anything else should be justified against that
  constraint before it's added.
- Two distinct color palettes exist on purpose: `COLORS` for tasks, `PERSON_COLORS` for people.
  Don't merge them.
- The `initial-data` script tag is the single source of truth for "what state does this file
  open with." `serializeState()` / the load-on-boot logic near the bottom of the script both
  read/write that shape: `{ planTitle, planStart, planEnd, team, tasks }`.

## Development history

Reflected in the commit history on `main`: prototype → task/subtask hierarchy → the current
drag-pill, multi-assignee, save/export version. The first two stages used to live on as their
own standalone files (`v1-prototype.html`, `v2-hierarchy.html`) for browsability; they've since
been removed from the tree, so the evolution now lives in the commit history only.

## Plans / next steps

- **Deployment**: currently just static GitHub Pages serving `index.html` (a redirect stub) →
  `tnt.html` — no backend, no persistence beyond the save-a-file model. That's the current
  ceiling: a plan only exists as a file someone is holding, so there's no shared "live" state
  between collaborators unless they keep re-sending saved snapshots.
- **Live/shared state (under consideration)**: a Supabase backend (Postgres + Supabase
  Realtime) with the frontend deployed on Vercel, so a plan could live at a URL and update
  live for everyone looking at it, instead of round-tripping saved `.html` files. Not started —
  this would be a real architectural change (multi-file app, build step, hosting, auth for who
  can edit), so it's a deliberate step up in complexity from the single-file philosophy above
  and should be scoped as a distinct fork/branch of the project rather than bolted onto
  `tnt.html`.
- **Chat-driven previs (under consideration)**: a chat interface inside the tool where you
  describe an event or project in plain language and it populates the team and task/subtask
  structure for you — a first-draft "exploded view" of the plan (like the assembly diagram in
  a furniture manual) rather than a blank Gantt chart. You'd still edit everything by hand
  afterward; this is about skipping the blank-page problem, not about full autonomy. Needs an
  LLM API call, which is a step away from the fully offline/no-account philosophy above, so
  scope it carefully (e.g. bring-your-own-API-key) before building.
- **Card export polish**: the PNG export (`buildTaskExportCard` / `buildPersonExportCard` in
  `tnt.html`) is meant to mirror the corresponding live UI section as closely as possible —
  task cards mirror the subtask timeline rows, person cards mirror the Team rollup. Keep both
  in sync if the live styling changes, since it's a separate code path (`html2canvas` renders
  an off-screen DOM clone, not a screenshot of the real UI).
- Everything above should stay scoped to `tnt.html` unless a decision is made to actually
  branch into the Supabase/Vercel version — don't let backend work leak into the static file
  by accident.
