# 260522-pttv-runtime

Public runtime HTML files for PTTV (Parker Thatch TV) Live Comment Monitor.

These are the standalone HTML/JS UIs injected into `example.com` tabs during live PTTV sessions, plus a standalone demo harness for smoke-testing without going live:

- **`PTTV-Live-Tracker.html`** — Q/C/S tracker with Active/Archive sub-tabs, `aired` (📺 marker-fill) and `to-do` (🚩 follow-up) flags per item, localStorage persistence, `firstSeenAt` timestamps. **Currently Schema 1.2.1 / Tracker v2.1.1** (260523 b) — version declared in the file's first-line HTML comment.
- **`PTTV-Live-Tracker-Demo.html`** — same code paths as production, but with isolated localStorage keys (`pttv_demo_*`), an embedded 40-item mock dataset, and a Demo controls bar (Load 10/25/40 items · Clear · Show schema sample). Standalone smoke test for Schema 1.2+ — open directly in any browser, no Chrome extension or live show required. Open via [raw.githack](https://raw.githack.com/mrgyvr/260522-pttv-runtime/main/PTTV-Live-Tracker-Demo.html).
- **`PTTV-Heartbeat.html`** — Web Worker-driven heartbeat for auto mode. Survives Chrome background-tab throttling. **Currently v1.0** — version declared in the file's first-line HTML comment.

## Why public

These files contain zero sensitive data — just generic UI scaffolding (a Q/C/S checklist, a ticking counter, mock fan-club mentions). Hosting them publicly lets the PTTV Genesis Prompt fetch them at runtime via raw URLs, with no GitHub auth complications.

## Companion repo (private)

The private companion repo with archives, Genesis Prompt, README, session todos, and everything else PTTV-specific:
https://github.com/mrgyvr/260522-pttv-live-monitor

## Fetch URLs

Used by the PTTV Genesis Prompt (v3.4+) during session startup:

- Tracker: https://raw.githubusercontent.com/mrgyvr/260522-pttv-runtime/main/PTTV-Live-Tracker.html
- Heartbeat: https://raw.githubusercontent.com/mrgyvr/260522-pttv-runtime/main/PTTV-Heartbeat.html
- Demo (not fetched by Genesis — open directly): https://raw.githack.com/mrgyvr/260522-pttv-runtime/main/PTTV-Live-Tracker-Demo.html

These URLs are stable across content updates — when a tracker bumps internally from Schema 1.2 → 1.3, the URL doesn't change, so Genesis-side fetch URLs stay correct.

## Versioning

**Filenames are unversioned** (as of 260523 migration). Version info lives in each file's first-line HTML comment (e.g., `<!-- Schema 1.2.1 / Tracker v2.1.1 -->`) and in git history. Bumps overwrite the file in place — the fetch URL stays constant, callers don't need to update. Reading `git log <filename> --oneline` gives the bump history.

This replaces the previous filename-versioning approach (`PTTV-[Thing] (v[major.minor]).[ext]`), which created file-tree clutter that git already handles natively.

## Sync state with private repo

The private companion repo's `PTTV-Project-README.md` is the master file-index for the whole PTTV system. When public-repo files change, the private README's sync-state section gets a matching bump. As of 260523 b, both repos are in sync at Schema 1.2.1.
