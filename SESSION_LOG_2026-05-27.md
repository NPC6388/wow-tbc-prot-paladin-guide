# Session Log — Combat Expertise vs Improved Sanctity Aura

**Date:** 2026-05-27
**Project:** TBC Paladin Tanking Guide
**Working Directory:** `C:\Users\matth\Desktop\AI\BiS\wow-tbc`
**File touched:** `index.html` (the core guide)

---

## Objective

Answer a theorycrafting question, then turn it into guide content:

> What is the net effect of **5/5 Combat Expertise + Sanctity Aura** vs **3/5 Combat Expertise + 2/2 Improved Sanctity Aura** in a raid?

Then: produce a standalone review page → merge it into the guide → change the guide's Sanctity build to adopt the 3/5 CE + 2/2 Improved Sanctity Aura allocation.

---

## Work Completed

### 1. Reviewed existing expertise content in the guide

- Stat tables already correct: Expertise Rating 3.9423/pt, soft cap 26 (eliminates 6.5% boss dodge), ~0.8–1.2 TPS/pt.
- Both build tables listed **Combat Expertise 5/5 = "+10 expertise, +10% stamina"** and flagged it "Never Drop."
- **Improved Sanctity Aura was not mentioned anywhere.**

### 2. Verified the mechanics (web research)

- **Combat Expertise** = **+1 Expertise, +2% Stamina per rank** → 5/5 = **+5 Expertise, +10% Stamina** (no crit). The guide's "+10 expertise" was **wrong**. Corroborated by the guide's own reference profile showing Expertise = 5 with no expertise gear.
- **Sanctity Aura** carries two effects: +10% Holy (Effect #1) and a dormant all-schools modifier (Effect #2).
- **Improved Sanctity Aura** fills Effect #2: **+1% per rank → 2/2 = +2% to ALL damage** (physical + every magic school) for the party.
- **TBC auras are party-only** (5-person group, 30 yd / 40 with Aura Mastery), **not raid-wide**.

### 3. The analysis (the answer)

Trade for Option B (3/5 CE + 2/2 Imp. Sanctity), both keep Sanctity Aura 1/1:
- **Lose:** 2 Expertise (+0.5% boss dodge & parry — trivial threat loss) and 4% Stamina (~350–500 HP at T4/T5).
- **Gain:** +2% to all damage for up to 4 partymates **and** +2% to your own threat.

**Verdict:** Option B wins for raid throughput — own threat slightly up (the +2% self all-damage beats the dodge loss), party DPS clearly up, survivability slightly down. Keep 5/5 CE only on punishing progression hits or when your party has no DPS to benefit.

### 4. Built standalone review page → merged into guide

- Created `expertise_vs_sanctity_analysis.html` (guide's CSS), user approved, then **deleted** it.
- Merged as a new `<h2>` section **"Combat Expertise vs Improved Sanctity Aura"** (anchor `#expertise-vs-sanctity`) after Build Comparison, with TOC entry.
- Applied the **"+10 → +5 expertise"** correction in both build tables and softened the Mandatory Talents box.

### 5. Critical verification detour (talent-tree feasibility)

The standard Sanctity tank build is rigidly 0/40/21, which raised a real concern: if **Improved Sanctity Aura were a deeper (25-point) talent**, the requested 0/38/23 swap would be **impossible**. Web sources conflicted, so I verified against hard data:

- Decoded real WoWHead talent-calc strings (Protection & Retribution) by position.
- Cross-referenced **WoWSims TBC talent data** (`github.com/wowsims/tbc/.../talents/paladin.ts`), which encodes `rowIdx`/`colIdx`/`prereqLocation` per talent.

**Confirmed:** Improved Sanctity Aura is **rowIdx 4 (tier 5, 20 points), colIdx 3 — same row as Sanctity Aura (col 2), with Sanctity Aura as its prerequisite.** So the 2-point swap to **0/38/23 is legal.** Original analysis stood; the "always 0/40/21" was convention, not a constraint.

### 6. Changed the guide's Sanctity build to 0/38/23

Verified new talent string (CE at Prot position 21; Imp. Sanctity appended at Ret position 15):
`-053050305000015232103-052050203003012`  (Prot sum 38, Ret sum 23)

Updated everywhere: TOC, section header, build card + description, **both** WoWHead links, Protection table (38 pts, CE 3/5), Retribution table (23 pts, new Improved Sanctity Aura 2/2 row), Build Comparison (header, Party Aura row, Raid Utility row, shared-core bullet), Mandatory Talents box, analysis-section intro, 3 stray `0/40/21` mentions, and a new **v1.4 changelog** entry.

**Avenger's Shield build left untouched** (still 0/43/18, CE 5/5).

---

## Key Findings / Corrections

| Item | Before | After (verified) |
|---|---|---|
| Combat Expertise 5/5 | +10 expertise | **+5 expertise**, +10% stamina (+1/+2% per rank) |
| Improved Sanctity Aura 2/2 | (absent) | **+2% all damage** to party (party-only, 30 yd) |
| Imp. Sanctity tree position | unknown | **Ret tier 5 (20 pts), row 4 col 3**, prereq Sanctity Aura |
| Sanctity build | 0/40/21 | **0/38/23** |

---

## State / Next Steps

- **Not committed.** All changes are working-tree edits to `index.html`. On `main` — branch before committing.
- Standalone analysis file deleted (content lives in the guide).
- Possible follow-up: Pursuit of Justice is listed 3/3 in the guide — WoWSims data shows it as a 3-rank talent so this is fine, but worth a glance if doing a broader talent-value audit.
