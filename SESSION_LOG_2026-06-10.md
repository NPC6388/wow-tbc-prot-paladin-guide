# Session Log — Seal of Righteousness SP Coefficient Correction

**Date:** 2026-06-10 (Wed)
**Project:** TBC Paladin Tanking Guide
**Working Directory:** `C:\Users\matth\Desktop\AI\BiS\wow-tbc`
**Repo:** `wow-tbc-prot-paladin-guide` (live — https://npc6388.github.io/wow-tbc-prot-paladin-guide/)

---

## Objective

Finish propagating the corrected **Seal of Righteousness (SoR) spell-power coefficient** through every chart and every piece of text whose results depend on it.

---

## When the error was discovered

The SoR coefficient bug was **discovered during the 2026-06-09 fresh editorial read-through** of `index.html`. That pass flagged it as the **top internal contradiction**: the ability table, coefficient appendix, and verification note had already been corrected to **0.092 × weapon speed (≈0.166 at 1.8s)** — explicitly noting the old flat **0.2 "over-estimates SoR threat by ≈20%"** — but the **live chart engine still used `SOR_COEFF = 0.2`** (base 44.2), and the Wrath-of-Air / Windfury / Wizard Oil contribution math was still built on 0.2 as well. So the prose disavowed 0.2 while every seal chart and buff table was still computed from it.

The correction was acted on today (2026-06-10).

---

## Work Completed

### 1. Fixed the authoritative chart engine
- `SOR_COEFF = 0.2` → **`0.092 * WS`** (= 0.1656 at the guide's 1.8s weapon), with an updated comment explaining the weapon-speed scaling and the ~20% over-estimate of the old value.
- The second 5-minute SP-sweep function (`steadyStateTPS`) had a hardcoded `(44.2 + sp * 0.20)` → **`(44.2 + sp * 0.092 * _WS)`**.
- Everything downstream of the engine now recomputes automatically: the seal-crossover per-stack table, the cumulative-threat catch-up chart, the seal-swap TPS displays, the opener-comparison table, and both 5-minute SP-sweep charts.

### 2. Fixed the static buff-contribution math (was half-propagated)
The Windfury side had already been moved to the corrected value (WF ~65/58, `WF_PROC` ≈ 582 ≈ 585), but the **Wrath of Air numbers and the formula/derivation blocks were still on 0.2**. Brought everything into agreement:
- **WF per-proc formula block:** SoR proc `44.2 + 709×0.20 = 186.2` → `44.2 + 709×0.166 = 161.6`; `~389 threat` → `~338`; total `~636` → `~585`; `~71 TPS` → `~65`.
- **WF per-proc table:** base `~68 TPS` → `~63`, Imp `~71 TPS` → `~65`.
- **Wizard Oil per-ability table** (SoR row): coefficient `0.20` → `0.166`; `+9.2 dmg / +17.6 threat` → `+7.6 / +14.5`.
- **WoA per-ability table** (SoR row): coefficient `0.20` → `0.166`; `+22.2 dmg / +42.2 threat` → `+18.4 / +35.0`.
- **WoA contribution tip:** SoR `42.2 threat → +23.5 TPS` → `35.0 → +19.5`; total WoA (101 SP) `~71` → `~67`; Imp WoA (121 SP) `~85` → `~81`; 5-min totals `~21,300 / ~25,500` → `~20,100 / ~24,300`.

### 3. Propagated the WoA cascade through every comparison
- **Package table:** WoA+Oil (Imp) `~85+~23=~108` → `~81+~23=~104`; base `~71+~23=~94` → `~67+~23=~90`.
- **Head-to-head summary:** WoA `~71/~21,300` → `~67/~20,100`; Imp WoA `~85/~25,500` → `~81/~24,300`.
- **Totem twisting:** WoA leg `~88%×71=~63` → `~88%×67=~59`; combined twist `~128 TPS / ~7,700` → `~124 / ~7,440`; the comparison rows (108→104, 94→90, 85→81 and their 60s totals); every `~128 TPS` twist mention → `~124`.
- **Verdicts / decision trees / one-line bottom line:** every `~108`/`~85`/`~43-swing`/`~128` reference updated to `~104`/`~81`/`~39`/`~124`.
- **Cumulative-buff chart JS constants:** `WOA_TPS 71→67`, `IMPWOA_TPS 85→81`, `WOAOIL_TPS 108→104`, `WOAOIL_BASE_TPS 94→90`, `TWIST_WOA_TPS 71→67`.

---

---

# Part 2 — Consistency reconcile (same day)

After the coefficient propagation, the user asked to address the two pre-existing inconsistencies I'd flagged. Both fixed.

### 4. Top-3 seal charts + per-ability table reconciled to the engine

The three overview charts (Active / Judged / Combined) and the per-ability threat table were independent hand-estimate sets that **omitted the 2pc Justicar +10%** (on seal procs / SoC DoT) and the **average spell-crit** the engine applies to judgements — so they ran ~7–10% below the verified engine, and the analysis-section combined-SoR (333) didn't match the chart (318).

Confirmed with the user that **judgements do crit in TBC** (JoR 1.5×, JoB 2×, JoC 1.5× — only the SoR proc and SoC/SoV DoT can't), so the crit-averaged engine values are the correct ones. Brought both presentations up to the engine:
- **Charts:** SoR 188, SoC DoT 188, JoC 182, JoR 145, JoB 128; combined **Pure SoR 333, Pure SoC 370, Seal-swap 558** (y-axis max 550→600). Tooltips + key-takeaways updated.
- **Per-ability table:** the table's own footnote already promised "639–709 SP, crit included," but the rows were on an older ~490–557 SP basis without crit/set-bonuses. Recomputed every row to that basis against the engine: Consec 273–290, Holy Shield 173–176 (incl. 4pc Justicar + Imp HS), Avenger's Shield 1,276–1,301, JoB 118–128, SoR 174–188, JoR 133–145, SoC DoT 180–188, JoC 174–182, Exorcism 118–123, Holy Wrath 1,615–1,679. Also fixed the talents-section Holy Shield reference (126–130 → 173–176) to match.
- **Worked example ("Threat Example: 709 SP")** converted to the same universal math (was base per-cast formulas): Holy Shield 362 → **468** (4pc + Imp HS), JoB 1,168 → **1,279** (avg melee crit), JoR 1,376 → **1,452** (avg spell crit); Consec (2,320) and Avenger's Shield (1,301) unchanged since neither is crit-averaged in the engine. Each now divides cleanly into its table TPS (JoR 1,452/10 = 145, HS 468×3/8 = 176, JoB 1,279/10 = 128).

### 5. Buff section put on one consistent model

- **Wizard Oil ~23 → ~28 TPS.** WoA is 67 TPS at +101 SP (0.667 TPS/SP); Oil's +42 SP must scale to ~28, not 23. (5-min 6,900 → 8,400.)
- **Base Windfury ~58 → ~63 TPS.** Its own per-proc model gives (226 physical + 338 SoR)/9s = 62.7. (5-min 17,400 → 18,900.)
- **DPS column corrected** to match the TPS (it had undercounted): WoA ~26→35, Imp WoA ~32→42, Oil ~11→15, base WF ~28→33, Imp WF ~32→34. Reworded the "WoA and WF nearly identical on DPS" caveat — they're close on raw DPS (~33–35) but WoA's TPS lead comes from all of it being RF-amplified Holy.
- **Knock-on:** the Oil fix lifts WoA + Oil from ~104 to **~109 TPS** (Imp) / ~95 (base); swing over Windfury ~39 → ~44. Re-cascaded through the package table, head-to-head summary, twist comparison, verdicts, one-line bottom line, and the cumulative-buff chart JS constants.

### 6. Avenger's Shield crit correction

On review, the user challenged my claim that AS "cannot crit." Verified: **Avenger's Shield is a direct-damage Holy nuke and does crit (spell crit, 1.5×)** — no "cannot crit" flag on its Wowhead TBC entry, and the guide's own Conviction-vs-ImpSotC section (L2636) already treats AS as a spell-crit-benefiting ability (it lists Consecration/Holy Shield/SoR proc/SoC DoT as the things that *can't* crit, and notes "Sanctity has no Avenger's Shield"). The chart engine had wrongly modelled AS without crit.

Fixed: added `× (1 + SC*0.5)` to the engine `AS` constant (per-cast **1,301 → 1,373** at 709 SP), updated the ability-table range (1,276–1,301 → **1,326–1,373**, note now says "crits 1.5× (spell)"), and the worked example (1,301 → **1,373**). The AS-build TPS and cumulative charts recompute from the constant. Consecration and Holy Shield genuinely can't crit and were left alone (the web sources confirm Consec specifically cannot crit).

All folded into the **v1.9** changelog entry.

---

---

# Part 3 — Moved unverified sections to a holding file (v2.0)

At the user's request, stripped not-yet-verified sections out of the live guide into a new standalone file **`review prior to inclusion.html`** (shares the guide's `<head>`/CSS so it renders), pending review before re-inclusion. Moved: **Engineering, Weapon/Shield/Libram selection, Enchantments, Gems & Professions, Essential Macros, WeakAuras, Addons, Simulators & Tools, Crit & Crush Immunity Calculator.** Gear Optimization keeps its AOE/Boss/Mitigation/Off-Tank gear-set guidance (only weapon/shield/libram subsections moved). All moved content is static HTML (no charts/scripts cross the boundary), so the engine and all charts are untouched. TOC trimmed; no body cross-links pointed into the moved sections. Changelog **v2.0** added.

---

## Files Touched

- **`index.html`** — Part 1: engine `SOR_COEFF` + sweep function; WF/Oil/WoA per-ability tables and formula blocks; WoA/twist/package cascade; cumulative-buff chart constants. Part 2: three seal-comparison charts + tooltips + key-takeaways; full per-ability threat table; talents-section HS reference; buff-section Oil/base-WF/DPS reconcile + re-cascade; **v1.9** changelog entry.
- **`SESSION_LOG_2026-06-10.md`** — this log.
