# Plan

Task: WUI-011 — Persistent job store (SQLite)
Acceptance: jobs survive server restart; history page lists prior jobs

Assumptions:
- Use a single SQLite DB file under `data/` (for example `data/jobs.db`) with a lightweight table for jobs.
- The existing Queue/History view can read from the same persisted store for now (no new UI fields required).

Implementation steps:
- Add a small SQLite-backed job store (schema + CRUD helpers) and initialize it on startup.
- Replace in-memory `app.state.jobs` reads with DB queries ordered by creation time.
- Update the upload handler to insert job rows into SQLite after writing files to disk.
- Ensure the root page renders persisted jobs for both Queue and History views.
- Update tests to use a temporary DB path and verify jobs persist across a simulated app restart.
- Update `docs/tree.md` if new modules or data paths are added.
- Record test/lint results in `.agent/worker_report.md`.

Files likely to touch:
- `mlx_ui/app.py`
- `mlx_ui/db.py` (or similar new module)
- `tests/test_app.py`
- `docs/tree.md`
- `.agent/worker_report.md`

Verification:
- `make test`
- `make lint`
