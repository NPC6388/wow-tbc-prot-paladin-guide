# Session Log — JoR Coefficient Fix, SoR Opener Flip & Talent Theory

**Dates:** 2026-06-08 (Mon) – 2026-06-09 (Tue)
**Project:** TBC Paladin Tanking Guide
**Working Directory:** `C:\Users\matth\Desktop\AI\BiS\wow-tbc`
**Repo:** `wow-tbc-prot-paladin-guide` (live — https://npc6388.github.io/wow-tbc-prot-paladin-guide/)

---

## Objective

Recheck the Judgement of Righteousness scaling math, fix what it breaks, and build out talent theory — ending with a self-contained guide (no talent link-outs).

---

## Work Completed

### 1. JoR coefficient corrected to 0.728 (`75a025b`)

The trigger: a request to recheck how **Judgement of Blood (JoB)** scales vs **Judgement of Righteousness (JoR)** with spell power.

- Found the guide's JS used **base 162 (rank 7) + SP coefficient 0.429** for JoR, while its own data appendix cited the correct **base 208 (rank 9) + 0.728** (Wowhead TBC `spell=27157`). The generic 0.429 is the cast-time coefficient most judgements share (JoB, JoC, JoV, Exorcism, HoW); JoR uniquely has the higher **0.728**.
- **Crossover:** with 0.728, **JoR out-scales JoB above ~400 SP**. At the guide's 709-SP raid profile JoR is the bigger judgement (~145 vs ~128 TPS) and the bigger snap — the opposite of what the guide claimed.
- Propagated 0.728 / base 208 through **every JS calculator, the static seal charts, and the WoA / Wizard Oil contribution tables**; recomputed every dependent figure (WoA ~65→71 TPS, Imp WoA ~78→85, Oil ~21→23, WoA+Oil ~99→108, twist ~122→128, all 5-min/60s totals and the buff-threat chart slopes).

### 2. SoC DoT verification — *no* bug (`75a025b`)

Mid-task I suspected the Seal of Corruption DoT was overcounted (~188 vs an apparent ~119 TPS). On the user's instruction to **verify first**, cross-checked WoWWiki Blood Corruption: base **30/tick/stack (= 10 DPS/stack), +17% SP per tick at 5 stacks**, ticks every 3s. That reconciles to **188 TPS at 709 SP / 5 stacks** — the sim's `10 + SP*0.034/3` is **correct** (the "10" is DPS, not per-tick). My ~119 was a misread; the crossover chart stands. Good call to check.

### 3. Ability table + crossover chart (`75a025b`)

- Added **Seal of Corruption DoT (180–188 TPS @ 5 stk)**, **Judgement of Corruption (167–173 @ 5 stk)**, and **Judgement of Righteousness (128–138)** rows to the Paladin Ability Threat Values table; the 709-SP threat example now lists JoR (1,376) above JoB (1,168). Tidied the appendix's misleading "base 10 per tick" wording.
- Extended the **"When does SoC overtake SoR?" cumulative chart from 60s → 240s**: with the higher JoR, the pure-SoC crossover moved from ~40s out to **~182s** (seal-swap crossover ~50s). Verified the new crossover by replicating the sim in Node.

### 4. Stat-priority list expanded (`75a025b`)

Fleshed out the top-level 3-step priority (uncrittable → avoidance → stamina/SP): the Defense 490/485 thresholds and five-benefits-per-point edge, Block vs Dodge/Parry vs Agility, and the throughput-vs-survival framing for the Stamina/SP knob.

### 5. Opener flipped: SoB→JoB ⟶ SoR→JoR (`75a025b`)

Since JoR out-snaps JoB at raid SP, the **pull opener is now Seal of Righteousness → Judge Righteousness** throughout the guide, with **SoB→JoB kept as the sub-~400 SP (leveling) opener**. Added a `sorSnap` mode to the `simulate()` engine (JoR snap → re-seal SoC), repointed the recommended-hybrid and Ret-JotC sims and the build-TPS sims, relabeled the cumulative-threat charts ("SoR → JotC (recommended)", "SoB Opener (low-gear)"), and updated ~20 prose spots (Horde-opener section, rotation steps, pre-pull sequence, macros, opener-comparison table/verdict, WoA verdict). Also changed the mana-cost line "Seal of Blood: 210" → "Seal: 210".

### 6. Improved SotC corrected — purely a crit debuff (`ac2b245`)

The guide claimed 2/3 Imp SotC "strengthens the JotC Holy-damage debuff." That's a vanilla-ism; in **TBC 2.3+ the damage bonus was folded into the base spell**, so Imp SotC is **only** the +1/2/3% crit-to-be-hit debuff (all attacks, melee + spell) and the **+219 debuff is identical at any rank** (Warcraft Wiki). Fixed in four places.

### 7. Sanctity build retuned to max threat (`104a2c4`)

Applied the two talent trade-off findings to the live Sanctity build (still **0/38/23**): **1H Weapon Spec 3/5 → 5/5** and **Improved SotC 2/3 → 3/3**, funded by **Combat Expertise 3/5 → 1/5** and **Conviction 2/5 → 1/5**. Combat Expertise is **~0 threat** (a survivability talent); Imp SotC's spell crit feeds the judgements where Conviction's melee crit doesn't. Updated talent tables, both calculator links, comparison rows, the build-TPS sim (`dmgMul` 1.06→1.10, melee land 0.935→0.930), the JS build comment, and the mandatory-talents note. Changelog v1.7.

### 8. Talent theory: rated tables + 3 specs, inlined (`104a2c4`)

Built a **Threat vs Survivability Talents** mini-guide and **inlined it as a native section** (`#threat-vs-survivability-talents`):
- Every threat and every survivability talent **rated ★–★★★★★**, plus the **non-negotiable tanking core** (uncrit/uncrush + the 1.9× engine).
- Three ready-to-apply specs with **full point-by-point sheets** and **verified one-click calculator links**:
  - **Max Threat 0/38/23** — `…/-053041305000015252101-050350103003012`
  - **Balanced 0/43/18** — `…/-0530513050000152421051-050050203003`
  - **Max Survival 0/48/13** — `…/-0530513350002102421551-050050003`
- The talent-calc strings were **decoded from the guide's two validated build links** and sum-checked to 61. (The user supplied a screenshot to pin **Spell Warding to Protection slot 13**, fixing the Max-Survival string.)
- A relative threat/survivability index chart.

### 9. Trade-off analysis inlined as a collapsed box (`7f1799a`)

Folded the per-point math (**Conviction vs Improved SotC**, **1H Weapon Spec vs Combat Expertise**) into a **collapsed-by-default `<details>` box** at the end of the Builds section (`#talent-tradeoffs`), with both interactive calculations (computed from the guide's coefficients) and both charts ported inline. The box **auto-opens** when navigated to via its anchor. Repointed every in-guide "(why)/(math)" link to it.

---

## Key Takeaways

- **JoR's coefficient is 0.728, not the generic 0.429** — it's the one judgement that scales harder. This single number flips the opener (SoR→JoR over SoB→JoB above ~400 SP) and makes the SoC-vs-SoR cumulative crossover much later (~182s).
- **Combat Expertise is a survivability talent, not a threat one** (~0 TPS in the sim — almost nothing a prot paladin does is dodgeable). 1H Weapon Spec is ~+27 TPS/rank. So for threat, max Spec before Expertise.
- **Conviction (melee-only) < Improved SotC (all attacks) for a prot paladin**, because the judgements crit off *spell* crit.
- **Verify before "fixing":** the SoC DoT "bug" wasn't one — pausing to cross-check WoWWiki saved a wrong propagation that would have erased the SoC>SoR crossover.
- **Single source of truth again:** both standalone analysis pages were inlined and deleted, leaving the guide self-contained with no talent link-outs.

---

## Files Touched

- **`index.html`** — JoR 0.728 propagation; SoC/JoC/JoR ability-table rows; 240s crossover chart; stat-priority expansion; SoR→JoR opener (`sorSnap` sim mode) guide-wide; Imp SotC correction; Sanctity build retuned to max threat; inlined `#threat-vs-survivability-talents` section; inlined `#talent-tradeoffs` collapsed box; TOC + callout wiring.
- **Created then deleted** (inlined into `index.html`) — `talent_threat_vs_survivability.html`, `sanctity_conviction_vs_impsotc.html`.

### Commits this session
- `75a025b` — Fix JoR coefficient to 0.728; flip opener to SoR; add talent deep-dive pages
- `ac2b245` — Correct Improved SotC: TBC 2.3+ is purely the crit debuff, not a debuff buff
- `104a2c4` — Tune Sanctity build to max threat; inline the talent threat/survivability mini-guide
- `7f1799a` — Inline the Conviction/ImpSotC & 1HWS/CE trade-off page as a collapsed box

---

## Not Committed / Left As-Is

- `04318 prot talents.txt` — pre-existing working-tree modification; left untouched.
- Untracked screenshots, `changes for full guide.txt`, and `.claude/` — left untracked.
