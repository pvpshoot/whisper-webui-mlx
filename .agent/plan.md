# Plan

Task: WUI-021 — Results browsing + download

Acceptance: history page shows per-job links to view/download TXT and other generated formats

Assumptions:
- Results live under `data/results/<job_id>/` and are safe to expose via file download routes.
- Job history already exists and includes job IDs that map to results directories.

Implementation steps:
- Review current history rendering in `mlx_ui/templates/index.html` and job metadata access in `mlx_ui/app.py` to confirm what fields are available per job.
- Add a helper to list result files for a job by scanning `data/results/<job_id>/`, filtering non-files, and sorting deterministically.
- Add a download/view endpoint (e.g., `/results/{job_id}/{filename}`) using `FileResponse`, with path traversal protection and 404 for missing files.
- Update the History section in the template to show per-job lists of result links (TXT emphasized) and a “no results yet” fallback.
- Extend tests to create fake result files and assert history renders links and download endpoints return file content.

Files likely to touch:
- `mlx_ui/app.py`
- `mlx_ui/templates/index.html`
- `tests/test_app.py`

Verification steps:
- `make test`
- `make lint`
