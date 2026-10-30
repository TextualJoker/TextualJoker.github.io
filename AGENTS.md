# Dev portal (textualjoker.github.io) — the terrain

The PUBLISHED build. GitHub Pages serves this public repo from its root. The
SOURCE (entries, build scripts, tests, dev-log flow) is the private sibling
`../tj-site`; read its `CLAUDE.md` before changing anything here.

| Repo | Role | Visibility |
|---|---|---|
| `../tj-site` | source: `content/entries/`, `scripts/`, tests | private |
| `tj-deploy` (this) | published build | public |

**Local quirks that surprise people.**

- ⛔ `index.html` (and `main.js`, `feed.xml`, `assets/`) is now a BUILD
  ARTEFACT of NecroSpec-alpha's `deploy_v2.py` — it overwrites all of them
  whole on every run, last-write-wins, and it went live for real 2026-10-30
  (`b0cb6c7`). Never hand-edit `index.html` or `main.js`. Decision + evidence:
  `docs/devsite-v2-index-ownership-2026-10-30.md`.
- ⛔ `../tj-site/scripts/build-portal.mjs` no longer lands a devlog entry here
  — there is no `<ul class="log">` region left in `index.html` for it to write
  into (deploy_v2.py's SPA shell), and anything it wrote would be discarded
  by the next `deploy_v2.py` run regardless. It now validates the entry
  (tags, length) and no-ops, by design, rather than throwing
  (PORTAL-DEVLOG-PUBLISH-BROKEN-BY-DEVSITE-V2, 2026-10-30). How a new entry
  reaches the live v2 page is **decided, not yet wired**: NecroSpec-alpha's
  `tools/harvest/html-facts/devsite-v2/sync_logitems.py` reads tj-site's own
  `content/entries/*.md` directly — the old harvest-from-this-repo's-rendered-
  HTML path is a closed NecroSpec→NecroSpec loop since `deploy_v2.py` took
  over `index.html` whole, and can never see a new entry again
  (`PORTAL-DEVLOG-LANDING-REDESIGN`,
  `NecroSpec-alpha/docs/necrospec-devlog-ingest-seam-2026-10-30.md`). The
  cron step to run it and land the result is `portal:PORTAL-DEVLOG-INGEST-WIRING`
  (queued, gated on a test fix); nothing in this repo changes for it.
- Building is not publishing, for what `deploy_v2.py` still does write: that
  artefact is not live until `git push` from this repo.
- ⛔ `ai-delivery-programme/` and `founding-engineering-plan/` are the
  OWNER'S OWN plans for his new company, not a former employer's documents.
  Keep them; never remove or delist them as part of any offboarding (owner
  2026-10-19). They are `noindex, nofollow` on purpose — public but unlisted,
  and in the NecroSpec dev-site spec. No refresh script (retired 2026-10-24).
  Decision: `docs/work-pages-public-unlisted-2026-10-14.md`.
- `quest.json` ships alongside `index.html` (`../tj-site/scripts/portal-quest.mjs`);
  `assets/quest.json` is a second, NecroSpec-owned copy `deploy_v2.py` writes —
  same content, two homes, not yet unified.
- The dev log is nudged daily by `portal/devlog-due` (`~/agent-os/projects/portal/jobs/`).
  `portal/update-portal-stats` still runs daily but has been a silent no-op
  since the 2026-10-30 go-live — its `<b class="stat-installs">` marker does
  not exist in `deploy_v2.py`'s SPA shell. See the decision doc.
