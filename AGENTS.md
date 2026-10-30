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
  (`b0cb6c7`). `../tj-site/scripts/build-portal.mjs` still lands a fresh
  devlog entry here first (NecroSpec's own bump step reads that landing), but
  `deploy_v2.py` runs after it in the same daily chain and overwrites
  whatever build-portal.mjs wrote — so build-portal.mjs's own output is never
  what ships. Never hand-edit `index.html` or `main.js`. Decision + evidence:
  `docs/devsite-v2-index-ownership-2026-10-30.md`.
- Building is not publishing. The build writes `index.html`; the entry is not
  live until `git push` from this repo.
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
