# Worker Report

Task: WUI-020 - Integrate `wtm` CLI transcription

What changed:
- Added a WTM-backed transcriber that builds the CLI command with language/output dir and validates TXT output.
- Switched the worker default transcriber to the WTM implementation.
- Added a subprocess-mocked transcriber test to avoid running the real model.
- Updated the project tree docs to include the new test file.

Files changed:
- mlx_ui/transcriber.py
- mlx_ui/worker.py
- tests/test_transcriber.py
- docs/tree.md

Commands run:
- make test (pass)
- make lint (pass)
