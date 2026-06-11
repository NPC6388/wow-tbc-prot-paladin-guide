# Session Log — Seal Swap rename recovery, stack-timer correction, ELI5 rotations, chart cleanups

**Date:** 2026-06-11 (Thu)
**Project:** TBC Paladin Tanking Guide
**Working Directory:** `C:\Users\matth\Desktop\AI\BiS\wow-tbc`
**Repo:** `wow-tbc-prot-paladin-guide` (live — https://npc6388.github.io/wow-tbc-prot-paladin-guide/)

---

## Context

The session began as **crash recovery**: the PC had crashed during an earlier open session, so we started by reading the in-guide changelog (then at **v2.9**, committed as `c0a3470`) and diffing the working tree to see where work had stopped. The uncommitted state turned out to be an **incomplete reversal of the v2.9 "Hybrid" naming back to "Seal Swap"** — ~70% done, with leftover "Hybrid" prose, a doubled-`@J2` and a `vsSeal Swap` typo, and a half-edited (self-contradictory) v2.9 changelog entry.

Three commits came out of the session: **v3.0 → v3.2**.

---

## Part 1 — Finish the "Hybrid" → "Seal Swap" rename (v3.0) · `ae1ed65`

The earlier (crashed) session had standardized the SoC↔SoR rotation name to "Hybrid" in v2.9, then started backing it out. Per the user's decision, **finished the revert to "Seal Swap"**:
- Renamed all remaining user-visible "Hybrid" → "Seal Swap" (prose definitions, the "Past ~1050 SP" tip, the per-stack table description). Left the unrelated **"Hybrid DPS"** gear-set name and internal JS variable names (`cumHybrid`, etc.) alone.
- Fixed two typos: doubled `@J2` in the catch-up-chart intro, and `vsSeal Swap` (missing space) in the 5-minute-TPS heading.
- **Restored the v2.9 changelog entry** to its original wording (it accurately records the Hybrid standardization as history) instead of leaving it half-edited.
- Added the **v3.0** changelog entry documenting the rename-back.
- **Deleted the stale `04318 prot talents.txt`** scratch file (its uncommitted Sanctity sheet had pre-v1.7 point numbers; removed at the user's request).

---

## Part 2 — Stack-timer correction, ELI5 rotations, tooltips, snap opener (v3.1) · `e6304ce`

From a fresh batch of notes in `changes for full guide.txt`:

### Mechanics fix — JoC does NOT refresh the Blood Corruption stack timer
The core correction (reconciled the user's items 1 + 6): **stacks are applied / the 15s timer refreshed only by melee hits with SoC active.** A judge consumes the seal and deals damage at the current stack count but neither rolls a new stack nor refreshes the timer.
- **Removed** the (incorrect) "Judging Corruption also rolls for a stack" tip box, which had claimed JoC could refresh the timer even while parked in SoR.
- Rewrote the Seal Swap definition + seal-management box to the consistent flow: **judge → re-seal SoC → let a melee refresh the timer → swap to SoR until ~9s remain on the stacks (or the next judge is due) → back to SoC.**
- The discrete-event sim already modelled this correctly (re-seal SoC, wait for a melee refresh before swapping); **only the prose was wrong.**

### New section: ELI5 Full Rotations (`#eli5-rotations`)
Plain-steps rotation for the four single-target cases (responsible for JotC or not × non-Demon/Undead or Demon/Undead), the shared **SoR→JoR opener**, the 5-stacks goal + "judge a 3–4 stack anyway / hold SoC before a Shatter-type mechanic" reminders, and a **verified advantage table** (Seal Swap + JotC over Pure SoR).
- **Verified the advantage numbers** by re-running the guide's own 5-minute `simSeal` logic in Node: 16.3k / 32.3k / 47.9k / 63.6k / 79.6k at 1–5 min — confirming the ">16k…>79k" figures. (Steady-state TPS: SoR 309, Seal Swap 436, Seal Swap+JotC 574.)

### Chart tooltips made legible
Set a **global opaque Chart.js tooltip default** (`Chart.defaults.plugins.tooltip`) — the default semi-transparent background let the lines bleed through. One change covers every chart.

### 60s comparison chart opens realistically
Added a **JoR snap at t=0** to the Seal Swap line (and, for a fair comparison, the SoR Only baseline and the JotC seal-swap variants) instead of cold-stacking SoC from zero — opening on SoC is never safe. Adding the same snap to both sides leaves the crossovers intact.

### Reframed the openers
There are **two judgement openers — JoR and JotC** — so JotC is no longer called a "third" opener. The sub-~400-SP SoB→JoB note is kept as the low-gear substitution.

---

## Part 3 — Chart cleanups, AOE rotation, blessing-spam filler (v3.2) · `a2e89b6`

From a further batch of notes:

### 60s seal-comparison chart
- **Removed the SoC + JotC line** (it opened with a 0-stack JoC, which you'd never cast) — sim state, accumulator, dataset, and note all dropped.
- **Added the missing definition** for the Seal Swap + Ret JotC line (the chart had 5 lines but the text only defined 4).
- **Re-ordered the rotation definitions by highest threat at 60s** (Ret JotC → self JotC → Seal Swap → SoR Only).
- Switched the chart to **full-resolution data** (every 0.1s instead of 7 ten-second points) so the mouseover reads smoothly at every point, like the other threat charts.

### Opener-comparison timelines
**Removed the SoC opener** from both the Standard and Demon/Undead graphs, the intro text, and the chart-note readouts (plus the now-unused `sim1a`/`sim2a`). The opener-comparison **table** keeps its SoC-opener row as the "why it's wasted (0-stack JoC = 0 damage)" explanation — confirmed with the user to keep that note.

### ELI5 additions
- **AOE / multi-target rotation:** Pure SoR on the highest-priority mob; Consecration + Holy Shield (+ RF, + Avenger's Shield if specced) as pack threat; watch the rest of the pack with a threat-plate overlay.
- **Blessing-spam filler note:** casting **Greater Blessing of Might on the largest class group** during empty GCDs (mana permitting) is free RF-amplified threat — links to the `#blessing-spam` (Greater Blessing Threat) section.

---

## Verification (each commit)
- All **11 inline `<script>` blocks parse** clean (`new Function` syntax check) after every JS change.
- Advantage table cross-checked against the live 5-minute sim (matched).
- Grep sweeps confirmed: no remaining "judge refreshes/rolls a stack" prose, no "third opener" framing, removed datasets gone, `#blessing-spam` / `#eli5-rotations` anchors resolve, SoB low-gear note preserved.

## Files Touched
- **`index.html`** — Part 1: Seal Swap rename + typo fixes + v2.9 restore + **v3.0** changelog. Part 2: stack-timer prose correction; ELI5 Full Rotations section; global tooltip default; 60s snap-opener; opener reframe; **v3.1** changelog. Part 3: 60s chart line removal/reorder/full-res; opener-chart SoC removal; AOE rotation + blessing-spam note; **v3.2** changelog.
- **`04318 prot talents.txt`** — deleted (Part 1).
- **`SESSION_LOG_2026-06-11.md`** — this log.

## Commits
- `ae1ed65` — v3.0 (Hybrid → Seal Swap rename + talents-file deletion)
- `e6304ce` — v3.1 (stack-timer correction, ELI5, tooltips, snap opener, opener reframe)
- `a2e89b6` — v3.2 (chart cleanups, AOE rotation, blessing-spam filler)

All pushed to `main`.
