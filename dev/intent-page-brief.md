# /intent/ — page design brief

Brainstormed 2026-07-15. Decisions locked with Hossain: URL `/intent/`; gate-centered
scope with the loop shown; section-0 effect visual = the duplicate-payment kill;
concept page in the CLDD skin (no version timeline — the repo has no releases yet).

## What the page is

The destination for the homepage's "Intent Layer" work card (currently unlinked).
A concept page for the **authorization plane** of the ATLAS treasury intent loop:
`treasury-intent-controller` — the deterministic Go gate that is the sole authority
to emit one durable `ACHIEVED` record. Treasury payments (class 1) are the worked
example; the framing stays domain-agnostic, matching the homepage card.

Visual language: identical token set to `/cldd/` (ink/panel/gold IBM Plex system,
eyebrows, `.section` frames, pills, reveal-on-scroll, prefers-reduced-motion
fallbacks). Brand: `hp / intent.`

## Section 0 — the effect (CLDD-style intro, above the hero)

- **Eyebrow:** `the effect of running the intent layer`
- **H1:** "A duplicate payment doesn't get caught. **It becomes impossible.**"
  (dim second line: "Same key, one changed field — refused at the dispatch edge,
  by construction.")
- **Lede:** An irreversible action is authorized only by a reproducible, measured
  demonstration that it meets declared criteria. The gate is the sole emitter of a
  single durable `ACHIEVED` record — and **no record ⟹ no value moved**.
- **Without / with rows** (`.fx` pattern):
  - *without* — At-most-once is an assertion: dedup lives in adapter logic and
    retry queues, audited after the fact. A retried near-duplicate can settle twice
    before anyone reads the log.
  - *with intent layer* — The idempotency key is a **declared, first-class gate
    criterion**: required (absent ⟹ unevaluable ⟹ fail-closed), reserved at the
    dispatch edge. Same key + changed field ⟹ **FAILED_AT_DISPATCH**. At-most-once
    holds on the settlement log **by construction**.
- **Visual (the loop-visual analogue):** ring with four lifecycle nodes —
  `01 declare · 02 verify · 03 re-check · 04 emit` — plus the two **amber**
  idempotency checkpoints rendered distinctly (they're the signature of the system,
  as in the README's mermaid). Center readout cycles the duplicate-payment kill:
  1. `intent 7f3a… · DECLARED · key pay-2026-07-042` — ✓
  2. `VERIFYING · criteria pass · none unevaluable` — ✓
  3. `dispatch edge · volatile re-check holds` — ✓
  4. `key reserved · ACHIEVED · one durable record` — ✓ (gold)
  5. `replay: same key · amount changed` — ⚠
  6. `collision → FAILED_AT_DISPATCH` — ✗
  7. `settlement log: 1 record · value moved once` — final frontier-style state (gold, longest hold)
  Reduced motion ⇒ jump straight to state 7.

## Hero

- Eyebrow: `treasury-intent-controller · the authorization plane`
- H: "**Nothing moves until the gate says so.**"
- Lede: deterministic Go gate; tri-state fail-closed scoring (`Fail` or
  `Unevaluable` ⟹ denied — unevaluable never collapses into a pass); volatile
  facts re-checked at the dispatch edge by the same authority; every run replays
  byte-identically from a logical-clock event log.
- Pills: `deterministic — byte-identical replay` · `fail-closed on unevaluable` ·
  `kill/restart proven` · `Go gate + Python scorer`
- Terminal panel (the CLDD install-block analogue): a wire transcript instead of
  pip — `POST /v2/intents` → lifecycle events → `GET /v2/events?since=` →
  the `ACHIEVED` record a consumer settles from.
- CTAs: GitHub repo ↗ · back to `#loop` / home.

## Body sections

1. **The lifecycle** (`#lifecycle`, loop-strip analogue) — 4-step strip
   *declare → score → re-check → emit*, with the state machine named:
   `DECLARED → RESOLVING → ACTIVE → VERIFYING → {ACHIEVED | FAILED | FAILED_AT_DISPATCH}`.
   Scope note (CLDD's "Scope" pattern): **emit-and-observe** — the gate's job ends
   at the durable record; it settles nothing and never calls out.
2. **Six invariants** (`#invariants`) — the README's invariants as a 3×2 card grid:
   sole emitter · tri-state fail-closed · stable vs volatile · idempotency by
   construction · determinism/replay · durability (kill/restart over the same
   `TIC_DATA_DIR`, seq continues gapless).
3. **The loop around the gate** (`#loop`) — three planes, one strip:
   ATLAS `IntentSpec` (signed, expert-attested criteria — the gate *consumes*,
   never authors) → **the gate** (this page) → COMPASS settlement consumer
   (pulls `GET /v2/events?since=cursor`, recomputes from observed `ACHIEVED` only,
   keyed ledger ⟹ at-most-once end-to-end — the same declared key on both sides).
   Honesty boundaries stated in-line, CLDD "reading caveats" style: wheel-backed
   artifact reader is Linux/CI-only (its test lane skips visibly); the criteria/
   threshold config on the consumer side is app config bound to the pinned spec
   hash (recorded parity debt); no production claim.
4. **Contracts** (`#contracts`, policy-grid analogue) — "what a contract is allowed
   to claim": `CONTRACT.md` (slice 1) · `CONTRACT-DURABILITY.md` (durability +
   emit-and-observe deltas) · `CONTRACT-SCORER.md` (`/ml/evaluate` wire seam) —
   most-recent-contract-wins rule; golden wire fixtures as the byte-level seam.

## Footer

Thesis line: `declare → verify → re-check → emit.` / "No record ⟹ no value moved."
Links: home · GitHub repo · email.

## Companion change

Homepage `index.html`: link the "Intent Layer" work card to `/intent/` with the
`→ /intent` source affordance, matching the CLDD card.

## Honesty rules for copy

- Every number on the page must be a repo fact (states, invariants, contract
  count, fsync-per-append, tri-state). No invented metrics, no version timeline
  until the repo actually cuts releases.
- Status is "built and verified — slice 1 + durability + live scoring seam";
  pending slices (settlement-consumer productionization, wheel-backed reader,
  IntentSpec resolver extraction) are named, not hidden.
