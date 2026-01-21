# Worker Report

Task: WUI-050 — Update check at startup

What changed:
- Added update check helper with URL resolution, local version detection, and version comparison logging.
- Triggered update check on startup in a daemon thread with opt-out via env/app state.
- Added update check tests and documented the env overrides.

Files changed:
- mlx_ui/update_check.py
- mlx_ui/app.py
- tests/test_update_check.py
- tests/test_app.py
- docs/dev.md
- docs/tree.md

Commands run + result:
- make test (pass)
- make lint (pass)
