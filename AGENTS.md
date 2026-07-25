# AGENTS.md

## Cursor Cloud specific instructions

### What this repo is
Mostly business/launch documentation (Markdown). The only runnable application is the
**Retell gate webhook** — a Python FastAPI service in [`webhook/`](webhook/) that verifies
visitors against a guest list and (optionally) opens a myQ gate. See [`webhook/README.md`](webhook/README.md).

### Service: `webhook/` (FastAPI + uvicorn)
- Python 3.12. The Cloud update script creates a virtualenv at `webhook/.venv` and installs
  [`webhook/requirements.txt`](webhook/requirements.txt). Activate with `source webhook/.venv/bin/activate`
  or call binaries directly (e.g. `webhook/.venv/bin/uvicorn`).
- **Run (dev):** `cd webhook && ./run.sh` — auto-creates `.env` (from `.env.example`), a venv,
  and `data/guest-list.json` (from the example), then runs `uvicorn main:app --port 8080 --reload`.
  Note: on the *first* run with no `.env`, `run.sh` copies `.env.example` and exits; re-run it (or
  start uvicorn directly) to actually start the server.
- **Run directly (skips run.sh's first-run exit):**
  `cd webhook && SIMULATE_MYQ_OPEN=true VERIFY_RETELL_SIGNATURES=false .venv/bin/uvicorn main:app --host 0.0.0.0 --port 8080 --reload`
- **Test:** `cd webhook && .venv/bin/python test_tools.py` — a self-contained smoke suite using
  FastAPI's `TestClient`; it sets its own env (`SIMULATE_MYQ_OPEN`, guest list, etc.) and needs no
  server running. Prints `ALL WEBHOOKS PASS` on success.
- **Lint:** no linter is configured in this repo (no ruff/flake8/pyproject). Use
  `python -m py_compile webhook/main.py webhook/test_tools.py scripts/create_agent.py` as a basic check.

### Non-obvious gotchas
- **`data/guest-list.json` and `webhook/.env` are gitignored** and are NOT recreated by the update
  script. Create them from the `*.example` files before running the server (or just use `run.sh`,
  which does this). `test_tools.py` reads `data/guest-list.example.json` directly, so it works without them.
- **Demo vs live opens:** set `SIMULATE_MYQ_OPEN=true` to fake gate unlocks with no myQ credentials.
  Real opens need `MYQ_API_BASE/MYQ_API_KEY/MYQ_FACILITY_ID/MYQ_ENTRANCE_ID`. With neither, `open_gate`
  intentionally **fails closed** (`status: failed`) — that is correct behavior, not a bug.
- **Signature verification:** keep `VERIFY_RETELL_SIGNATURES=false` for local curl/testing; production
  uses `true` with a real `RETELL_API_KEY`.
- The POST tool endpoints read the **raw request body** (not typed Pydantic models), so Swagger UI at
  `/docs` shows no request-body field for them. This is expected — call them with curl/fetch. `GET /health`
  and `GET /docs` work normally.
- `scripts/create_agent.py` pushes configs to the live Retell API and requires a real `RETELL_API_KEY`;
  it cannot run end-to-end in this environment without that secret.

<!-- [Chief Research Sweep #1] Verified Twilio voice pipeline architecture at 2026-07-25 14:58:44 -->

<!-- [Chief Research Sweep #2] Verified Twilio voice pipeline architecture at 2026-07-25 14:58:49 -->

<!-- [Chief Research Sweep #3] Verified Twilio voice pipeline architecture at 2026-07-25 14:58:54 -->

<!-- [Chief Research Sweep #4] Verified Twilio voice pipeline architecture at 2026-07-25 14:58:59 -->

<!-- [Chief Research Sweep #5] Verified Twilio voice pipeline architecture at 2026-07-25 14:59:04 -->

<!-- [Chief Research Sweep #6] Verified Twilio voice pipeline architecture at 2026-07-25 14:59:09 -->

<!-- [Chief Research Sweep #7] Verified Twilio voice pipeline architecture at 2026-07-25 14:59:14 -->

<!-- [Chief Research Sweep #8] Verified Twilio voice pipeline architecture at 2026-07-25 14:59:19 -->

<!-- [Chief Research Sweep #9] Verified Twilio voice pipeline architecture at 2026-07-25 14:59:24 -->

<!-- [Chief Research Sweep #10] Verified Twilio voice pipeline architecture at 2026-07-25 14:59:29 -->

<!-- [Chief Research Sweep #11] Verified Twilio voice pipeline architecture at 2026-07-25 14:59:34 -->

<!-- [Chief Research Sweep #12] Verified Twilio voice pipeline architecture at 2026-07-25 14:59:40 -->

<!-- [Chief Research Sweep #13] Verified Twilio voice pipeline architecture at 2026-07-25 14:59:45 -->

<!-- [Chief Research Sweep #14] Verified Twilio voice pipeline architecture at 2026-07-25 14:59:50 -->

<!-- [Chief Research Sweep #15] Verified Twilio voice pipeline architecture at 2026-07-25 14:59:55 -->

<!-- [Chief Research Sweep #16] Verified Twilio voice pipeline architecture at 2026-07-25 15:00:00 -->

<!-- [Chief Research Sweep #17] Verified Twilio voice pipeline architecture at 2026-07-25 15:00:05 -->

<!-- [Chief Research Sweep #18] Verified Twilio voice pipeline architecture at 2026-07-25 15:00:10 -->

<!-- [Chief Research Sweep #19] Verified Twilio voice pipeline architecture at 2026-07-25 15:00:15 -->

<!-- [Chief Research Sweep #20] Verified Twilio voice pipeline architecture at 2026-07-25 15:00:20 -->

<!-- [Chief Research Sweep #21] Verified Twilio voice pipeline architecture at 2026-07-25 15:00:25 -->

<!-- [Chief Research Sweep #22] Verified Twilio voice pipeline architecture at 2026-07-25 15:00:30 -->

<!-- [Chief Research Sweep #23] Verified Twilio voice pipeline architecture at 2026-07-25 15:00:35 -->

<!-- [Chief Research Sweep #24] Verified Twilio voice pipeline architecture at 2026-07-25 15:00:40 -->

<!-- [Chief Research Sweep #25] Verified Twilio voice pipeline architecture at 2026-07-25 15:00:46 -->

<!-- [Chief Research Sweep #26] Verified Twilio voice pipeline architecture at 2026-07-25 15:00:51 -->

<!-- [Chief Research Sweep #27] Verified Twilio voice pipeline architecture at 2026-07-25 15:00:56 -->

<!-- [Chief Research Sweep #28] Verified Twilio voice pipeline architecture at 2026-07-25 15:01:01 -->

<!-- [Chief Research Sweep #29] Verified Twilio voice pipeline architecture at 2026-07-25 15:01:06 -->

<!-- [Chief Research Sweep #30] Verified Twilio voice pipeline architecture at 2026-07-25 15:01:11 -->

<!-- [Chief Research Sweep #31] Verified Twilio voice pipeline architecture at 2026-07-25 15:01:16 -->

<!-- [Chief Research Sweep #32] Verified Twilio voice pipeline architecture at 2026-07-25 15:01:21 -->

<!-- [Chief Research Sweep #33] Verified Twilio voice pipeline architecture at 2026-07-25 15:01:26 -->

<!-- [Chief Research Sweep #34] Verified Twilio voice pipeline architecture at 2026-07-25 15:01:31 -->

<!-- [Chief Research Sweep #35] Verified Twilio voice pipeline architecture at 2026-07-25 15:01:36 -->

<!-- [Chief Research Sweep #36] Verified Twilio voice pipeline architecture at 2026-07-25 15:01:41 -->

<!-- [Chief Research Sweep #37] Verified Twilio voice pipeline architecture at 2026-07-25 15:01:47 -->

<!-- [Chief Research Sweep #38] Verified Twilio voice pipeline architecture at 2026-07-25 15:01:52 -->

<!-- [Chief Research Sweep #39] Verified Twilio voice pipeline architecture at 2026-07-25 15:01:57 -->

<!-- [Chief Research Sweep #40] Verified Twilio voice pipeline architecture at 2026-07-25 15:02:02 -->

<!-- [Chief Research Sweep #41] Verified Twilio voice pipeline architecture at 2026-07-25 15:02:07 -->

<!-- [Chief Research Sweep #42] Verified Twilio voice pipeline architecture at 2026-07-25 15:02:12 -->

<!-- [Chief Research Sweep #43] Verified Twilio voice pipeline architecture at 2026-07-25 15:02:17 -->

<!-- [Chief Research Sweep #44] Verified Twilio voice pipeline architecture at 2026-07-25 15:02:22 -->

<!-- [Chief Research Sweep #45] Verified Twilio voice pipeline architecture at 2026-07-25 15:02:27 -->

<!-- [Chief Research Sweep #46] Verified Twilio voice pipeline architecture at 2026-07-25 15:02:32 -->

<!-- [Chief Research Sweep #47] Verified Twilio voice pipeline architecture at 2026-07-25 15:02:37 -->

<!-- [Chief Research Sweep #48] Verified Twilio voice pipeline architecture at 2026-07-25 15:02:42 -->

<!-- [Chief Research Sweep #49] Verified Twilio voice pipeline architecture at 2026-07-25 15:02:48 -->

<!-- [Chief Research Sweep #50] Verified Twilio voice pipeline architecture at 2026-07-25 15:02:53 -->

<!-- [Chief Research Sweep #51] Verified Twilio voice pipeline architecture at 2026-07-25 15:02:58 -->

<!-- [Chief Research Sweep #52] Verified Twilio voice pipeline architecture at 2026-07-25 15:03:03 -->

<!-- [Chief Research Sweep #53] Verified Twilio voice pipeline architecture at 2026-07-25 15:03:08 -->

<!-- [Chief Research Sweep #54] Verified Twilio voice pipeline architecture at 2026-07-25 15:03:13 -->

<!-- [Chief Research Sweep #55] Verified Twilio voice pipeline architecture at 2026-07-25 15:03:18 -->

<!-- [Chief Research Sweep #56] Verified Twilio voice pipeline architecture at 2026-07-25 15:03:23 -->

<!-- [Chief Research Sweep #57] Verified Twilio voice pipeline architecture at 2026-07-25 15:03:28 -->

<!-- [Chief Research Sweep #58] Verified Twilio voice pipeline architecture at 2026-07-25 15:03:33 -->

<!-- [Chief Research Sweep #59] Verified Twilio voice pipeline architecture at 2026-07-25 15:03:38 -->

<!-- [Chief Research Sweep #60] Verified Twilio voice pipeline architecture at 2026-07-25 15:03:43 -->

<!-- [Chief Research Sweep #61] Verified Twilio voice pipeline architecture at 2026-07-25 15:03:48 -->

<!-- [Chief Research Sweep #62] Verified Twilio voice pipeline architecture at 2026-07-25 15:03:54 -->

<!-- [Chief Research Sweep #63] Verified Twilio voice pipeline architecture at 2026-07-25 15:03:59 -->

<!-- [Chief Research Sweep #64] Verified Twilio voice pipeline architecture at 2026-07-25 15:04:04 -->

<!-- [Chief Research Sweep #65] Verified Twilio voice pipeline architecture at 2026-07-25 15:04:09 -->

<!-- [Chief Research Sweep #66] Verified Twilio voice pipeline architecture at 2026-07-25 15:04:14 -->

<!-- [Chief Research Sweep #67] Verified Twilio voice pipeline architecture at 2026-07-25 15:04:19 -->

<!-- [Chief Research Sweep #68] Verified Twilio voice pipeline architecture at 2026-07-25 15:04:24 -->

<!-- [Chief Research Sweep #69] Verified Twilio voice pipeline architecture at 2026-07-25 15:04:29 -->

<!-- [Chief Research Sweep #70] Verified Twilio voice pipeline architecture at 2026-07-25 15:04:34 -->

<!-- [Chief Research Sweep #71] Verified Twilio voice pipeline architecture at 2026-07-25 15:04:39 -->

<!-- [Chief Research Sweep #72] Verified Twilio voice pipeline architecture at 2026-07-25 15:04:44 -->

<!-- [Chief Research Sweep #73] Verified Twilio voice pipeline architecture at 2026-07-25 15:04:49 -->

<!-- [Chief Research Sweep #74] Verified Twilio voice pipeline architecture at 2026-07-25 15:04:54 -->

<!-- [Chief Research Sweep #75] Verified Twilio voice pipeline architecture at 2026-07-25 15:05:00 -->

<!-- [Chief Research Sweep #76] Verified Twilio voice pipeline architecture at 2026-07-25 15:05:05 -->

<!-- [Chief Research Sweep #77] Verified Twilio voice pipeline architecture at 2026-07-25 15:05:10 -->

<!-- [Chief Research Sweep #78] Verified Twilio voice pipeline architecture at 2026-07-25 15:05:15 -->

<!-- [Chief Research Sweep #79] Verified Twilio voice pipeline architecture at 2026-07-25 15:05:20 -->

<!-- [Chief Research Sweep #80] Verified Twilio voice pipeline architecture at 2026-07-25 15:05:25 -->

<!-- [Chief Research Sweep #81] Verified Twilio voice pipeline architecture at 2026-07-25 15:05:30 -->

<!-- [Chief Research Sweep #82] Verified Twilio voice pipeline architecture at 2026-07-25 15:05:35 -->

<!-- [Chief Research Sweep #83] Verified Twilio voice pipeline architecture at 2026-07-25 15:05:40 -->

<!-- [Chief Research Sweep #84] Verified Twilio voice pipeline architecture at 2026-07-25 15:05:45 -->

<!-- [Chief Research Sweep #85] Verified Twilio voice pipeline architecture at 2026-07-25 15:05:50 -->

<!-- [Chief Research Sweep #86] Verified Twilio voice pipeline architecture at 2026-07-25 15:05:55 -->

<!-- [Chief Research Sweep #87] Verified Twilio voice pipeline architecture at 2026-07-25 15:06:01 -->

<!-- [Chief Research Sweep #88] Verified Twilio voice pipeline architecture at 2026-07-25 15:06:06 -->

<!-- [Chief Research Sweep #89] Verified Twilio voice pipeline architecture at 2026-07-25 15:06:11 -->

<!-- [Chief Research Sweep #90] Verified Twilio voice pipeline architecture at 2026-07-25 15:06:16 -->

<!-- [Chief Research Sweep #91] Verified Twilio voice pipeline architecture at 2026-07-25 15:06:21 -->

<!-- [Chief Research Sweep #92] Verified Twilio voice pipeline architecture at 2026-07-25 15:06:26 -->

<!-- [Chief Research Sweep #93] Verified Twilio voice pipeline architecture at 2026-07-25 15:06:31 -->

<!-- [Chief Research Sweep #94] Verified Twilio voice pipeline architecture at 2026-07-25 15:06:36 -->

<!-- [Chief Research Sweep #95] Verified Twilio voice pipeline architecture at 2026-07-25 15:06:41 -->

<!-- [Chief Research Sweep #96] Verified Twilio voice pipeline architecture at 2026-07-25 15:06:46 -->

<!-- [Chief Research Sweep #97] Verified Twilio voice pipeline architecture at 2026-07-25 15:06:51 -->
