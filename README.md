# DemandGen Dashboard

Kanban-style status board for Matan's DemandGen projects — built for the weekly 1:1 with his manager.

**Live URL:** https://shmil123.github.io/demandgen-dashboard/ — this is what gets shared with his manager.

**Local file:** `docs/index.html` (open directly in a browser to preview before deploying — double-click, or `open docs/index.html`). The file lives under `docs/` (not the repo root) because GitHub Pages is configured to serve from `main` branch, `/docs` path — same convention as `badge-scanner/`.

## What it shows
- **Timeline / Ownership / Scope of work** — 3 dropdowns above the board, each showing live counts; they combine (hard filter — non-matching cards drop out of the board entirely)
- **Status Overview** tiles: total, live/ongoing, waiting on others, needs attention — click a tile to highlight (dim, not hide) matching cards, click again to reset
- Board grouped by status (Live → Ongoing → Waiting → Stuck → Didn't Start → In Queue → Done)
- Inside a card's detail modal, click "✓ Mark as Done" to move it to the **Done** column (or "↺ Reopen" to bring it back) — saved to this browser via localStorage, same as pinning. ⚠️ This does NOT change the underlying `PROJECTS` data or the deployed site — it's a personal, per-browser override. If Matan wants a project to show as Done for his manager too, he needs to say so explicitly so the `status` field gets set to `"done"` in the data and redeployed
- Each card's left edge is colored by urgency (red = due this week, amber = due next week, gray = due later/TBD) — same meaning as the Timeline dropdown
- Click ★ on any card to pin it to "Your Priority Queue" at the top — a personal, click-driven priority list independent of status/deadline, saved to this browser via localStorage
- Click anywhere else on a card (or a Priority Queue item) to open a detail modal — for multi-step projects it shows a checklist with done/pending steps and a progress bar; for single-line projects it just shows the next step
- Deadline chips — dated deadlines auto-flag as "soon" (≤10d) or "urgent" (≤5d/overdue) based on today's date

## Updating it
All project data lives in the `PROJECTS` array inside `docs/index.html`'s `<script>` block. Each project has `status`, `owner`, `urgency` (now/soon/later), `scope` (task/project), `deadline`, `link`, and `next`. `next` is either a plain string (single next step, no tracking) or an array of `{text, done}` objects for multi-step projects — flip `done` to `true` as Matan reports progress on each step. Edit that array (or ask Claude to) whenever any of these change — no build step, just save and refresh locally.

## Deploying
Editing the local file does **not** update the live URL by itself — it only updates once pushed. Deploy with:
```
cd demandgen-dashboard
git add -A && git commit -m "update dashboard" && git push
```
GitHub Pages rebuilds automatically, usually live within ~30–60 seconds. Matan's workflow: he edits/asks Claude to edit the dashboard locally over multiple turns, then explicitly asks to "update/deploy the dashboard online" — only then should this push happen, not after every single local edit.

Tracked in memory: `project_demandgen_dashboard.md`
