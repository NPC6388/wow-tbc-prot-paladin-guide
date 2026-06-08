# Session Log — Weekend: Party Buffs, Seal Analysis Integration & Build TPS Chart

**Dates:** 2026-06-06 (Sat) – 2026-06-07 (Sun)
**Project:** TBC Paladin Tanking Guide
**Working Directory:** `C:\Users\matth\Desktop\AI\BiS\wow-tbc`
**Repo:** `wow-tbc-prot-paladin-guide` (live — https://npc6388.github.io/wow-tbc-prot-paladin-guide/)

---

## Objective

A weekend of consolidation and new analysis, in four parts:

1. Build a WoA vs Windfury vs Wizard Oil party-buff comparison, then fold it into the guide as a native section (single source of truth).
2. Integrate the standalone Seal & Judgement threat analysis into the guide and overhaul the rotation / stat-priority / aura sections around it.
3. Add a **Build TPS comparison chart** to the Builds section: Sanctity (0/38/23) vs Avenger's Shield (0/43/18) under one rotation.
4. Fix an incorrect Blessing of Sanctuary description (mana on block).

---

## Work Completed

### 1. Party Buffs: WoA vs Windfury vs Wizard Oil (`34199ee`, `0e1e6ee`)

- Built `buff_comparison_woa_wf_wizoil.html` with the full model and cumulative-threat chart, correcting several TBC mechanics:
  - **Windfury Totem is a temporary weapon imbue** that shares the weapon slot with Wizard Oil — applying oil overwrites the WF buff. **Winds of Aggravation (WoA) is a stat aura that stacks with oil.** So the real choice is **WoA + Oil (~99 TPS)** vs **Windfury alone (~65 TPS)**.
  - **Totem twisting** is viable throughout TBC (the WF buff persists through the swap; only killed in WotLK 3.0) and stacks both air effects (~122 TPS).
  - **Wizard Oil always beats Mana Oil** for a threat tank; **SoB is a pull-only judge**, not a sustained seal (so the sustained comparison always runs under SoR).
- Then **inlined the whole analysis into `index.html`** as a native `#party-buffs` section (per-ability tables, combining-buffs package table, totem twisting, head-to-head, verdict, cumulative chart) using the guide's own styling; added the supporting CSS classes; replaced the external TOC sub-link with an in-page entry; and **deleted the standalone page** so there's one source of truth.

### 2. Seal & Judgement Threat Analysis integration + overhaul (`f6faf73`)

- **Inlined the seals analysis** (openers, SoC→SoR swap, JotC self vs Ret-supplied, JoW timing, interactive charts) as a native guide section, and **removed the two standalone pages it replaced** (`prot_paladin_rotations.html`, `soc_vs_sor_timeline.html`).
- **Seal TPS combined chart** now shows active + judged threat per seal on a shared y-axis. Key takeaways: **SoC single-target, SoR for AOE / sub-30s fights, SoB pull-only; drop Seal of Command.**
- **JoC scales per Blood Corruption stack** (0 at 0 stacks); only SoB/SoR apply meaningful first-judgement threat.
- **Reworked Stat Priorities** (uncrittable > avoidance > stamina/SP) and the AOE / boss-threat / boss-mitigation priority lists; removed the SP-vs-AP scaling section and the EH-by-tier table.
- Boss rotation now defers to the analysis section; removed SoB-beyond-opener and the Spiritual Attunement synergy note; clarified LoH does not cause Forbearance.
- **Auras are party-wide, not raid-wide**; documented 2/2 Improved Sanctity Aura; fixed low-contrast links on colored cards; updated the worked example to the 709-SP reference profile.

### 3. Build TPS comparison chart (`17ea7f8`)

Added a cumulative-threat line chart at the end of the Builds section (`#build-tps`, plus a TOC entry) comparing the two specs under **one identical rotation — SoB + Ret JotC @ 1s** — on the guide's reference gear. It went through a few iterations on request (TPS bars → a 2×2 grouped bar with a solo scenario → a single-rotation line chart → the final **5-minute** line chart).

**Final chart:** cumulative threat over a full 5-minute fight.
- **Sanctity (0/38/23):** ~428,300 threat (~1,428 avg TPS).
- **Avenger's Shield (0/43/18):** ~402,900 threat (~1,343 avg TPS).
- Sanctity leads by **~+25,400 threat (+6.3%)**, with the **durable crossover called out at ~13s** (dashed marker on the chart + in the note). Avenger's leads only at the very start off its on-pull Avenger's Shield hit.

**Model:** reuses the guide's existing `simulate()` engine (the same one behind the "SoB + Ret JotC @ 1s" opener line). The only inputs that differ are the talent deltas:
- **Avenger's:** ×1.08 (4/5 1H Weapon Spec), 94% melee land (5 Expertise), **casts Avenger's Shield** (pull + 30s recast).
- **Sanctity:** ×1.06 (3/5 Spec) × 1.10 (Sanctity Aura, +10% Holy) × 1.02 (2/2 Imp. Sanctity, +2% all) = ×1.189 on every term; 93.5% melee land (3 Expertise, +0.5% boss dodge); **no Avenger's Shield**.
- **Assumption:** the Ret paladin supplying JotC is in a *different* party, so only the Sanctity build brings the aura to your own group — the scenario where you'd actually run it.

**Engine changes (all backward-compatible — every existing chart verified unchanged):**
- `simulate()` gained optional cfg params: `dmgMul`, `meleeLand`, `hasAS`, and `dur` (all default to prior behavior).
- Added an **Avenger's Shield 30s recast timer** (gated by `hasAS`, first recast at 30s) so the Avenger's build is modeled fairly over long fights — previously the sim only fired the one pull cast, which would have understated it over 5 minutes.

> An interim version also modeled a **solo "only paladin" scenario** (self-applied JotC via the SoB→JotC hybrid, with the Sanctity build's 2/3 Improved Seal of the Crusader giving a stronger debuff + 2% boss crit). That was dropped when the chart was narrowed to one rotation; the supporting `bossCritBonus`/`jotcDebuff` parameters were reverted so no dead code was left in the engine.

### 4. Blessing of Sanctuary mana-on-block fix (`17ea7f8`)

User caught that the guide described Blessing of Sanctuary as giving **mana on block** — incorrect for TBC. Per the in-game tooltip, BoSanc (R5) provides **flat damage reduction (−80/hit)** and **46 Holy damage to the attacker on block** (a threat source, ×1.9 RF) — the mana-on-avoidance component is a **WotLK** addition. Corrected in **four places**: the blessing comparison chart tooltip, the "#1 tank blessing" bullet, and both build talent tables. (The two reference/citation tables were already correct.)

---

## Key Takeaways

- **Single source of truth:** the weekend's theme was folding standalone analysis pages (party buffs, seals, rotations, SoC/SoR timeline) into `index.html` as native sections and deleting the originals, so nothing can drift out of sync.
- **Sanctity (0/38/23) beats Avenger's (0/43/18) on sustained single-target threat** (~+6% over a 5-min fight) *when no Ret paladin is in your party*: Sanctity Aura's +10% Holy and Imp. Sanctity's +2% all damage apply to every threat source (all paladin threat is Holy) and compound for the whole fight, outweighing the lower Weapon Spec, 2 fewer Expertise, and the lost Avenger's Shield. Avenger's keeps its edge in **utility** (ranged pull, daze, AOE), not TPS.
- **Model fairness matters with the window length:** extending the comparison to 5 minutes required modeling the Avenger's Shield 30s recast — a detail that's invisible in a 20s window but ~9 extra casts over a real fight.
- **Blessing of Sanctuary has no mana return in TBC** — that mechanic arrived in WotLK.

---

## Files Touched

- **`index.html`** — `#party-buffs` section (inlined) + CSS classes; `#seal-threat-analysis` section + rotation/stat/aura overhaul; `#build-tps` Build TPS chart + TOC entry + `simulate()` engine params and AS recast; Blessing of Sanctuary corrections.
- **Deleted** — `buff_comparison_woa_wf_wizoil.html`, `prot_paladin_rotations.html`, `soc_vs_sor_timeline.html` (all inlined into `index.html`).

### Commits this weekend
- `34199ee` (Sat) — Add WoA vs Windfury vs Wizard Oil buff comparison; wire into guide
- `0e1e6ee` (Sat) — Inline the Party Buffs comparison into the guide; remove standalone page
- `f6faf73` (Sun) — Integrate Seal & Judgement Threat Analysis; rotation/stat/aura overhaul
- `17ea7f8` (Sun) — Add 5-min Build TPS comparison chart; fix BoSanc mana error

---

## Not Committed / Left As-Is

- `04318 prot talents.txt` — modified in the working tree before this weekend's chart work; left untouched.
- Untracked screenshots, `changes for full guide.txt`, and `.claude/` — left untracked.
