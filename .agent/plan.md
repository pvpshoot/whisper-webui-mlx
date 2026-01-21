# Plan

Task: WUI-020 — Integrate `wtm` CLI transcription

Acceptance: for a job, system runs `wtm` with chosen language and produces at least `.txt` in `data/results/<job_id>/`

Assumptions:
- `wtm` is installed and available on PATH (or a configurable path), and the model has been downloaded.
- Tests should not invoke the real ML model; subprocess calls will be mocked.

Implementation steps:
- Inspect the current transcriber interface and worker flow to locate where to swap the fake transcriber for a CLI-backed implementation.
- Implement a `wtm`-backed transcriber that builds the CLI command with the selected language and output directory, captures errors, and writes results under `data/results/<job_id>/`.
- Ensure the worker uses the new transcriber path and records failures cleanly without breaking the queue.
- Add configuration hooks if needed (e.g., optional `WTM_PATH`) and keep logs readable while avoiding secret exposure.
- Update tests to mock subprocess execution, create a fake `.txt` result, and assert job status/result paths without running the model.

Files likely to touch:
- `mlx_ui/transcriber.py`
- `mlx_ui/worker.py`
- `mlx_ui/app.py`
- `tests/test_worker.py`
- `tests/test_app.py`

Verification steps:
- `make test`
- `make lint`
