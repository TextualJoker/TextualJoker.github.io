# PORTAL-DEVSITE-V2-BROKEN-ANCHORS — verified not a real bug, 2026-11-02

**Decision:** no code change lands in this repo for this row. The ~44 dead
`#anchor` links (founding-engineering-plan, index.html devlog nav) and the
5-page `id="archive"` lookup the row named are checker false positives, not
breakage a real visitor hits. `index.html`/`main.js` are NecroSpec-alpha's
`deploy_v2.py` build artefacts (`AGENTS.md`) — nothing here was hand-edited,
and editing them would be both forbidden and pointless (next run overwrites
them).

**Why:** necrospec's own `necrospec:NECROSPEC-DEVSITE-UNACCOUNTED-RESEARCH`
(filed 2026-10-30) already diagnosed this exact set — 4 index.html links + 40
founding-engineering-plan links + 5 archive lookups = the 49 `html_facts`
unaccounted entries this row's own text cites — confirmed live in headless
Chromium that none are real devsite bugs, only gaps in `html_facts`' own
crawler (no reveal-interaction model, no `#a/b` fallback, treats each SPA
route as an independent script).

This pass independently re-verified all three against the live built
`main.js` in this checkout rather than taking that finding on trust:

- **`id="archive"`**: `document.getElementById("archive")` is read inside
  `useState(null)` + `useEffect`, so a page without that id gets `null`
  stored, never a throw — confirmed by reading the minified source directly.
- **`#a/b` founding-engineering-plan links**: the shared hash resolver
  (`main.js`, the function right before `pagereveal`) splits on `/`, looks
  the prefix up in a registry, and falls back to the bare suffix id when the
  prefix isn't one of its own groups — the suffix ids are present in the
  static markup, so these resolve.
- **index.html paginated devlog links**: the list page's mount effect reads
  `window.location.hash` and, if the target id isn't on the page yet, loops
  fetching further pages (no UI click needed) until it finds the matching
  entry, then forces a native hash-scroll via `location.replace(location.href)`
  once the element exists. A real visitor following the link gets the entry
  automatically; nothing is dead.

**Not done here:** the design question necrospec's research row leaves open
— whether to make `html_facts` model SPA interactions/shared-script routes,
or relax its unaccounted-must-be-zero gate — is necrospec's own call, already
tracked there (`necrospec:NECROSPEC-DEVSITE-UNACCOUNTED-RESEARCH`), and the
devsite pin bump it blocks is necrospec's pipeline, not this repo's. Nothing
new filed for it from here.
