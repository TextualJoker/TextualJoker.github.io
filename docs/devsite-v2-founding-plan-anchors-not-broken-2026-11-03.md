# PORTAL-DEVSITE-FOUNDING-PLAN-BROKEN-ANCHORS — gate cleared, verified not a real bug, 2026-11-03

**Decision:** no code change lands in this repo for this row either. The gate,
`necrospec:NECROSPEC-DEVSITE-ANCHOR-IDS`, is now `DONE`: its second dispatch
(`job_4388b5`, 2026-11-03) built the production spec and drove it with
Playwright and found **neither half of its own title reproduces** on current
`main` — no code change landed there either, so there is nothing fixed to
redeploy here. This row's two symptoms (`#archive` nav, founding-engineering-
plan anchor ids) are the same underlying claims as the already-closed
`portal:PORTAL-DEVSITE-V2-BROKEN-ANCHORS`
(`docs/devsite-v2-anchors-not-broken-2026-11-02.md`); this pass re-confirms
that verdict independently rather than taking the gate's closure on trust.

**Re-verified live in this checkout:**

- **`main.js` `#archive` lookup** (row cites line 1205; current build has it
  at 1237 — line drift from the rebuilds since, same code):
  `et.useEffect(()=>{N(document.getElementById("archive"))},[])` — stored in
  `useState(null)`, read inside an effect, never dereferenced synchronously.
  A route without the id gets `null` and renders nothing extra. No throw, no
  broken nav.
- **founding-engineering-plan "sequential ids 01, 02…" claim**: these ids are
  real and intentional, not a mismatch. Each stage's `<section id="s-phaseN">`
  (e.g. `s-phase1` for "Decide and fund") matches the id the TOC's `Ie`
  component targets for that stage — confirmed by locating both the TOC
  entry (`id:"s-phase1"`) and the rendered `(0,e.jsxs)("section",{id:"s-phase1"...`
  in the live `main.js`. The `"01"`/`"02"`/`"05-2"`… labels are the
  *individual step* numbers inside each stage (the `H` step component,
  `label:"01"`), used by the page's own "Reset all steps" control
  (`items:["01","02",...,"24-2"]`) — globally unique across the whole plan,
  not reused per stage, so there's no collision to break a link.
- necrospec's own second-pass finding on the identically-worded "sequential
  ids" claim (harvested-spec `#why-this-rating[-N]` ids) turned out to be a
  documented `::: details` disclosure id-mint, not a defect — a different
  page element than the stage/step ids checked above, but the same shape of
  false alarm.

**Not done here:** same as the sibling row — any emitter-side modelling
question (e.g. `NECROSPEC-UI-PLAIN-HEADING-NO-ID`, already filed by
`job_e87723`) is necrospec's own backlog, not this repo's.
