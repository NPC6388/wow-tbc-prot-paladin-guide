# Session Log — 2026-06-20

**Project:** TBC Paladin Tanking Guide
**Working Directory:** `C:\Users\matth\Desktop\AI\BiS\wow-tbc`

---

## Damage & Threat per Mana section (v3.4) · `f4f12ef`

New section under **Combat Mechanics**, after Mana Management (`#mana-efficiency`): two charts + tables ranking every offensive ability (auras excluded) by mana efficiency at the raid-buffed 709-SP profile.

### What was added
- **Damage per Mana** — table + horizontal bar chart.
- **Threat per Mana** — table + chart, also including **blessing spam** (threat-only, ~0 damage).
- **Methodology / caveats** collapsible: per-cast (≈ per-8s) model, seal re-seal amortization over the ~8s judge cycle, judgements "borrowing" seal-built stacks, per-target/AOE multipliers (Consecration & Holy Wrath × pack size, Avenger's Shield × up to 3), and every mana cost.

### Headline ranking (single target, 709 SP)
Threat/mana: **JoC 12.2 > JoR 9.7 > JoB 8.5 > SoR/SoC 7.2 > Exorcism 6.6 > Holy Shield 5.0 > Consec 3.5 > blessing spam 1.9 ≈ Holy Wrath 1.9 > Avenger's Shield 1.7 > Seal of Blood 1.1.** Damage/mana is the same shape ÷ 1.9 (blessing spam drops out). Confirms the existing rotation/mana guidance — Judgement & Holy Shield are highest priority *and* highest efficiency; Consecration is the mana hog you drop first.

### Consecration Rank 5 vs Rank 6 (added to both charts)
Rank 5 keeps the **full SP coefficient** (downrank penalty only hits sub-level-20 ranks; R5 is level 60) at 66% of the mana, so at raid SP it's **more efficient than R6**: ~2.5 vs 1.9 dmg/mana and ~4.8 vs 3.5 threat/mana (~89% of R6's per-cast output). Downranking note added: stretch uptime with R5, max throughput with R6.

### Mana-cost correction
- **Consecration R6 mana 561 → 660.** Benediction reduces **only Seals and Judgements**, not Consecration (verified on Wowhead + community sources), so the prior 561 (which assumed a 15% Benediction discount) was wrong.
- Updated the dependent Mana Management math: full rotation **~1,201 → ~1,300 mana**/8s cycle, **~53s → ~49s** sustain at 8k mana without returns. No TPS/threat numbers affected.

### Mana costs used (verified)
Consecration R6 660 / R5 435, Holy Shield 280, Avenger's Shield 780, Exorcism 295, Holy Wrath 825 (Wowhead TBC); Seal 210 and Judgement ~150 (5/5 Benediction); Greater Blessing of Might 295.

## Files Touched
- **`index.html`** — new `#mana-efficiency` section (2 charts + tables + methodology), Consecration mana fix in Mana Management, TOC entry, **v3.4** changelog.
- **`SESSION_LOG_2026-06-20.md`** — this log.

## Commits
- `f4f12ef` — v3.4 (Damage & Threat per Mana section, Consec R5/R6, Consec mana fix). Pushed to `main`.

---

## TODO / Next session
- [ ] **Look into creating a WeakAura for a Prot Paladin to help with the Seal Swap rotation.** Goal: a visual aid that makes the SoC→SoR seal swap easy to execute live — e.g. track Blood Corruption stack count + remaining duration on the target, show when to re-seal SoC vs swap to SoR, flag when stacks are about to fall off (~9s left / before a Shatter-type mechanic), and surface the judge cooldown. Cross-reference the Seal & Judgement Threat Analysis section's documented swap flow (judge → re-seal SoC → let a melee refresh the timer → swap to SoR until ~9s remain or next judge → back to SoC). Consider whether to ship the WeakAura import string in the guide (the WeakAuras subsection currently lives in the `review prior to inclusion.html` holding file).
