# PROJECT (single source of truth for the harness)

PROJECT_NAME: "whisper-webui-mlx"
REPO_KIND: "new repo"

## Brief (1–2 paragraphs)
Build a **local macOS app for Apple Silicon (M1+)** that exposes a **Web UI on localhost** to manage **offline transcription** of audio/video files using the engine from `whisper-turbo-mlx` via its CLI `wtm` (MLX).

Turn the current console workflow (e.g. `wtm ... --any_lang=True`) into a tool that is easy to deploy on another M1+ Mac with **one command**, supports **batch uploads**, a **strictly sequential** processing queue (no parallelism), **job history + downloads**, optional **Telegram delivery of TXT results**, and (in the final phase) **live recording + chunked transcription**.

## Primary stack
Python 3.11+
- Backend/Web: FastAPI + Uvicorn
- Templates/UI: Jinja2 + minimal vanilla JS (no external CDNs; must work offline)
- Storage: SQLite (jobs metadata) + local filesystem (uploads/results/logs)
- Worker: a single sequential worker consuming a persistent queue
- Transcription: subprocess call to `wtm` with explicit language selection

## Commands (choose defaults if unknown)
TEST_CMD: "make test"
LINT_CMD: "make lint"
FORMAT_CMD: "make fmt"
RUN_CMD: "make run"

## Policies
DO_NOT_TOUCH_OUTSIDE_REPO: true
NETWORK_ALLOWED: "no"   # Implement “check updates” as best-effort and fully optional at runtime.
AUTO_COMMIT: "no"

## Budgets (soft)
PLANNER_MAX_MINUTES: 2
WORKER_MAX_MINUTES: 12
JUDGE_MAX_MINUTES: 3

## Definition of Done (global)
- Web UI runs on localhost only
- After initial install/models download, the app works fully offline
- Transcription queue is strictly sequential (one job at a time)
- Uploads + results are stored under repo-local directories (safe local storage)
- Queue view + History view work and allow viewing/downloading results (at minimum .txt)
- Logs exist and make failures diagnosable
- Telegram send is optional, non-breaking on failure, and secrets never leak
- Tests pass (TEST_CMD) and are stable; no tests should require the real ML model unless explicitly marked/integration

## Optional notes / constraints
- Platform is macOS Apple Silicon only (M1+). Assume user runs this locally on such a machine.
- The repo must provide a one-command setup/run script that installs deps, downloads models, starts server, and opens a browser.
- No remote access: bind only to 127.0.0.1 / localhost.
