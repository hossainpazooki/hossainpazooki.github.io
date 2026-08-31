# / (homepage) — datum · intent · rigor rebuild brief

Brainstormed 2026-08-31. Decisions locked with Hossain: direction B
("three planes, one section") from the design canvas; **full rebuild** of
`index.html`; taxonomy as drawn (ATLAS under INTENT, CLDD + CLUE under
RIGOR); no `/datum` umbrella page yet; **paper is the default theme**;
tech trimmed to essentials — on the page (skills grid → one band) and in
the implementation (three JS behaviors, no more).

## What the page is

The homepage reorganized around three named programs — every project an
instrument of exactly one:

| program | creed | instruments |
|---|---|---|
| **DATUM** | what is known | vantage · parallax · baseline · meridian (proposed) |
| **INTENT** | what may act | intent-plane · treasury gate · atlas |
| **RIGOR** | what keeps both honest | rigor · deploy layer (provisional) · cldd · clue |

Visual language: the existing token set (ink/paper palettes, IBM Plex
Mono/Sans + Space Grotesk, gold accent, eyebrows, hairline borders,
reveal-on-scroll, reduced-motion fallbacks). Full rebuild means new
information architecture, not a new brand. The signature moment moves
from the integrity-gate panel (retired) to the cross-section figure.

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
- the theme script's final `apply()` fallback flips the same way as the
  bootstrap.

A stored ink choice is still honored — only the no-preference fallback
changes. `color-scheme: light` on base, `dark` under ink.

## Header

Sticky, mechanics unchanged. Nav is the thesis:
`datum · intent · rigor · career · blog` + theme switch. Band links go
to in-page fragments `#datum` / `#intent` / `#rigor` (fragments don't
collide with the `/intent` and `/rigor` paths).

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
- CTAs: `Walk the section ↓` (primary, → `#datum`, the first program
  band — the figure itself is already above the fold) · `GitHub ↗`
  (ghost).
- The integrity-gate panel is **retired**; its creed survives in the
  figure labels and the footer.

## The cross-section (signature figure)

Full-width, directly under the hero, `role="img"` with a prose
`aria-label`. Drafting conventions carry claim state: **solid = built,
dashed = proposed**.

- **RIGOR — the audit boundary**: dashed gold enclosure around
  everything, tab label top-right; its rail row sits inside the
  boundary's bottom edge (rigor · cldd · clue chips).
- **INTENT plane** (upper band): three cells — intent-plane · treasury
  gate · atlas.
- **Gate interface line** between the bands: dashed rule with three
  small gate squares; caption `actions touch the data plane only
  through gates · fail-closed on unevaluable`.
- **DATUM bedrock** (lower band, faint 135° hatch): four cells —
  vantage · parallax · baseline · meridian (meridian's cell rendered
  with the ○ proposed lamp and a dashed border).
- Section markers `A —` / `— A′` at the sides.
- Every cell is a link (destinations under Program bands below).
- Load animation, one-time: datum settles first, intent above it, then
  the rigor boundary traces around both — interpret → execute → attest
  as motion. Reduced motion ⇒ fully drawn, static.

## Program bands (replaces "systems" duo + work ledger)

One section per program: eyebrow `program 01 · datum` (02 · intent,
03 · rigor), creed as H2, one lede paragraph, then instrument rows in
ledger style — `name · effect · evidence · lamp` — with the lamp legend
printed once above the first band:
`● done — the row's word says how (built · verified · shipped ·
published) · ◐ concept / provisional · ○ proposed — unclaimed`.

### 01 · DATUM — "What is known."

Lede: a shared reference frame for checkable financial-data claims —
produced point-in-time, adversarially re-derived, recorded as dated,
replayable verdicts.

| row | effect | evidence | lamp | link |
|---|---|---|---|---|
| vantage | An as-of date returns only what was filed and accepted by that date — across restatements. | 86.6M gold facts · 63/69 quarters · 6 refused | ● verified | repo ↗ |
| parallax | The consumer side re-derives every number and trusts nothing it did not recompute. | adversarial twin of vantage | ◐ concept | repo ↗ |
| baseline | The public catalog of dated, replayable verdicts — the fixed separation underneath both. | one read surface · one Reader protocol | ◐ concept | /baseline |
| meridian | An event-sourced portfolio ledger whose every number can be recomputed, by anyone, to the byte. | P1–P6 unclaimed · design locked 2026-08-31 | ○ proposed | repo ↗ |

### 02 · INTENT — "What may act."

Lede: a fail-closed authorization plane for irreversible actions —
agents propose, a deterministic gate disposes, one durable record per
decision.

| row | effect | evidence | lamp | link |
|---|---|---|---|---|
| intent-plane | Agents propose, the gate disposes — one durable record per decision, re-verifiable without trusting the gate. | declarant + verifier · LangChain / MCP / reporting adapters | ● built | repo ↗ |
| treasury gate | A duplicate of an irreversible action isn't caught — it's impossible. | sole emitter of ACHIEVED · byte-identical replay | ● verified | /intent |
| atlas | Contradictory multi-jurisdiction regulation compiled into signed, content-addressed, executable artifacts. | five-gate stack · 1,326 Rust↔Python equivalence scenarios | ● verified | repo ↗ |

### 03 · RIGOR — "What keeps both honest."

Lede: the discipline turned on the work itself — refute a claim before
believing it, keep built-vs-planned honest, never let an agent write
git history.

| row | effect | evidence | lamp | link |
|---|---|---|---|---|
| rigor | Don't trust the claim — try to break it; never let an agent write your git history. | 20 skills · 8 commands · 11 gates · stdlib-only | ● shipped | /rigor |
| └ deploy layer | Six deployment-discipline properties, promoted only after ≥2 independent domains. | fixture-tested · zero domains · ADR-0013 | ◐ provisional | (sub-row of rigor) |
| cldd | Closed-loop default detection — plant the truth, hide it the way real approval policies do, escalate until correction fails. | essay published in Towards AI · Jul 2026 | ● published | /cldd |
| clue | Upstream label correction — catch mislabeled samples through cross-omics concordance before they poison downstream. | F1 0.914 on the organizers' own key | ● verified | repo ↗ |

## Proof strip

The four facts survive, relabeled `what the section is load-tested by`,
each tracing to its band or the career entry:
`86.6M gold facts` (→ #datum) · `five-gate` (→ #intent) ·
`fail-closed` (→ #intent) · `34% fewer` (→ #job-orawell).

## Writing (condensed)

One essay card — "When You Can't Measure What Matters" — with the
existing meta line (`9 min read · published in towards ai · code &
data: cldd`) and `all posts /blog →`. It loses top billing to the
triad; the duo layout is retired.

## Career & skills (condensed)

- Timeline keeps all four roles + education row; bullets trimmed to
  **≤2 per role** (Orawell keeps the team-lead line and the 34% gate
  line; earlier roles keep one line each).
- Skills grid (2×2, 16 items) → **one band, four cells, one chip-line
  each**:
  - data — Scala · Spark · Delta Lake · Databricks · Airflow · dbt
  - correctness — fail-closed gates · eval harnesses · signed artifacts
  - agents & LLMs — PydanticAI · hybrid RAG · confidence calibration
  - systems — Python · Rust · Go · TypeScript · Kubernetes · PostgreSQL

## Footer

Line 1: `datum → intent → rigor · below the line, above the line,
around both.`
Line 2 (kept from today): `interpret → execute → attest. AI you can
prove, not just trust.`
Links unchanged (site, GitHub, LinkedIn, email).

## Implementation essentials

- One static `index.html`, no build step, fonts unchanged.
- JS = exactly three behaviors: theme switch (localStorage `hp-theme`),
  IntersectionObserver reveal, one-time figure settle (class toggle,
  CSS transitions). The verdict animation retires with the gate panel.
- noscript: paper theme, everything revealed, switch hidden.
- Mobile: figure planes stack (label above cells); intent cells 3→1,
  datum 4→2→1; instrument rows fold to two lines (name + lamp / effect);
  band nav links hide at the same breakpoint the current nav collapses.
- Legacy fragments: grep subpages + blog for `/#systems`, `/#work`,
  `/#skills` home links and repoint to the new ids in the same change.
  `#career` and `#job-orawell` ids are kept.
- A11y: figure `aria-label` describes all three planes; lamps always
  paired with words, never color alone; focus-visible and selection
  styles unchanged.

## Honesty rules for copy

- Every number is a repo fact: 86.6M gold facts, 181M bronze rows,
  16,667 filers, 63/69 quarters, 6 refused, 34% fewer denials, 1,326
  scenarios, F1 0.914, 20 skills / 8 commands / 11 gates, P1–P6,
  design locked 2026-08-31. Nothing else quantitative may appear.
- Statuses are restated from each repo's own state of record, never
  upgraded: meridian is **○ proposed** everywhere (dashed in the
  figure) until its STATUS.md moves; parallax and baseline stay
  ◐ concept; rigor's deploy layer stays ◐ provisional until the
  feedback ledger promotes it.
- Solid = built, dashed = proposed — applied consistently in the figure.
- No production claims anywhere the repos make none.
