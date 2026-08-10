# DemandGen Dashboard

Kanban-style status board for Matan's DemandGen projects — built for the weekly 1:1 with his manager.

**Open:** `index.html` in any browser (double-click, or `open index.html`).

## What it shows
- **Timeline / Ownership / Scope of work** — 3 dropdowns above the board, each showing live counts; they combine (hard filter — non-matching cards drop out of the board entirely)
- **Status Overview** tiles: total, live/ongoing, waiting on others, needs attention — click a tile to highlight (dim, not hide) matching cards, click again to reset
- Board grouped by status (Live → Ongoing → Waiting → Stuck → Didn't Start → In Queue)
- Each card's left edge is colored by urgency (red = due this week, amber = due next week, gray = due later/TBD) — same meaning as the Timeline dropdown
- Click ★ on any card to pin it to "Your Priority Queue" at the top — a personal, click-driven priority list independent of status/deadline, saved to this browser via localStorage
- Click anywhere else on a card (or a Priority Queue item) to open a detail modal — for multi-step projects it shows a checklist with done/pending steps and a progress bar; for single-line projects it just shows the next step
- Deadline chips — dated deadlines auto-flag as "soon" (≤10d) or "urgent" (≤5d/overdue) based on today's date

## Updating it
All project data lives in the `PROJECTS` array inside `index.html`'s `<script>` block. Each project has `status`, `owner`, `urgency` (now/soon/later), `scope` (task/project), `deadline`, `link`, and `next`. `next` is either a plain string (single next step, no tracking) or an array of `{text, done}` objects for multi-step projects — flip `done` to `true` as Matan reports progress on each step. Edit that array (or ask Claude to) whenever any of these change — no build step, just save and refresh.

Tracked in memory: `project_demandgen_dashboard.md`
