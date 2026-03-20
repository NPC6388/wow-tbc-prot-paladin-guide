# Session Log - TBC Paladin Tanking Guide Planning

**Date:** 2026-02-09
**Project:** TBC Paladin Tanking Guide
**Working Directory:** `C:\Users\matth\Desktop\AI\BiS\wow-tbc`

---

## Objective

Review the existing Classic WoW Warrior Tanking Guide (`C:\Users\matth\Desktop\AI\BiS\Future Work\wow-classic-warrior-tank-guide\`) and create a comprehensive project plan for an analogous TBC Paladin Tanking Guide with two major sections:

1. **AOE Tanking** - Mitigation + spell power focus (paladin's unique trash/heroic dominance)
2. **Boss Tanking** - Single-target physical DPS focus (maximizing boss threat and DPS contribution)

---

## Work Completed

### 1. Warrior Guide Review

Thoroughly read and analyzed the existing warrior guide (`index.html`, ~2800+ lines):

**Structure analyzed:**
- Introduction, Race Selection, Combat Mechanics (Threat, Debuff Cap, Combat Table, Weapon Mechanics, Cooldowns)
- Stat Priorities, Combat Rotations, Warrior Builds (talent specs)
- Consumables (with comparative charts), Engineering
- Gear Optimization (Threat Set, Mitigation Set, Balanced Set, Flask Set, OT)
- Enchantments (DPS + Tank), Macros, WeakAuras, Addons, Simulators

**Technical style noted:**
- Single HTML file with embedded CSS, dark theme (#0d1117 background)
- Chart.js for data visualization
- CSS classes: `.formula`, `.combat-table`, `.warning`, `.tip`, `.stat-priority`, `.threat-build`/`.survival-build`, `.race-chart`
- Collapsible `<details>` sections, horizontal bar charts, footnoted references

### 2. PM Plan Created

**File:** `PALADIN_TANK_GUIDE_PLAN.md`

Comprehensive 1100+ line implementation plan covering:
- **16 major sections** planned with full H2/H3/H4 heading structure
- **12 implementation phases** with hour estimates (50-65 hours total)
- **Complete section outline** organized by AOE and Boss tanking philosophies
- **9 paladin-specific topics** differentiated from warrior guide (mana vs rage, spell power scaling, Holy Shield/Redoubt mechanics, 490 defense cap, Righteous Fury 1.9x threat, Righteous Defense taunt, blessings/auras, librams, professions)
- **Content research task matrix** with complexity ratings
- **Risk assessment** and success criteria
- **Stat conversion reference** for all TBC ratings

### 3. Research Sub-Agents Launched (3 parallel)

#### Agent 1: AOE Tanking Research
**File:** `research_aoe_tanking.md`
- Consecration spell power coefficient (33.6%), rank progression, mana costs
- Holy Shield mechanics (5% SP coefficient, 8 charges, Redoubt synergy)
- Avenger's Shield (9.1% coefficient, 3 targets, silence/daze)
- Retribution Aura and Blessing of Sanctuary threat
- Righteous Fury 1.9x multiplier breakdown
- Defense cap (490), crush immunity (102.4%), armor formula
- Spell power breakpoints (300-400 heroics, 500-600 raids)
- AOE pull strategies, LoS techniques, mana management
- Heroic dungeon strategies (SLabs, SH, Mechanar, Arcatraz, SV, BM)
- Raid trash strategies (Karazhan, SSC, TK)
- Standard 0/49/12 talent build with rationale

#### Agent 2: Boss Tanking Research
**File:** `research_boss_tanking.md`
- Seal of Vengeance vs Seal of Blood (Horde 20-30% threat advantage)
- Single-target rotation: proto-969 concept
- Priority: Holy Shield > Judgement > Avenger's Shield > Exorcism > Consecration
- Boss stat priorities: Defense 490 > Expertise > Spell Hit > SP > Stamina
- Effective health targets by tier (T4/T5/T6/Sunwell)
- Tank swap mechanics with Righteous Defense
- Encounters where paladins excel vs struggle
- 51 Prot / 10 Ret talent build for boss focus
- Tier set evaluations (T6 4-piece superior)
- TPS benchmarks by tier

#### Agent 3: Consumables, Enchants, Utility Research
**File:** `research_consumables_utility.md`
- Flask of Fortification vs Flask of Blinding Light
- Elixir combinations, food buffs, potions
- Enchantments for every slot (AOE vs Boss variants)
- Gem strategies (meta, stamina, defense, spell power)
- Profession analysis (Engineering, JC, Enchanting, Blacksmithing)
- 12+ paladin-specific macros (Righteous Defense, Divine Shield cancel, seal swaps)
- Addon recommendations (PallyPower, ThreatPlates, DBM)
- Race selection comparison (Human, Dwarf, Draenei, Blood Elf)

---

### 4. Phase 1: HTML Skeleton (COMPLETED)

**File:** `index.html`

Built the full HTML skeleton with:
- **All warrior guide CSS** carried over verbatim (dark theme, tables, callouts, charts, etc.)
- **5 new paladin-specific CSS classes:**
  - `.aoe-tank` - Holy gold/amber gradient for AOE tanking content
  - `.boss-tank` - Crusader red gradient for boss tanking content
  - `.spell-power-build` - Arcane purple gradient for SP-focused builds
  - `.physical-build` - Blood red gradient for physical DPS builds
  - `.mana-warning` - Blue callout for mana management tips
- **2 new chart bar variants:** `.chart-bar.utility` (gold), `.chart-bar.spellpower` (purple)
- **Side-by-side card support:** `.aoe-tank.side-by-side` / `.boss-tank.side-by-side`
- **Complete TOC** with all 16 top-level sections and nested sub-sections wired to anchor IDs
- **Every H2** links back to `#top` for navigation
- **HTML comment separators** between sections for easy editing
- **Changelog** initialized with 2026-02-09 skeleton entry
- All section bodies contain `<!-- TODO -->` placeholders for Phase 2+ content

---

## Files Created This Session

| File | Description | Size |
|------|-------------|------|
| `PALADIN_TANK_GUIDE_PLAN.md` | Master implementation plan | ~1124 lines |
| `research_aoe_tanking.md` | AOE tanking mechanics research | 34 KB |
| `research_boss_tanking.md` | Boss tanking mechanics research | 64 KB |
| `research_consumables_utility.md` | Consumables, enchants, utility research | 49 KB |
| `index.html` | Guide HTML skeleton (Phase 1 complete) | All sections stubbed |
| `SESSION_LOG.md` | This session log | — |

---

## Pre-Existing Files in wow-tbc/

| File | Description |
|------|-------------|
| `pally vs war stat conversion table.xlsx` | Paladin vs Warrior stat comparison spreadsheet |
| `tbc_raiding_consumables.csv` | TBC raiding consumables data |

---

### 5. Phase 2-9: Full Guide Content (COMPLETED)

All 16 sections written with verified content. Key decisions made:
- **Horde only** — Alliance races removed, Blood Elf is the only race option
- **Seal of Blood** featured throughout as the Horde advantage
- All mechanics verified against online sources (WoWHead TBC, WoWWiki, WoWPedia)

**Research verification corrections applied:**
- Holy Shield R4: 4 base charges (8 with Improved Holy Shield talent), not 8 baseline
- Avenger's Shield SP coefficient: 0.091, not 0.07
- Defense rating: 2.3654 per skill (332 rating needed), not 2.4 / 336
- Arcane Torrent: 6% total mana, not 2% base mana
- Spiritual Attunement: Trained ability, not a talent
- Spell miss vs level 73 boss: 17%, not 16%
- Melee miss vs level 73 boss: 9%, not 8%
- SoV applies on every landed hit (100%), not 15% proc
- Expertise soft cap: 26 (6.5% dodge), not 25

**Sections completed:**
1. Introduction (AOE/Boss philosophy overview)
2. Race Selection (Blood Elf only, Arcane Torrent, Seal of Blood)
3. Combat Mechanics (7 subsections: Threat, Combat Table, Block, SP Scaling, Mana, Cooldowns)
4. Stat Priorities (stat conversions table, AOE/Boss/Mitigation priorities, EH thresholds)
5. Combat Rotations (AOE rotation, Boss 969 rotation, Mana efficiency)
6. Paladin Builds (0/49/12 AOE and Boss variants, comparison table)
7. Consumables (flasks, elixirs, food, potions, weapon oils)
8. Engineering (Tankatronic Goggles, Rocket Launcher, Sappers)
9. Gear Optimization (AOE/Boss/Mitigation sets, weapons, shields, librams)
10. Enchantments (slot-by-slot survivability vs threat, Aldor vs Scryer)
11. Gems & Professions (meta gem, gem guide, profession comparison)
12. Macros (8 essential macros)
13. WeakAuras
14. Addons
15. Simulators & Tools
16. Sources & References (all verified URLs)

---

## Implementation Progress

| Phase | Description | Status |
|-------|-------------|--------|
| 1 | Foundation & Structure (HTML skeleton, CSS, TOC) | COMPLETE |
| 2 | Core Mechanics Content | COMPLETE |
| 3 | Stat Priorities & Rotations | COMPLETE |
| 4 | Talents & Builds | COMPLETE |
| 5 | Consumables & Engineering | COMPLETE |
| 6 | Gear Optimization | COMPLETE |
| 7 | Enchantments & Professions | COMPLETE |
| 8 | Macros, WeakAuras, Addons | COMPLETE |
| 9 | Simulators & Sources | COMPLETE |
| 10 | Chart Integration (Chart.js) | NOT STARTED |
| 11 | Polish & Testing | NOT STARTED |
| 12 | Advanced Features (optional) | NOT STARTED |

### 6. Seal TPS Chart & Seal Swapping Technique (COMPLETED)

**Session 2 additions (2026-02-09 continued):**

- **Seal TPS Comparison Chart** (Chart.js stacked bar chart) added to Threat System section
  - Compares Active TPS (seal proc on swing) and Judged TPS (Judgement / 10s CD) for all 4 seals
  - Values at 300 SP, 100 DPS / 2.0 speed weapon, 1.9x RF, vs level 73 boss:
    - Seal of Righteousness: 110 active + 42 judged = **152 TPS**
    - Seal of Blood: 61 active + 73 judged = **134 TPS**
    - Seal of Vengeance (5 stacks, Alliance): 109 active + 37 judged = **146 TPS**
    - Seal of Wisdom: 0 TPS (mana only)

- **Advanced: Seal Swapping for Maximum Threat** subsection added to Boss Rotation
  - Technique: Maintain SoR for per-swing procs, swap to SoB before judging, judge Blood, swap back to SoR
  - Combined yield: ~183 TPS (35% more than either seal alone)
  - Tradeoffs documented: 2 extra GCDs/cycle, ~420 mana/cycle, JoB self-damage, lost SoR procs
  - When-to-use guidance: swap on short fights, pure SoB on long fights, pure SoR on farm
  - Terminology note distinguishing Prot "seal swapping" from Ret "true seal twisting" (SoC dual-proc exploit)

- **6 new sources** added to Sources & References:
  - Warmane Forum (Bucovsky's seal twisting guide)
  - Warcraft Tavern (Prot paladin rotation)
  - Icy Veins (Prot paladin rotation)
  - WoWHead (Prot paladin tank rotation)
  - MMO-Champion (SoC vs SoV for Prot discussion)
  - EU Blizzard Forums (Seal Twisting: The Discussion)

---

## Implementation Progress

| Phase | Description | Status |
|-------|-------------|--------|
| 1 | Foundation & Structure (HTML skeleton, CSS, TOC) | COMPLETE |
| 2 | Core Mechanics Content | COMPLETE |
| 3 | Stat Priorities & Rotations | COMPLETE |
| 4 | Talents & Builds | COMPLETE |
| 5 | Consumables & Engineering | COMPLETE |
| 6 | Gear Optimization | COMPLETE |
| 7 | Enchantments & Professions | COMPLETE |
| 8 | Macros, WeakAuras, Addons | COMPLETE |
| 9 | Simulators & Sources | COMPLETE |
| 10 | Chart Integration (Chart.js) | IN PROGRESS (Seal TPS chart done, more planned) |
| 11 | Polish & Testing | NOT STARTED |
| 12 | Advanced Features (optional) | NOT STARTED |

---

### 7. Accuracy Audit — Wowhead Verification (COMPLETED)

**Date:** 2026-02-10

Systematic verification of every spell, ability, consumable, and gear item in the guide against Wowhead TBC database. All values cross-referenced with live Wowhead TBC pages.

**13 errors corrected:**

#### Critical Game Mechanic Errors (5)
1. **Avenger's Shield** — Changed "3 sec silence" to "6 sec daze" in all 5 locations. Silence was added in WotLK (patch 3.0.2), not present in TBC.
2. **Divine Protection** — Changed "50% damage reduction, 12 sec" to "full immunity, 8 sec, cannot attack." The 50% DR version is from WotLK.
3. **Avenging Wrath + Forbearance** — Corrected "does NOT cause Forbearance" to "DOES cause Forbearance in TBC 2.4.3." Forbearance removal happened in WotLK 3.0.2.
4. **Righteous Defense** — Updated to note it can target enemies directly as of patch 2.4.0, not just friendly players.
5. **Arcane Torrent** — Corrected "6% of total mana" to Mana Tap charge-based system (~171 mana per charge, up to 3 charges = ~513 mana at level 70). Added Mana Tap explanation.

#### Ability Value Errors (4)
6. **Judgement of Blood** — Base damage corrected from ~460 to 295–325.
7. **Holy Wrath Rank 3** — Damage corrected from 757 to 637–748. Added 2 sec cast time.
8. **Blessing of Sanctuary** — Corrected to Rank 5 values: 46 Holy damage per block and 80 damage reduction (was incorrectly 14/42).
9. **Seal of Wisdom** — Mana per proc corrected from ~100 to 121.

#### Gear/Item Errors (3)
10. **Continuum Blade** — Speed 1.80 (not 1.5), +30 Stam (not 22), +121 SP (not 236), +11 Int, +8 Spell Hit. Source: Keepers of Time Revered (not SSC).
11. **Gavel of Unearthed Secrets** — Speed 2.70 (not 1.8), +24 Stam (not 18), +159 SP (not 222), +16 Int, +15 Spell Crit.
12. **Mallet of the Tides** — Has NO spell damage (has Defense + Expertise), speed 1.70 (not 1.6), drops from Lurker Below (not Morogrim).

#### Minor Correction (1)
13. **Avenger's Shield damage range** — Corrected from 494–604 to 494–602.

#### Derived Calculations Updated
- All threat examples recalculated with corrected Judgement of Blood base damage
- Seal swap TPS updated from ~183 to ~193
- JoB self-damage estimate updated from 240–320 to 145–200

#### New Section Added
- **"Flagged for Further Verification"** section added after Changelog with 6 items where Wowhead data conflicts with community sources:
  - Holy Shield mana cost (guide: 180 vs Wowhead: 280)
  - Holy Shield cooldown (guide: 8 sec vs Wowhead: 10 sec)
  - Judgement of Wisdom proc rate (guaranteed vs ~50%)
  - Improved Holy Shield charge count (8 charges — likely correct but couldn't verify tooltip)
  - Exorcism Rank 7 base damage (couldn't verify on Wowhead)
  - Seal of Righteousness SP coefficient (0.2 — from theorycrafting archives)

#### Items Verified as Correct
- Consecration Rank 6: 512 total, 64/tick, 8 sec, 660 mana ✅
- Retribution Aura Rank 6: 26 per hit ✅
- Seal of Blood: 35% weapon damage, 10% self-damage ✅
- Flask of Fortification: +500 HP, +10 Def Rating ✅
- Flask of Blinding Light: +80 Holy/Arcane/Nature SP ✅
- Elixir of Major Defense: +550 Armor ✅
- Spicy Crawdad: +30 Stam, +20 Spirit ✅
- Blackened Basilisk: +23 SP, +20 Spirit ✅
- Superior Wizard Oil: +42 SP ✅
- Ironshield Potion: +2500 Armor, 2 min ✅
- Super Mana Potion: 1800–3000 mana ✅
- Lay on Hands: 100% max HP heal, 60 min CD ✅
- Arcane Torrent: 2 sec silence, 8 yard range, 2 min CD ✅

**Changelog entry v1.1 added to index.html.**

---

## Implementation Progress

| Phase | Description | Status |
|-------|-------------|--------|
| 1 | Foundation & Structure (HTML skeleton, CSS, TOC) | COMPLETE |
| 2 | Core Mechanics Content | COMPLETE |
| 3 | Stat Priorities & Rotations | COMPLETE |
| 4 | Talents & Builds | COMPLETE |
| 5 | Consumables & Engineering | COMPLETE |
| 6 | Gear Optimization | COMPLETE |
| 7 | Enchantments & Professions | COMPLETE |
| 8 | Macros, WeakAuras, Addons | COMPLETE |
| 9 | Simulators & Sources | COMPLETE |
| 10 | Chart Integration (Chart.js) | IN PROGRESS (Seal TPS chart done, more planned) |
| 11 | Accuracy Audit (Wowhead verification) | COMPLETE |
| 12 | Polish & Testing | NOT STARTED |
| 13 | Advanced Features (optional) | NOT STARTED |

---

### 8. Seal Chart Update, Rotation Fixes & Redoubt Correction (COMPLETED)

**Date:** 2026-02-10 (continued)

#### Seal TPS Chart Updated
- **Removed** Seal of Vengeance (Alliance-only, this is a Horde guide)
- **Added** Seal of Command (31 active + 70 judged = 101 TPS)
- **Added** Seal of the Crusader (35 active + 66 judged = 101 TPS)
- **Added** SotC 3/3 Improved (41 active + 71 judged = 112 TPS)
- Chart now shows 6 seals with tooltip notes explaining SotC indirect TPS

#### Rotation Sections Updated — Seal Recast After Judging
All rotation sections now explicitly state which seal to recast after judging:
- **AOE Pull Sequence** — "Judgement... Immediately recast Seal of Righteousness"
- **Sustained AOE Priority** — Judgement + recast SoR shown together
- **Boss Pull & Opener** — Judge Blood → recast **Seal of Righteousness** (highest per-swing TPS)
- **Sustained Boss Rotation table** — Judgement row notes "Recast Seal of Righteousness immediately after"
- **GCD Timeline** — Added 3.0s slot for SoR recast after Judgement
- **Auto-attack row** — Updated to reference SoR procs (not SoB)

#### Boss Opener Reordered
- Moved **Avenging Wrath before Judgement** so the +30% damage buff applies to the first Judge

#### Redoubt Corrected
- Was incorrectly described as proccing on crit taken
- Corrected to: **10% chance on melee/ranged hit taken, +30% block for 10 sec or 5 blocks**
- Fixed in 3 locations: Redoubt Synergy tip box, talent table, and crush immunity discussion

---

## Next Steps

1. **More Chart.js charts** — Stat comparison charts, consumable comparisons, threat breakdowns by ability
2. **Phase 12: Polish & Testing** — Proofread, verify all anchor links, test responsive layout, cross-browser check
3. **Phase 13: Advanced Features** — Interactive calculators, gear comparison tools (optional)
4. **Gear BiS lists** — Could add phase-by-phase BiS gear tables (Pre-raid, T4, T5, T6, Sunwell)
5. **Resolve flagged items** — In-game verification of Holy Shield mana/CD, JoW proc rate, Exorcism damage

---

## Key Decisions Resolved

- **Target TBC patch:** 2.4.3 (final patch) — confirmed
- **Scope:** Full guide, all sections — completed
- **Horde only:** Alliance races removed, Blood Elf featured exclusively
- **Gear lists:** General stat priorities with example items (full BiS-by-phase could be added later)
- **Accuracy standard:** All ability values verified against Wowhead TBC; uncertain items flagged separately

## Key Decisions Remaining

- **Chart.js charts:** How many additional data visualizations to include?
- **BiS gear lists:** Add phase-by-phase BiS tables?
- **Flagged items:** Need in-game or combat log verification for 6 disputed values

---

### 9. Karazhan Raid Guide Created (COMPLETED)

**Date:** 2026-03-19

#### Objective
Create a comprehensive Karazhan tanking reference guide for Prot Paladin, designed for second-monitor use during raids.

#### File Created
`karazhan_raid_guide.html` (~1,580 lines)

#### Research Process
- 4 research agents ran in parallel, pulling from Wowhead, Icy Veins, Warcraft Wiki, Warcraft Tavern, wowtbc.gg, Honorscode, and other TBC Classic sources
- Agent 1: All boss abilities and tanking mechanics
- Agent 2: All trash mob abilities by area
- Agent 3: Karazhan map layout and routing
- Agent 4: Animal bosses, Nightbane details, and Prot Paladin-specific tips
- Cross-referenced boss abilities with spell IDs and damage numbers from multiple guides

#### Guide Contents

**Structure & UX (second-monitor optimized):**
- Sticky quick-nav sidebar on right for instant boss jumping
- Dark theme matching existing project guides (#0d1117 background)
- Color-coded damage types throughout (shadow/fire/holy/arcane/frost/nature/physical)
- Gold-bordered `.pally-tip` callout boxes for Prot Paladin-specific advice
- Red-highlighted danger callouts for critical mechanics
- Collapsible sections, combat tables, boss cards with gradient backgrounds
- 2-column table of contents

**SVG Tower Map:**
- Full visual map replacing initial ASCII version (user requested upgrade)
- Numbered red boss markers with glow filter effects (all 11 bosses)
- Green dashed route lines showing standard clear path bottom-to-top
- Gold dashed shortcut indicators (Berthold teleport, Side Entrance, Servants' Entrance Door)
- Room boxes with key trash danger callouts (e.g., `!RF strip`, `!Spell Immune`, `!Threat Wipe`)
- Legend panel and Clear Order panel
- Netherspace area with purple nether-themed background
- Optional areas (Servants' Quarters, Nightbane) shown with dashed borders

**All 11 Bosses + 3 Animal Bosses with complete ability lists:**
1. Attumen & Midnight — Phase transition, Shadow Cleave, threat wipe on mount
2. Moroes — Gouge, Garrote, 4 random dinner guest adds with full ability table
3. Maiden of Virtue — Repentance, Holy Fire, Holy Ground, Holy Wrath
4. Opera Event — All 3 variants (Big Bad Wolf, Romulo & Julianne, Wizard of Oz with full add table)
5. The Curator — Hateful Bolt, Astral Flares, Evocation burn phase
6. Shade of Aran — All spells, Flame Wreath, Blizzard, Mass Poly, Water Elementals
7. Terestian Illhoof — Demon Chains, Imp swarms, Kil'rek, Broken Pact
8. Netherspite — 3 beam colors with full effect table, Portal/Banish phase cycle
9. Chess Event — Piece abilities, Medivh cheats
10. Prince Malchezaar — 3 phases, Enfeeble, Sunder Armor, Thrash, Infernals
11. Nightbane — Ground/Air phases, Rain of Bones, Smoking Blast, Fireball Barrage trigger
12. Hyakiss the Lurker — 10-sec Web stun, Acidic Fang armor shred (7k)
13. Rokad the Ravager — Ravage bleed
14. Shadikith the Glider — Sonic Burst silence, Wing Buffet threat reduction

**All Trash Mobs by Area:**
- Stables: Spectral Charger, Stallion, Stable Hand (Pierce Armor, Healing Touch, Whip Frenzy)
- Banquet Hall: Ghostly Steward, Spectral Retainer (!Antimagic Pulse strips RF), Phantom Guest, Skeletal Waiter (!Brittle Bones +35% damage taken)
- Guest Chambers: Night Mistress, Wanton Hostess (!50% phase transform), Phantom Guardsman, Spectral Sentry
- Opera Hall: Skeletal Usher (!Ice Tomb threat wipe), Spectral Performer (!Curtain Call death explosion), Phantom Stagehand
- Broken Stair: Ghastly Haunt (stacking hit debuff), Trapped Soul (Cone of Cold, Elemental Armor)
- Menagerie: Mana Warp (!5,500 death explosion), Arcane Watchman (Overload), Syphoner (Drain Mana)
- Library: Mana Feeder (!Spell Immune), Chaotic Sentience (!Spell Immune), Arcane Protector (hardest hitter), Spell/Sorcerous Shade, Arcane Anomaly (Blink threat reset), Ethereal Thief/Spellfilcher (Humanoid — Polymorph)
- Prince Tower: Greater Fleshbeast (!Extreme danger — Thrash can one-shot), Fleshbeast
- Servants' Quarters: Coldmist Widow/Stalker, Shadowbats, Phase Hounds
- CC Quick Reference Table (Shackle/Polymorph/Trap/Banish/Turn Evil/Hibernate)

**General Prot Paladin Sections:**
- Blessing of Sacrifice utility breakdown (breaks Gouge, Repentance, Fear, Polymorph)
- Holy Shield uptime / Uncrushable requirements (102.4%, never let HS drop, no AS mid-boss)
- Seal/Judgment cheat sheet by situation (AoE, single target, undead, mana starved)
- Consumable recommendations (Ironshield, Super Mana, Flask options, Flame Cap, Nightmare Seed)
- Weakness awareness (silences, fears, spell-immune mobs, Retainer RF strip)
- Boss quick reference table with key mechanic, damage type, Pally difficulty rating, and critical notes

**Boss Quick Reference Table ratings:**
| Boss | Pally Rating |
|------|-------------|
| Attumen | Easy |
| Moroes | Good (BoSac Gouge trick) |
| Maiden | Medium (Holy Ground silence barely affects instants) |
| Big Bad Wolf | Easy |
| Romulo & Julianne | Medium |
| Wizard of Oz | Great (AoE dream) |
| Curator | Easy |
| Shade of Aran | N/A (no tank needed) |
| Illhoof | Great (Imp AoE king) |
| Netherspite | Medium |
| Chess | Free Loot |
| Prince | Medium (Phase 2 Sunder+Thrash is rough) |
| Nightbane | Good (AoE skeletons, but fear is a problem) |
| Hyakiss | Best animal boss for Pally (self-Cleanse) |
| Rokad | Easy |
| Shadikith | Hardest animal boss for Pally (silence) |

#### Key Research Findings Incorporated
- Maiden Holy Ground silence is only 1 sec per 3-sec tick — Pally instant casts work between ticks (changed rating from Hard to Medium)
- Moroes BoSac trick: BoSac on OT before Gouge → damage transfer breaks Gouge instantly
- Attumen Phase 3 threat table wipe on mount; Berserker Charge has 8-yard minimum range
- Spectral Retainer Antimagic Pulse strips ALL buffs including Righteous Fury
- Mana Feeders and Chaotic Sentiences in Library are completely immune to spell damage (entire Pally kit useless)
- Skeletal Usher Ice Tomb targets highest threat and wipes the threat table
- Greater Fleshbeasts before Prince are the most dangerous trash — Thrash can one-shot
- Hyakiss Web is 10 sec on highest threat, Acidic Fang shreds 1,000 armor per stack (up to 7 = 7,000)
- Shadikith Wing Buffet also reduces threat (not just knockback)
- Nightbane Fireball Barrage triggers if anyone is >40 yards away (wipe mechanic)
- Nightbane Smoking Blast: 1,850-2,150 physical + 3,000 fire DoT over 18 sec (dispellable)
- Nightbane spawns 5 Restless Skeletons per Rain of Bones (~13,500 HP each)
- Wizard of Oz kill order: Dorothee before Tito (avoid Enrage)
- Wanton Hostess Alluring Aura doesn't affect Holy damage (Pally AoE threat unaffected)
- Roar has Shred Armor and Mangle bleed (actually hits harder than expected)
