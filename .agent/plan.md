# Plan

Task: WUI-010 — Upload endpoint + local storage
Acceptance: user can upload multiple files; files saved under `data/uploads/` and jobs are created

Assumptions:
- In-memory job records are acceptable until SQLite persistence is added in WUI-011.
- A simple HTML multipart form on the Queue tab is sufficient for initial upload UX.

Implementation steps:
- Add an uploads base directory (default `data/uploads/`) and ensure it exists on startup or on first upload.
- Implement a POST upload endpoint that accepts multiple files and writes them to the uploads directory with unique per-job identifiers.
- Create minimal job records (id, filename, status, created_at, upload_path) stored in memory and returned to the template.
- Update the Queue panel template to show the upload form and render newly queued jobs.
- Add tests that upload multiple files via TestClient and assert files are written under `data/uploads/` and jobs are registered.
- Record test/lint results in `.agent/worker_report.md`.

Files likely to touch:
- `mlx_ui/app.py`
- `mlx_ui/templates/index.html`
- `tests/test_app.py`
- `docs/tree.md`
- `.agent/worker_report.md`

Verification:
- `make test`
- `make lint`
