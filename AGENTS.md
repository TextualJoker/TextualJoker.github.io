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
- `ai-delivery-programme/` holds work-account artifacts refreshed by
  `../tj-site/scripts/refresh-programme.mjs`. Those pages are
  `noindex, nofollow` on purpose — unlisted working documents.
- `quest.json` ships alongside `index.html` (`../tj-site/scripts/portal-quest.mjs`).
- The install counter is rewritten daily by the Agent OS job
  `portal/update-portal-stats`; the dev log is nudged daily by `portal/devlog-due`
  (both in `~/agent-os/projects/portal/jobs/`).
