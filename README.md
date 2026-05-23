# 260522-pttv-runtime

Public runtime HTML files for PTTV (Parker Thatch TV) Live Comment Monitor.

These are the standalone HTML/JS UIs injected into `example.com` tabs during live PTTV sessions:

- **`PTTV-Live-Tracker.html`** — Q/C/S tracker with Active/Archive sub-tabs, localStorage persistence, firstSeenAt timestamps. (Currently v2.0 internally; version declared in the file's first-line HTML comment.)
- **`PTTV-Heartbeat.html`** — Web Worker-driven heartbeat for auto mode. Survives Chrome background-tab throttling. (Currently v1.0 internally; version declared in the file's first-line HTML comment.)

## Why public

These files contain zero sensitive data — just generic UI scaffolding (a Q/C/S checklist and a ticking counter). Hosting them publicly lets the PTTV Genesis Prompt fetch them at runtime via raw URLs, with no GitHub auth complications.

## Companion repo (private)

The private companion repo with archives, Genesis Prompt, README, session todos, and everything else PTTV-specific:
https://github.com/mrgyvr/260522-pttv-live-monitor

## Fetch URLs

Used by the PTTV Genesis Prompt (v3.4+) during session startup:

- Tracker: https://raw.githubusercontent.com/mrgyvr/260522-pttv-runtime/main/PTTV-Live-Tracker.html
- Heartbeat: https://raw.githubusercontent.com/mrgyvr/260522-pttv-runtime/main/PTTV-Heartbeat.html

These URLs are stable across content updates — when a tracker bumps internally from v2.0 → v2.1, the URL doesn't change, so Genesis-side fetch URLs stay correct.

## Versioning

**Filenames are unversioned** (as of 260523 migration). Version info lives in each file's first-line HTML comment (e.g., `<!-- PTTV-Live-Tracker (v2.0) -->`) and in git history. Bumps overwrite the file in place — the fetch URL stays constant, callers don't need to update. Reading `git log <filename> --oneline` gives the bump history.

This replaces the previous filename-versioning approach (`PTTV-[Thing] (v[major.minor]).[ext]`), which created file-tree clutter that git already handles natively.
