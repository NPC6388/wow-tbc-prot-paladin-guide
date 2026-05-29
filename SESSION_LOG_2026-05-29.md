# Session Log — Sanctity Build Respec, Repo Consolidation & Defense Fix

**Date:** 2026-05-29
**Project:** TBC Paladin Tanking Guide
**Working Directory:** `C:\Users\matth\Desktop\AI\BiS\wow-tbc`
**Repos touched:** `wow-tbc-prot-paladin-guide` (live), `wow-classic-warrior-tank-guide`

---

## Objective

A sequence of asks across the session:

1. Change the Sanctity build in the paladin guide to a new allocation (rename + talent swap to Improved Seal of the Crusader over Improved Judgement).
2. Figure out why the change wasn't showing on the live GitHub Pages site.
3. Determine which of two divergent copies of the guide was the most accurate, and get the accurate one live.
4. Consolidate the paladin guide so it isn't duplicated across two repos.
5. Remove a second, stale copy of the *warrior* guide.
6. Correct the heroic-only defense floor from 465 to 485 (level 72 crit immunity).

---

## Work Completed

### 1. Sanctity build respec (`index.html`)

User's new allocation (still **0/38/23**, Protection tree unchanged):

- **Retribution swap:** dropped **2/2 Improved Judgement**, added **2/3 Improved Seal of the Crusader**.
- **Rationale (user's):** Improved Judgement's 8s Judgement cooldown desyncs the steady-state 969 cadence. Improved Seal of the Crusader instead gives a raid-wide **+2% chance for the boss to be critically hit** (verified via Warcraft Tavern / WoWWiki — +1% crit-to-be-hit per rank vs the judged target) plus a stronger Judgement of the Crusader Holy-damage debuff, without disturbing the rotation.
- **Rename:** "Sanctity Aura Build" → **"Sanctity Build (Max Threat Raid without Ret Paladin in your party)"** (h3, h4, and TOC).
- **Talent calc link:** Ret string `052050203003012` → `050250203003012` (positions 3 and 4 flipped: Imp Judgement 2→0, Imp Seal of Crusader 0→2). Verified the swap is point-legal and the totals stay 38/23.
- **Downstream edits:** Ret talent table row, build-comparison table (Judgement CD now 10s for both builds; added a "Boss Crit Debuff" row), build-choice tips, and the boss-rotation Judgement cooldown note ("10 sec (8 with talent)" → "10 sec", since neither recommended build now takes Imp Judgement). New v1.5 changelog entry.

### 2. Diagnosing the "not live" problem

The edit was correct but invisible on the live site because of repo confusion:

- **Git root** is `BiS/` (= `wow-classic-warrior-tank-guide`), and its Pages serves the *warrior* guide from `BiS/index.html`.
- The paladin guide I edited lived at `BiS/wow-tbc/index.html` — a file that had been **added then reverted** off the warrior repo, so it wasn't deployed anywhere.
- The **live** paladin guide is a separate repo, `wow-tbc-prot-paladin-guide` (https://npc6388.github.io/wow-tbc-prot-paladin-guide/), cloned locally at `BiS/wow-tbc/wow-tbc-repo-temp/`.

### 3. Which copy is more accurate?

The two copies had **diverged** — each had a different "v1.4":

- Working copy (`wow-tbc/index.html`): v1.4 = Combat Expertise vs Improved Sanctity Aura; Sanctity **0/38/23**.
- Live copy (`wow-tbc-repo-temp/index.html`): v1.4 = Spell Power Coefficient Accuracy Pass; Sanctity **0/40/21**.

Compared the actual theorycrafting content (not just changelog labels). **The working copy is the strict superset:** it already contains the live copy's coefficient work (same 0.429 / 1.000 values, the 0.166 SotC per-swing coeff, JoB self-damage detail) **and adds** a full Sources & Citations section, 2pc/4pc Justicar modeling, a realistic 709-SP reference profile, the seal-swap combined-TPS analysis, and the Combat Expertise section. Conclusion: publishing the working copy loses nothing.

### 4. Publishing + repo consolidation

- Copied the working `index.html` over the live repo's copy, committed, pushed → Sanctity change went live.
- **Undid** the unpushed warrior-repo commit that had re-added `wow-tbc/index.html` (kept files on disk), so the paladin guide is no longer tracked in the warrior repo.
- Verified all shared files between the loose `wow-tbc/` dir and the clone were **content-identical** (only CRLF differences) — no divergence to reconcile beyond `index.html`.
- **Published the unique loose files** the clone didn't have: `prot_paladin_rotations.html`, `soc_vs_sor_timeline.html`, `buff_comparison_woa_wf_wizoil.html`, `research_professions.md`, `SESSION_LOG_2026-05-27.md`, `SESSION_LOG_2026-05-28.md`, `04318 prot talents.txt`, plus the pending `SESSION_LOG.md` update (committed + pushed to the paladin repo).
- **Relocated the checkout in place:** moved the clone's `.git` up into `BiS/wow-tbc/`, preserved the screenshot and `.claude/` (untracked), removed the redundant `wow-tbc-repo-temp/` dir, and normalized the working tree. `BiS/wow-tbc/` **is now the single `wow-tbc-prot-paladin-guide` checkout** (had to transform in place rather than rename, because the shell's working directory pins `wow-tbc/`).
- Added `wow-tbc/` to the warrior repo's `.gitignore` and **pushed it** so the paladin guide can never be re-absorbed into the warrior repo.

### 5. Removed the stale warrior-guide clone

`BiS/Future Work/wow-classic-warrior-tank-guide/` was a second full clone of the warrior repo — **6 commits behind, no uncommitted/unpushed work** (everything already on the remote). Confirmed safe and deleted it. The other `Future Work/` files (tankenheimer guide, trinket comparison, etc.) were left untouched.

### 6. Defense floor fix (`index.html`)

Heroic bosses/mobs are level 72, so the crit-immunity defense floor is **485, not 465**. Corrected both occurrences:

- AOE Threat Set gearing priorities: "can drop to 465" → "can drop to **485** (level 72 crit immunity)".
- AOE stat-priority notes: "(465 for level 72 trash)" → "(**485** for level 72 mobs)".

Now consistent with the guide's existing Resilience vs Defense section. Logged under v1.5. Committed + pushed.

---

## Key Takeaways

- **Improved Seal of the Crusader > Improved Judgement** for the threat-focused Sanctity build: the +2% raid-wide crit-to-be-hit debuff on the boss is a party DPS *and* threat gain, and it doesn't break the 969 rotation the way an 8s Judgement CD does.
- The paladin guide had silently **forked into two repos** with divergent histories. The locally-edited `wow-tbc/index.html` was the more advanced fork; the public site was running an older one. Always confirm which file the live Pages site actually serves before assuming an edit will appear.
- After consolidation there is now **exactly one copy of each guide**: warrior at `BiS/` → `wow-classic-warrior-tank-guide`; paladin at `BiS/wow-tbc/` → `wow-tbc-prot-paladin-guide` (gitignored by the warrior repo).

---

## Files Touched

- **`index.html`** (paladin repo) — Sanctity build respec + rename, talent-calc link, comparison table, tips, rotation note, v1.5 changelog; later the 465→485 defense fix.
- **Published into the paladin repo** — `prot_paladin_rotations.html`, `soc_vs_sor_timeline.html`, `buff_comparison_woa_wf_wizoil.html`, `research_professions.md`, `SESSION_LOG_2026-05-27.md`, `SESSION_LOG_2026-05-28.md`, `04318 prot talents.txt`, `SESSION_LOG.md`.
- **`.gitignore`** (warrior repo) — added `wow-tbc/`.
- **Deleted** — `BiS/Future Work/wow-classic-warrior-tank-guide/` (stale clone).
- **Structural** — `BiS/wow-tbc/` converted from a loose folder into the `wow-tbc-prot-paladin-guide` checkout; nested `wow-tbc-repo-temp/` removed.

### Paladin repo commits this session
- `cb15e2c` — Update guide to current working version (Sanctity respec + accumulated theorycrafting now live)
- `e989933` — Add remaining paladin working files
- `d2bcbc6` — Fix heroic defense floor: 465 → 485

### Warrior repo commit this session
- `a61617a` — Ignore `wow-tbc/` (Prot Paladin guide has its own repo)
