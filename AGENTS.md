# Dev portal (textualjoker.github.io) — the terrain

The PUBLISHED build. GitHub Pages serves this public repo from its root. The
SOURCE (entries, build scripts, tests, dev-log flow) is the private sibling
`../tj-site`; read its `CLAUDE.md` before changing anything here.

| Repo | Role | Visibility |
|---|---|---|
| `../tj-site` | source: `content/entries/`, `scripts/`, tests | private |
| `tj-deploy` (this) | published build | public |

**Local quirks that surprise people.**

- ⛔ `index.html` is a BUILD ARTEFACT of `../tj-site/scripts/build-portal.mjs`.
  Never hand-edit it. Edit the entry or script in tj-site, rebuild, then commit
  the artefact here.
- Building is not publishing. The build writes `index.html`; the entry is not
  live until `git push` from this repo.
- ⛔ `ai-delivery-programme/` and `founding-engineering-plan/` are the
  OWNER'S OWN plans for his new company, not a former employer's documents.
  Keep them; never remove or delist them as part of any offboarding (owner
  2026-10-19). They are `noindex, nofollow` on purpose — public but unlisted,
  and in the NecroSpec dev-site spec. No refresh script (retired 2026-10-24).
  Decision: `docs/work-pages-public-unlisted-2026-10-14.md`.
- `quest.json` ships alongside `index.html` (`../tj-site/scripts/portal-quest.mjs`).
- The install counter is rewritten daily by the Agent OS job
  `portal/update-portal-stats`; the dev log is nudged daily by `portal/devlog-due`
  (both in `~/agent-os/projects/portal/jobs/`).
