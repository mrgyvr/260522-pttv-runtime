# 260522-pttv-runtime

Public runtime HTML files for PTTV (Parker Thatch TV) Live Comment Monitor.

These are the standalone HTML/JS UIs injected into `example.com` tabs during live PTTV sessions:

- **`PTTV-Live-Tracker (v2.0).html`** — Q/C/S tracker with Active/Archive sub-tabs, localStorage persistence, firstSeenAt timestamps.
- **`PTTV-Heartbeat (v1.0).html`** — Web Worker-driven heartbeat for auto mode. Survives Chrome background-tab throttling.

## Why public

These files contain zero sensitive data — just generic UI scaffolding (a Q/C/S checklist and a ticking counter). Hosting them publicly lets the PTTV Genesis Prompt fetch them at runtime via raw URLs, with no GitHub auth complications.

## Companion repo (private)

The private companion repo with archives, Genesis Prompt, README, session todos, and everything else PTTV-specific:
https://github.com/mrgyvr/260522-pttv-live-monitor

## Fetch URLs

Used by the PTTV Genesis Prompt (v3.4+) during session startup:

- Tracker: https://raw.githubusercontent.com/mrgyvr/260522-pttv-runtime/main/PTTV-Live-Tracker%20(v2.0).html
- Heartbeat: https://raw.githubusercontent.com/mrgyvr/260522-pttv-runtime/main/PTTV-Heartbeat%20(v1.0).html

## Versioning

Filenames carry semantic versions: `PTTV-[Thing] (v[major.minor]).[ext]`. Bumps create new files alongside (not replacements) so old fetch URLs keep working until callers migrate. Genesis Prompt always pins to a specific version in its fetch URL.
