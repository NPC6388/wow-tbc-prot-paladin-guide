# Session Log — Air Totem & Wizard Oil Threat Comparison

**Date:** 2026-05-28
**Project:** TBC Paladin Tanking Guide
**Working Directory:** `C:\Users\matth\Desktop\AI\BiS\wow-tbc`
**File created:** `buff_comparison_woa_wf_wizoil.html`

---

## Objective

User question, in two parts:

1. For a Prot Paladin tank, compare the **DPS and TPS contribution** of three party/self buffs:
   - **Wrath of Air Totem** (+101 spell power, Air slot)
   - **Windfury Totem** (extra melee attack proc, Air slot — mutually exclusive with WoA)
   - **Superior Wizard Oil** (+42 spell damage, self-applied weapon coat)
2. Then extend the chart to model **totem twisting** — what does the threat curve look like if the shaman alternates WF and WoA on a cycle?

Output requirement: standalone HTML page opened in a new browser tab, styled to match the existing `prot_paladin_rotations.html` guide.

---

## Work Completed

### 1. Baseline reuse

Reused the gear/raid-buff profile from the main rotation guide so numbers stay consistent:
- 556 SP, 496 AP, 1.8s spell-power weapon (41 weapon DPS)
- 10% melee crit / 10% spell crit
- 2/2 Improved Holy Shield (8 charges, +20% HS damage)
- 2pc Justicar (×1.10 on seal procs / SoC DoT — does **not** apply to judgements)
- 1.9× Righteous Fury, level 73 boss
- Spell miss 11.89%, melee miss 6%
- Seal of Righteousness as default seal

### 2. Per-ability tables built for all three buffs

For each buff, computed Δdamage and Δthreat for every Holy ability with an SP coefficient (or every melee swing, for WF):

| Ability | SP Coef | Notes |
|---|---|---|
| SoR proc | 0.20 | 2pc Justicar applies, cannot crit |
| JoR | 0.429 | Spell crit 1.5×, no Justicar |
| SoC DoT (5 stacks) | 0.17/tick or 0.85 total | 2pc Justicar applies, cannot crit |
| JoC | 0.429 | Spell crit, no Justicar |
| Consecration | 0.125/tick or 1.000 total | 8 ticks, cannot crit |
| Holy Shield | 0.05/block or 0.40 full | ×1.20 from Imp HS |
| Avenger's Shield | 0.193 | Corrected from 0.091 in earlier audit |
| Exorcism / Holy Wrath | 0.429 / 0.286 | Undead/Demon only |
| SoB (proc) | **0** | Pure weapon damage — WoA/Oil do nothing |

### 3. Steady-state TPS contribution

Same rotation (SoR + JoR/10s + Consec/8s + HS/10s), Imp variants assumed for talents:

| Buff | +DPS | +TPS | 5-min threat |
|---|---|---|---|
| Superior Wizard Oil (+42 SP) | ~11 | **~21** | ~6,300 |
| Wrath of Air Totem (+101 SP) | ~26 | **~65** | ~19,500 |
| Imp WoA (+121 SP, 2/2) | ~32 | **~78** | ~23,400 |
| Windfury Totem (Rank 5 base, +445 AP) | ~28 | **~58** | ~17,400 |
| Imp Windfury (+578 AP, 2/2) | ~32 | **~65** | ~19,500 |

**Verdict (single-totem):** Imp WoA wins on TPS because every gain is Holy (1.9× RF multiplier). Imp WF ties on DPS. Wizard Oil is always-worth-it as a self-buff. SoB tanking neutralizes WoA/Oil's spell scaling — swap to Mana Oil + take WF.

### 4. Totem twisting analysis (follow-up question)

**Critical TBC mechanic confirmed:** in TBC 2.4.3, Windfury Totem is a **continuous aura**, not a pulse-and-persist buff like vanilla or WotLK. Replacing WF with WoA ends the WF proc effect immediately — **no overlap window**. Twisting gives strict alternating uptime.

Modeled a 10s/10s twist cycle (50% uptime each):

| Strategy | 60s threat | Verdict |
|---|---|---|
| Imp WoA full uptime (Resto/Ele) | 4,680 | **Best for tank TPS** |
| Imp WoA + base WF twist (Resto) | ~4,070 | −13% vs Imp WoA |
| Base WoA full uptime | ~3,900 | — |
| Imp WF + base WoA twist (Enh) | ~3,890 | Same as Imp WF alone |
| Imp WF full uptime (Enh) | ~3,880 | — |

**Conclusion:** For the Prot Paladin's individual TPS, twisting is a wash or a slight loss compared to running one Imp totem full-time. The benefit of twisting is **for the party as a whole** (melee group gets WF, caster group gets WoA), not for the tank specifically. The tank has no reason to ask for twisting.

### 5. Chart.js visualizations

Cumulative-threat-over-60s line chart with 5 series:
- Imp WoA (+121 SP) — solid blue, smooth slope at 78 TPS
- WoA (+101 SP) — dashed light blue, slope at 65 TPS
- Imp WF — orange stepped line, ~582 threat spikes every ~9s
- Twist (WF + base WoA, 10s/10s) — purple, alternating ramp/step shape
- Wizard Oil — green, slope at 21 TPS

The twist line visibly converges with base WoA by t=60s, demonstrating the "no net gain" point.

---

## Key Takeaways Surfaced

- **Wrath of Air Totem** is the strongest single threat contributor among the three (~65 TPS base, ~78 TPS with 2/2 Imp WoA from a Resto shaman) **because every gain rides Righteous Fury**.
- **Windfury Totem (Imp)** matches Imp WoA on DPS but loses on TPS — half its damage is physical (no RF multiplier).
- **Superior Wizard Oil is universally worth it** (always +21 TPS), except on Seal of Blood rotations where Mana Oil is the better trade.
- **Twisting WF↔WoA in TBC has no overlap window** (unlike WotLK) — strict alternating, no synergy bonus. Net threat for the tank is identical to running one totem full-time.

---

## Files Touched

- **Created:** `buff_comparison_woa_wf_wizoil.html` — standalone 3-buff comparison page, links back to `prot_paladin_rotations.html`.

No edits to the main guide were requested or made.

---

# Session Continuation — Seal Swap, Totem Scaling, Gear Refresh & Sanctity Build Rewrite

**Same date (2026-05-28), later in the session.** All work below is in `soc_vs_sor_timeline.html` and `index.html`.

## Objective (continuation)

Several discrete asks layered on top of the buff comparison work:

1. Add a 5-minute, seals-and-judgements-only TPS timeline comparing three rotations:
   - Pure SoC (`SoC → JSoC → SoC`)
   - Pure SoR (`SoR → JSoR → SoR`)
   - Seal swap (`SoC → JSoC → SoR → SoC → JSoC` — 5s on SoR after each judge, then back to SoC to refresh stacks)
2. Compare WFT vs Wrath of Air scaling against the seal swap, at two SP levels (400, 800), to answer "does either totem scale with gear?"
3. Reshape that comparison into an SP-sweep so divergence is obvious without staring at two charts.
4. Convert the existing "When Does SoC Overtake SoR?" table into a continuous timeline graph (60s cap, annotated crossover points).
5. Pull the current sixtyupgrades stat block into the guide assumptions, then remove Wizard Oil from the assumed baseline.
6. Rewrite the Sanctity Aura build to match the user's actual allocation.
7. Cosmetic: rename the H1 author tag.

## Work Completed

### 1. `soc_vs_sor_timeline.html` — new charts and consistency fixes

#### Seal-only 5-min TPS comparison
- Built a parameterized seal-only discrete-event sim (`runSealSim(strategy)`) covering Pure SoC, Pure SoR, and Seal Swap. Single GCD judge macro modeled (judge + re-seal in one 1.5s GCD). All three start in steady state (5 stacks pre-applied where applicable).
- Plotted as **running-average TPS** over 300s (y-capped at 1000 with 100-step gridlines after a couple of iterations on visibility) and **cumulative threat** over 300s. Both charts: legends sorted by final value, tooltips sorted highest-to-lowest to match the visual stacking.

#### "When Does SoC Overtake SoR?" timeline
- Added below the existing per-stack table; uses the same simulator the table reads from, so the crossover time printed on the chart matches the table's "SoC ahead" row exactly.
- 60-second window (tried 5min → 2min → 60s before crossover visibility was clean). Annotates "5 stacks @ 14.4s" (dashed gray) and both crossovers: Swap > SoR at ~25.1s (purple) and Pure SoC > SoR at ~30s (orange).
- Extended the existing crossover table to include a third column `Cum. Swap`, sourced from `sealSimSwap`. Phase 2 iterates to 35s to capture both crossovers. Row backgrounds highlight the swap and SoC crossovers in their respective colors.

#### Single source of truth for table + chart
- Pulled the discrete-event simulator out of the chart IIFE and into the outer scope (`sealSimSoC`, `sealSimSoR`, `sealSimSwap` arrays). The crossover table now reads cumulative threat from these arrays via `simCumAt(sim, t)`. Previously the table's Phase 2 used a simplified `swapTPS` constant that over-counted SoR proc uptime — it would report a crossover at ~19.7s when the discrete sim showed 25.1s. Now consistent.

#### Totem scaling: WFT vs WoA on the seal swap
- New parameterized seal-swap simulator that takes `sp` and `wfAP`. WoA modeled as the same rotation with SP=baseSP+101, no WF procs. WFT modeled as baseSP with extra-attack-every-9s (physical at boss armor, plus a seal-proc on the extra swing).
- Started as two separate charts (SP=400, SP=800), then combined per user request into one chart with 4 lines: dashed for SP=400, solid for SP=800; orange for WFT, cyan for WoA. Applied a 5-second centered moving-average smoother to remove discrete-event wiggles from WF procs/seal swaps.
- The combined-chart note panel auto-computes WFT's lead at each SP level and the widening factor. With the new gear constants (see below), WFT widens its lead at higher SP because the seal-proc-on-extra-swing scales with SP while WoA's +101 flat contribution doesn't.

#### Seal-rotation scaling vs spell power
- User wanted convergence/divergence between rotations to be visually obvious. Pivoted from time-on-X / dashed-vs-solid to **SP-on-X, TPS-on-Y** parameter sweep:
  - X-axis: SP from 0 to 1200 in steps of 50.
  - 3 lines: Pure SoC, Pure SoR, Seal Swap.
  - Each data point is the steady-state TPS from a 120s simulation, averaged over seconds 60–120 to dodge the early ramp.
- Note panel shows snapshot TPS at SP=0/400/800/1200 plus each rotation's slope in TPS-per-100-SP, so "which scales hardest with gear" is unambiguous.

### 2. Gear assumption refresh from sixtyupgrades

User pasted character-sheet screenshots from `https://sixtyupgrades.com/tbc/set/gG3jNZLAnMr6GEv99ZzyKh`. Updated the gear-assumption tables in `soc_vs_sor_timeline.html`, `prot_paladin_rotations.html`, `index.html`, and `buff_comparison_woa_wf_wizoil.html`:

| Stat | Old | New |
|---|---|---|
| Attack Power | 496 | **436** |
| Spell Damage | 444 | **639** |
| Healing | 444 | **639** |
| Crit Chance | 6.77% | **6.29%** |
| Spell Crit | 6.96% | **7.86%** |
| Armor | 14,172 | **15,139** |
| Defense | 497 | **500** |
| Block Chance | 22.80% | **24.32%** |
| Dodge Chance | 16.41% | **16.47%** |
| Parry Chance | 17.19% | **16.00%** |
| Total Avoidance | 67.28% | **67.79%** |

- **Weapon:** "41 DPS / 1.8s spell-power weapon (e.g. Continuum Blade)" → **Fang of the Leviathan** (41.1 DPS, 1.80 speed, +40 SP, +21 spell crit rating, +221 spell-damage proc).
- **Set bonus:** 2pc Justicar (T4) → **4/5 Justicar**. Added 4pc bonus: *"Increases the damage dealt by your Holy Shield by 15."* Modeled as a flat `JUSTICAR_4P_HS = 15` constant folded into the `HS_BLK` formula (`(155 + SP*0.05 + 15) * RF * 1.20`).

### 3. Remove Wizard Oil from baseline assumptions

User followed up: don't assume Wizard Oil in calculations.

- Raid-buffed SP: 751 (639 + oil 42 + flask 70) → **709** (639 + flask 70 only).
- Oil framed as a "situational comparison only" in the assumption block — it stays in the Buff Contribution Breakdown section as informational, since that section computes the +42 SP delta independently of baseline.
- JS constant `const SP = 751` → `const SP = 709` in both `soc_vs_sor_timeline.html` and `prot_paladin_rotations.html`.
- Also bumped `MC = 0.10 → 0.095` and `SC = 0.10 → 0.11` to reflect the new unbuffed crit values; `WDPS = 41 → 41.1`; `AP_BASE = 496 → 436` (4 occurrences in `soc_vs_sor_timeline.html`, 2 in `prot_paladin_rotations.html`).
- All `simulateAllRotations(751, …)`/`(514, …)` and `simFL(751, …)`/`(514, …)` calls collapsed to 709 (the previous WFT scenarios were already at 514 = 444 + 70 flask, which is now just 709 = 639 + 70). Renamed `scnOil` → `scnNoTotem` since "Scenario 1" is now "Flask only, no totem, no oil" — the bare baseline.
- All scenario headings and chart titles reworded: "Wizard Oil + Flask" → "Flask only (no shaman)".
- Manually recomputed the per-cast example numbers in the Buff Contribution table for WF-extra-swing-seal-proc (was SP=556/751, now 709) and in the standalone WF proc economics formula in `buff_comparison_woa_wf_wizoil.html`.

### 4. Tooltips/legends sorted by visual order

Across the new charts, `tooltip.itemSort: (a, b) => b.parsed.y - a.parsed.y` and dataset arrays `.sort(...)` by final-tick value so the legend's top-to-bottom order matches the lines' top-to-bottom order on the right edge of the chart. Small UX win, called out by the user explicitly.

### 5. `index.html` — Sanctity Aura build rewrite

User confirmed their actual Sanctity build differs from the guide's. New build:

- **Protection (38 points, total unchanged)**: Toughness **4/5** (was 5/5), **Blessing of Kings 1/1** (was 0/1). The 1 point freed from Toughness funds Kings. Combat Expertise stays at 3/5. All other Protection talents unchanged.
- **Retribution (23 points, unchanged)**: Conviction stays at 2/5. (Walked back an earlier wrong assumption I made that the freed point went to Conviction — it didn't.)
- Build code stays **0/38/23**, but its identity changed: was *"No Kings — for raids with another paladin"*, now **"Max Threat Raid, no Ret Paladin in your party"** (the new defining condition is the absence of a Ret paladin overlapping Sanctity Aura, not Kings coverage).
- WoWHead URLs updated to `…-053041305000015232103-052050203003012` (positions 5 and 6 of the Protection string flipped: Toughness 5→4, BoK 0→1).
- **Build comparison table** "Blessing of Kings" row: "No — another paladin must provide Kings" → "Yes (+10% all stats) — funded by Toughness 4/5".
- **Build comparison table** "Best For" row: "Raids with multiple paladins (someone else provides Kings)" → "Raids where no Retribution paladin is in your party (Sanctity Aura doesn't overlap)".
- **"Which build should I use?" tip box** reworked to put Kings in the *shared* core (since both builds now have it) and list the actual Sanctity gains (Sanctity + Improved Sanctity + Improved Judgement 8s CD) on the gain side, with Avenger's Shield itself on the loss side.
- **"Both builds share" survivability summary** updated to remove Toughness from the shared list (now 4/5 in Sanctity vs 5/5 in Avenger's).

### 6. Cosmetic

- `<h1>Tankenheimer's TBC Paladin Tanking Guide</h1>` → `<h1>Lollerskate's TBC Paladin Tanking Guide</h1>` in `index.html`.

---

## Files Touched (continuation)

- **`soc_vs_sor_timeline.html`** — added seal-only 5-min comparison (TPS + cumulative), seal-overtake-SoR timeline, WFT-vs-WoA combined comparison chart, seal-rotation scaling vs SP chart. Extended crossover table with `Cum. Swap` column. Refactored single-source-of-truth simulator. Gear refresh + Wizard Oil baseline removal applied throughout (SP=709, WDPS=41.1, MC=0.095, SC=0.11, AP_BASE=436, +JUSTICAR_4P_HS).
- **`prot_paladin_rotations.html`** — gear refresh + Wizard Oil baseline removal. JS constants (`SP`, `MC`, `SC`, `WDPS`, `AP_BASE`) updated.
- **`buff_comparison_woa_wf_wizoil.html`** — baseline assumption switched to 709 SP / flask-only / Fang of the Leviathan / 4pc Justicar. WF proc economics formula recomputed.
- **`index.html`** — gear table refresh, Sanctity build rewritten (Toughness 4/5 + BoK 1/1), build-comparison table corrections, "Which build should I use?" tip reframed, H1 renamed to Lollerskate's.

## Key Takeaways from This Continuation

- **Seal swap is the dominant pure-seal+judgement strategy** at every SP level tested. Its lead over Pure SoR widens with gear; Pure SoC catches Pure SoR ~5 seconds later than Seal Swap does (~30s vs ~25.1s).
- **WFT scales with gear, WoA doesn't.** WoA's +101 SP is a fixed flat contribution; WFT's extra-swing seal-proc scales linearly with the paladin's SP via the seal coefficient, so WFT's lead over WoA widens noticeably from SP=400 to SP=800.
- The crossover table's old simplified `swapTPS` math over-counted SoR proc uptime by assuming ~100% rather than ~50% of the swap cycle. Replacing it with discrete-event simulation lookups fixed a ~5-second discrepancy with the chart.
- The Sanctity build's *raison d'être* changed: it's no longer "the build you take when another paladin covers Kings", it's "the build you take when no Ret paladin overlaps your Sanctity Aura".
