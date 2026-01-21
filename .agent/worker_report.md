# Worker Report

Task: WUI-021 — Results browsing + download

What changed:
- Added result file indexing plus a safe download endpoint.
- Rendered per-job result links with view/download actions in History.
- Added tests covering history links and the results endpoint.

Files changed:
- mlx_ui/app.py
- mlx_ui/templates/index.html
- tests/test_app.py

Commands run:
- make test (pass)
- make lint (pass)
