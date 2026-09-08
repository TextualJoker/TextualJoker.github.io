# Dev portal (textualjoker.github.io) — the terrain

A published site, not an agent lane. GitHub Pages serves this repo directly.

**Local quirks that surprise people.**

- ⛔ `index.html` is a BUILD ARTEFACT of
  `GridJoy-v2/scripts/portal/build-portal.mjs`. Never hand-edit it. Edit the
  entry source, rebuild, then commit the artefact.
- Building is not publishing. The build writes `index.html`; the entry is not
  live until `git push` from this repo.
- `ai-delivery-programme/` holds work-account artifacts refreshed by
  `GridJoy-v2/scripts/portal/refresh-programme.mjs`. Those pages are
  `noindex, nofollow` on purpose — unlisted working documents.
- `quest.json` ships alongside `index.html` and is set in the same tick.
