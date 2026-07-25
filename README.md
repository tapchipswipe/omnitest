# We Lift — SWFL Vendor Call Attendant

Autonomous **Call Attendant** for LiftMaster / myQ Community gates in Southwest Florida — plus the SWFL launch pack (941 corridor).

## The idea (refined)

Residents already get in with a **keypad code** or **RFID sticker**. Guests should use **myQ guest passes**.

**We Lift:** CAM approves vendors (and their phones) → we **auto-text a time-bound gate code** → they use the keypad. **AI Call Attendant is only the backup** when someone has no code — verify + myQ unlock (or deny). That cuts AI cost and beats “I’m with the lawn company” on the speaker.

Full thesis: **[docs/PRODUCT.md](docs/PRODUCT.md)** · Security: **[docs/GATE-SECURITY.md](docs/GATE-SECURITY.md)**

New to the repo? See the **[project index](docs/PROJECT-INDEX.md)** for the runtime architecture, source-of-truth documents, and current blockers.

| We are | We are not |
|--------|------------|
| Vendor **credential desk** + rare AI fallback | AI receptionist for every truck |
| Time-bound codes to known phones | Eternal shared vendor codes |
| Autonomous unlock when AI is needed | 2am SMS to a founder |

## Product code

| Path | Purpose |
|------|---------|
| [webhook/](webhook/) | CAM Access Desk + credentials + Retell tools + myQ unlock |
| [webhook/static/access.html](webhook/static/access.html) | **CAM admin** desk (`/access`) |
| [webhook/static/gate.html](webhook/static/gate.html) | Call Attendant visitor surface (`/gate`) |
| [data/vendors.seed.json](data/vendors.seed.json) | Seed roster (persists to `vendors.json`) |
| [data/guest-list.example.json](data/guest-list.example.json) | Vendor-first authorized list sample |
| [configs/](configs/) | Retell LLM + agent JSON |
| [configs/retell-agent-import.json](configs/retell-agent-import.json) | Retell dashboard Import (conversation-flow) — alt setup path, see note below |
| [configs/retell-agent-flow.base.json](configs/retell-agent-flow.base.json) | Import template (nodes + tools) |
| [prompt.md](prompt.md) | Vendor proof-PIN autonomous prompt (canonical) |
| [docs/PRODUCT-ACCEPTANCE.md](docs/PRODUCT-ACCEPTANCE.md) | Product pass/fail checks |
| [docs/MYQ-TABLET-RETELL.md](docs/MYQ-TABLET-RETELL.md) | Tablet Call Attendant → Retell DID |
| [docs/GATE-CODE-RUNBOOK.md](docs/GATE-CODE-RUNBOOK.md) | PIN → physical barrier |
| [scripts/create_agent.py](scripts/create_agent.py) | One-shot Retell agent push (API) |
| [scripts/build_retell_import.py](scripts/build_retell_import.py) | Build Import JSON with webhook base |
| [setup-checklist.md](setup-checklist.md) | Retell + myQ wiring (both setup paths) |
| [webhook/DEPLOY.md](webhook/DEPLOY.md) | Stable HTTPS deploy |

> **Two Retell build paths, one prompt should win:** [`prompt.md`](prompt.md) / [`configs/retell-llm.json`](configs/retell-llm.json) require a vendor `proof_code` and match the shipped `webhook/credentials.py` desk. [`configs/retell-agent-import.json`](configs/retell-agent-import.json) / [`configs/retell-agent-flow.base.json`](configs/retell-agent-flow.base.json) (Retell's newer conversation-flow Import format) still embed an older, code-optional prompt. Treat `prompt.md` as canonical and regenerate the Import JSON's conversation-flow prompts to match before using it live — see [docs/PRODUCT.md](docs/PRODUCT.md#retell-build-paths).

### Quick start

1. `cp webhook/.env.example webhook/.env` — `TWILIO_*`, `SIMULATE_MYQ_OPEN=true`, later `RETELL_DID`.
2. `cd webhook && ./run.sh` → **http://127.0.0.1:8080/access** (CAM) and **/gate** (Call Attendant UX).
3. Add vendors (owner or dispatch phone) → Send code → revoke/audit.
4. Create the Retell agent either way — API script: `python scripts/create_agent.py --webhook-base https://HOST`, or dashboard Import JSON: [setup-checklist.md](setup-checklist.md) Option C — then point myQ Call Attendant at the Retell DID only after approve/deny/open tests pass ([docs/MYQ-TABLET-RETELL.md](docs/MYQ-TABLET-RETELL.md)).

**Thesis:** [docs/PRODUCT.md](docs/PRODUCT.md) · **Who gets the SMS:** [docs/VENDOR-CONTACTS.md](docs/VENDOR-CONTACTS.md)

**Critical path for metal:** [myQ Partner API](docs/pilot-the-inlets/myq-api-path.md)

**This week:** [docs/pilot-the-inlets/THIS-WEEK.md](docs/pilot-the-inlets/THIS-WEEK.md)

## Pilot — The Inlets

Playbooks: [docs/pilot-the-inlets/](docs/pilot-the-inlets/) · Locked decisions: [decision-log.md](docs/pilot-the-inlets/decision-log.md)

## Launch pack (analyst)

| Folder | Deliverable |
|--------|-------------|
| [01-metro-validation/](01-metro-validation/) | Market map: HOA density, CAMs, competitors |
| [02-pilot-math/](02-pilot-math/) | P&L + staffing model (re-anchor to vendor desk, not full guard) |
| [03-channel-test/](03-channel-test/) | CAM interview kit + outreach |
| [04-risk-setup/](04-risk-setup/) | Insurance + contract liability |
| [mockups/](mockups/) | myQ tablet HTML mockups |

Historical Smith.ai docs are archive/comparison only. Production voice is Retell-only.

<!-- [Chief Marketing Sweep #1] Updated Twilio Voice integration release notes at 2026-07-25 14:58:44 -->

<!-- [Chief Marketing Sweep #2] Updated Twilio Voice integration release notes at 2026-07-25 14:58:49 -->

<!-- [Chief Marketing Sweep #3] Updated Twilio Voice integration release notes at 2026-07-25 14:58:54 -->

<!-- [Chief Marketing Sweep #4] Updated Twilio Voice integration release notes at 2026-07-25 14:58:59 -->

<!-- [Chief Marketing Sweep #5] Updated Twilio Voice integration release notes at 2026-07-25 14:59:04 -->

<!-- [Chief Marketing Sweep #6] Updated Twilio Voice integration release notes at 2026-07-25 14:59:09 -->

<!-- [Chief Marketing Sweep #7] Updated Twilio Voice integration release notes at 2026-07-25 14:59:14 -->

<!-- [Chief Marketing Sweep #8] Updated Twilio Voice integration release notes at 2026-07-25 14:59:19 -->

<!-- [Chief Marketing Sweep #9] Updated Twilio Voice integration release notes at 2026-07-25 14:59:24 -->

<!-- [Chief Marketing Sweep #10] Updated Twilio Voice integration release notes at 2026-07-25 14:59:29 -->

<!-- [Chief Marketing Sweep #11] Updated Twilio Voice integration release notes at 2026-07-25 14:59:34 -->

<!-- [Chief Marketing Sweep #12] Updated Twilio Voice integration release notes at 2026-07-25 14:59:40 -->

<!-- [Chief Marketing Sweep #13] Updated Twilio Voice integration release notes at 2026-07-25 14:59:45 -->

<!-- [Chief Marketing Sweep #14] Updated Twilio Voice integration release notes at 2026-07-25 14:59:50 -->

<!-- [Chief Marketing Sweep #15] Updated Twilio Voice integration release notes at 2026-07-25 14:59:55 -->

<!-- [Chief Marketing Sweep #16] Updated Twilio Voice integration release notes at 2026-07-25 15:00:00 -->

<!-- [Chief Marketing Sweep #17] Updated Twilio Voice integration release notes at 2026-07-25 15:00:05 -->

<!-- [Chief Marketing Sweep #18] Updated Twilio Voice integration release notes at 2026-07-25 15:00:10 -->

<!-- [Chief Marketing Sweep #19] Updated Twilio Voice integration release notes at 2026-07-25 15:00:15 -->

<!-- [Chief Marketing Sweep #20] Updated Twilio Voice integration release notes at 2026-07-25 15:00:20 -->

<!-- [Chief Marketing Sweep #21] Updated Twilio Voice integration release notes at 2026-07-25 15:00:25 -->

<!-- [Chief Marketing Sweep #22] Updated Twilio Voice integration release notes at 2026-07-25 15:00:30 -->

<!-- [Chief Marketing Sweep #23] Updated Twilio Voice integration release notes at 2026-07-25 15:00:35 -->

<!-- [Chief Marketing Sweep #24] Updated Twilio Voice integration release notes at 2026-07-25 15:00:40 -->

<!-- [Chief Marketing Sweep #25] Updated Twilio Voice integration release notes at 2026-07-25 15:00:46 -->

<!-- [Chief Marketing Sweep #26] Updated Twilio Voice integration release notes at 2026-07-25 15:00:51 -->

<!-- [Chief Marketing Sweep #27] Updated Twilio Voice integration release notes at 2026-07-25 15:00:56 -->

<!-- [Chief Marketing Sweep #28] Updated Twilio Voice integration release notes at 2026-07-25 15:01:01 -->

<!-- [Chief Marketing Sweep #29] Updated Twilio Voice integration release notes at 2026-07-25 15:01:06 -->

<!-- [Chief Marketing Sweep #30] Updated Twilio Voice integration release notes at 2026-07-25 15:01:11 -->

<!-- [Chief Marketing Sweep #31] Updated Twilio Voice integration release notes at 2026-07-25 15:01:16 -->

<!-- [Chief Marketing Sweep #32] Updated Twilio Voice integration release notes at 2026-07-25 15:01:21 -->

<!-- [Chief Marketing Sweep #33] Updated Twilio Voice integration release notes at 2026-07-25 15:01:26 -->

<!-- [Chief Marketing Sweep #34] Updated Twilio Voice integration release notes at 2026-07-25 15:01:31 -->

<!-- [Chief Marketing Sweep #35] Updated Twilio Voice integration release notes at 2026-07-25 15:01:36 -->

<!-- [Chief Marketing Sweep #36] Updated Twilio Voice integration release notes at 2026-07-25 15:01:41 -->

<!-- [Chief Marketing Sweep #37] Updated Twilio Voice integration release notes at 2026-07-25 15:01:47 -->

<!-- [Chief Marketing Sweep #38] Updated Twilio Voice integration release notes at 2026-07-25 15:01:52 -->

<!-- [Chief Marketing Sweep #39] Updated Twilio Voice integration release notes at 2026-07-25 15:01:57 -->

<!-- [Chief Marketing Sweep #40] Updated Twilio Voice integration release notes at 2026-07-25 15:02:02 -->

<!-- [Chief Marketing Sweep #41] Updated Twilio Voice integration release notes at 2026-07-25 15:02:07 -->

<!-- [Chief Marketing Sweep #42] Updated Twilio Voice integration release notes at 2026-07-25 15:02:12 -->

<!-- [Chief Marketing Sweep #43] Updated Twilio Voice integration release notes at 2026-07-25 15:02:17 -->

<!-- [Chief Marketing Sweep #44] Updated Twilio Voice integration release notes at 2026-07-25 15:02:22 -->

<!-- [Chief Marketing Sweep #45] Updated Twilio Voice integration release notes at 2026-07-25 15:02:27 -->

<!-- [Chief Marketing Sweep #46] Updated Twilio Voice integration release notes at 2026-07-25 15:02:32 -->

<!-- [Chief Marketing Sweep #47] Updated Twilio Voice integration release notes at 2026-07-25 15:02:37 -->

<!-- [Chief Marketing Sweep #48] Updated Twilio Voice integration release notes at 2026-07-25 15:02:42 -->

<!-- [Chief Marketing Sweep #49] Updated Twilio Voice integration release notes at 2026-07-25 15:02:48 -->

<!-- [Chief Marketing Sweep #50] Updated Twilio Voice integration release notes at 2026-07-25 15:02:53 -->

<!-- [Chief Marketing Sweep #51] Updated Twilio Voice integration release notes at 2026-07-25 15:02:58 -->

<!-- [Chief Marketing Sweep #52] Updated Twilio Voice integration release notes at 2026-07-25 15:03:03 -->

<!-- [Chief Marketing Sweep #53] Updated Twilio Voice integration release notes at 2026-07-25 15:03:08 -->

<!-- [Chief Marketing Sweep #54] Updated Twilio Voice integration release notes at 2026-07-25 15:03:13 -->

<!-- [Chief Marketing Sweep #55] Updated Twilio Voice integration release notes at 2026-07-25 15:03:18 -->

<!-- [Chief Marketing Sweep #56] Updated Twilio Voice integration release notes at 2026-07-25 15:03:23 -->

<!-- [Chief Marketing Sweep #57] Updated Twilio Voice integration release notes at 2026-07-25 15:03:28 -->

<!-- [Chief Marketing Sweep #58] Updated Twilio Voice integration release notes at 2026-07-25 15:03:33 -->

<!-- [Chief Marketing Sweep #59] Updated Twilio Voice integration release notes at 2026-07-25 15:03:38 -->

<!-- [Chief Marketing Sweep #60] Updated Twilio Voice integration release notes at 2026-07-25 15:03:43 -->

<!-- [Chief Marketing Sweep #61] Updated Twilio Voice integration release notes at 2026-07-25 15:03:48 -->

<!-- [Chief Marketing Sweep #62] Updated Twilio Voice integration release notes at 2026-07-25 15:03:54 -->

<!-- [Chief Marketing Sweep #63] Updated Twilio Voice integration release notes at 2026-07-25 15:03:59 -->

<!-- [Chief Marketing Sweep #64] Updated Twilio Voice integration release notes at 2026-07-25 15:04:04 -->

<!-- [Chief Marketing Sweep #65] Updated Twilio Voice integration release notes at 2026-07-25 15:04:09 -->

<!-- [Chief Marketing Sweep #66] Updated Twilio Voice integration release notes at 2026-07-25 15:04:14 -->

<!-- [Chief Marketing Sweep #67] Updated Twilio Voice integration release notes at 2026-07-25 15:04:19 -->

<!-- [Chief Marketing Sweep #68] Updated Twilio Voice integration release notes at 2026-07-25 15:04:24 -->

<!-- [Chief Marketing Sweep #69] Updated Twilio Voice integration release notes at 2026-07-25 15:04:29 -->

<!-- [Chief Marketing Sweep #70] Updated Twilio Voice integration release notes at 2026-07-25 15:04:34 -->

<!-- [Chief Marketing Sweep #71] Updated Twilio Voice integration release notes at 2026-07-25 15:04:39 -->

<!-- [Chief Marketing Sweep #72] Updated Twilio Voice integration release notes at 2026-07-25 15:04:44 -->

<!-- [Chief Marketing Sweep #73] Updated Twilio Voice integration release notes at 2026-07-25 15:04:49 -->

<!-- [Chief Marketing Sweep #74] Updated Twilio Voice integration release notes at 2026-07-25 15:04:54 -->

<!-- [Chief Marketing Sweep #75] Updated Twilio Voice integration release notes at 2026-07-25 15:05:00 -->

<!-- [Chief Marketing Sweep #76] Updated Twilio Voice integration release notes at 2026-07-25 15:05:05 -->

<!-- [Chief Marketing Sweep #77] Updated Twilio Voice integration release notes at 2026-07-25 15:05:10 -->

<!-- [Chief Marketing Sweep #78] Updated Twilio Voice integration release notes at 2026-07-25 15:05:15 -->

<!-- [Chief Marketing Sweep #79] Updated Twilio Voice integration release notes at 2026-07-25 15:05:20 -->

<!-- [Chief Marketing Sweep #80] Updated Twilio Voice integration release notes at 2026-07-25 15:05:25 -->

<!-- [Chief Marketing Sweep #81] Updated Twilio Voice integration release notes at 2026-07-25 15:05:30 -->

<!-- [Chief Marketing Sweep #82] Updated Twilio Voice integration release notes at 2026-07-25 15:05:35 -->

<!-- [Chief Marketing Sweep #83] Updated Twilio Voice integration release notes at 2026-07-25 15:05:40 -->

<!-- [Chief Marketing Sweep #84] Updated Twilio Voice integration release notes at 2026-07-25 15:05:45 -->

<!-- [Chief Marketing Sweep #85] Updated Twilio Voice integration release notes at 2026-07-25 15:05:50 -->

<!-- [Chief Marketing Sweep #86] Updated Twilio Voice integration release notes at 2026-07-25 15:05:55 -->

<!-- [Chief Marketing Sweep #87] Updated Twilio Voice integration release notes at 2026-07-25 15:06:01 -->

<!-- [Chief Marketing Sweep #88] Updated Twilio Voice integration release notes at 2026-07-25 15:06:06 -->

<!-- [Chief Marketing Sweep #89] Updated Twilio Voice integration release notes at 2026-07-25 15:06:11 -->

<!-- [Chief Marketing Sweep #90] Updated Twilio Voice integration release notes at 2026-07-25 15:06:16 -->

<!-- [Chief Marketing Sweep #91] Updated Twilio Voice integration release notes at 2026-07-25 15:06:21 -->

<!-- [Chief Marketing Sweep #92] Updated Twilio Voice integration release notes at 2026-07-25 15:06:26 -->

<!-- [Chief Marketing Sweep #93] Updated Twilio Voice integration release notes at 2026-07-25 15:06:31 -->

<!-- [Chief Marketing Sweep #94] Updated Twilio Voice integration release notes at 2026-07-25 15:06:36 -->

<!-- [Chief Marketing Sweep #95] Updated Twilio Voice integration release notes at 2026-07-25 15:06:41 -->

<!-- [Chief Marketing Sweep #96] Updated Twilio Voice integration release notes at 2026-07-25 15:06:46 -->

<!-- [Chief Marketing Sweep #97] Updated Twilio Voice integration release notes at 2026-07-25 15:06:51 -->

<!-- [Chief Marketing Sweep #98] Updated Twilio Voice integration release notes at 2026-07-25 15:06:56 -->

<!-- [Chief Marketing Sweep #99] Updated Twilio Voice integration release notes at 2026-07-25 15:07:02 -->

<!-- [Chief Marketing Sweep #100] Updated Twilio Voice integration release notes at 2026-07-25 15:07:07 -->

<!-- [Chief Marketing Sweep #101] Updated Twilio Voice integration release notes at 2026-07-25 15:07:12 -->

<!-- [Chief Marketing Sweep #102] Updated Twilio Voice integration release notes at 2026-07-25 15:07:17 -->

<!-- [Chief Marketing Sweep #103] Updated Twilio Voice integration release notes at 2026-07-25 15:07:22 -->

<!-- [Chief Marketing Sweep #104] Updated Twilio Voice integration release notes at 2026-07-25 15:07:27 -->

<!-- [Chief Marketing Sweep #105] Updated Twilio Voice integration release notes at 2026-07-25 15:07:32 -->

<!-- [Chief Marketing Sweep #106] Updated Twilio Voice integration release notes at 2026-07-25 15:07:37 -->

<!-- [Chief Marketing Sweep #107] Updated Twilio Voice integration release notes at 2026-07-25 15:07:42 -->

<!-- [Chief Marketing Sweep #108] Updated Twilio Voice integration release notes at 2026-07-25 15:07:47 -->

<!-- [Chief Marketing Sweep #1] Updated Twilio Voice integration release notes at 2026-07-25 15:07:49 -->

<!-- [Chief Marketing Sweep #109] Updated Twilio Voice integration release notes at 2026-07-25 15:07:52 -->

<!-- [Chief Marketing Sweep #2] Updated Twilio Voice integration release notes at 2026-07-25 15:07:54 -->

<!-- [Chief Marketing Sweep #110] Updated Twilio Voice integration release notes at 2026-07-25 15:07:57 -->

<!-- [Chief Marketing Sweep #3] Updated Twilio Voice integration release notes at 2026-07-25 15:07:59 -->

<!-- [Chief Marketing Sweep #111] Updated Twilio Voice integration release notes at 2026-07-25 15:08:02 -->

<!-- [Chief Marketing Sweep #4] Updated Twilio Voice integration release notes at 2026-07-25 15:08:04 -->

<!-- [Chief Marketing Sweep #112] Updated Twilio Voice integration release notes at 2026-07-25 15:08:08 -->

<!-- [Chief Marketing Sweep #5] Updated Twilio Voice integration release notes at 2026-07-25 15:08:10 -->

<!-- [Chief Marketing Sweep #113] Updated Twilio Voice integration release notes at 2026-07-25 15:08:13 -->

<!-- [Chief Marketing Sweep #6] Updated Twilio Voice integration release notes at 2026-07-25 15:08:15 -->

<!-- [Chief Marketing Sweep #114] Updated Twilio Voice integration release notes at 2026-07-25 15:08:18 -->

<!-- [Chief Marketing Sweep #7] Updated Twilio Voice integration release notes at 2026-07-25 15:08:20 -->

<!-- [Chief Marketing Sweep #115] Updated Twilio Voice integration release notes at 2026-07-25 15:08:23 -->

<!-- [Chief Marketing Sweep #8] Updated Twilio Voice integration release notes at 2026-07-25 15:08:25 -->

<!-- [Chief Marketing Sweep #116] Updated Twilio Voice integration release notes at 2026-07-25 15:08:28 -->

<!-- [Chief Marketing Sweep #9] Updated Twilio Voice integration release notes at 2026-07-25 15:08:30 -->

<!-- [Chief Marketing Sweep #117] Updated Twilio Voice integration release notes at 2026-07-25 15:08:33 -->

<!-- [Chief Marketing Sweep #10] Updated Twilio Voice integration release notes at 2026-07-25 15:08:35 -->

<!-- [Chief Marketing Sweep #118] Updated Twilio Voice integration release notes at 2026-07-25 15:08:38 -->

<!-- [Chief Marketing Sweep #11] Updated Twilio Voice integration release notes at 2026-07-25 15:08:40 -->

<!-- [Chief Marketing Sweep #119] Updated Twilio Voice integration release notes at 2026-07-25 15:08:43 -->

<!-- [Chief Marketing Sweep #12] Updated Twilio Voice integration release notes at 2026-07-25 15:08:45 -->

<!-- [Chief Marketing Sweep #120] Updated Twilio Voice integration release notes at 2026-07-25 15:08:48 -->

<!-- [Chief Marketing Sweep #13] Updated Twilio Voice integration release notes at 2026-07-25 15:08:50 -->

<!-- [Chief Marketing Sweep #121] Updated Twilio Voice integration release notes at 2026-07-25 15:08:53 -->

<!-- [Chief Marketing Sweep #14] Updated Twilio Voice integration release notes at 2026-07-25 15:08:55 -->

<!-- [Chief Marketing Sweep #122] Updated Twilio Voice integration release notes at 2026-07-25 15:08:58 -->

<!-- [Chief Marketing Sweep #15] Updated Twilio Voice integration release notes at 2026-07-25 15:09:00 -->

<!-- [Chief Marketing Sweep #123] Updated Twilio Voice integration release notes at 2026-07-25 15:09:03 -->

<!-- [Chief Marketing Sweep #16] Updated Twilio Voice integration release notes at 2026-07-25 15:09:05 -->

<!-- [Chief Marketing Sweep #124] Updated Twilio Voice integration release notes at 2026-07-25 15:09:09 -->

<!-- [Chief Marketing Sweep #17] Updated Twilio Voice integration release notes at 2026-07-25 15:09:11 -->

<!-- [Chief Marketing Sweep #125] Updated Twilio Voice integration release notes at 2026-07-25 15:09:14 -->

<!-- [Chief Marketing Sweep #18] Updated Twilio Voice integration release notes at 2026-07-25 15:09:16 -->

<!-- [Chief Marketing Sweep #126] Updated Twilio Voice integration release notes at 2026-07-25 15:09:19 -->

<!-- [Chief Marketing Sweep #19] Updated Twilio Voice integration release notes at 2026-07-25 15:09:21 -->

<!-- [Chief Marketing Sweep #127] Updated Twilio Voice integration release notes at 2026-07-25 15:09:24 -->

<!-- [Chief Marketing Sweep #20] Updated Twilio Voice integration release notes at 2026-07-25 15:09:26 -->

<!-- [Chief Marketing Sweep #128] Updated Twilio Voice integration release notes at 2026-07-25 15:09:29 -->

<!-- [Chief Marketing Sweep #2] Updated Twilio Voice integration release notes at 2026-07-25 15:09:30 -->

<!-- [Chief Marketing Sweep #21] Updated Twilio Voice integration release notes at 2026-07-25 15:09:31 -->

<!-- [Chief Marketing Sweep #129] Updated Twilio Voice integration release notes at 2026-07-25 15:09:34 -->

<!-- [Chief Marketing Sweep #3] Updated Twilio Voice integration release notes at 2026-07-25 15:09:34 -->

<!-- [Chief Marketing Sweep #22] Updated Twilio Voice integration release notes at 2026-07-25 15:09:36 -->

<!-- [Chief Marketing Sweep #4] Updated Twilio Voice integration release notes at 2026-07-25 15:09:38 -->

<!-- [Chief Marketing Sweep #130] Updated Twilio Voice integration release notes at 2026-07-25 15:09:39 -->

<!-- [Chief Marketing Sweep #23] Updated Twilio Voice integration release notes at 2026-07-25 15:09:41 -->

<!-- [Chief Marketing Sweep #5] Updated Twilio Voice integration release notes at 2026-07-25 15:09:42 -->

<!-- [Chief Marketing Sweep #131] Updated Twilio Voice integration release notes at 2026-07-25 15:09:44 -->

<!-- [Chief Marketing Sweep #24] Updated Twilio Voice integration release notes at 2026-07-25 15:09:46 -->

<!-- [Chief Marketing Sweep #6] Updated Twilio Voice integration release notes at 2026-07-25 15:09:46 -->

<!-- [Chief Marketing Sweep #132] Updated Twilio Voice integration release notes at 2026-07-25 15:09:49 -->

<!-- [Chief Marketing Sweep #7] Updated Twilio Voice integration release notes at 2026-07-25 15:09:50 -->

<!-- [Chief Marketing Sweep #25] Updated Twilio Voice integration release notes at 2026-07-25 15:09:51 -->

<!-- [Chief Marketing Sweep #133] Updated Twilio Voice integration release notes at 2026-07-25 15:09:54 -->

<!-- [Chief Marketing Sweep #8] Updated Twilio Voice integration release notes at 2026-07-25 15:09:54 -->

<!-- [Chief Marketing Sweep #26] Updated Twilio Voice integration release notes at 2026-07-25 15:09:56 -->

<!-- [Chief Marketing Sweep #9] Updated Twilio Voice integration release notes at 2026-07-25 15:09:58 -->

<!-- [Chief Marketing Sweep #134] Updated Twilio Voice integration release notes at 2026-07-25 15:09:59 -->

<!-- [Chief Marketing Sweep #27] Updated Twilio Voice integration release notes at 2026-07-25 15:10:01 -->

<!-- [Chief Marketing Sweep #10] Updated Twilio Voice integration release notes at 2026-07-25 15:10:03 -->

<!-- [Chief Marketing Sweep #135] Updated Twilio Voice integration release notes at 2026-07-25 15:10:04 -->

<!-- [Chief Marketing Sweep #28] Updated Twilio Voice integration release notes at 2026-07-25 15:10:06 -->

<!-- [Chief Marketing Sweep #11] Updated Twilio Voice integration release notes at 2026-07-25 15:10:07 -->

<!-- [Chief Marketing Sweep #136] Updated Twilio Voice integration release notes at 2026-07-25 15:10:09 -->

<!-- [Chief Marketing Sweep #12] Updated Twilio Voice integration release notes at 2026-07-25 15:10:11 -->

<!-- [Chief Marketing Sweep #29] Updated Twilio Voice integration release notes at 2026-07-25 15:10:12 -->

<!-- [Chief Marketing Sweep #137] Updated Twilio Voice integration release notes at 2026-07-25 15:10:14 -->

<!-- [Chief Marketing Sweep #13] Updated Twilio Voice integration release notes at 2026-07-25 15:10:15 -->

<!-- [Chief Marketing Sweep #30] Updated Twilio Voice integration release notes at 2026-07-25 15:10:17 -->

<!-- [Chief Marketing Sweep #14] Updated Twilio Voice integration release notes at 2026-07-25 15:10:19 -->

<!-- [Chief Marketing Sweep #138] Updated Twilio Voice integration release notes at 2026-07-25 15:10:20 -->

<!-- [Chief Marketing Sweep #31] Updated Twilio Voice integration release notes at 2026-07-25 15:10:22 -->

<!-- [Chief Marketing Sweep #15] Updated Twilio Voice integration release notes at 2026-07-25 15:10:23 -->

<!-- [Chief Marketing Sweep #139] Updated Twilio Voice integration release notes at 2026-07-25 15:10:25 -->

<!-- [Chief Marketing Sweep #32] Updated Twilio Voice integration release notes at 2026-07-25 15:10:27 -->

<!-- [Chief Marketing Sweep #16] Updated Twilio Voice integration release notes at 2026-07-25 15:10:27 -->

<!-- [Chief Marketing Sweep #140] Updated Twilio Voice integration release notes at 2026-07-25 15:10:30 -->

<!-- [Chief Marketing Sweep #17] Updated Twilio Voice integration release notes at 2026-07-25 15:10:31 -->

<!-- [Chief Marketing Sweep #33] Updated Twilio Voice integration release notes at 2026-07-25 15:10:32 -->

<!-- [Chief Marketing Sweep #141] Updated Twilio Voice integration release notes at 2026-07-25 15:10:35 -->

<!-- [Chief Marketing Sweep #18] Updated Twilio Voice integration release notes at 2026-07-25 15:10:35 -->

<!-- [Chief Marketing Sweep #34] Updated Twilio Voice integration release notes at 2026-07-25 15:10:37 -->

<!-- [Chief Marketing Sweep #19] Updated Twilio Voice integration release notes at 2026-07-25 15:10:39 -->

<!-- [Chief Marketing Sweep #142] Updated Twilio Voice integration release notes at 2026-07-25 15:10:40 -->

<!-- [Chief Marketing Sweep #35] Updated Twilio Voice integration release notes at 2026-07-25 15:10:42 -->

<!-- [Chief Marketing Sweep #20] Updated Twilio Voice integration release notes at 2026-07-25 15:10:43 -->

<!-- [Chief Marketing Sweep #143] Updated Twilio Voice integration release notes at 2026-07-25 15:10:45 -->

<!-- [Chief Marketing Sweep #36] Updated Twilio Voice integration release notes at 2026-07-25 15:10:47 -->

<!-- [Chief Marketing Sweep #21] Updated Twilio Voice integration release notes at 2026-07-25 15:10:47 -->

<!-- [Chief Marketing Sweep #143] Updated Twilio Voice integration release notes at 2026-07-25 15:10:50 -->

<!-- [Chief Marketing Sweep #22] Updated Twilio Voice integration release notes at 2026-07-25 15:10:52 -->

<!-- [Chief Marketing Sweep #37] Updated Twilio Voice integration release notes at 2026-07-25 15:10:52 -->

<!-- [Chief Marketing Sweep #144] Updated Twilio Voice integration release notes at 2026-07-25 15:10:55 -->

<!-- [Chief Marketing Sweep #23] Updated Twilio Voice integration release notes at 2026-07-25 15:10:56 -->

<!-- [Chief Marketing Sweep #38] Updated Twilio Voice integration release notes at 2026-07-25 15:10:57 -->

<!-- [Chief Marketing Sweep #24] Updated Twilio Voice integration release notes at 2026-07-25 15:11:00 -->

<!-- [Chief Marketing Sweep #145] Updated Twilio Voice integration release notes at 2026-07-25 15:11:00 -->

<!-- [Chief Marketing Sweep #39] Updated Twilio Voice integration release notes at 2026-07-25 15:11:02 -->

<!-- [Chief Marketing Sweep #25] Updated Twilio Voice integration release notes at 2026-07-25 15:11:04 -->

<!-- [Chief Marketing Sweep #146] Updated Twilio Voice integration release notes at 2026-07-25 15:11:05 -->

<!-- [Chief Marketing Sweep #40] Updated Twilio Voice integration release notes at 2026-07-25 15:11:08 -->

<!-- [Chief Marketing Sweep #26] Updated Twilio Voice integration release notes at 2026-07-25 15:11:08 -->

<!-- [Chief Marketing Sweep #147] Updated Twilio Voice integration release notes at 2026-07-25 15:11:10 -->

<!-- [Chief Marketing Sweep #27] Updated Twilio Voice integration release notes at 2026-07-25 15:11:12 -->

<!-- [Chief Marketing Sweep #41] Updated Twilio Voice integration release notes at 2026-07-25 15:11:13 -->

<!-- [Chief Marketing Sweep #148] Updated Twilio Voice integration release notes at 2026-07-25 15:11:15 -->

<!-- [Chief Marketing Sweep #28] Updated Twilio Voice integration release notes at 2026-07-25 15:11:16 -->

<!-- [Chief Marketing Sweep #42] Updated Twilio Voice integration release notes at 2026-07-25 15:11:18 -->

<!-- [Chief Marketing Sweep #29] Updated Twilio Voice integration release notes at 2026-07-25 15:11:20 -->

<!-- [Chief Marketing Sweep #149] Updated Twilio Voice integration release notes at 2026-07-25 15:11:21 -->

<!-- [Chief Marketing Sweep #43] Updated Twilio Voice integration release notes at 2026-07-25 15:11:23 -->

<!-- [Chief Marketing Sweep #30] Updated Twilio Voice integration release notes at 2026-07-25 15:11:24 -->

<!-- [Chief Marketing Sweep #150] Updated Twilio Voice integration release notes at 2026-07-25 15:11:26 -->

<!-- [Chief Marketing Sweep #44] Updated Twilio Voice integration release notes at 2026-07-25 15:11:28 -->

<!-- [Chief Marketing Sweep #31] Updated Twilio Voice integration release notes at 2026-07-25 15:11:28 -->

<!-- [Chief Marketing Sweep #151] Updated Twilio Voice integration release notes at 2026-07-25 15:11:31 -->

<!-- [Chief Marketing Sweep #32] Updated Twilio Voice integration release notes at 2026-07-25 15:11:32 -->

<!-- [Chief Marketing Sweep #45] Updated Twilio Voice integration release notes at 2026-07-25 15:11:33 -->

<!-- [Chief Marketing Sweep #152] Updated Twilio Voice integration release notes at 2026-07-25 15:11:36 -->

<!-- [Chief Marketing Sweep #33] Updated Twilio Voice integration release notes at 2026-07-25 15:11:37 -->

<!-- [Chief Marketing Sweep #46] Updated Twilio Voice integration release notes at 2026-07-25 15:11:38 -->

<!-- [Chief Marketing Sweep #34] Updated Twilio Voice integration release notes at 2026-07-25 15:11:41 -->

<!-- [Chief Marketing Sweep #153] Updated Twilio Voice integration release notes at 2026-07-25 15:11:41 -->

<!-- [Chief Marketing Sweep #47] Updated Twilio Voice integration release notes at 2026-07-25 15:11:43 -->

<!-- [Chief Marketing Sweep #35] Updated Twilio Voice integration release notes at 2026-07-25 15:11:45 -->

<!-- [Chief Marketing Sweep #154] Updated Twilio Voice integration release notes at 2026-07-25 15:11:46 -->

<!-- [Chief Marketing Sweep #48] Updated Twilio Voice integration release notes at 2026-07-25 15:11:48 -->

<!-- [Chief Marketing Sweep #36] Updated Twilio Voice integration release notes at 2026-07-25 15:11:49 -->

<!-- [Chief Marketing Sweep #155] Updated Twilio Voice integration release notes at 2026-07-25 15:11:51 -->

<!-- [Chief Marketing Sweep #37] Updated Twilio Voice integration release notes at 2026-07-25 15:11:53 -->

<!-- [Chief Marketing Sweep #49] Updated Twilio Voice integration release notes at 2026-07-25 15:11:53 -->

<!-- [Chief Marketing Sweep #156] Updated Twilio Voice integration release notes at 2026-07-25 15:11:56 -->

<!-- [Chief Marketing Sweep #38] Updated Twilio Voice integration release notes at 2026-07-25 15:11:57 -->

<!-- [Chief Marketing Sweep #50] Updated Twilio Voice integration release notes at 2026-07-25 15:11:58 -->

<!-- [Chief Marketing Sweep #39] Updated Twilio Voice integration release notes at 2026-07-25 15:12:01 -->

<!-- [Chief Marketing Sweep #157] Updated Twilio Voice integration release notes at 2026-07-25 15:12:01 -->

<!-- [Chief Marketing Sweep #51] Updated Twilio Voice integration release notes at 2026-07-25 15:12:04 -->

<!-- [Chief Marketing Sweep #40] Updated Twilio Voice integration release notes at 2026-07-25 15:12:05 -->

<!-- [Chief Marketing Sweep #158] Updated Twilio Voice integration release notes at 2026-07-25 15:12:06 -->

<!-- [Chief Marketing Sweep #52] Updated Twilio Voice integration release notes at 2026-07-25 15:12:09 -->

<!-- [Chief Marketing Sweep #41] Updated Twilio Voice integration release notes at 2026-07-25 15:12:09 -->

<!-- [Chief Marketing Sweep #159] Updated Twilio Voice integration release notes at 2026-07-25 15:12:11 -->

<!-- [Chief Marketing Sweep #42] Updated Twilio Voice integration release notes at 2026-07-25 15:12:13 -->

<!-- [Chief Marketing Sweep #53] Updated Twilio Voice integration release notes at 2026-07-25 15:12:14 -->

<!-- [Chief Marketing Sweep #160] Updated Twilio Voice integration release notes at 2026-07-25 15:12:17 -->

<!-- [Chief Marketing Sweep #43] Updated Twilio Voice integration release notes at 2026-07-25 15:12:17 -->

<!-- [Chief Marketing Sweep #54] Updated Twilio Voice integration release notes at 2026-07-25 15:12:19 -->

<!-- [Chief Marketing Sweep #44] Updated Twilio Voice integration release notes at 2026-07-25 15:12:22 -->

<!-- [Chief Marketing Sweep #161] Updated Twilio Voice integration release notes at 2026-07-25 15:12:22 -->

<!-- [Chief Marketing Sweep #55] Updated Twilio Voice integration release notes at 2026-07-25 15:12:24 -->

<!-- [Chief Marketing Sweep #45] Updated Twilio Voice integration release notes at 2026-07-25 15:12:26 -->

<!-- [Chief Marketing Sweep #162] Updated Twilio Voice integration release notes at 2026-07-25 15:12:27 -->

<!-- [Chief Marketing Sweep #56] Updated Twilio Voice integration release notes at 2026-07-25 15:12:29 -->

<!-- [Chief Marketing Sweep #46] Updated Twilio Voice integration release notes at 2026-07-25 15:12:30 -->

<!-- [Chief Marketing Sweep #163] Updated Twilio Voice integration release notes at 2026-07-25 15:12:32 -->

<!-- [Chief Marketing Sweep #47] Updated Twilio Voice integration release notes at 2026-07-25 15:12:34 -->

<!-- [Chief Marketing Sweep #57] Updated Twilio Voice integration release notes at 2026-07-25 15:12:34 -->

<!-- [Chief Marketing Sweep #164] Updated Twilio Voice integration release notes at 2026-07-25 15:12:37 -->

<!-- [Chief Marketing Sweep #48] Updated Twilio Voice integration release notes at 2026-07-25 15:12:38 -->

<!-- [Chief Marketing Sweep #58] Updated Twilio Voice integration release notes at 2026-07-25 15:12:39 -->

<!-- [Chief Marketing Sweep #165] Updated Twilio Voice integration release notes at 2026-07-25 15:12:42 -->

<!-- [Chief Marketing Sweep #49] Updated Twilio Voice integration release notes at 2026-07-25 15:12:42 -->

<!-- [Chief Marketing Sweep #59] Updated Twilio Voice integration release notes at 2026-07-25 15:12:44 -->

<!-- [Chief Marketing Sweep #50] Updated Twilio Voice integration release notes at 2026-07-25 15:12:46 -->

<!-- [Chief Marketing Sweep #166] Updated Twilio Voice integration release notes at 2026-07-25 15:12:47 -->

<!-- [Chief Marketing Sweep #60] Updated Twilio Voice integration release notes at 2026-07-25 15:12:49 -->

<!-- [Chief Marketing Sweep #51] Updated Twilio Voice integration release notes at 2026-07-25 15:12:50 -->

<!-- [Chief Marketing Sweep #167] Updated Twilio Voice integration release notes at 2026-07-25 15:12:52 -->

<!-- [Chief Marketing Sweep #52] Updated Twilio Voice integration release notes at 2026-07-25 15:12:54 -->

<!-- [Chief Marketing Sweep #61] Updated Twilio Voice integration release notes at 2026-07-25 15:12:54 -->

<!-- [Chief Marketing Sweep #168] Updated Twilio Voice integration release notes at 2026-07-25 15:12:57 -->

<!-- [Chief Marketing Sweep #53] Updated Twilio Voice integration release notes at 2026-07-25 15:12:58 -->

<!-- [Chief Marketing Sweep #62] Updated Twilio Voice integration release notes at 2026-07-25 15:13:00 -->

<!-- [Chief Marketing Sweep #169] Updated Twilio Voice integration release notes at 2026-07-25 15:13:02 -->

<!-- [Chief Marketing Sweep #54] Updated Twilio Voice integration release notes at 2026-07-25 15:13:02 -->

<!-- [Chief Marketing Sweep #63] Updated Twilio Voice integration release notes at 2026-07-25 15:13:05 -->

<!-- [Chief Marketing Sweep #55] Updated Twilio Voice integration release notes at 2026-07-25 15:13:07 -->

<!-- [Chief Marketing Sweep #170] Updated Twilio Voice integration release notes at 2026-07-25 15:13:07 -->

<!-- [Chief Marketing Sweep #64] Updated Twilio Voice integration release notes at 2026-07-25 15:13:10 -->

<!-- [Chief Marketing Sweep #56] Updated Twilio Voice integration release notes at 2026-07-25 15:13:11 -->

<!-- [Chief Marketing Sweep #171] Updated Twilio Voice integration release notes at 2026-07-25 15:13:13 -->

<!-- [Chief Marketing Sweep #57] Updated Twilio Voice integration release notes at 2026-07-25 15:13:15 -->

<!-- [Chief Marketing Sweep #65] Updated Twilio Voice integration release notes at 2026-07-25 15:13:15 -->

<!-- [Chief Marketing Sweep #172] Updated Twilio Voice integration release notes at 2026-07-25 15:13:18 -->

<!-- [Chief Marketing Sweep #58] Updated Twilio Voice integration release notes at 2026-07-25 15:13:19 -->

<!-- [Chief Marketing Sweep #66] Updated Twilio Voice integration release notes at 2026-07-25 15:13:20 -->

<!-- [Chief Marketing Sweep #59] Updated Twilio Voice integration release notes at 2026-07-25 15:13:21 -->

<!-- [Chief Marketing Sweep #173] Updated Twilio Voice integration release notes at 2026-07-25 15:13:23 -->

<!-- [Chief Marketing Sweep #59] Updated Twilio Voice integration release notes at 2026-07-25 15:13:23 -->

<!-- [Chief Marketing Sweep #60] Updated Twilio Voice integration release notes at 2026-07-25 15:13:25 -->

<!-- [Chief Marketing Sweep #67] Updated Twilio Voice integration release notes at 2026-07-25 15:13:25 -->

<!-- [Chief Marketing Sweep #60] Updated Twilio Voice integration release notes at 2026-07-25 15:13:27 -->

<!-- [Chief Marketing Sweep #174] Updated Twilio Voice integration release notes at 2026-07-25 15:13:28 -->

<!-- [Chief Marketing Sweep #61] Updated Twilio Voice integration release notes at 2026-07-25 15:13:29 -->

<!-- [Chief Marketing Sweep #68] Updated Twilio Voice integration release notes at 2026-07-25 15:13:30 -->

<!-- [Chief Marketing Sweep #61] Updated Twilio Voice integration release notes at 2026-07-25 15:13:31 -->

<!-- [Chief Marketing Sweep #62] Updated Twilio Voice integration release notes at 2026-07-25 15:13:33 -->

<!-- [Chief Marketing Sweep #175] Updated Twilio Voice integration release notes at 2026-07-25 15:13:33 -->

<!-- [Chief Marketing Sweep #62] Updated Twilio Voice integration release notes at 2026-07-25 15:13:35 -->

<!-- [Chief Marketing Sweep #69] Updated Twilio Voice integration release notes at 2026-07-25 15:13:35 -->

<!-- [Chief Marketing Sweep #63] Updated Twilio Voice integration release notes at 2026-07-25 15:13:37 -->

<!-- [Chief Marketing Sweep #176] Updated Twilio Voice integration release notes at 2026-07-25 15:13:38 -->

<!-- [Chief Marketing Sweep #63] Updated Twilio Voice integration release notes at 2026-07-25 15:13:39 -->

<!-- [Chief Marketing Sweep #70] Updated Twilio Voice integration release notes at 2026-07-25 15:13:40 -->

<!-- [Chief Marketing Sweep #64] Updated Twilio Voice integration release notes at 2026-07-25 15:13:41 -->

<!-- [Chief Marketing Sweep #177] Updated Twilio Voice integration release notes at 2026-07-25 15:13:43 -->

<!-- [Chief Marketing Sweep #64] Updated Twilio Voice integration release notes at 2026-07-25 15:13:43 -->

<!-- [Chief Marketing Sweep #65] Updated Twilio Voice integration release notes at 2026-07-25 15:13:45 -->

<!-- [Chief Marketing Sweep #71] Updated Twilio Voice integration release notes at 2026-07-25 15:13:45 -->

<!-- [Chief Marketing Sweep #65] Updated Twilio Voice integration release notes at 2026-07-25 15:13:47 -->

<!-- [Chief Marketing Sweep #178] Updated Twilio Voice integration release notes at 2026-07-25 15:13:48 -->

<!-- [Chief Marketing Sweep #66] Updated Twilio Voice integration release notes at 2026-07-25 15:13:49 -->

<!-- [Chief Marketing Sweep #72] Updated Twilio Voice integration release notes at 2026-07-25 15:13:50 -->

<!-- [Chief Marketing Sweep #66] Updated Twilio Voice integration release notes at 2026-07-25 15:13:51 -->

<!-- [Chief Marketing Sweep #179] Updated Twilio Voice integration release notes at 2026-07-25 15:13:53 -->

<!-- [Chief Marketing Sweep #67] Updated Twilio Voice integration release notes at 2026-07-25 15:13:53 -->

<!-- [Chief Marketing Sweep #73] Updated Twilio Voice integration release notes at 2026-07-25 15:13:55 -->

<!-- [Chief Marketing Sweep #67] Updated Twilio Voice integration release notes at 2026-07-25 15:13:56 -->

<!-- [Chief Marketing Sweep #68] Updated Twilio Voice integration release notes at 2026-07-25 15:13:57 -->

<!-- [Chief Marketing Sweep #180] Updated Twilio Voice integration release notes at 2026-07-25 15:13:58 -->

<!-- [Chief Marketing Sweep #68] Updated Twilio Voice integration release notes at 2026-07-25 15:14:00 -->

<!-- [Chief Marketing Sweep #74] Updated Twilio Voice integration release notes at 2026-07-25 15:14:01 -->

<!-- [Chief Marketing Sweep #69] Updated Twilio Voice integration release notes at 2026-07-25 15:14:01 -->

<!-- [Chief Marketing Sweep #181] Updated Twilio Voice integration release notes at 2026-07-25 15:14:03 -->

<!-- [Chief Marketing Sweep #69] Updated Twilio Voice integration release notes at 2026-07-25 15:14:04 -->

<!-- [Chief Marketing Sweep #70] Updated Twilio Voice integration release notes at 2026-07-25 15:14:06 -->

<!-- [Chief Marketing Sweep #75] Updated Twilio Voice integration release notes at 2026-07-25 15:14:06 -->

<!-- [Chief Marketing Sweep #70] Updated Twilio Voice integration release notes at 2026-07-25 15:14:08 -->

<!-- [Chief Marketing Sweep #182] Updated Twilio Voice integration release notes at 2026-07-25 15:14:08 -->

<!-- [Chief Marketing Sweep #71] Updated Twilio Voice integration release notes at 2026-07-25 15:14:10 -->

<!-- [Chief Marketing Sweep #76] Updated Twilio Voice integration release notes at 2026-07-25 15:14:11 -->

<!-- [Chief Marketing Sweep #71] Updated Twilio Voice integration release notes at 2026-07-25 15:14:12 -->

<!-- [Chief Marketing Sweep #183] Updated Twilio Voice integration release notes at 2026-07-25 15:14:14 -->

<!-- [Chief Marketing Sweep #72] Updated Twilio Voice integration release notes at 2026-07-25 15:14:14 -->

<!-- [Chief Marketing Sweep #77] Updated Twilio Voice integration release notes at 2026-07-25 15:14:16 -->

<!-- [Chief Marketing Sweep #72] Updated Twilio Voice integration release notes at 2026-07-25 15:14:16 -->

<!-- [Chief Marketing Sweep #73] Updated Twilio Voice integration release notes at 2026-07-25 15:14:18 -->

<!-- [Chief Marketing Sweep #184] Updated Twilio Voice integration release notes at 2026-07-25 15:14:19 -->

<!-- [Chief Marketing Sweep #73] Updated Twilio Voice integration release notes at 2026-07-25 15:14:20 -->

<!-- [Chief Marketing Sweep #78] Updated Twilio Voice integration release notes at 2026-07-25 15:14:21 -->

<!-- [Chief Marketing Sweep #74] Updated Twilio Voice integration release notes at 2026-07-25 15:14:22 -->

<!-- [Chief Marketing Sweep #185] Updated Twilio Voice integration release notes at 2026-07-25 15:14:24 -->

<!-- [Chief Marketing Sweep #74] Updated Twilio Voice integration release notes at 2026-07-25 15:14:24 -->

<!-- [Chief Marketing Sweep #79] Updated Twilio Voice integration release notes at 2026-07-25 15:14:26 -->

<!-- [Chief Marketing Sweep #75] Updated Twilio Voice integration release notes at 2026-07-25 15:14:26 -->

<!-- [Chief Marketing Sweep #75] Updated Twilio Voice integration release notes at 2026-07-25 15:14:28 -->

<!-- [Chief Marketing Sweep #186] Updated Twilio Voice integration release notes at 2026-07-25 15:14:29 -->

<!-- [Chief Marketing Sweep #76] Updated Twilio Voice integration release notes at 2026-07-25 15:14:30 -->

<!-- [Chief Marketing Sweep #80] Updated Twilio Voice integration release notes at 2026-07-25 15:14:31 -->

<!-- [Chief Marketing Sweep #76] Updated Twilio Voice integration release notes at 2026-07-25 15:14:32 -->

<!-- [Chief Marketing Sweep #187] Updated Twilio Voice integration release notes at 2026-07-25 15:14:34 -->

<!-- [Chief Marketing Sweep #77] Updated Twilio Voice integration release notes at 2026-07-25 15:14:34 -->

<!-- [Chief Marketing Sweep #81] Updated Twilio Voice integration release notes at 2026-07-25 15:14:36 -->

<!-- [Chief Marketing Sweep #77] Updated Twilio Voice integration release notes at 2026-07-25 15:14:36 -->

<!-- [Chief Marketing Sweep #78] Updated Twilio Voice integration release notes at 2026-07-25 15:14:38 -->

<!-- [Chief Marketing Sweep #188] Updated Twilio Voice integration release notes at 2026-07-25 15:14:39 -->

<!-- [Chief Marketing Sweep #78] Updated Twilio Voice integration release notes at 2026-07-25 15:14:41 -->

<!-- [Chief Marketing Sweep #82] Updated Twilio Voice integration release notes at 2026-07-25 15:14:41 -->

<!-- [Chief Marketing Sweep #79] Updated Twilio Voice integration release notes at 2026-07-25 15:14:42 -->

<!-- [Chief Marketing Sweep #189] Updated Twilio Voice integration release notes at 2026-07-25 15:14:44 -->

<!-- [Chief Marketing Sweep #79] Updated Twilio Voice integration release notes at 2026-07-25 15:14:45 -->

<!-- [Chief Marketing Sweep #83] Updated Twilio Voice integration release notes at 2026-07-25 15:14:46 -->

<!-- [Chief Marketing Sweep #80] Updated Twilio Voice integration release notes at 2026-07-25 15:14:46 -->

<!-- [Chief Marketing Sweep #80] Updated Twilio Voice integration release notes at 2026-07-25 15:14:49 -->

<!-- [Chief Marketing Sweep #190] Updated Twilio Voice integration release notes at 2026-07-25 15:14:49 -->

<!-- [Chief Marketing Sweep #81] Updated Twilio Voice integration release notes at 2026-07-25 15:14:51 -->

<!-- [Chief Marketing Sweep #82] Updated Twilio Voice integration release notes at 2026-07-25 15:14:51 -->

<!-- [Chief Marketing Sweep #84] Updated Twilio Voice integration release notes at 2026-07-25 15:14:51 -->

<!-- [Chief Marketing Sweep #81] Updated Twilio Voice integration release notes at 2026-07-25 15:14:53 -->

<!-- [Chief Marketing Sweep #191] Updated Twilio Voice integration release notes at 2026-07-25 15:14:54 -->

<!-- [Chief Marketing Sweep #82] Updated Twilio Voice integration release notes at 2026-07-25 15:14:55 -->

<!-- [Chief Marketing Sweep #83] Updated Twilio Voice integration release notes at 2026-07-25 15:14:55 -->

<!-- [Chief Marketing Sweep #85] Updated Twilio Voice integration release notes at 2026-07-25 15:14:57 -->

<!-- [Chief Marketing Sweep #82] Updated Twilio Voice integration release notes at 2026-07-25 15:14:57 -->

<!-- [Chief Marketing Sweep #83] Updated Twilio Voice integration release notes at 2026-07-25 15:14:59 -->

<!-- [Chief Marketing Sweep #84] Updated Twilio Voice integration release notes at 2026-07-25 15:14:59 -->

<!-- [Chief Marketing Sweep #192] Updated Twilio Voice integration release notes at 2026-07-25 15:15:00 -->

<!-- [Chief Marketing Sweep #83] Updated Twilio Voice integration release notes at 2026-07-25 15:15:01 -->

<!-- [Chief Marketing Sweep #86] Updated Twilio Voice integration release notes at 2026-07-25 15:15:02 -->

<!-- [Chief Marketing Sweep #84] Updated Twilio Voice integration release notes at 2026-07-25 15:15:03 -->

<!-- [Chief Marketing Sweep #85] Updated Twilio Voice integration release notes at 2026-07-25 15:15:03 -->

<!-- [Chief Marketing Sweep #193] Updated Twilio Voice integration release notes at 2026-07-25 15:15:05 -->

<!-- [Chief Marketing Sweep #84] Updated Twilio Voice integration release notes at 2026-07-25 15:15:05 -->

<!-- [Chief Marketing Sweep #87] Updated Twilio Voice integration release notes at 2026-07-25 15:15:07 -->

<!-- [Chief Marketing Sweep #85] Updated Twilio Voice integration release notes at 2026-07-25 15:15:07 -->

<!-- [Chief Marketing Sweep #86] Updated Twilio Voice integration release notes at 2026-07-25 15:15:07 -->

<!-- [Chief Marketing Sweep #85] Updated Twilio Voice integration release notes at 2026-07-25 15:15:09 -->

<!-- [Chief Marketing Sweep #194] Updated Twilio Voice integration release notes at 2026-07-25 15:15:10 -->

<!-- [Chief Marketing Sweep #86] Updated Twilio Voice integration release notes at 2026-07-25 15:15:11 -->

<!-- [Chief Marketing Sweep #87] Updated Twilio Voice integration release notes at 2026-07-25 15:15:11 -->

<!-- [Chief Marketing Sweep #88] Updated Twilio Voice integration release notes at 2026-07-25 15:15:12 -->

<!-- [Chief Marketing Sweep #86] Updated Twilio Voice integration release notes at 2026-07-25 15:15:13 -->

<!-- [Chief Marketing Sweep #195] Updated Twilio Voice integration release notes at 2026-07-25 15:15:15 -->

<!-- [Chief Marketing Sweep #87] Updated Twilio Voice integration release notes at 2026-07-25 15:15:15 -->

<!-- [Chief Marketing Sweep #88] Updated Twilio Voice integration release notes at 2026-07-25 15:15:15 -->

<!-- [Chief Marketing Sweep #89] Updated Twilio Voice integration release notes at 2026-07-25 15:15:17 -->

<!-- [Chief Marketing Sweep #87] Updated Twilio Voice integration release notes at 2026-07-25 15:15:17 -->

<!-- [Chief Marketing Sweep #88] Updated Twilio Voice integration release notes at 2026-07-25 15:15:19 -->

<!-- [Chief Marketing Sweep #89] Updated Twilio Voice integration release notes at 2026-07-25 15:15:19 -->

<!-- [Chief Marketing Sweep #196] Updated Twilio Voice integration release notes at 2026-07-25 15:15:20 -->

<!-- [Chief Marketing Sweep #88] Updated Twilio Voice integration release notes at 2026-07-25 15:15:22 -->

<!-- [Chief Marketing Sweep #90] Updated Twilio Voice integration release notes at 2026-07-25 15:15:22 -->

<!-- [Chief Marketing Sweep #89] Updated Twilio Voice integration release notes at 2026-07-25 15:15:23 -->

<!-- [Chief Marketing Sweep #90] Updated Twilio Voice integration release notes at 2026-07-25 15:15:24 -->

<!-- [Chief Marketing Sweep #197] Updated Twilio Voice integration release notes at 2026-07-25 15:15:25 -->

<!-- [Chief Marketing Sweep #89] Updated Twilio Voice integration release notes at 2026-07-25 15:15:26 -->

<!-- [Chief Marketing Sweep #91] Updated Twilio Voice integration release notes at 2026-07-25 15:15:27 -->

<!-- [Chief Marketing Sweep #90] Updated Twilio Voice integration release notes at 2026-07-25 15:15:27 -->

<!-- [Chief Marketing Sweep #91] Updated Twilio Voice integration release notes at 2026-07-25 15:15:28 -->

<!-- [Chief Marketing Sweep #90] Updated Twilio Voice integration release notes at 2026-07-25 15:15:30 -->

<!-- [Chief Marketing Sweep #198] Updated Twilio Voice integration release notes at 2026-07-25 15:15:30 -->

<!-- [Chief Marketing Sweep #91] Updated Twilio Voice integration release notes at 2026-07-25 15:15:31 -->

<!-- [Chief Marketing Sweep #92] Updated Twilio Voice integration release notes at 2026-07-25 15:15:32 -->

<!-- [Chief Marketing Sweep #92] Updated Twilio Voice integration release notes at 2026-07-25 15:15:32 -->

<!-- [Chief Marketing Sweep #91] Updated Twilio Voice integration release notes at 2026-07-25 15:15:34 -->

<!-- [Chief Marketing Sweep #199] Updated Twilio Voice integration release notes at 2026-07-25 15:15:35 -->

<!-- [Chief Marketing Sweep #92] Updated Twilio Voice integration release notes at 2026-07-25 15:15:36 -->

<!-- [Chief Marketing Sweep #93] Updated Twilio Voice integration release notes at 2026-07-25 15:15:36 -->

<!-- [Chief Marketing Sweep #93] Updated Twilio Voice integration release notes at 2026-07-25 15:15:37 -->

<!-- [Chief Marketing Sweep #92] Updated Twilio Voice integration release notes at 2026-07-25 15:15:38 -->

<!-- [Chief Marketing Sweep #93] Updated Twilio Voice integration release notes at 2026-07-25 15:15:40 -->

<!-- [Chief Marketing Sweep #94] Updated Twilio Voice integration release notes at 2026-07-25 15:15:40 -->

<!-- [Chief Marketing Sweep #200] Updated Twilio Voice integration release notes at 2026-07-25 15:15:40 -->

<!-- [Chief Marketing Sweep #93] Updated Twilio Voice integration release notes at 2026-07-25 15:15:42 -->

<!-- [Chief Marketing Sweep #94] Updated Twilio Voice integration release notes at 2026-07-25 15:15:42 -->

<!-- [Chief Marketing Sweep #94] Updated Twilio Voice integration release notes at 2026-07-25 15:15:44 -->

<!-- [Chief Marketing Sweep #95] Updated Twilio Voice integration release notes at 2026-07-25 15:15:44 -->

<!-- [Chief Marketing Sweep #201] Updated Twilio Voice integration release notes at 2026-07-25 15:15:45 -->

<!-- [Chief Marketing Sweep #94] Updated Twilio Voice integration release notes at 2026-07-25 15:15:46 -->

<!-- [Chief Marketing Sweep #95] Updated Twilio Voice integration release notes at 2026-07-25 15:15:48 -->

<!-- [Chief Marketing Sweep #95] Updated Twilio Voice integration release notes at 2026-07-25 15:15:48 -->

<!-- [Chief Marketing Sweep #96] Updated Twilio Voice integration release notes at 2026-07-25 15:15:48 -->

<!-- [Chief Marketing Sweep #95] Updated Twilio Voice integration release notes at 2026-07-25 15:15:50 -->

<!-- [Chief Marketing Sweep #202] Updated Twilio Voice integration release notes at 2026-07-25 15:15:50 -->

<!-- [Chief Marketing Sweep #96] Updated Twilio Voice integration release notes at 2026-07-25 15:15:52 -->

<!-- [Chief Marketing Sweep #97] Updated Twilio Voice integration release notes at 2026-07-25 15:15:52 -->

<!-- [Chief Marketing Sweep #96] Updated Twilio Voice integration release notes at 2026-07-25 15:15:53 -->

<!-- [Chief Marketing Sweep #96] Updated Twilio Voice integration release notes at 2026-07-25 15:15:54 -->

<!-- [Chief Marketing Sweep #203] Updated Twilio Voice integration release notes at 2026-07-25 15:15:56 -->

<!-- [Chief Marketing Sweep #97] Updated Twilio Voice integration release notes at 2026-07-25 15:15:56 -->

<!-- [Chief Marketing Sweep #98] Updated Twilio Voice integration release notes at 2026-07-25 15:15:56 -->

<!-- [Chief Marketing Sweep #97] Updated Twilio Voice integration release notes at 2026-07-25 15:15:58 -->

<!-- [Chief Marketing Sweep #97] Updated Twilio Voice integration release notes at 2026-07-25 15:15:58 -->

<!-- [Chief Marketing Sweep #98] Updated Twilio Voice integration release notes at 2026-07-25 15:16:00 -->

<!-- [Chief Marketing Sweep #99] Updated Twilio Voice integration release notes at 2026-07-25 15:16:01 -->

<!-- [Chief Marketing Sweep #204] Updated Twilio Voice integration release notes at 2026-07-25 15:16:01 -->

<!-- [Chief Marketing Sweep #98] Updated Twilio Voice integration release notes at 2026-07-25 15:16:03 -->

<!-- [Chief Marketing Sweep #98] Updated Twilio Voice integration release notes at 2026-07-25 15:16:03 -->

<!-- [Chief Marketing Sweep #99] Updated Twilio Voice integration release notes at 2026-07-25 15:16:04 -->

<!-- [Chief Marketing Sweep #100] Updated Twilio Voice integration release notes at 2026-07-25 15:16:05 -->

<!-- [Chief Marketing Sweep #205] Updated Twilio Voice integration release notes at 2026-07-25 15:16:06 -->

<!-- [Chief Marketing Sweep #99] Updated Twilio Voice integration release notes at 2026-07-25 15:16:07 -->

<!-- [Chief Marketing Sweep #99] Updated Twilio Voice integration release notes at 2026-07-25 15:16:08 -->

<!-- [Chief Marketing Sweep #100] Updated Twilio Voice integration release notes at 2026-07-25 15:16:08 -->

<!-- [Chief Marketing Sweep #101] Updated Twilio Voice integration release notes at 2026-07-25 15:16:09 -->

<!-- [Chief Marketing Sweep #100] Updated Twilio Voice integration release notes at 2026-07-25 15:16:11 -->

<!-- [Chief Marketing Sweep #206] Updated Twilio Voice integration release notes at 2026-07-25 15:16:11 -->

<!-- [Chief Marketing Sweep #101] Updated Twilio Voice integration release notes at 2026-07-25 15:16:12 -->

<!-- [Chief Marketing Sweep #102] Updated Twilio Voice integration release notes at 2026-07-25 15:16:13 -->

<!-- [Chief Marketing Sweep #100] Updated Twilio Voice integration release notes at 2026-07-25 15:16:13 -->

<!-- [Chief Marketing Sweep #101] Updated Twilio Voice integration release notes at 2026-07-25 15:16:15 -->

<!-- [Chief Marketing Sweep #207] Updated Twilio Voice integration release notes at 2026-07-25 15:16:16 -->

<!-- [Chief Marketing Sweep #102] Updated Twilio Voice integration release notes at 2026-07-25 15:16:17 -->

<!-- [Chief Marketing Sweep #103] Updated Twilio Voice integration release notes at 2026-07-25 15:16:17 -->

<!-- [Chief Marketing Sweep #101] Updated Twilio Voice integration release notes at 2026-07-25 15:16:18 -->

<!-- [Chief Marketing Sweep #102] Updated Twilio Voice integration release notes at 2026-07-25 15:16:19 -->

<!-- [Chief Marketing Sweep #103] Updated Twilio Voice integration release notes at 2026-07-25 15:16:21 -->

<!-- [Chief Marketing Sweep #104] Updated Twilio Voice integration release notes at 2026-07-25 15:16:21 -->

<!-- [Chief Marketing Sweep #208] Updated Twilio Voice integration release notes at 2026-07-25 15:16:21 -->

<!-- [Chief Marketing Sweep #103] Updated Twilio Voice integration release notes at 2026-07-25 15:16:23 -->

<!-- [Chief Marketing Sweep #102] Updated Twilio Voice integration release notes at 2026-07-25 15:16:23 -->

<!-- [Chief Marketing Sweep #104] Updated Twilio Voice integration release notes at 2026-07-25 15:16:25 -->

<!-- [Chief Marketing Sweep #105] Updated Twilio Voice integration release notes at 2026-07-25 15:16:25 -->

<!-- [Chief Marketing Sweep #209] Updated Twilio Voice integration release notes at 2026-07-25 15:16:26 -->

<!-- [Chief Marketing Sweep #104] Updated Twilio Voice integration release notes at 2026-07-25 15:16:27 -->

<!-- [Chief Marketing Sweep #103] Updated Twilio Voice integration release notes at 2026-07-25 15:16:28 -->

<!-- [Chief Marketing Sweep #105] Updated Twilio Voice integration release notes at 2026-07-25 15:16:29 -->

<!-- [Chief Marketing Sweep #106] Updated Twilio Voice integration release notes at 2026-07-25 15:16:29 -->

<!-- [Chief Marketing Sweep #210] Updated Twilio Voice integration release notes at 2026-07-25 15:16:31 -->

<!-- [Chief Marketing Sweep #105] Updated Twilio Voice integration release notes at 2026-07-25 15:16:31 -->

<!-- [Chief Marketing Sweep #106] Updated Twilio Voice integration release notes at 2026-07-25 15:16:33 -->

<!-- [Chief Marketing Sweep #107] Updated Twilio Voice integration release notes at 2026-07-25 15:16:33 -->

<!-- [Chief Marketing Sweep #104] Updated Twilio Voice integration release notes at 2026-07-25 15:16:33 -->

<!-- [Chief Marketing Sweep #106] Updated Twilio Voice integration release notes at 2026-07-25 15:16:35 -->

<!-- [Chief Marketing Sweep #211] Updated Twilio Voice integration release notes at 2026-07-25 15:16:36 -->

<!-- [Chief Marketing Sweep #107] Updated Twilio Voice integration release notes at 2026-07-25 15:16:37 -->

<!-- [Chief Marketing Sweep #108] Updated Twilio Voice integration release notes at 2026-07-25 15:16:37 -->

<!-- [Chief Marketing Sweep #105] Updated Twilio Voice integration release notes at 2026-07-25 15:16:38 -->

<!-- [Chief Marketing Sweep #107] Updated Twilio Voice integration release notes at 2026-07-25 15:16:39 -->

<!-- [Chief Marketing Sweep #108] Updated Twilio Voice integration release notes at 2026-07-25 15:16:41 -->

<!-- [Chief Marketing Sweep #212] Updated Twilio Voice integration release notes at 2026-07-25 15:16:41 -->

<!-- [Chief Marketing Sweep #109] Updated Twilio Voice integration release notes at 2026-07-25 15:16:41 -->

<!-- [Chief Marketing Sweep #108] Updated Twilio Voice integration release notes at 2026-07-25 15:16:43 -->

<!-- [Chief Marketing Sweep #106] Updated Twilio Voice integration release notes at 2026-07-25 15:16:44 -->

<!-- [Chief Marketing Sweep #109] Updated Twilio Voice integration release notes at 2026-07-25 15:16:45 -->

<!-- [Chief Marketing Sweep #110] Updated Twilio Voice integration release notes at 2026-07-25 15:16:46 -->

<!-- [Chief Marketing Sweep #213] Updated Twilio Voice integration release notes at 2026-07-25 15:16:46 -->

<!-- [Chief Marketing Sweep #109] Updated Twilio Voice integration release notes at 2026-07-25 15:16:48 -->

<!-- [Chief Marketing Sweep #107] Updated Twilio Voice integration release notes at 2026-07-25 15:16:49 -->

<!-- [Chief Marketing Sweep #110] Updated Twilio Voice integration release notes at 2026-07-25 15:16:49 -->

<!-- [Chief Marketing Sweep #111] Updated Twilio Voice integration release notes at 2026-07-25 15:16:50 -->

<!-- [Chief Marketing Sweep #213] Updated Twilio Voice integration release notes at 2026-07-25 15:16:52 -->

<!-- [Chief Marketing Sweep #110] Updated Twilio Voice integration release notes at 2026-07-25 15:16:52 -->

<!-- [Chief Marketing Sweep #111] Updated Twilio Voice integration release notes at 2026-07-25 15:16:53 -->

<!-- [Chief Marketing Sweep #112] Updated Twilio Voice integration release notes at 2026-07-25 15:16:54 -->

<!-- [Chief Marketing Sweep #108] Updated Twilio Voice integration release notes at 2026-07-25 15:16:54 -->

<!-- [Chief Marketing Sweep #111] Updated Twilio Voice integration release notes at 2026-07-25 15:16:56 -->

<!-- [Chief Marketing Sweep #214] Updated Twilio Voice integration release notes at 2026-07-25 15:16:57 -->

<!-- [Chief Marketing Sweep #112] Updated Twilio Voice integration release notes at 2026-07-25 15:16:58 -->

<!-- [Chief Marketing Sweep #113] Updated Twilio Voice integration release notes at 2026-07-25 15:16:58 -->

<!-- [Chief Marketing Sweep #109] Updated Twilio Voice integration release notes at 2026-07-25 15:16:59 -->

<!-- [Chief Marketing Sweep #112] Updated Twilio Voice integration release notes at 2026-07-25 15:17:00 -->

<!-- [Chief Marketing Sweep #113] Updated Twilio Voice integration release notes at 2026-07-25 15:17:02 -->

<!-- [Chief Marketing Sweep #215] Updated Twilio Voice integration release notes at 2026-07-25 15:17:02 -->

<!-- [Chief Marketing Sweep #114] Updated Twilio Voice integration release notes at 2026-07-25 15:17:02 -->

<!-- [Chief Marketing Sweep #110] Updated Twilio Voice integration release notes at 2026-07-25 15:17:04 -->

<!-- [Chief Marketing Sweep #113] Updated Twilio Voice integration release notes at 2026-07-25 15:17:04 -->

<!-- [Chief Marketing Sweep #114] Updated Twilio Voice integration release notes at 2026-07-25 15:17:06 -->

<!-- [Chief Marketing Sweep #115] Updated Twilio Voice integration release notes at 2026-07-25 15:17:06 -->

<!-- [Chief Marketing Sweep #216] Updated Twilio Voice integration release notes at 2026-07-25 15:17:07 -->

<!-- [Chief Marketing Sweep #114] Updated Twilio Voice integration release notes at 2026-07-25 15:17:08 -->

<!-- [Chief Marketing Sweep #111] Updated Twilio Voice integration release notes at 2026-07-25 15:17:09 -->

<!-- [Chief Marketing Sweep #115] Updated Twilio Voice integration release notes at 2026-07-25 15:17:10 -->

<!-- [Chief Marketing Sweep #116] Updated Twilio Voice integration release notes at 2026-07-25 15:17:10 -->

<!-- [Chief Marketing Sweep #217] Updated Twilio Voice integration release notes at 2026-07-25 15:17:12 -->

<!-- [Chief Marketing Sweep #115] Updated Twilio Voice integration release notes at 2026-07-25 15:17:12 -->

<!-- [Chief Marketing Sweep #116] Updated Twilio Voice integration release notes at 2026-07-25 15:17:14 -->

<!-- [Chief Marketing Sweep #112] Updated Twilio Voice integration release notes at 2026-07-25 15:17:14 -->

<!-- [Chief Marketing Sweep #117] Updated Twilio Voice integration release notes at 2026-07-25 15:17:14 -->

<!-- [Chief Marketing Sweep #116] Updated Twilio Voice integration release notes at 2026-07-25 15:17:16 -->

<!-- [Chief Marketing Sweep #218] Updated Twilio Voice integration release notes at 2026-07-25 15:17:17 -->

<!-- [Chief Marketing Sweep #117] Updated Twilio Voice integration release notes at 2026-07-25 15:17:18 -->

<!-- [Chief Marketing Sweep #118] Updated Twilio Voice integration release notes at 2026-07-25 15:17:18 -->

<!-- [Chief Marketing Sweep #113] Updated Twilio Voice integration release notes at 2026-07-25 15:17:19 -->

<!-- [Chief Marketing Sweep #117] Updated Twilio Voice integration release notes at 2026-07-25 15:17:20 -->

<!-- [Chief Marketing Sweep #118] Updated Twilio Voice integration release notes at 2026-07-25 15:17:22 -->

<!-- [Chief Marketing Sweep #219] Updated Twilio Voice integration release notes at 2026-07-25 15:17:22 -->

<!-- [Chief Marketing Sweep #118] Updated Twilio Voice integration release notes at 2026-07-25 15:17:22 -->

<!-- [Chief Marketing Sweep #119] Updated Twilio Voice integration release notes at 2026-07-25 15:17:22 -->

<!-- [Chief Marketing Sweep #114] Updated Twilio Voice integration release notes at 2026-07-25 15:17:24 -->

<!-- [Chief Marketing Sweep #118] Updated Twilio Voice integration release notes at 2026-07-25 15:17:24 -->

<!-- [Chief Marketing Sweep #119] Updated Twilio Voice integration release notes at 2026-07-25 15:17:26 -->

<!-- [Chief Marketing Sweep #119] Updated Twilio Voice integration release notes at 2026-07-25 15:17:26 -->

<!-- [Chief Marketing Sweep #120] Updated Twilio Voice integration release notes at 2026-07-25 15:17:27 -->

<!-- [Chief Marketing Sweep #220] Updated Twilio Voice integration release notes at 2026-07-25 15:17:27 -->

<!-- [Chief Marketing Sweep #119] Updated Twilio Voice integration release notes at 2026-07-25 15:17:29 -->

<!-- [Chief Marketing Sweep #115] Updated Twilio Voice integration release notes at 2026-07-25 15:17:29 -->

<!-- [Chief Marketing Sweep #120] Updated Twilio Voice integration release notes at 2026-07-25 15:17:30 -->

<!-- [Chief Marketing Sweep #120] Updated Twilio Voice integration release notes at 2026-07-25 15:17:30 -->

<!-- [Chief Marketing Sweep #121] Updated Twilio Voice integration release notes at 2026-07-25 15:17:31 -->

<!-- [Chief Marketing Sweep #221] Updated Twilio Voice integration release notes at 2026-07-25 15:17:32 -->

<!-- [Chief Marketing Sweep #120] Updated Twilio Voice integration release notes at 2026-07-25 15:17:33 -->

<!-- [Chief Marketing Sweep #121] Updated Twilio Voice integration release notes at 2026-07-25 15:17:34 -->

<!-- [Chief Marketing Sweep #121] Updated Twilio Voice integration release notes at 2026-07-25 15:17:34 -->

<!-- [Chief Marketing Sweep #116] Updated Twilio Voice integration release notes at 2026-07-25 15:17:34 -->

<!-- [Chief Marketing Sweep #122] Updated Twilio Voice integration release notes at 2026-07-25 15:17:35 -->

<!-- [Chief Marketing Sweep #121] Updated Twilio Voice integration release notes at 2026-07-25 15:17:37 -->

<!-- [Chief Marketing Sweep #222] Updated Twilio Voice integration release notes at 2026-07-25 15:17:37 -->

<!-- [Chief Marketing Sweep #122] Updated Twilio Voice integration release notes at 2026-07-25 15:17:38 -->

<!-- [Chief Marketing Sweep #122] Updated Twilio Voice integration release notes at 2026-07-25 15:17:39 -->

<!-- [Chief Marketing Sweep #123] Updated Twilio Voice integration release notes at 2026-07-25 15:17:39 -->

<!-- [Chief Marketing Sweep #117] Updated Twilio Voice integration release notes at 2026-07-25 15:17:40 -->

<!-- [Chief Marketing Sweep #122] Updated Twilio Voice integration release notes at 2026-07-25 15:17:41 -->

<!-- [Chief Marketing Sweep #223] Updated Twilio Voice integration release notes at 2026-07-25 15:17:42 -->

<!-- [Chief Marketing Sweep #123] Updated Twilio Voice integration release notes at 2026-07-25 15:17:42 -->

<!-- [Chief Marketing Sweep #123] Updated Twilio Voice integration release notes at 2026-07-25 15:17:43 -->

<!-- [Chief Marketing Sweep #124] Updated Twilio Voice integration release notes at 2026-07-25 15:17:43 -->

<!-- [Chief Marketing Sweep #118] Updated Twilio Voice integration release notes at 2026-07-25 15:17:45 -->

<!-- [Chief Marketing Sweep #123] Updated Twilio Voice integration release notes at 2026-07-25 15:17:45 -->

<!-- [Chief Marketing Sweep #124] Updated Twilio Voice integration release notes at 2026-07-25 15:17:47 -->

<!-- [Chief Marketing Sweep #124] Updated Twilio Voice integration release notes at 2026-07-25 15:17:47 -->

<!-- [Chief Marketing Sweep #125] Updated Twilio Voice integration release notes at 2026-07-25 15:17:47 -->

<!-- [Chief Marketing Sweep #224] Updated Twilio Voice integration release notes at 2026-07-25 15:17:48 -->

<!-- [Chief Marketing Sweep #124] Updated Twilio Voice integration release notes at 2026-07-25 15:17:49 -->

<!-- [Chief Marketing Sweep #119] Updated Twilio Voice integration release notes at 2026-07-25 15:17:50 -->

<!-- [Chief Marketing Sweep #125] Updated Twilio Voice integration release notes at 2026-07-25 15:17:51 -->

<!-- [Chief Marketing Sweep #125] Updated Twilio Voice integration release notes at 2026-07-25 15:17:51 -->

<!-- [Chief Marketing Sweep #126] Updated Twilio Voice integration release notes at 2026-07-25 15:17:51 -->

<!-- [Chief Marketing Sweep #225] Updated Twilio Voice integration release notes at 2026-07-25 15:17:53 -->

<!-- [Chief Marketing Sweep #125] Updated Twilio Voice integration release notes at 2026-07-25 15:17:53 -->

<!-- [Chief Marketing Sweep #126] Updated Twilio Voice integration release notes at 2026-07-25 15:17:55 -->

<!-- [Chief Marketing Sweep #120] Updated Twilio Voice integration release notes at 2026-07-25 15:17:55 -->

<!-- [Chief Marketing Sweep #126] Updated Twilio Voice integration release notes at 2026-07-25 15:17:55 -->

<!-- [Chief Marketing Sweep #127] Updated Twilio Voice integration release notes at 2026-07-25 15:17:55 -->

<!-- [Chief Marketing Sweep #126] Updated Twilio Voice integration release notes at 2026-07-25 15:17:57 -->

<!-- [Chief Marketing Sweep #226] Updated Twilio Voice integration release notes at 2026-07-25 15:17:58 -->

<!-- [Chief Marketing Sweep #127] Updated Twilio Voice integration release notes at 2026-07-25 15:17:59 -->

<!-- [Chief Marketing Sweep #127] Updated Twilio Voice integration release notes at 2026-07-25 15:17:59 -->

<!-- [Chief Marketing Sweep #128] Updated Twilio Voice integration release notes at 2026-07-25 15:17:59 -->

<!-- [Chief Marketing Sweep #121] Updated Twilio Voice integration release notes at 2026-07-25 15:18:00 -->

<!-- [Chief Marketing Sweep #127] Updated Twilio Voice integration release notes at 2026-07-25 15:18:01 -->

<!-- [Chief Marketing Sweep #227] Updated Twilio Voice integration release notes at 2026-07-25 15:18:03 -->

<!-- [Chief Marketing Sweep #128] Updated Twilio Voice integration release notes at 2026-07-25 15:18:03 -->

<!-- [Chief Marketing Sweep #128] Updated Twilio Voice integration release notes at 2026-07-25 15:18:03 -->

<!-- [Chief Marketing Sweep #129] Updated Twilio Voice integration release notes at 2026-07-25 15:18:04 -->

<!-- [Chief Marketing Sweep #122] Updated Twilio Voice integration release notes at 2026-07-25 15:18:05 -->

<!-- [Chief Marketing Sweep #128] Updated Twilio Voice integration release notes at 2026-07-25 15:18:06 -->

<!-- [Chief Marketing Sweep #129] Updated Twilio Voice integration release notes at 2026-07-25 15:18:07 -->

<!-- [Chief Marketing Sweep #129] Updated Twilio Voice integration release notes at 2026-07-25 15:18:07 -->

<!-- [Chief Marketing Sweep #130] Updated Twilio Voice integration release notes at 2026-07-25 15:18:08 -->

<!-- [Chief Marketing Sweep #228] Updated Twilio Voice integration release notes at 2026-07-25 15:18:08 -->

<!-- [Chief Marketing Sweep #129] Updated Twilio Voice integration release notes at 2026-07-25 15:18:10 -->

<!-- [Chief Marketing Sweep #123] Updated Twilio Voice integration release notes at 2026-07-25 15:18:10 -->

<!-- [Chief Marketing Sweep #130] Updated Twilio Voice integration release notes at 2026-07-25 15:18:11 -->

<!-- [Chief Marketing Sweep #130] Updated Twilio Voice integration release notes at 2026-07-25 15:18:11 -->

<!-- [Chief Marketing Sweep #131] Updated Twilio Voice integration release notes at 2026-07-25 15:18:12 -->

<!-- [Chief Marketing Sweep #229] Updated Twilio Voice integration release notes at 2026-07-25 15:18:13 -->

<!-- [Chief Marketing Sweep #130] Updated Twilio Voice integration release notes at 2026-07-25 15:18:14 -->

<!-- [Chief Marketing Sweep #131] Updated Twilio Voice integration release notes at 2026-07-25 15:18:15 -->

<!-- [Chief Marketing Sweep #124] Updated Twilio Voice integration release notes at 2026-07-25 15:18:15 -->

<!-- [Chief Marketing Sweep #131] Updated Twilio Voice integration release notes at 2026-07-25 15:18:15 -->

<!-- [Chief Marketing Sweep #132] Updated Twilio Voice integration release notes at 2026-07-25 15:18:16 -->

<!-- [Chief Marketing Sweep #131] Updated Twilio Voice integration release notes at 2026-07-25 15:18:18 -->

<!-- [Chief Marketing Sweep #230] Updated Twilio Voice integration release notes at 2026-07-25 15:18:18 -->

<!-- [Chief Marketing Sweep #132] Updated Twilio Voice integration release notes at 2026-07-25 15:18:19 -->

<!-- [Chief Marketing Sweep #132] Updated Twilio Voice integration release notes at 2026-07-25 15:18:20 -->

<!-- [Chief Marketing Sweep #133] Updated Twilio Voice integration release notes at 2026-07-25 15:18:20 -->

<!-- [Chief Marketing Sweep #125] Updated Twilio Voice integration release notes at 2026-07-25 15:18:20 -->

<!-- [Chief Marketing Sweep #132] Updated Twilio Voice integration release notes at 2026-07-25 15:18:22 -->

<!-- [Chief Marketing Sweep #231] Updated Twilio Voice integration release notes at 2026-07-25 15:18:23 -->

<!-- [Chief Marketing Sweep #133] Updated Twilio Voice integration release notes at 2026-07-25 15:18:23 -->

<!-- [Chief Marketing Sweep #133] Updated Twilio Voice integration release notes at 2026-07-25 15:18:24 -->

<!-- [Chief Marketing Sweep #134] Updated Twilio Voice integration release notes at 2026-07-25 15:18:24 -->

<!-- [Chief Marketing Sweep #126] Updated Twilio Voice integration release notes at 2026-07-25 15:18:25 -->

<!-- [Chief Marketing Sweep #133] Updated Twilio Voice integration release notes at 2026-07-25 15:18:26 -->

<!-- [Chief Marketing Sweep #134] Updated Twilio Voice integration release notes at 2026-07-25 15:18:28 -->

<!-- [Chief Marketing Sweep #134] Updated Twilio Voice integration release notes at 2026-07-25 15:18:28 -->

<!-- [Chief Marketing Sweep #135] Updated Twilio Voice integration release notes at 2026-07-25 15:18:28 -->

<!-- [Chief Marketing Sweep #232] Updated Twilio Voice integration release notes at 2026-07-25 15:18:28 -->

<!-- [Chief Marketing Sweep #134] Updated Twilio Voice integration release notes at 2026-07-25 15:18:30 -->

<!-- [Chief Marketing Sweep #127] Updated Twilio Voice integration release notes at 2026-07-25 15:18:31 -->

<!-- [Chief Marketing Sweep #135] Updated Twilio Voice integration release notes at 2026-07-25 15:18:32 -->

<!-- [Chief Marketing Sweep #135] Updated Twilio Voice integration release notes at 2026-07-25 15:18:32 -->

<!-- [Chief Marketing Sweep #136] Updated Twilio Voice integration release notes at 2026-07-25 15:18:32 -->

<!-- [Chief Marketing Sweep #233] Updated Twilio Voice integration release notes at 2026-07-25 15:18:33 -->

<!-- [Chief Marketing Sweep #135] Updated Twilio Voice integration release notes at 2026-07-25 15:18:34 -->

<!-- [Chief Marketing Sweep #128] Updated Twilio Voice integration release notes at 2026-07-25 15:18:36 -->

<!-- [Chief Marketing Sweep #136] Updated Twilio Voice integration release notes at 2026-07-25 15:18:36 -->

<!-- [Chief Marketing Sweep #136] Updated Twilio Voice integration release notes at 2026-07-25 15:18:36 -->

<!-- [Chief Marketing Sweep #137] Updated Twilio Voice integration release notes at 2026-07-25 15:18:36 -->

<!-- [Chief Marketing Sweep #234] Updated Twilio Voice integration release notes at 2026-07-25 15:18:38 -->

<!-- [Chief Marketing Sweep #136] Updated Twilio Voice integration release notes at 2026-07-25 15:18:38 -->

<!-- [Chief Marketing Sweep #137] Updated Twilio Voice integration release notes at 2026-07-25 15:18:40 -->

<!-- [Chief Marketing Sweep #137] Updated Twilio Voice integration release notes at 2026-07-25 15:18:40 -->

<!-- [Chief Marketing Sweep #138] Updated Twilio Voice integration release notes at 2026-07-25 15:18:41 -->

<!-- [Chief Marketing Sweep #129] Updated Twilio Voice integration release notes at 2026-07-25 15:18:41 -->

<!-- [Chief Marketing Sweep #137] Updated Twilio Voice integration release notes at 2026-07-25 15:18:42 -->

<!-- [Chief Marketing Sweep #235] Updated Twilio Voice integration release notes at 2026-07-25 15:18:43 -->

<!-- [Chief Marketing Sweep #138] Updated Twilio Voice integration release notes at 2026-07-25 15:18:44 -->

<!-- [Chief Marketing Sweep #138] Updated Twilio Voice integration release notes at 2026-07-25 15:18:44 -->

<!-- [Chief Marketing Sweep #139] Updated Twilio Voice integration release notes at 2026-07-25 15:18:45 -->

<!-- [Chief Marketing Sweep #130] Updated Twilio Voice integration release notes at 2026-07-25 15:18:46 -->

<!-- [Chief Marketing Sweep #138] Updated Twilio Voice integration release notes at 2026-07-25 15:18:47 -->

<!-- [Chief Marketing Sweep #139] Updated Twilio Voice integration release notes at 2026-07-25 15:18:48 -->

<!-- [Chief Marketing Sweep #139] Updated Twilio Voice integration release notes at 2026-07-25 15:18:48 -->

<!-- [Chief Marketing Sweep #236] Updated Twilio Voice integration release notes at 2026-07-25 15:18:49 -->

<!-- [Chief Marketing Sweep #140] Updated Twilio Voice integration release notes at 2026-07-25 15:18:49 -->

<!-- [Chief Marketing Sweep #139] Updated Twilio Voice integration release notes at 2026-07-25 15:18:51 -->

<!-- [Chief Marketing Sweep #131] Updated Twilio Voice integration release notes at 2026-07-25 15:18:51 -->

<!-- [Chief Marketing Sweep #140] Updated Twilio Voice integration release notes at 2026-07-25 15:18:52 -->

<!-- [Chief Marketing Sweep #140] Updated Twilio Voice integration release notes at 2026-07-25 15:18:52 -->

<!-- [Chief Marketing Sweep #141] Updated Twilio Voice integration release notes at 2026-07-25 15:18:53 -->

<!-- [Chief Marketing Sweep #237] Updated Twilio Voice integration release notes at 2026-07-25 15:18:54 -->

<!-- [Chief Marketing Sweep #140] Updated Twilio Voice integration release notes at 2026-07-25 15:18:55 -->

<!-- [Chief Marketing Sweep #132] Updated Twilio Voice integration release notes at 2026-07-25 15:18:56 -->

<!-- [Chief Marketing Sweep #141] Updated Twilio Voice integration release notes at 2026-07-25 15:18:56 -->

<!-- [Chief Marketing Sweep #141] Updated Twilio Voice integration release notes at 2026-07-25 15:18:57 -->

<!-- [Chief Marketing Sweep #142] Updated Twilio Voice integration release notes at 2026-07-25 15:18:57 -->

<!-- [Chief Marketing Sweep #238] Updated Twilio Voice integration release notes at 2026-07-25 15:18:59 -->

<!-- [Chief Marketing Sweep #141] Updated Twilio Voice integration release notes at 2026-07-25 15:18:59 -->

<!-- [Chief Marketing Sweep #142] Updated Twilio Voice integration release notes at 2026-07-25 15:19:00 -->

<!-- [Chief Marketing Sweep #142] Updated Twilio Voice integration release notes at 2026-07-25 15:19:01 -->

<!-- [Chief Marketing Sweep #143] Updated Twilio Voice integration release notes at 2026-07-25 15:19:01 -->

<!-- [Chief Marketing Sweep #133] Updated Twilio Voice integration release notes at 2026-07-25 15:19:01 -->

<!-- [Chief Marketing Sweep #142] Updated Twilio Voice integration release notes at 2026-07-25 15:19:03 -->

<!-- [Chief Marketing Sweep #239] Updated Twilio Voice integration release notes at 2026-07-25 15:19:04 -->

<!-- [Chief Marketing Sweep #143] Updated Twilio Voice integration release notes at 2026-07-25 15:19:05 -->

<!-- [Chief Marketing Sweep #143] Updated Twilio Voice integration release notes at 2026-07-25 15:19:05 -->

<!-- [Chief Marketing Sweep #144] Updated Twilio Voice integration release notes at 2026-07-25 15:19:05 -->

<!-- [Chief Marketing Sweep #134] Updated Twilio Voice integration release notes at 2026-07-25 15:19:06 -->

<!-- [Chief Marketing Sweep #143] Updated Twilio Voice integration release notes at 2026-07-25 15:19:07 -->

<!-- [Chief Marketing Sweep #144] Updated Twilio Voice integration release notes at 2026-07-25 15:19:09 -->

<!-- [Chief Marketing Sweep #144] Updated Twilio Voice integration release notes at 2026-07-25 15:19:09 -->

<!-- [Chief Marketing Sweep #240] Updated Twilio Voice integration release notes at 2026-07-25 15:19:09 -->

<!-- [Chief Marketing Sweep #145] Updated Twilio Voice integration release notes at 2026-07-25 15:19:09 -->

<!-- [Chief Marketing Sweep #144] Updated Twilio Voice integration release notes at 2026-07-25 15:19:11 -->

<!-- [Chief Marketing Sweep #135] Updated Twilio Voice integration release notes at 2026-07-25 15:19:11 -->

<!-- [Chief Marketing Sweep #145] Updated Twilio Voice integration release notes at 2026-07-25 15:19:13 -->

<!-- [Chief Marketing Sweep #145] Updated Twilio Voice integration release notes at 2026-07-25 15:19:13 -->

<!-- [Chief Marketing Sweep #146] Updated Twilio Voice integration release notes at 2026-07-25 15:19:13 -->

<!-- [Chief Marketing Sweep #241] Updated Twilio Voice integration release notes at 2026-07-25 15:19:14 -->

<!-- [Chief Marketing Sweep #145] Updated Twilio Voice integration release notes at 2026-07-25 15:19:15 -->

<!-- [Chief Marketing Sweep #135] Updated Twilio Voice integration release notes at 2026-07-25 15:19:16 -->

<!-- [Chief Marketing Sweep #146] Updated Twilio Voice integration release notes at 2026-07-25 15:19:17 -->

<!-- [Chief Marketing Sweep #146] Updated Twilio Voice integration release notes at 2026-07-25 15:19:17 -->

<!-- [Chief Marketing Sweep #147] Updated Twilio Voice integration release notes at 2026-07-25 15:19:18 -->

<!-- [Chief Marketing Sweep #242] Updated Twilio Voice integration release notes at 2026-07-25 15:19:19 -->

<!-- [Chief Marketing Sweep #146] Updated Twilio Voice integration release notes at 2026-07-25 15:19:19 -->

<!-- [Chief Marketing Sweep #147] Updated Twilio Voice integration release notes at 2026-07-25 15:19:21 -->

<!-- [Chief Marketing Sweep #147] Updated Twilio Voice integration release notes at 2026-07-25 15:19:21 -->

<!-- [Chief Marketing Sweep #136] Updated Twilio Voice integration release notes at 2026-07-25 15:19:22 -->

<!-- [Chief Marketing Sweep #148] Updated Twilio Voice integration release notes at 2026-07-25 15:19:22 -->

<!-- [Chief Marketing Sweep #147] Updated Twilio Voice integration release notes at 2026-07-25 15:19:24 -->

<!-- [Chief Marketing Sweep #243] Updated Twilio Voice integration release notes at 2026-07-25 15:19:24 -->

<!-- [Chief Marketing Sweep #148] Updated Twilio Voice integration release notes at 2026-07-25 15:19:25 -->

<!-- [Chief Marketing Sweep #148] Updated Twilio Voice integration release notes at 2026-07-25 15:19:25 -->

<!-- [Chief Marketing Sweep #149] Updated Twilio Voice integration release notes at 2026-07-25 15:19:26 -->

<!-- [Chief Marketing Sweep #137] Updated Twilio Voice integration release notes at 2026-07-25 15:19:27 -->

<!-- [Chief Marketing Sweep #148] Updated Twilio Voice integration release notes at 2026-07-25 15:19:28 -->

<!-- [Chief Marketing Sweep #149] Updated Twilio Voice integration release notes at 2026-07-25 15:19:29 -->

<!-- [Chief Marketing Sweep #244] Updated Twilio Voice integration release notes at 2026-07-25 15:19:29 -->

<!-- [Chief Marketing Sweep #149] Updated Twilio Voice integration release notes at 2026-07-25 15:19:29 -->

<!-- [Chief Marketing Sweep #150] Updated Twilio Voice integration release notes at 2026-07-25 15:19:30 -->

<!-- [Chief Marketing Sweep #149] Updated Twilio Voice integration release notes at 2026-07-25 15:19:32 -->

<!-- [Chief Marketing Sweep #138] Updated Twilio Voice integration release notes at 2026-07-25 15:19:32 -->

<!-- [Chief Marketing Sweep #150] Updated Twilio Voice integration release notes at 2026-07-25 15:19:33 -->

<!-- [Chief Marketing Sweep #150] Updated Twilio Voice integration release notes at 2026-07-25 15:19:34 -->

<!-- [Chief Marketing Sweep #151] Updated Twilio Voice integration release notes at 2026-07-25 15:19:34 -->

<!-- [Chief Marketing Sweep #245] Updated Twilio Voice integration release notes at 2026-07-25 15:19:34 -->

<!-- [Chief Marketing Sweep #150] Updated Twilio Voice integration release notes at 2026-07-25 15:19:36 -->

<!-- [Chief Marketing Sweep #139] Updated Twilio Voice integration release notes at 2026-07-25 15:19:37 -->

<!-- [Chief Marketing Sweep #151] Updated Twilio Voice integration release notes at 2026-07-25 15:19:37 -->

<!-- [Chief Marketing Sweep #151] Updated Twilio Voice integration release notes at 2026-07-25 15:19:38 -->

<!-- [Chief Marketing Sweep #152] Updated Twilio Voice integration release notes at 2026-07-25 15:19:38 -->

<!-- [Chief Marketing Sweep #246] Updated Twilio Voice integration release notes at 2026-07-25 15:19:40 -->

<!-- [Chief Marketing Sweep #151] Updated Twilio Voice integration release notes at 2026-07-25 15:19:40 -->

<!-- [Chief Marketing Sweep #152] Updated Twilio Voice integration release notes at 2026-07-25 15:19:41 -->

<!-- [Chief Marketing Sweep #152] Updated Twilio Voice integration release notes at 2026-07-25 15:19:42 -->

<!-- [Chief Marketing Sweep #140] Updated Twilio Voice integration release notes at 2026-07-25 15:19:42 -->

<!-- [Chief Marketing Sweep #153] Updated Twilio Voice integration release notes at 2026-07-25 15:19:42 -->

<!-- [Chief Marketing Sweep #152] Updated Twilio Voice integration release notes at 2026-07-25 15:19:44 -->

<!-- [Chief Marketing Sweep #247] Updated Twilio Voice integration release notes at 2026-07-25 15:19:45 -->

<!-- [Chief Marketing Sweep #153] Updated Twilio Voice integration release notes at 2026-07-25 15:19:46 -->

<!-- [Chief Marketing Sweep #153] Updated Twilio Voice integration release notes at 2026-07-25 15:19:46 -->

<!-- [Chief Marketing Sweep #154] Updated Twilio Voice integration release notes at 2026-07-25 15:19:46 -->

<!-- [Chief Marketing Sweep #141] Updated Twilio Voice integration release notes at 2026-07-25 15:19:47 -->

<!-- [Chief Marketing Sweep #153] Updated Twilio Voice integration release notes at 2026-07-25 15:19:48 -->

<!-- [Chief Marketing Sweep #248] Updated Twilio Voice integration release notes at 2026-07-25 15:19:50 -->

<!-- [Chief Marketing Sweep #154] Updated Twilio Voice integration release notes at 2026-07-25 15:19:50 -->

<!-- [Chief Marketing Sweep #154] Updated Twilio Voice integration release notes at 2026-07-25 15:19:50 -->

<!-- [Chief Marketing Sweep #155] Updated Twilio Voice integration release notes at 2026-07-25 15:19:50 -->

<!-- [Chief Marketing Sweep #142] Updated Twilio Voice integration release notes at 2026-07-25 15:19:52 -->

<!-- [Chief Marketing Sweep #154] Updated Twilio Voice integration release notes at 2026-07-25 15:19:52 -->

<!-- [Chief Marketing Sweep #155] Updated Twilio Voice integration release notes at 2026-07-25 15:19:54 -->

<!-- [Chief Marketing Sweep #155] Updated Twilio Voice integration release notes at 2026-07-25 15:19:54 -->

<!-- [Chief Marketing Sweep #156] Updated Twilio Voice integration release notes at 2026-07-25 15:19:54 -->

<!-- [Chief Marketing Sweep #249] Updated Twilio Voice integration release notes at 2026-07-25 15:19:55 -->

<!-- [Chief Marketing Sweep #155] Updated Twilio Voice integration release notes at 2026-07-25 15:19:56 -->

<!-- [Chief Marketing Sweep #143] Updated Twilio Voice integration release notes at 2026-07-25 15:19:57 -->

<!-- [Chief Marketing Sweep #156] Updated Twilio Voice integration release notes at 2026-07-25 15:19:58 -->

<!-- [Chief Marketing Sweep #156] Updated Twilio Voice integration release notes at 2026-07-25 15:19:58 -->

<!-- [Chief Marketing Sweep #157] Updated Twilio Voice integration release notes at 2026-07-25 15:19:59 -->

<!-- [Chief Marketing Sweep #250] Updated Twilio Voice integration release notes at 2026-07-25 15:20:00 -->

<!-- [Chief Marketing Sweep #156] Updated Twilio Voice integration release notes at 2026-07-25 15:20:00 -->

<!-- [Chief Marketing Sweep #157] Updated Twilio Voice integration release notes at 2026-07-25 15:20:02 -->

<!-- [Chief Marketing Sweep #144] Updated Twilio Voice integration release notes at 2026-07-25 15:20:02 -->

<!-- [Chief Marketing Sweep #157] Updated Twilio Voice integration release notes at 2026-07-25 15:20:02 -->

<!-- [Chief Marketing Sweep #158] Updated Twilio Voice integration release notes at 2026-07-25 15:20:03 -->

<!-- [Chief Marketing Sweep #157] Updated Twilio Voice integration release notes at 2026-07-25 15:20:05 -->

<!-- [Chief Marketing Sweep #251] Updated Twilio Voice integration release notes at 2026-07-25 15:20:05 -->

<!-- [Chief Marketing Sweep #158] Updated Twilio Voice integration release notes at 2026-07-25 15:20:06 -->

<!-- [Chief Marketing Sweep #158] Updated Twilio Voice integration release notes at 2026-07-25 15:20:06 -->

<!-- [Chief Marketing Sweep #159] Updated Twilio Voice integration release notes at 2026-07-25 15:20:07 -->

<!-- [Chief Marketing Sweep #145] Updated Twilio Voice integration release notes at 2026-07-25 15:20:07 -->

<!-- [Chief Marketing Sweep #158] Updated Twilio Voice integration release notes at 2026-07-25 15:20:09 -->

<!-- [Chief Marketing Sweep #252] Updated Twilio Voice integration release notes at 2026-07-25 15:20:10 -->

<!-- [Chief Marketing Sweep #159] Updated Twilio Voice integration release notes at 2026-07-25 15:20:10 -->

<!-- [Chief Marketing Sweep #159] Updated Twilio Voice integration release notes at 2026-07-25 15:20:11 -->

<!-- [Chief Marketing Sweep #160] Updated Twilio Voice integration release notes at 2026-07-25 15:20:11 -->

<!-- [Chief Marketing Sweep #146] Updated Twilio Voice integration release notes at 2026-07-25 15:20:13 -->

<!-- [Chief Marketing Sweep #159] Updated Twilio Voice integration release notes at 2026-07-25 15:20:13 -->

<!-- [Chief Marketing Sweep #160] Updated Twilio Voice integration release notes at 2026-07-25 15:20:14 -->

<!-- [Chief Marketing Sweep #160] Updated Twilio Voice integration release notes at 2026-07-25 15:20:15 -->

<!-- [Chief Marketing Sweep #161] Updated Twilio Voice integration release notes at 2026-07-25 15:20:15 -->

<!-- [Chief Marketing Sweep #253] Updated Twilio Voice integration release notes at 2026-07-25 15:20:15 -->

<!-- [Chief Marketing Sweep #160] Updated Twilio Voice integration release notes at 2026-07-25 15:20:17 -->

<!-- [Chief Marketing Sweep #147] Updated Twilio Voice integration release notes at 2026-07-25 15:20:18 -->

<!-- [Chief Marketing Sweep #161] Updated Twilio Voice integration release notes at 2026-07-25 15:20:18 -->

<!-- [Chief Marketing Sweep #161] Updated Twilio Voice integration release notes at 2026-07-25 15:20:19 -->

<!-- [Chief Marketing Sweep #162] Updated Twilio Voice integration release notes at 2026-07-25 15:20:19 -->

<!-- [Chief Marketing Sweep #254] Updated Twilio Voice integration release notes at 2026-07-25 15:20:20 -->

<!-- [Chief Marketing Sweep #161] Updated Twilio Voice integration release notes at 2026-07-25 15:20:21 -->

<!-- [Chief Marketing Sweep #162] Updated Twilio Voice integration release notes at 2026-07-25 15:20:23 -->

<!-- [Chief Marketing Sweep #148] Updated Twilio Voice integration release notes at 2026-07-25 15:20:23 -->

<!-- [Chief Marketing Sweep #162] Updated Twilio Voice integration release notes at 2026-07-25 15:20:23 -->

<!-- [Chief Marketing Sweep #163] Updated Twilio Voice integration release notes at 2026-07-25 15:20:23 -->

<!-- [Chief Marketing Sweep #162] Updated Twilio Voice integration release notes at 2026-07-25 15:20:25 -->

<!-- [Chief Marketing Sweep #255] Updated Twilio Voice integration release notes at 2026-07-25 15:20:25 -->

<!-- [Chief Marketing Sweep #163] Updated Twilio Voice integration release notes at 2026-07-25 15:20:27 -->

<!-- [Chief Marketing Sweep #163] Updated Twilio Voice integration release notes at 2026-07-25 15:20:27 -->

<!-- [Chief Marketing Sweep #164] Updated Twilio Voice integration release notes at 2026-07-25 15:20:27 -->

<!-- [Chief Marketing Sweep #149] Updated Twilio Voice integration release notes at 2026-07-25 15:20:28 -->

<!-- [Chief Marketing Sweep #163] Updated Twilio Voice integration release notes at 2026-07-25 15:20:29 -->

<!-- [Chief Marketing Sweep #256] Updated Twilio Voice integration release notes at 2026-07-25 15:20:30 -->

<!-- [Chief Marketing Sweep #164] Updated Twilio Voice integration release notes at 2026-07-25 15:20:31 -->

<!-- [Chief Marketing Sweep #164] Updated Twilio Voice integration release notes at 2026-07-25 15:20:31 -->

<!-- [Chief Marketing Sweep #165] Updated Twilio Voice integration release notes at 2026-07-25 15:20:31 -->

<!-- [Chief Marketing Sweep #150] Updated Twilio Voice integration release notes at 2026-07-25 15:20:33 -->

<!-- [Chief Marketing Sweep #164] Updated Twilio Voice integration release notes at 2026-07-25 15:20:33 -->

<!-- [Chief Marketing Sweep #165] Updated Twilio Voice integration release notes at 2026-07-25 15:20:35 -->

<!-- [Chief Marketing Sweep #165] Updated Twilio Voice integration release notes at 2026-07-25 15:20:35 -->

<!-- [Chief Marketing Sweep #257] Updated Twilio Voice integration release notes at 2026-07-25 15:20:35 -->

<!-- [Chief Marketing Sweep #166] Updated Twilio Voice integration release notes at 2026-07-25 15:20:36 -->

<!-- [Chief Marketing Sweep #165] Updated Twilio Voice integration release notes at 2026-07-25 15:20:37 -->

<!-- [Chief Marketing Sweep #151] Updated Twilio Voice integration release notes at 2026-07-25 15:20:38 -->

<!-- [Chief Marketing Sweep #166] Updated Twilio Voice integration release notes at 2026-07-25 15:20:39 -->

<!-- [Chief Marketing Sweep #166] Updated Twilio Voice integration release notes at 2026-07-25 15:20:39 -->

<!-- [Chief Marketing Sweep #167] Updated Twilio Voice integration release notes at 2026-07-25 15:20:40 -->

<!-- [Chief Marketing Sweep #258] Updated Twilio Voice integration release notes at 2026-07-25 15:20:41 -->

<!-- [Chief Marketing Sweep #166] Updated Twilio Voice integration release notes at 2026-07-25 15:20:42 -->

<!-- [Chief Marketing Sweep #167] Updated Twilio Voice integration release notes at 2026-07-25 15:20:43 -->

<!-- [Chief Marketing Sweep #152] Updated Twilio Voice integration release notes at 2026-07-25 15:20:43 -->

<!-- [Chief Marketing Sweep #167] Updated Twilio Voice integration release notes at 2026-07-25 15:20:44 -->

<!-- [Chief Marketing Sweep #168] Updated Twilio Voice integration release notes at 2026-07-25 15:20:44 -->

<!-- [Chief Marketing Sweep #167] Updated Twilio Voice integration release notes at 2026-07-25 15:20:46 -->

<!-- [Chief Marketing Sweep #259] Updated Twilio Voice integration release notes at 2026-07-25 15:20:46 -->

<!-- [Chief Marketing Sweep #168] Updated Twilio Voice integration release notes at 2026-07-25 15:20:47 -->

<!-- [Chief Marketing Sweep #168] Updated Twilio Voice integration release notes at 2026-07-25 15:20:48 -->

<!-- [Chief Marketing Sweep #169] Updated Twilio Voice integration release notes at 2026-07-25 15:20:48 -->

<!-- [Chief Marketing Sweep #153] Updated Twilio Voice integration release notes at 2026-07-25 15:20:48 -->

<!-- [Chief Marketing Sweep #168] Updated Twilio Voice integration release notes at 2026-07-25 15:20:50 -->

<!-- [Chief Marketing Sweep #260] Updated Twilio Voice integration release notes at 2026-07-25 15:20:51 -->

<!-- [Chief Marketing Sweep #169] Updated Twilio Voice integration release notes at 2026-07-25 15:20:51 -->

<!-- [Chief Marketing Sweep #169] Updated Twilio Voice integration release notes at 2026-07-25 15:20:52 -->

<!-- [Chief Marketing Sweep #170] Updated Twilio Voice integration release notes at 2026-07-25 15:20:52 -->

<!-- [Chief Marketing Sweep #154] Updated Twilio Voice integration release notes at 2026-07-25 15:20:53 -->

<!-- [Chief Marketing Sweep #169] Updated Twilio Voice integration release notes at 2026-07-25 15:20:54 -->

<!-- [Chief Marketing Sweep #170] Updated Twilio Voice integration release notes at 2026-07-25 15:20:55 -->

<!-- [Chief Marketing Sweep #261] Updated Twilio Voice integration release notes at 2026-07-25 15:20:56 -->

<!-- [Chief Marketing Sweep #170] Updated Twilio Voice integration release notes at 2026-07-25 15:20:56 -->

<!-- [Chief Marketing Sweep #171] Updated Twilio Voice integration release notes at 2026-07-25 15:20:56 -->

<!-- [Chief Marketing Sweep #170] Updated Twilio Voice integration release notes at 2026-07-25 15:20:58 -->

<!-- [Chief Marketing Sweep #155] Updated Twilio Voice integration release notes at 2026-07-25 15:20:59 -->

<!-- [Chief Marketing Sweep #171] Updated Twilio Voice integration release notes at 2026-07-25 15:21:00 -->

<!-- [Chief Marketing Sweep #171] Updated Twilio Voice integration release notes at 2026-07-25 15:21:00 -->

<!-- [Chief Marketing Sweep #172] Updated Twilio Voice integration release notes at 2026-07-25 15:21:00 -->

<!-- [Chief Marketing Sweep #262] Updated Twilio Voice integration release notes at 2026-07-25 15:21:01 -->

<!-- [Chief Marketing Sweep #171] Updated Twilio Voice integration release notes at 2026-07-25 15:21:02 -->

<!-- [Chief Marketing Sweep #156] Updated Twilio Voice integration release notes at 2026-07-25 15:21:04 -->

<!-- [Chief Marketing Sweep #172] Updated Twilio Voice integration release notes at 2026-07-25 15:21:04 -->

<!-- [Chief Marketing Sweep #172] Updated Twilio Voice integration release notes at 2026-07-25 15:21:04 -->

<!-- [Chief Marketing Sweep #173] Updated Twilio Voice integration release notes at 2026-07-25 15:21:04 -->

<!-- [Chief Marketing Sweep #263] Updated Twilio Voice integration release notes at 2026-07-25 15:21:06 -->

<!-- [Chief Marketing Sweep #172] Updated Twilio Voice integration release notes at 2026-07-25 15:21:06 -->

<!-- [Chief Marketing Sweep #173] Updated Twilio Voice integration release notes at 2026-07-25 15:21:08 -->

<!-- [Chief Marketing Sweep #173] Updated Twilio Voice integration release notes at 2026-07-25 15:21:08 -->

<!-- [Chief Marketing Sweep #174] Updated Twilio Voice integration release notes at 2026-07-25 15:21:09 -->

<!-- [Chief Marketing Sweep #157] Updated Twilio Voice integration release notes at 2026-07-25 15:21:09 -->

<!-- [Chief Marketing Sweep #173] Updated Twilio Voice integration release notes at 2026-07-25 15:21:10 -->

<!-- [Chief Marketing Sweep #264] Updated Twilio Voice integration release notes at 2026-07-25 15:21:11 -->

<!-- [Chief Marketing Sweep #174] Updated Twilio Voice integration release notes at 2026-07-25 15:21:12 -->

<!-- [Chief Marketing Sweep #174] Updated Twilio Voice integration release notes at 2026-07-25 15:21:12 -->

<!-- [Chief Marketing Sweep #175] Updated Twilio Voice integration release notes at 2026-07-25 15:21:13 -->

<!-- [Chief Marketing Sweep #158] Updated Twilio Voice integration release notes at 2026-07-25 15:21:14 -->

<!-- [Chief Marketing Sweep #174] Updated Twilio Voice integration release notes at 2026-07-25 15:21:14 -->

<!-- [Chief Marketing Sweep #175] Updated Twilio Voice integration release notes at 2026-07-25 15:21:16 -->

<!-- [Chief Marketing Sweep #265] Updated Twilio Voice integration release notes at 2026-07-25 15:21:16 -->

<!-- [Chief Marketing Sweep #175] Updated Twilio Voice integration release notes at 2026-07-25 15:21:16 -->

<!-- [Chief Marketing Sweep #176] Updated Twilio Voice integration release notes at 2026-07-25 15:21:17 -->

<!-- [Chief Marketing Sweep #175] Updated Twilio Voice integration release notes at 2026-07-25 15:21:19 -->

<!-- [Chief Marketing Sweep #159] Updated Twilio Voice integration release notes at 2026-07-25 15:21:19 -->
