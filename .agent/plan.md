# Plan

Task: WUI-050 - Update check at startup
Acceptance: if online, checks for updates with timeout; if offline, no errors and app works

Assumptions:
- Update check can use a GitHub releases endpoint derived from git remote or UPDATE_CHECK_URL override.
- No UI changes are required beyond logging.

Implementation steps:
1) Add mlx_ui/update_check.py with helpers to resolve the update URL, read the local version, and expose check_for_updates(timeout=...).
2) Implement check_for_updates to fetch the latest version with a short timeout, compare to local, and log a concise message; swallow all network errors.
3) Trigger the update check from app startup in a daemon thread; allow disabling via DISABLE_UPDATE_CHECK=1.
4) Add tests for URL resolution, offline/URLError handling (no exception), and update check logging behavior.
5) Update docs to mention the update check and env overrides if missing.

Files likely to touch:
- mlx_ui/update_check.py
- mlx_ui/app.py
- tests/test_update_check.py
- docs/dev.md or README.md

Verification steps:
- make test
- make lint
