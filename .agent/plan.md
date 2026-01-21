# Plan

Task: WUI-002 — Minimal WebUI shell
Acceptance: localhost page renders with tabs: Queue + History, using server-side templates

Assumptions:
- A simple Jinja2-rendered HTML page with placeholder content satisfies the "shell" requirement.

Implementation steps:
- Add Jinja2 template rendering for the root route and pass the request context.
- Create a minimal HTML template that renders two tabs (Queue, History) with placeholder panels.
- Keep the layout lightweight and offline-friendly (no external assets).
- Update the root test to assert an HTML response and presence of "Queue" and "History" text.
- Update docs tree if a new templates directory is added.
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
