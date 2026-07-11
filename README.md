# team-and-tasks (tnt)

A single-file, no-install team planning tool: a Notion-style Gantt chart for tracking who is doing what and by when. The name is the idea. tnt is the small charge that gets a stuck project moving, the dynamite that turns a pile of tasks and a loose team into something that actually ships.

Open tnt.html in any browser, nothing to build, nothing to install. Or use the live version via GitHub Pages once it is enabled on this repo.

## Features

A task to subtask hierarchy with collapsible groups. Draggable timeline pills, where you can drag either edge to resize, drag the middle to move, or drag the date labels directly. Multi person assignment per subtask, rolled up to the task level. Per task and per person color coding, with a hover triggered color picker. A dedicated Team section where each person expands into a rollup of everything they are responsible for. Status tracking, to do, in progress, or done, that cycles from a click on the timeline pill, with a live percent complete stat. Drag and drop reordering for both subtasks and team members. Save a snapshot as a standalone HTML file with the current state baked in, so sharing a plan is just sending that one file. Copy the plan as plain text, or export every task and person as a Gantt-style PNG card bundled into a zip.

## Why

Built for coordinating a small event setup team across a handful of workstreams, where a normal shared doc or spreadsheet gets unwieldy fast but a full project management tool is overkill. It is a single HTML file on purpose. Easy to share, easy to fork, easy to keep forever.

## Development history

This tool went through three real stages, reflected in the commit history. First, a prototype: a flat task list grouped by category, with a pair of range sliders per row to set start and end dates. Second, a task and subtask hierarchy: restructured into collapsible task cards containing addable and editable subtasks, with a dynamic team list. Third, the current version: a full redesign with draggable timeline pills instead of sliders, multi person assignment with team level rollups, status tracking, per person and per task color coding, and Gantt-style card export.

## Where this is headed

Next up under consideration: a chat interface inside the tool itself where you describe an event or project in plain language and it drafts the team and task/subtask structure for you, the way an exploded-view diagram in an assembly manual gives you a first draft of how the pieces fit together before you start turning screws. You'd still edit everything by hand afterward — the goal is skipping the blank-page problem, not automating the planning itself.

## License

MIT, see LICENSE.
