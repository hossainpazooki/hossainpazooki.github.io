# / (homepage) — datum · intent · rigor rebuild brief

Brainstormed 2026-08-31. Decisions locked with Hossain: direction B
("three planes, one section") from the design canvas; **full rebuild**
of `index.html`; taxonomy as drawn (ATLAS under INTENT, CLDD + CLUE
under RIGOR); no `/datum` umbrella page yet; **paper is the default
theme**; the live LinkedIn headline featured up top; tech trimmed to
essentials. **Revised same day: minimal scroll surface** — the homepage
is the hero, the cross-section, and one bottom index. The program
bands, research section, proof strip, writing card, career timeline,
and skills band are cut from home; that content lives on the subpages,
the repos, `/blog`, and LinkedIn.

## What the page is

A two-viewport homepage. Viewport one: the headline, the name, the
cut. Viewport two: the rest of the cross-section and the index. The
figure is the site map — every cell links to its instrument — and the
index carries everything that isn't in the triad.

| program | creed | instruments |
|---|---|---|
| **DATUM** | what is known | vantage · parallax · baseline · meridian (proposed) |
| **INTENT** | what may act | intent-plane · treasury gate · atlas |
| **RIGOR** | what keeps both honest | rigor · cldd · clue |

Visual language: the existing token set (ink/paper palettes, IBM Plex
Mono/Sans + Space Grotesk, gold accent, eyebrows, hairline borders,
reduced-motion fallbacks). The signature moment is the cross-section;
the old integrity-gate panel is retired, its creed surviving in the
figure labels and the closing creed lines.

## Theme: paper default

Same five flips the blog made (see `feat(blog): paper is the blog's
default theme`), applied to `/`:

- base `:root` tokens become the **paper** palette; `[data-theme="ink"]`
  carries the dark overrides (today it's the reverse) — so the no-JS
  default is paper;
- static `data-theme` attribute on `<html>` → `"paper"`;
- `theme-color` meta default → `#F6F4EE`;
- head bootstrap fallback flips: `s === 'ink' ? 'ink' : 'paper'`
  (still reads `hp-theme`, legacy `baseline-theme`);
- switcher order `paper | ink`, paper initially pressed;
- the theme script's final `apply()` fallback flips the same way.

A stored ink choice is still honored — only the no-preference fallback
changes. `color-scheme: light` on base, `dark` under ink.

## Header

Sticky, minimal — no section anchors, the figure is the nav:
brand `HP.` · `blog` · `hossainpazooki.com ↗` · theme switch
(paper | ink).

## Hero

- Eyebrow — the current LinkedIn headline, verbatim, featured up top:
  `Building auditable agentic systems and the cost-efficient serving
  infrastructure they run on — New York`
- `<title>` and the meta description lead with the same headline
  (locked 2026-08-31 from the live LinkedIn profile).
- H1: `Hossain Pazooki` / dim second line `Three planes, one section.`
- Lede: "Everything I build sits somewhere in this cut: **a data plane
  for what is known, an authorization plane for what may act, and an
  audit boundary that holds both to their evidence.**"
- No CTA row — the figure sits directly below; contact lives in the
  index.

## The cross-section (the page's body)

Full-width, directly under the hero, `role="img"` replaced by a real
landmark: it's interactive navigation, so an `aria-label`ed `<nav>`
region whose cells are links. Drafting conventions carry claim state:
**solid = built, dashed = proposed**.

- **RIGOR — the audit boundary**: dashed gold enclosure around
  everything, tab label top-right; its rail row inside the boundary's
  bottom edge.
- **INTENT plane** (upper band): intent-plane → `/intent` (the concept
  page leads) · treasury gate ↗ treasury-intent-controller · atlas ↗
  regulatory-rule-engine.
- **Gate interface line** between the bands: dashed rule, three gate
  squares, caption `actions touch the data plane only through gates ·
  fail-closed on unevaluable`.
- **DATUM bedrock** (lower band, faint 135° hatch), baseline leads:
  baseline → `/baseline` · vantage ↗ pit-fundamentals-lakehouse
  ("point-in-time SEC fundamentals — 86.6M gold facts") · parallax ↗
  pit-revision-examiner · meridian ↗ repo — meridian's cell dashed
  with the ○ lamp and "design locked · unclaimed".
- **RIGOR rail**: rigor → `/rigor` ("plugin · 20 skills · 11 gates") ·
  cldd → `/cldd` · network-as-code ↗ repo (name-only chip — no
  descriptor invented until one is supplied) · clue ↗ repo.
- Section markers `A —` / `— A′` at the sides.
- Caption line under the figure, mono, split left/right:
  `every cell is a link — the section is the site map` ·
  `solid = built · dashed = proposed · statuses restated from each repo`.
- Load animation, one-time: datum settles first, intent above it, then
  the rigor boundary traces around both — interpret → execute → attest
  as motion. Reduced motion ⇒ fully drawn, static.

## The index (bottom)

One bordered block, three rows (`label · line · destination`), then the
creed line and ©. Everything cut from home resolves to a link here
(no contact row — email lives off-home; the blog stays in the header):

| row | line | destination |
|---|---|---|
| research | cross-model KV-cache transfer · `◐ in progress · paper in preparation` | GitHub ↗ (profile) |
| writing | when you can't measure what matters · towards ai, jul 2026 | Medium ↗ (the Towards AI essay) |
| career | algoverse (now) · orawell · engager · 3deo · penske media | LinkedIn ↗ |

Closing creed line under the block:
`interpret → execute → attest. AI you can prove, not just trust.`
Plus `© 2026 Hossain Pazooki · New York`. (The datum → intent → rigor
line was cut 2026-08-31.)

## Implementation essentials

- One static `index.html`, no build step, fonts unchanged.
- JS = exactly three behaviors: theme switch (localStorage `hp-theme`),
  a light reveal, one-time figure settle (class toggle, CSS
  transitions). The verdict animation retires with the gate panel.
- noscript: paper theme, everything revealed, switch hidden.
- Mobile: figure planes stack (label above cells); intent cells 3→1,
  datum 4→2→1; index rows fold to two lines (label + destination /
  line); header stays one row.
- Legacy fragments: repoint `/#systems`, `/#work`, `/#skills`,
  `/#career` links in subpages + blog to `/` (there are no in-page
  section targets anymore).
- A11y: the figure is a `<nav aria-label="…">` of real links; lamps and
  dashes always paired with words, never color alone; focus-visible
  and selection styles unchanged; hit targets ≥ 44px on touch.

## Honesty rules for copy

- The only numbers on the home surface are the figure's repo facts:
  `86.6M gold facts` (vantage cell) and `20 skills · 11 gates` (rigor
  chip). Everything else quantitative lives on the subpages and repos.
- Statuses are restated from each repo's own record, never upgraded:
  meridian is **○ proposed** — dashed cell, "design locked ·
  unclaimed" — until its STATUS.md moves; research is `◐ in progress ·
  paper in preparation` (live work, locked 2026-08-31 from the
  LinkedIn record; the open question stays off home). No result is
  claimed until the paper exists.
- Solid = built, dashed = proposed — applied consistently.
- No production claims anywhere the repos make none.
