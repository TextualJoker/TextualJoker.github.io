# Who owns `index.html` now that devsite v2 is live — 2026-10-30

**Decision:** NecroSpec-alpha's `deploy_v2.py` is the owner of `index.html`,
`main.js`, `feed.xml` and `assets/` — it overwrites each one whole, every run,
last-write-wins. `../tj-site/scripts/build-portal.mjs` is not a competing
owner: it is the chain's *intermediate* step (lands a fresh devlog entry so
NecroSpec's own bump can read it), and `deploy_v2.py` runs after it, same
cadence, and replaces whatever it wrote. Nothing needed to change in either
script for this — the chain was already wired to run in that order
(`devlog-due.mjs` → `devsite-bump-due.mjs` → a NecroSpec ghost's
`redraft_devsite.py --bump` → `devsite-deploy-due.mjs` → `deploy_v2.py`).

**Why now:** `portal:DEVSITE-V2-GO-LIVE` already ran `deploy_v2.py` for real —
commit `b0cb6c7` ("devsite v2: rebuild from NecroSpec-alpha c49d53b") landed
and pushed before this ticket closed. The question this ticket asked
("decide before go-live runs") was overtaken by events; this records the
decision retroactively, from the state go-live actually left.

**Checked 2026-10-30:** the live `index.html` is now a bare SPA shell
(`<div id="root">` + `<script src="/main.js">`), not server-rendered markup —
confirmed against the current file in this repo. It carries no
`<b class="stat-installs">` element and `main.js` has no live-counter
identifier (`totalInstalls`/`installCount`/etc. all absent) — the install
counter the old template rendered is not present in v2 in any form, static or
client-fetched.

**Consequence not fixed here:** `portal/update-portal-stats` (the Agent OS
job that regex-patches that marker and commits+pushes the result) has had
nothing to patch since the go-live commit and silently no-ops every run. Even
if the marker still existed, `deploy_v2.py`'s full-overwrite model would
discard any value it patched on the next run anyway — a direct regex-patch
of a generated file cannot coexist with a generator that owns the whole file.
Filed as a queue row rather than fixed here: retiring the cron vs. feeding the
install count into NecroSpec's own spec (so `deploy_v2.py` bakes it in) is a
real design choice, not this ticket's to make blind.

**Not touched:** `quest.json` (root, `portal-quest.mjs`-owned) and
`assets/quest.json` (`deploy_v2.py`-owned) now hold the same content in two
places. Harmless today; noted so it isn't mistaken for drift later.
