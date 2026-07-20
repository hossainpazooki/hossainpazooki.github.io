# Session learnings — homepage claim-ledger fixes

Date: 2026-07-19. Branch: `claude/portfolio-claim-ledger-fixes-k8zr7u` → PR #4.
Scope: content + structure pass on `index.html`, one count sync on `/rigor`.
No redesign — existing token set, nav, and the `/cldd` + `/intent` pages left alone.

## Ground rule that drove everything

**Every factual claim on the site must trace to a committed repo artifact, read or
recomputed this session.** Not memory, not the previous copy of the site, not the
seed prompt's own numbers. This rule caught real errors in *both* the live site and
the brief I was working from — see "Numbers the brief got wrong" below. When a claim
couldn't be confirmed, it was dropped, not softened.

Verification was done against read-only clones at these HEADs (record them — the
numbers below are only true as of these commits):

| repo | HEAD | dated |
|---|---|---|
| `regulatory-rule-engine` (ATLAS) | `e647be3` | 2026-07-15 |
| `cross-border-compliance-navigator` (COMPASS) | `cdb258a` | 2026-07-14 |
| `pit-fundamentals-lakehouse` (VANTAGE) | `fa97d80` | 2026-07-19 |
| `rigor` | `ba58192` | 2026-07-18 |
| `upstream-label-correction` (CLUE) | `a777cca` | 2026-07-14 |

## What was stale on the homepage (and the correction)

- **ATLAS "5-tier / T0–T4 consistency engine"** — banned framing, and the repo's own
  prose leads with a *different* slicing: a **five-gate verification stack** (schema,
  semantic, source-span, conflict, expert-attestation), verbatim from the trust
  pipeline in `README.md`. Note the repo *also* carries a T0–T4 "tier" taxonomy that
  is **not** a 1:1 rename of the gates — don't conflate them, and don't reintroduce
  "tier" for ATLAS. Migration "Gates 0–6" in that repo are delivery phases, a third
  unrelated meaning of "gate".
- **ATLAS tags PyO3 / Temporal** — PyO3 exists (feature-gated) but is not in the
  verified tag set; **Temporal is an explicit non-goal** living in a sibling Python
  repo (`ADR-0015`). Tags are now: Rust workspace · BLAKE3 content-addressed ·
  ed25519-signed · typed attestations · WASM verifier.
- **COMPASS "FastAPI · PydanticAI · React · TypeScript · EKS"** — wrong. The repo is
  **Next.js 15.5 · React 19 · TypeScript 5**, a client-side rule evaluator, an
  in-browser WASM verifier of ATLAS artifacts, and an NLI gate that retracts
  ungrounded rationale. No Python anywhere; FastAPI is self-documented as
  historical/out-of-graph; EKS is an unwired external proxy target. Deploys to Vercel.
- **COMPASS "GENIUS Act"** — **zero occurrences** in the repo. Real frameworks:
  MiCA, FCA, SEC/CFTC, FINMA, MAS. (The brief still said "GENIUS Act" — the ground
  rule is what caught it.)
- **"458+ tests" capability card** — dropped. Ambiguous provenance (it was actually a
  figure for the Orawell RCM stack, not ATLAS). The **450+ CI-gated** anchor now sits
  only on the Orawell career bullet. ATLAS's real count is ~155 pre-graph / ~187
  post-graph — "278/457/458" appear nowhere in that repo — so no ATLAS test count is
  shown at all.
- **CLUE "CPTAC/TCGA"** — the real CPTAC/TCGA/precisionFDA data is **gitignored, never
  committed**; where real matrices are run they're labelled *robustness, not
  validation*. The committed instrument is **synthetic multi-omics cohorts with
  planted, dial-able label corruption** (precisionFDA/NCI-CPTAC-style). Tag replaced.
- **Skills "Quant risk — VaR/CVaR"** — removed; realigned to the DE-pivot keyword set
  (point-in-time, validation harnesses, fail-closed gates, Scala/Spark/Delta,
  Databricks, ETL, evaluation infra). Agentic/LLM kept but no longer leading.
- **Headline "AI/ML Engineer & Tech Lead"** — retired for **Data Engineer · AI/ML
  Platforms & Evaluation** across title/eyebrow/meta/lede. The interpret→execute→attest
  hero block was preserved — it's the strongest thing on the page.

## Numbers the brief got wrong (verify-before-write earning its keep)

- **rigor: not "3 hooks / 8 gates".** README at HEAD says **"Two hooks"** and **"all 8
  check gates"**; the repo has exactly 2 hook files and 8 `check-*.mjs` scripts. So
  **2 hooks / 8 gates**. The two gates added since the old "6" were
  `check-tier-placement` and `check-learnings`. (Old site said 2/6.) The instruction
  to "take whatever the README says now" is the only reason this landed right.
- **VANTAGE gold facts = 86,615,392, not 86,616,395.** The `…395` figure is the
  **silver** count; gold is smaller by 1,003 rows (2013q1 orphan `adsh`s dropped by
  gold's inner join). Easy to mislabel — they're one line apart in the metrics doc.
- **VANTAGE stack: Deequ was removed 2026-07-18** for a native DataFrame DQ gate.
  Listing Deequ as *current* tech would be wrong; the card says "fail-closed DQ gate".
  (Confirmed counts: 181,351,169 bronze → 86,615,392 gold across 16,667 CIKs; 63/69
  quarters, 6 DQ-refused. Databricks-serverless publish CREDITED 2026-07-19.)

## Repo nuances a future edit must not "fix" backwards

These are cases where the *repo* contains something that looks like it contradicts
the shipped site, but doesn't — reverting to it would reintroduce a banned/wrong claim:

- **ATLAS carries both framings.** The five-gate trust pipeline AND a T0–T4
  `enum Tier` table coexist in-repo as different slicings (source-span folds into T1;
  expert-attestation is unnumbered). Seeing the tier table is **not** license to
  reintroduce "5-tier" — that framing is banned for this site.
- **PyO3 is genuinely in ATLAS** (feature-gated in `ke-artifact`, powers the Python
  wheel). It was dropped from the card to hold the five verified tags, *not* because
  it's absent. Temporal, by contrast, is truly refuted (ADR-0015 non-goal). Don't
  "restore" PyO3 thinking it was an error.
- **COMPASS's in-browser WASM verify path is real but flag-gated** pending the
  `@platform/atlas-artifact` publish; default mode is a committed provenance snapshot.
  The card phrases it architecturally on purpose — do not upgrade it to "live by
  default."
- **CLUE's real-data F1 0.914** exists but is on gitignored precisionFDA train data
  and the repo labels real-matrix runs "robustness, **not** validation." That's why
  the card claims neither the score nor the dataset names.

## Structure change

Added a featured **"Three systems, one discipline"** band directly under the hero so
`/rigor`, `/cldd`, `/intent` are visually primary and one click from above the fold,
each with its own effect one-liner. The four repo cards (VANTAGE, ATLAS, COMPASS,
CLUE) moved into "Selected work" below. New `systems` nav link + hero CTA point at it.

## Process notes for next time

- **Fan out the verification.** One read-only Explore agent per repo, each returning
  CONFIRMED/REFUTED + `path:line` evidence, was the right shape — parallel, and the
  structured verdicts dropped straight into edits.
- **Grep the built pages for banned strings before opening the PR.** Final sweep for
  `5-tier`, `457`, `458`, `PyO3`, `Temporal`, `VaR`, `at scale`, `high-throughput`,
  `CPTAC`, `TCGA`, `GENIUS`, and `FastAPI`/`EKS` *in the wrong context*. Zero hits.
  Watch the false positives: `initial-scale=1` (viewport meta) and the legitimately
  historical `FastAPI`/`EKS` in the Orawell employment bullet are fine — the banned
  context for those was the COMPASS card specifically.
- **Render before committing.** Use reduced-motion emulation
  (`emulateMedia({reducedMotion:'reduce'})`) or the scroll-reveal (`.reveal`,
  `opacity:0`) leaves full-page screenshots black. Chromium is at
  `/opt/pw-browsers/chromium-1194/chrome-linux/chrome`; playwright is a global module
  (`/opt/node22/lib/node_modules/playwright`), so import it by absolute path or set
  `NODE_PATH`.
- **Design tokens are shared across all four pages.** Any palette/token change (e.g.
  the amber-temperature question) must go sitewide or it breaks the visual continuity
  the featured band depends on. The accent is already amber-family: `--gold #E0A436`
  (muted amber-gold), `--gold-dim #7a5d22`, hover `#edb24a`/`#f3c269`, plus
  `rgba(224,164,54,…)` glow literals.
