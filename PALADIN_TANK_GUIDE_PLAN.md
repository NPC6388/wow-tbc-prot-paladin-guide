# TBC Paladin Tanking Guide - Implementation Plan

## 1. Project Overview

### Goals
- Create a comprehensive, single-page HTML guide for TBC Paladin tanking
- Mirror the quality, depth, and technical presentation of the existing Classic Warrior Tanking Guide
- Emphasize paladin's unique dual-nature tanking philosophy: AOE/trash dominance vs boss tanking
- Provide actionable, data-driven guidance with formulas, charts, and simulations
- Serve both new and experienced paladin tanks with mechanical depth and practical optimization strategies

### Target Audience
- Primary: TBC paladin tanks (both new and experienced)
- Secondary: Raid leaders understanding paladin tank capabilities and limitations
- Tertiary: Players considering paladin as a tanking alt or class reroll

### Technical Approach
- Single HTML file with embedded CSS (matching warrior guide architecture)
- Dark theme: background #0d1117, container #161b22
- Chart.js for visual data presentation (threat scaling, stat comparisons, consumable ROI)
- Responsive design with collapsible sections using `<details>` tags
- CSS classes from warrior guide: `.formula`, `.combat-table`, `.warning`, `.tip`, `.stat-priority`, `.threat-build/.survival-build`, `.race-chart`, `.toc`
- Additional paladin-specific classes: `.aoe-tank`, `.boss-tank`, `.spell-power-build`, `.physical-build`

---

## 2. Complete Section Outline

### A. Front Matter
#### H1: Tankenheimer's TBC Paladin Tanking Guide
- Subtitle: "The Holy Trinity of Protection - AOE Dominance, Boss Threat, and Raid Utility"
- **Table of Contents** (styled `.toc`)

---

### B. Core Sections

#### H2: Introduction
- Overview of paladin tanking in TBC
- Key philosophy: Two distinct tanking approaches (AOE vs Boss)
- When to use paladin tanks vs warriors/druids
- Guide methodology and sources
- **Complexity: Simple**

---

#### H2: Race Selection (Alliance & Horde)
##### H3: Alliance Races
- Human (Diplomacy, Spirit, Sword/Mace Specialization)
- Dwarf (Stoneform, Frost Resistance)
- Draenei (Gift of the Naaru, +1% Hit Aura)

##### H3: Horde Races
- Blood Elf (Arcane Torrent, Silence/Mana Restore, +1% Crit Aura)

##### H3: Racial Comparison Charts
- Threat/DPS contribution (horizontal bar charts)
- Survivability contribution
- Raid utility contribution (unique to paladins - aura synergies)
- **Complexity: Medium** (requires racial ability math and chart generation)

---

#### H2: Combat Mechanics
##### H3: Threat System & Formulas
- TBC threat mechanics (identical to Classic for most abilities)
- **Righteous Fury**: 90% increased Holy threat with 3/3 Improved Righteous Fury talent
  - Formula: `Base Threat × 1.9` for Holy damage/healing
- Paladin threat formulas by ability:
  - **Consecration**: `(Damage × 1.9) + (Healing Threat × 1.9)`
  - **Holy Shield**: `(Block Damage × 1.9) + (Proc Damage × 1.9)`
  - **Avenger's Shield**: `(Damage × 1.9)` per target
  - **Seal of Vengeance/Blood**: `(DOT Tick × 1.9) + (Stack Application × 1.9)`
  - **Judgement of Righteousness**: `(Damage × 1.9)`
  - **Blessing of Sanctuary**: `(Proc Damage × 1.9)`
- Comparison to Defensive Stance (1.3x modifier for warriors)

##### H3: Debuff Slots & Raid Coordination
- TBC debuff limit (40 slots, up from 16 in Classic)
- Paladin-specific priority debuffs:
  - Seal of Vengeance/Blood (5 stacks)
  - Judgement of Light/Wisdom
- Coordination with other classes

##### H3: Combat Table Mechanics
- TBC combat table order: **Miss > Dodge > Parry > Block > Crit > Crush > Hit**
- **Critical Defense Cap**: 490 Defense (5.6% crit suppression + boss level difference)
  - Formula: `Defense Rating Required = (490 - 350 Base Defense) × 2.3654 = 331.116 Defense Rating`
- **Crush Immunity**: Achievable via Block-capping (102.4% avoidance + block)
  - Formula: `Miss% + Dodge% + Parry% + Block% ≥ 102.4%`
  - Paladin advantage: Holy Shield (+30% block for 10 seconds, 8-second cooldown = near-100% uptime)
- **Uncrittable vs Uncrushable**: Key thresholds and gearing priorities

##### H3: Block Mechanics (Paladin-Specific)
- **Holy Shield**:
  - Base: 30% increased block chance for 10 seconds
  - 4 charges (blocks 4 attacks)
  - Damage proc per block
  - Redoubt synergy (6 seconds of +30% block after crit)
- **Block Value Scaling**:
  - Base formula: `(Shield Block Value + Strength/20 - 1) × Block%`
  - Spell Power contribution: `Blessing of Sanctuary = 35 + (0.25 × Spell Power)`
- Holy Shield + Redoubt interaction (overlapping block buffs)

##### H3: Spell Power vs Attack Power (Threat Scaling)
- **Spell Power Abilities**:
  - Consecration: `64 + (0.04 × Spell Power × 1.15)` per tick over 8 seconds
  - Holy Shield: `65 + (0.05 × Spell Power)` per block
  - Avenger's Shield: `494 + (0.07 × Spell Power)` per target
  - Seal of Righteousness (proc): `Weapon Damage × 0.11 + (0.032 × Spell Power)`
- **Attack Power Abilities**:
  - Seal of Vengeance/Blood: 5-stack DOT scales with AP and weapon damage
  - Judgement of Blood/Vengeance
  - Auto-attacks (expertise/hit contribution)
- Chart comparing threat output: Spell Power vs Attack Power builds

##### H3: Mana Management
- Mana as a resource (vs Rage for warriors)
- Base mana regen: `Spirit × 0.125` (continues during combat for paladins)
- **Spiritual Attunement**: 10% of healing received restored as mana
- **Seal of Wisdom**: Mana restore on melee attacks
- **Judgement of Wisdom**: Mana restore on target attacks
- MP5 vs Spirit vs Spiritual Attunement gearing
- Mana cooldowns: Divine Illumination, Mana Potions, Demonic/Dark Runes
- Threat-per-Mana (TPM) optimization

##### H3: Crucial Tanking Cooldowns
- **Holy Shield** (8s CD, 10s duration): Block cap maintenance
- **Avenger's Shield** (30s CD): AOE pull, silence, ranged threat
- **Divine Protection** (5 min CD): 50% damage reduction, 12 seconds (forbearance)
- **Divine Shield** (5 min CD): Full immunity, 12 seconds (forbearance, threat drop)
- **Lay on Hands** (60 min CD): Full heal (forbearance, threat generation)
- **Blessing of Protection** (5 min CD): Physical immunity on ally (forbearance)
- **Righteous Defense** (15s CD): Taunt (3 targets, transfers threat)
- **Avenging Wrath** (3 min CD): 30% increased damage/healing, 20 seconds

##### H3: Threat Cooldowns (DPS Contribution)
- **Avenging Wrath**: 30% damage boost (20s, 3min CD)
- **Divine Illumination**: Free spells for 15s (2min CD) - Consecration spam
- **Trinkets**: Spell power vs attack power on-use trinkets
- **Engineering**: Goblin Sapper Charge, Flame Reflector
- **Consumables**: Haste potions, spell power elixirs

---

#### H2: Stat Priorities

##### H3: Critical Stat Conversions & Thresholds (TBC)
- **Defense Rating**: `2.3654 rating = 1 defense skill`
  - Cap: 490 defense (331 defense rating at level 70)
- **Dodge Rating**: `18.9231 rating = 1% dodge`
- **Parry Rating**: `23.6538 rating = 1% parry`
- **Block Rating**: `7.8846 rating = 1% block`
- **Hit Rating**: `15.77 rating = 1% hit` (melee/physical)
  - Cap: 9% hit vs raid boss (142 hit rating)
- **Spell Hit Rating**: `12.62 rating = 1% spell hit`
  - Cap: 16% spell hit (202 spell hit rating) - reduced by talents
- **Expertise Rating**: `3.9423 rating = 1 expertise (0.25% dodge reduction)`
  - Soft cap: 56 expertise (14% dodge reduction, ~221 expertise rating)
  - Hard cap: 140 expertise (35% parry reduction, not achievable in TBC)
- **Haste Rating**: `15.77 rating = 1% haste` (melee)
- **Spell Haste Rating**: `15.77 rating = 1% spell haste`
- **Crit Rating**: `22.08 rating = 1% crit` (melee)
- **Spell Crit Rating**: `22.08 rating = 1% spell crit`
- **Resilience Rating**: `39.423 rating = 1% crit reduction`

##### H3: AOE Tanking Stat Priority
```
Defense (to 490 cap) > Stamina > Spell Damage > Spell Hit (to cap) >
Block Value > Armor > Intellect/MP5 > Dodge/Parry > Haste
```
- Rationale: Defense cap for uncrittable, Spell Damage scales AOE threat (Consecration, Holy Shield, Avenger's Shield)
- Block Value: Increases Holy Shield threat and mitigation
- Spell Hit: Ensures Consecration/Holy Shield lands (16% cap, reduced by talents)
- Intellect/MP5: Mana sustain for long trash pulls
- Chart: Threat-per-point comparison for each stat (AOE scenarios)

##### H3: Boss Tanking Stat Priority (Threat Focus)
```
Defense (to 490 cap) > Stamina > Hit (to 9%) > Expertise (to soft cap) >
Strength/AP > Spell Damage > Crit > Haste > Dodge/Parry
```
- Rationale: Physical DPS optimization for Seal of Vengeance/Blood stacking
- Hit/Expertise: Maximizes white damage and Seal procs
- Strength/AP: Scales Seal DOT and auto-attack damage
- Spell Damage: Still valuable for Consecration/Holy Shield threat
- Chart: Single-target threat scaling by stat

##### H3: Boss Tanking Stat Priority (Mitigation Focus)
```
Defense (to 490 cap) > Stamina > Dodge > Parry > Block Value >
Armor > Resilience > Hit/Expertise
```
- For progression/learning fights where threat is less critical
- Emphasizes crush immunity and spike damage reduction
- Block Value still preferred over pure avoidance (Holy Shield synergy)

##### H3: Comparative Analysis: Spell Power vs Physical Stats
- Table comparing 100 spell damage vs 100 AP for threat generation
- Chart: TPS (Threat Per Second) by gear archetype
  - Full spell power build
  - Hybrid build (balanced SP/AP)
  - Full physical build
  - Mitigation-heavy build
- Simulation results from TBC tanking simulators

---

#### H2: Combat Rotations

##### H3: AOE Tanking Rotation (Trash/Heroics)
**Pull Sequence**:
1. **Avenger's Shield** (ranged pull, silence)
2. **Holy Shield** (activate before contact)
3. **Consecration** (immediate on pack arrival)
4. **Judgement** (Seal of Wisdom/Light)
5. **Seal of Righteousness** (AOE threat procs)

**Sustained AOE Threat**:
- Priority: `Holy Shield (on CD) > Consecration (maintain uptime) > Judgement (on CD) > Seal of Righteousness`
- Mana management: Judge Seal of Wisdom if mana < 30%
- Positioning: Face pack away from raid, back to wall (no parry/dodge from behind)
- **Retribution Aura**: Passive AOE threat from enemy attacks

##### H3: Boss Tanking Rotation (Single-Target)
**Pre-Pull**:
1. Seal of Vengeance/Blood
2. Holy Shield (5 seconds before pull)
3. Pre-pot (Haste or Spell Power)

**Opening**:
1. **Avenger's Shield** (ranged pull)
2. **Judgement** (apply Seal DOT, refresh Seal)
3. **Consecration**
4. **Holy Shield** (refresh on CD)
5. **Exorcism** (if Undead/Demon)

**Sustained Threat**:
- Priority: `Holy Shield (on CD) > Seal of Vengeance/Blood (maintain) > Judgement (on CD) > Consecration (maintain) > Exorcism (if applicable) > Avenger's Shield (on CD)`
- 5-stack Seal of Vengeance/Blood maintenance (DOT snapshots on application)
- Mana sustain via Spiritual Attunement and Judgement of Wisdom
- Threat dump: Avenging Wrath + Divine Illumination (Consecration spam)

##### H3: Mana Efficiency Rotation (Extended Fights)
- Low-mana alternative: Drop Consecration, focus on Seal/Judgement/Holy Shield
- Seal of Wisdom usage windows
- Spiritual Attunement optimization (intentionally taking damage for mana)
- Chart: Mana consumption per rotation type

---

#### H2: Paladin Builds (Talent Specs)

##### H3: Protection AOE Tank Build (0/49/12)
- **Full Protection Tree** (49 points):
  - 5/5 Redoubt
  - 3/3 Precision (3% spell hit)
  - 3/3 Improved Righteous Fury (6% stamina, threat modifier)
  - 5/5 Toughness (10% armor)
  - 5/5 Blessing of Sanctuary
  - 1/1 Holy Shield
  - 3/3 Anticipation (5% defense)
  - 5/5 Sacred Duty (6% stamina, reduces Holy Shield CD)
  - 1/1 Avenger's Shield
  - 3/3 Improved Holy Shield (damage boost)
  - 2/2 Ardent Defender (damage reduction at low HP)
  - 1/1 Improved Righteous Fury
  - 5/5 Combat Expertise (10% expertise, 6% crit)
  - 1/1 Avenger's Shield
- **Holy Tree** (12 points):
  - 5/5 Divine Strength (+10% strength)
  - 5/5 Divine Intellect (+10% intellect)
  - 2/5 Healing Light or 2/3 Improved Seal of Righteousness
- Talent calculator link
- **Use Case**: Heroic dungeons, trash-heavy raids (SSC/TK/BT trash)

##### H3: Protection Boss Tank Build (0/47/14)
- **Protection Tree** (47 points): Similar to above, but drop some AOE-centric talents
  - Possible drops: Improved Holy Shield damage, points from Redoubt
- **Retribution Tree** (14 points):
  - 5/5 Benediction (mana cost reduction)
  - 3/3 Improved Judgements (reduced CD)
  - 5/5 Conviction (+5% crit)
  - 1/1 Seal of Blood/Vengeance (if not baseline)
- Talent calculator link
- **Use Case**: Main tank on bosses requiring high single-target threat

##### H3: Hybrid Retribution-Tank Build (5/11/45)
- For off-tank/DPS hybrid roles in 25-man raids
- Light Protection investment, Heavy Retribution
- **Use Case**: Niche, not recommended for serious tanking

##### H3: Talent Comparison Table
- Table comparing builds side-by-side:
  - AOE threat output
  - Single-target threat output
  - Survivability
  - Mana efficiency
  - Raid utility

---

#### H2: Consumables

##### H3: Pre-Raid Consumables (Mandatory)
- **Elixir of Major Agility** (Guardian, 35 agility, 170 armor)
- **Elixir of Major Fortitude** (Battle, 250 HP, 10 HP5)
- **Flask of Fortification** (500 HP, 10 defense rating) - for progression
- **Flask of Chromatic Wonder** (all stats +18) - hybrid option
- **Blackened Basilisk** (food, 23 spell damage, 20 spirit)
- **Fisherman's Feast** (food, 30 stamina, 20 spirit) - mitigation alternative

##### H3: Combat Consumables
- **Elixir of Major Defense** (Guardian, 550 armor) - stacks with agility elixir
- **Elixir of Draenic Wisdom** (Battle, +30 int, +30 spirit)
- **Elixir of Mastery** (Battle, +15 all stats)
- **Super Mana Potion** (1800-3000 mana, 2min CD)
- **Haste Potion** (Battle, +400 haste, 15s)
- **Destruction Potion** (+120 spell damage, 15s)
- **Ironshield Potion** (+2500 armor, 2min)

##### H3: Consumable Comparison Charts (Chart.js)
- **Spell Damage Consumables**: Chart comparing TPS increase
  - Elixir of Major Firepower (+55 spell damage)
  - Flask of Pure Death (+80 spell damage)
  - Destruction Potion (+120 spell damage, 15s)
- **Stamina Consumables**: Chart comparing effective HP
  - Flask of Fortification
  - Elixir of Major Fortitude
  - Food buffs
- **Cost-Benefit Analysis**: Gold per TPS point

##### H3: Raid Buffs & Debuffs
- Paladin-provided buffs:
  - Blessing of Kings (+10% stats)
  - Blessing of Sanctuary (damage reduction, mana on block)
  - Blessing of Wisdom (mana regen)
  - Judgement of Wisdom (mana on hit)
  - Judgement of Light (healing on hit)
- Key external buffs for paladin tanks:
  - Mark of the Wild (+14 all stats, armor)
  - Prayer of Fortitude (stamina)
  - Arcane Intellect (intellect)
  - Shadow Protection (shadow resist)

---

#### H2: Engineering

##### H3: Goblin Engineering
- **Goblin Sapper Charge**: AOE threat/damage on trash pulls
  - Threat calculation: `(Damage × 1.9)` with Righteous Fury
- **Rocket Boots**: Mobility for repositioning
- **Flame Reflector**: Fire resistance cooldown
- **Frost Deflector**: Frost resistance cooldown

##### H3: Gnomish Engineering
- **Gnomish Poultryizer**: Limited utility for tanks
- **Gnomish Battle Chicken**: DPS pet, not ideal for tanks

##### H3: Engineering Gear
- **Justicar's Chestguard** (not engineering-specific, but optimal)
- **Tankatronic Goggles**: Stamina/defense helmet (pre-raid BiS)
- **Furious Gizmatic Goggles**: Spell damage option (threat-focused)

---

#### H2: Gear Optimization Strategy

##### H3: AOE Threat Set (Heroics/Trash)
**Priorities**:
1. Defense to 490 cap (uncrittable)
2. Spell Damage (Consecration/Holy Shield scaling)
3. Spell Hit to 16% cap (reduced by talents to ~13% from gear)
4. Block Value (Holy Shield threat)
5. Stamina (survivability floor)
6. Intellect/MP5 (mana sustain)

**Example Gear**:
- **Head**: Justicar's Dreadplate Headguard (T5) - spell damage, defense
- **Neck**: Verdant Sphere of Protection (Kael'thas, spell damage)
- **Shoulders**: Justicar's Dreadplate Pauldrons (T5)
- **Chest**: Panzar'thar Breastplate (Gruul, spell damage, block value)
- **Hands**: Gauntlets of the Bold (badge vendor, spell damage)
- **Legs**: Legplates of the Holy Juggernaut (BT, spell damage, block value)
- **Feet**: Boots of Righteous Fortitude (Badges, spell damage)
- **Trinkets**: Commendation of Kael'thas (spell damage), Figurine - Empyrean Tortoise (defense)
- **Libram**: Libram of Repentance (Consecration damage)

##### H3: Boss Threat Set (Single-Target)
**Priorities**:
1. Defense to 490 cap
2. Hit to 9% cap (142 hit rating)
3. Expertise to soft cap (221 expertise rating)
4. Strength/Attack Power
5. Spell Damage (still valuable for Consecration)
6. Stamina
7. Crit/Haste

**Example Gear**:
- More emphasis on physical DPS stats: hit, expertise, strength
- Weapons: Fast 1-handers for Seal of Vengeance proc rate
  - **Continuum Blade** (Doomwalker, fast speed)
  - **Mallet of the Tides** (Morogrim, spell damage)

##### H3: Mitigation Set (Progression)
**Priorities**:
1. Defense to 490 cap
2. Stamina (effective HP)
3. Dodge/Parry (avoidance)
4. Block Value (spike reduction via Holy Shield)
5. Armor
6. Resilience (crit/crit damage reduction)

**Example Gear**:
- Focus on pure survivability stats
- Shield: **Bulwark of Azzinoth** (Illidan, massive stamina/armor)
- Trinkets: **Commendation of Kael'thas** + **Figurine - Empyrean Tortoise**

##### H3: Flask Set Optimization
- How to gear differently when using Flask of Fortification
- Stamina thresholds for specific encounters (e.g., Hydross tank, 18k+ HP)
- Trading threat stats for survivability with flask safety net

##### H3: Off-Tank (OT) Considerations
- Hybrid gearing for OT/DPS roles in 25-man content
- Retribution off-pieces with stamina/defense
- When to swap between tank and DPS sets mid-raid

##### H3: Shield Selection
- **Tankard O' Terror** (Hyjal, spell damage, block value)
- **Bulwark of Azzinoth** (Illidan, stamina, armor, dodge)
- **Shield of Impenetrable Darkness** (Badges, defense, block value)
- **Crest of the Sha'tar** (Reputation, entry-level)

##### H3: Weapon Selection
- **Speed Matters**: Faster weapons = more Seal procs
  - **Continuum Blade** (1.5 speed, Doomwalker)
  - **Gavel of Unearthed Secrets** (1.5 speed, Arca, spell damage)
- **Spell Damage Weapons**:
  - **Mallet of the Tides** (Morogrim)
  - **Crystalforged War Axe** (Gruul)

##### H3: Libram Optimization
- **Libram of Repentance** (SSC trash, +88 Consecration damage)
- **Libram of the Lightbringer** (Badges, +53 block value to Holy Shield)
- **Libram of Saints Departed** (Karazhan, healing/threat)

---

#### H2: Enchantments

##### H3: AOE Tank Enchantments
- **Head**: Glyph of the Defender (+16 defense, +17 dodge, Aldor/Scryer)
- **Shoulders**: Greater Inscription of the Knight (+15 defense, +10 dodge, Aldor) or Greater Inscription of Warding (+15 defense, +10 dodge, Scryer)
- **Cloak**: Enchant Cloak - Steelweave (+12 defense) or Subtlety (threat reduction, not ideal)
- **Chest**: Enchant Chest - Major Resilience (+15 resilience)
- **Bracers**: Enchant Bracer - Major Stamina (+15 stamina)
- **Gloves**: Enchant Gloves - Spell Strike (+15 spell hit, +15 spell damage)
- **Legs**: Nethercleft Leg Armor (+40 stamina, +12 agility) or Nethercobra Leg Armor (+50 AP, +12 crit - not ideal)
- **Boots**: Enchant Boots - Fortitude (+12 stamina) or Vitality (+4 HP5, +9 stamina)
- **Shield**: Enchant Shield - Tough Shield (+18 block value) or Major Stamina (+15 stamina)
- **Weapon**: Enchant Weapon - Major Spellpower (+40 spell damage) or Mongoose (+120 agility proc, haste)

##### H3: Boss Tank Enchantments
- **Gloves**: Enchant Gloves - Superior Agility (+15 agility) or Major Strength (+15 strength)
- **Weapon**: Enchant Weapon - Mongoose (+120 agility proc, haste) or Major Spellpower (+40 spell damage)
- Rest similar to AOE enchants

##### H3: Enchanting as a Profession
- **Ring Enchants** (Enchanters only):
  - Enchant Ring - Stamina (+7.5 stamina per ring)
  - Enchant Ring - Spellpower (+12 spell damage per ring)

---

#### H2: Essential Macros

##### H3: General Macros
- **Righteous Fury Toggle**
```
#showtooltip Righteous Fury
/cancelaura Righteous Fury [modifier:shift]
/cast Righteous Fury
```

- **Blessing Rotation Macro**
```
#showtooltip
/cast [modifier:shift, @mouseover] Blessing of Kings
/cast [modifier:ctrl, @mouseover] Blessing of Wisdom
/cast [@mouseover] Blessing of Sanctuary
```

##### H3: Tanking Macros
- **Holy Shield + Avenger's Shield Combo**
```
#showtooltip Avenger's Shield
/cast Holy Shield
/cast Avenger's Shield
```

- **Righteous Defense (Taunt)**
```
#showtooltip Righteous Defense
/cast [@mouseovertarget, help] [@targettarget, help] Righteous Defense
```

- **Consecration (Position Locked)**
```
#showtooltip Consecration
/cast [nomod] Consecration
/cast [modifier:shift] !Consecration
```

- **Divine Shield Threat Drop Recovery**
```
#showtooltip Divine Shield
/stopcasting
/cast Divine Shield
/cancelaura Divine Shield [modifier:shift]
```

##### H3: Cooldown Macros
- **Emergency Cooldown Stack**
```
#showtooltip Divine Protection
/cast Holy Shield
/cast Divine Protection
/use [item name: stamina trinket]
/cast Lay on Hands [modifier:shift]
```

- **Threat Dump Macro**
```
#showtooltip Avenging Wrath
/cast Avenging Wrath
/cast Divine Illumination
/cast Consecration
```

##### H3: Utility Macros
- **Cleanse + Judgement Combo**
```
#showtooltip Cleanse
/cast [@mouseover, help] [@target, help] [@player] Cleanse
/cast Judgement
```

- **Seal Swap Macro**
```
#showtooltip
/cast [nomod] Seal of Vengeance
/cast [modifier:shift] Seal of Wisdom
/cast [modifier:ctrl] Seal of Righteousness
```

---

#### H2: Essential WeakAuras for Paladins

##### H3: Recommended WeakAuras Collection
- **Holy Shield Timer**: Uptime tracker, CD alert
- **Consecration Timer**: Ground effect duration, CD alert
- **Seal of Vengeance Stacks**: Displays current DOT stacks (1-5)
- **Righteous Fury Active**: Warning when inactive in tank spec
- **Mana Bar**: Large, centered mana display
- **Spiritual Attunement Tracker**: Mana gained in last 10 seconds
- **Cooldown Tracker**: Avenger's Shield, Avenging Wrath, Divine Protection, Divine Shield
- **Forbearance Tracker**: Large warning for Forbearance debuff
- **Blessing Tracker**: Missing raid blessings alert
- **Threat Meter Integration**: WeakAura tied to Omen/Details threat

---

#### H2: Essential Addons for Paladins

##### H3: General Addons
- **Deadly Boss Mods (DBM)** or **BigWigs**: Encounter warnings
- **Details! Damage Meter**: Threat tracking (replaces Omen)
- **WeakAuras 2**: Custom alerts and trackers
- **Bartender4** or **Dominos**: Action bar customization
- **Grid2** or **VuhDo**: Raid frame customization (for emergency heals/BoP)

##### H3: Dungeons & Raids
- **PallyPower**: Blessing management for raids
- **ClassicCastbars**: Enemy cast bars (for interrupts with Avenger's Shield)
- **ThreatPlates**: Nameplate threat indicators (color-coded)
- **Method Raid Tools**: Cooldown tracking for raid utility

##### H3: Paladin-Specific
- **PaladinBuffsClassic**: Buff duration optimization
- **JudgeMe**: Judgement timer and optimization

---

#### H2: Simulators & Tools

##### H3: Available TBC Simulators
- **TBC Paladin Tank Simulator** (if exists - research needed)
- **Rawr**: Gear optimization tool (TBC support)
- **TankPoints**: EH and survivability calculations
- **SimulationCraft** (limited TBC support, verify availability)

##### H3: Online Tools & Calculators
- **WoWHead TBC Database**: Gear, talent calculator
- **Legacy-WoW Paladin Tanking Resources**
- **Elitist Jerks Archive**: TBC paladin theorycrafting
- **Maintankadin Forums Archive**: Paladin tank community research

##### H3: Spreadsheets
- **Paladin Tank Threat Calculator** (create custom or find existing)
- **Block Value vs Spell Damage Comparison**
- **Mana Efficiency Calculator**

---

#### H2: Sources & References

##### H3: Complete Research Sources
- Elitist Jerks TBC Paladin forums
- Maintankadin TBC archive
- WoWHead TBC database
- Blizzard TBC patch notes
- Private server research (if applicable, with disclaimer)
- TBC class mechanics documentation

---

#### H2: Changelog

##### H3: [Date] - Initial Release
- Initial guide publication
- All sections complete

---

## 3. Content Research Tasks

### A. TBC Paladin Mechanics Research
| Topic | Research Needed | Complexity |
|-------|----------------|------------|
| **Righteous Fury threat modifier** | Confirm exact 90% Holy threat with 3/3 talent | Simple |
| **Consecration scaling** | Spell damage coefficient (0.04 × SP × 1.15?) | Medium |
| **Holy Shield scaling** | Damage per block formula with spell damage | Medium |
| **Avenger's Shield scaling** | Spell damage coefficient (0.07 × SP?) | Medium |
| **Seal of Vengeance/Blood** | DOT stacking mechanics, AP scaling, snapshot behavior | Complex |
| **Spiritual Attunement** | Exact conversion rate (10% of healing?), caps, limitations | Medium |
| **Block cap mechanics** | Formula for crush immunity, Holy Shield uptime calculation | Complex |
| **Defense cap** | Confirm 490 defense = uncrittable at 70 vs raid boss | Simple |
| **Combat table order** | Verify TBC combat table: Miss > Dodge > Parry > Block > Crit > Crush > Hit | Medium |
| **Mana regeneration** | Spirit coefficient, MP5 vs Spirit comparison | Medium |
| **Threat-per-Mana (TPM)** | Calculate for each ability, create efficiency ranking | Complex |
| **Redoubt + Holy Shield interaction** | Do block% buffs stack additively or multiplicatively? | Medium |
| **Blessing of Sanctuary** | Spell damage scaling for proc damage (0.25 × SP?) | Medium |

### B. Stat Threshold Research
| Stat | Threshold | Verification Needed |
|------|-----------|---------------------|
| **Defense Rating** | 2.3654 rating = 1 defense | Confirm TBC conversion |
| **Defense Cap** | 490 defense (331 rating) | Verify uncrittable threshold |
| **Hit Rating** | 15.77 rating = 1% hit | Confirm TBC conversion |
| **Hit Cap** | 9% (142 hit rating) | Verify vs raid boss |
| **Spell Hit Rating** | 12.62 rating = 1% spell hit | Confirm TBC conversion |
| **Spell Hit Cap** | 16% (202 rating) - 3% from talents = 13% from gear | Verify with Precision talent |
| **Expertise Rating** | 3.9423 rating = 1 expertise | Confirm TBC conversion |
| **Expertise Soft Cap** | 56 expertise (14%, ~221 rating) | Verify dodge reduction |
| **Block Rating** | 7.8846 rating = 1% block | Confirm TBC conversion |
| **Crush Immunity** | 102.4% avoidance + block | Verify formula |

### C. Racial Ability Research
| Race | Ability | Research Focus |
|------|---------|----------------|
| **Draenei** | Gift of the Naaru | Healing amount, threat generation, mana via Spiritual Attunement |
| **Draenei** | Heroic Presence | +1% hit aura, raid stacking |
| **Blood Elf** | Arcane Torrent | Mana restore amount, silence range, CD |
| **Blood Elf** | +1% Crit Aura | Raid stacking, benefit for paladin tank |
| **Human** | Sword/Mace Specialization | Expertise value (+5 weapon skill = ~3.75 expertise?) |
| **Dwarf** | Stoneform | Bleed/poison removal, armor buff, CD |

### D. Gear Set Research
- **Pre-raid BiS**: Craft/dungeon gear for fresh 70s
- **Karazhan/Gruul/Mag BiS**: T4 content
- **SSC/TK BiS**: T5 content (Justicar set)
- **BT/Hyjal BiS**: T6 content
- **Sunwell BiS**: T6.5 content (if guide covers 2.4)
- **Badge Vendor Gear**: Best badge purchases for each slot
- **Crafted Gear**: Blacksmithing, Leatherworking (mail?), Tailoring (cloth threat pieces?)

### E. Consumable Cost-Benefit Analysis
- Gold prices (server-dependent, use average)
- Threat-per-gold (TPG) calculations
- Survivability-per-gold calculations
- Priority list for budget-conscious tanks

### F. Chart Data Collection
- **Race comparison**: Threat output, survivability, utility (horizontal bar charts)
- **Stat scaling**: TPS per point of each stat (line chart)
- **Consumable ROI**: Gold cost vs TPS increase (bar chart)
- **Spell Power vs AP**: Threat comparison by gear archetype (grouped bar chart)
- **Mana efficiency**: Rotation TPM comparison (bar chart)

---

## 4. Implementation Phases

### Phase 1: Foundation & Structure (Estimated: 4-6 hours)
**Tasks**:
1. Create HTML file skeleton with dark theme CSS (copy from warrior guide)
2. Define paladin-specific CSS classes:
   - `.aoe-tank` (green gradient, similar to `.survival-build`)
   - `.boss-tank` (orange gradient, similar to `.threat-build`)
   - `.spell-power-build` (purple/arcane gradient)
   - `.physical-build` (red/blood gradient)
   - `.mana-warning` (blue, for mana-related tips)
3. Build Table of Contents structure with all H2/H3 anchors
4. Add navigation links ("Back to Top")
5. **Deliverable**: Empty HTML structure with styled TOC

### Phase 2: Core Mechanics Content (Estimated: 10-12 hours)
**Tasks**:
1. Write **Introduction** section
2. Write **Race Selection** section with comparison logic
3. Write **Combat Mechanics** sections:
   - Threat System & Formulas (8 subsections, including formulas for all abilities)
   - Debuff Slots
   - Combat Table Mechanics
   - Block Mechanics
   - Spell Power vs Attack Power
   - Mana Management
   - Cooldowns (2 subsections)
4. **Deliverable**: Complete mechanics documentation with formulas in `.formula` class blocks

### Phase 3: Stat Priorities & Rotations (Estimated: 6-8 hours)
**Tasks**:
1. Write **Stat Priorities** section:
   - Stat conversion table (`.combat-table`)
   - AOE tanking priority (`.stat-priority` card, green gradient)
   - Boss threat priority (`.stat-priority` card, orange gradient)
   - Boss mitigation priority (`.stat-priority` card, blue gradient)
   - Comparative analysis (require chart data)
2. Write **Combat Rotations** section:
   - AOE rotation (`.aoe-tank` card)
   - Boss rotation (`.boss-tank` card)
   - Mana efficiency rotation
3. **Deliverable**: Stat priority and rotation guides

### Phase 4: Talents & Builds (Estimated: 3-4 hours)
**Tasks**:
1. Research optimal TBC paladin tank talent builds
2. Create 3 talent spec sections (AOE, Boss, Hybrid)
3. Link to external talent calculators (WoWHead TBC)
4. Build comparison table (`.combat-table`)
5. **Deliverable**: Talent build recommendations

### Phase 5: Consumables & Engineering (Estimated: 4-5 hours)
**Tasks**:
1. Research TBC consumables (elixirs, flasks, food, potions)
2. Write **Consumables** section with subsections:
   - Pre-raid consumables
   - Combat consumables
   - Raid buffs & debuffs
3. Collect cost data for cost-benefit chart (placeholder data acceptable)
4. Write **Engineering** section (Goblin vs Gnomish)
5. **Deliverable**: Complete consumable and engineering guides

### Phase 6: Gear Optimization (Estimated: 8-10 hours)
**Tasks**:
1. Research BiS gear for each set type:
   - AOE Threat Set
   - Boss Threat Set
   - Mitigation Set
   - Flask Set
   - OT Set
2. Research shield, weapon, and libram options
3. Write **Gear Optimization Strategy** section (6 subsections)
4. Create gear tables (`.combat-table`) with item names, sources, stats
5. **Deliverable**: Complete gear recommendations

### Phase 7: Enchantments & Professions (Estimated: 2-3 hours)
**Tasks**:
1. Research TBC enchantments for each slot
2. Write **Enchantments** section:
   - AOE tank enchants
   - Boss tank enchants
   - Enchanting profession benefits
3. Add profession-specific notes (JC, Leatherworking, etc.)
4. **Deliverable**: Enchanting guide

### Phase 8: Macros, WeakAuras, Addons (Estimated: 4-5 hours)
**Tasks**:
1. Write paladin-specific macros:
   - General (3-4 macros)
   - Tanking (4-5 macros)
   - Cooldowns (2-3 macros)
   - Utility (2-3 macros)
2. Research essential WeakAuras for TBC paladin tanks
3. Write **WeakAuras** section (7+ WeakAura recommendations)
4. Write **Addons** section:
   - General addons
   - Dungeons & raids
   - Paladin-specific
5. **Deliverable**: Macro, WeakAura, and addon guides

### Phase 9: Simulators & Sources (Estimated: 2-3 hours)
**Tasks**:
1. Research TBC paladin tank simulators and tools
2. Write **Simulators & Tools** section (3 subsections)
3. Compile **Sources & References** section
4. Add **Changelog** section template
5. **Deliverable**: Reference materials and tooling section

### Phase 10: Chart Integration (Estimated: 6-8 hours)
**Tasks**:
1. Implement Chart.js visualizations:
   - **Race comparison charts** (horizontal bar charts, 2 charts: Threat and Survivability)
   - **Stat scaling chart** (line chart showing TPS per stat point)
   - **Consumable ROI chart** (bar chart comparing gold cost vs TPS increase)
   - **Spell Power vs AP chart** (grouped bar chart comparing builds)
   - **Mana efficiency chart** (bar chart comparing rotation TPM)
2. Style charts to match dark theme
3. Add chart tooltips and legends
4. **Deliverable**: Functional, styled Chart.js visualizations

### Phase 11: Polish & Testing (Estimated: 3-4 hours)
**Tasks**:
1. Proofread all content
2. Verify all internal anchor links work
3. Test responsive design (mobile, tablet, desktop)
4. Verify all external links (talent calculators, WoWHead, etc.)
5. Add `.warning` and `.tip` callout boxes where appropriate
6. Ensure consistent formatting across sections
7. **Deliverable**: Publication-ready HTML guide

### Phase 12: Advanced Features (Optional, Estimated: 4-6 hours)
**Tasks**:
1. Add collapsible `<details>` sections for verbose content
2. Implement search functionality (Ctrl+F enhancement)
3. Add "Print-Friendly" CSS media query
4. Create shareable anchor links for specific subsections
5. **Deliverable**: Enhanced user experience features

---

## 5. Key Paladin-Specific Topics (vs Warrior Guide)

### A. Mana vs Rage Resource System
**Complexity: Medium**

**Key Differences**:
- **Mana regeneration**: Spirit-based regen (0.125 × Spirit) continues during combat for paladins
- **Spiritual Attunement**: Converts 10% of healing received into mana (unique paladin mechanic)
- **Seal of Wisdom**: Mana restore on melee swings (alternative to Seal of Vengeance)
- **Judgement of Wisdom**: Raid-wide mana restore on target attacks
- **Mana efficiency**: Paladins must balance threat output with mana consumption (unlike warriors who generate rage from damage)

**Content Requirements**:
- Mana management subsection under Combat Mechanics
- MP5 vs Spirit vs Spiritual Attunement gearing comparison
- Mana efficiency rotation (low-mana situations)
- Chart: Threat-per-Mana (TPM) for each ability

---

### B. Spell Power Scaling for Threat
**Complexity: High**

**Key Differences**:
- Paladins have **spell-based threat abilities** (Consecration, Holy Shield, Avenger's Shield) that scale with **Spell Damage**
- Warriors rely purely on physical stats (Hit, Expertise, AP, Crit)
- **Hybrid stat prioritization**: Paladins benefit from both Spell Damage (AOE threat) and AP/Hit/Expertise (single-target threat)

**Spell Power Formulas to Research**:
- **Consecration**: `Total Damage = 64 + (Spell Power × Coefficient × Ticks)`
  - Coefficient likely ~0.04 per tick, 8 ticks over 8 seconds, improved by talents (~1.15 multiplier)
- **Holy Shield**: `Proc Damage = 65 + (Spell Power × Coefficient)`
  - Coefficient likely ~0.05 per block
- **Avenger's Shield**: `Damage per Target = Base + (Spell Power × Coefficient)`
  - Coefficient likely ~0.07
- **Blessing of Sanctuary**: `Proc Damage = 35 + (Spell Power × 0.25)`

**Content Requirements**:
- Spell power formulas for each ability (`.formula` blocks)
- Chart comparing Spell Power vs Attack Power builds for threat
- Gear recommendations split by AOE (spell power) and Boss (physical) priorities

---

### C. Holy Shield / Redoubt Block Mechanics
**Complexity: High**

**Key Differences**:
- **Holy Shield**: Active ability (8s CD, 10s duration) providing +30% block chance and dealing damage on blocks
  - Near-100% uptime possible with Sacred Duty talent (reduces CD)
  - 4 block charges (consumes 1 charge per block)
- **Redoubt**: Proc buff (+30% block for 6 seconds) triggered by critical hits taken
  - Synergy with Holy Shield: Overlapping block buffs
- **Crush Immunity**: Achievable by block-capping (102.4% combined avoidance + block)
  - Formula: `Miss% + Dodge% + Parry% + Block% ≥ 102.4%`
  - Holy Shield enables crush immunity without excessive avoidance stacking

**Content Requirements**:
- Holy Shield mechanics subsection (uptime calculation, charge consumption)
- Redoubt + Holy Shield interaction explanation
- Crush immunity formula and gearing thresholds
- Block value scaling (Holy Shield damage and threat)
- Chart: Effective block% by gear level (with/without Holy Shield)

---

### D. 490 Defense Cap in TBC (vs 440 in Classic)
**Complexity: Simple**

**Key Differences**:
- **Classic**: 440 defense to become uncrittable (for level 60 tanks vs level 63 bosses)
- **TBC**: **490 defense** to become uncrittable (for level 70 tanks vs level 73 raid bosses)
  - Formula: `Defense Rating Required = (490 - 350 Base Defense) × 2.3654 = 331.116 Defense Rating`
- Defense provides:
  - +0.04% miss, dodge, parry, block per defense point
  - -0.04% crit chance taken per defense point

**Content Requirements**:
- Defense cap explanation (why 490?)
- Defense rating conversion formula (2.3654 rating = 1 defense skill)
- Stat priority emphasis on reaching 490 defense before all other stats
- `.warning` callout: Never tank raid bosses below 490 defense

---

### E. Paladin-Specific Threat Modifiers
**Complexity: Medium**

**Key Differences**:
- **Righteous Fury**: 90% increased Holy threat (with 3/3 Improved Righteous Fury talent)
  - Base Righteous Fury: 60% increased threat
  - Talent: +30% additional threat
  - Total modifier: `Base Threat × 1.9` for Holy damage and healing
- **Comparison to Defensive Stance**: Warriors get 1.3x threat modifier in Defensive Stance
  - Paladins have **46% higher threat modifier** than warriors (1.9 vs 1.3)
- **Holy damage abilities**: All Holy damage (Consecration, Holy Shield, Avenger's Shield, Seal of Righteousness, Exorcism) benefits from Righteous Fury

**Content Requirements**:
- Righteous Fury mechanics explanation
- Threat formula for each Holy ability: `(Damage × 1.9)`
- Comparison table: Paladin vs Warrior threat modifiers
- `.tip` callout: Paladin's threat advantage on AOE/trash

---

### F. No Taunt Until TBC (Righteous Defense)
**Complexity: Simple**

**Key Differences**:
- **Classic Paladins**: No taunt ability (major limitation)
- **TBC Paladins**: **Righteous Defense** (15s CD, 30-yard range)
  - Targets a friendly player
  - Taunts up to 3 enemies attacking that player
  - Transfers 100% of that player's threat to the paladin
- **Limitations**:
  - Cannot target self (must target a raid member being attacked)
  - 3-target cap (vs single-target taunt for warriors)
  - Longer CD than warrior Taunt (15s vs 8s)

**Content Requirements**:
- Righteous Defense mechanics explanation
- Macro for mouseover Righteous Defense (target ally, taunt their attackers)
- Comparison to warrior Taunt
- `.warning` callout: Righteous Defense limitations (cannot taunt boss directly if you don't have threat)

---

### G. Blessings, Auras, and Raid Utility
**Complexity: Medium**

**Key Differences**:
- **Blessings**: Paladins provide raid-wide buffs (Greater Blessings, 30-minute duration)
  - Blessing of Kings (+10% all stats)
  - Blessing of Sanctuary (damage reduction, mana on block/dodge/parry)
  - Blessing of Wisdom (mana regen)
  - Blessing of Might (attack power)
- **Auras**: Passive raid-wide buffs (40-yard range)
  - **Retribution Aura**: Deals Holy damage to attackers (threat generation for paladin tank)
  - Devotion Aura (armor)
  - Concentration Aura (interrupt resistance)
  - Shadow/Fire/Frost Resistance Auras
- **Judgements**: Debuffs on targets that benefit the raid
  - Judgement of Wisdom (mana on hit)
  - Judgement of Light (healing on hit)
  - Judgement of the Crusader (reduced armor, increased Holy damage taken)

**Content Requirements**:
- Blessing selection guide for tanks (Sanctuary for self, Kings for raid)
- Retribution Aura threat calculation (passive AOE threat)
- Judgement priority (Wisdom for mana-intensive fights, Light for healing)
- Raid utility comparison: Paladin vs Warrior vs Druid tanks
- `.tip` callout: Use Retribution Aura for passive AOE threat on trash

---

### H. Libram Slot Optimization
**Complexity: Low**

**Key Differences**:
- **Paladins** have a unique relic slot: **Libram**
- **Warriors** use ranged weapon slot (gun/bow/thrown for stat stick)
- Librams provide bonuses to specific paladin abilities

**Key TBC Librams for Tanks**:
- **Libram of Repentance** (SSC trash drop): +88 Consecration damage (best AOE threat libram)
- **Libram of the Lightbringer** (Badge vendor): +53 block value to Holy Shield (best mitigation libram)
- **Libram of Saints Departed** (Karazhan): Increases healing/threat on specific abilities

**Content Requirements**:
- Libram comparison table (`.combat-table`)
- Best-in-slot libram for AOE tanking (Repentance)
- Best-in-slot libram for boss tanking (Lightbringer or Repentance)
- Where to acquire each libram

---

### I. JC/Enchanting Profession Advantages
**Complexity: Low**

**Key Differences**:
- **Jewelcrafting** (TBC-exclusive profession):
  - Access to **Jewelcrafter-only gems**: +18 stamina gems (vs +12 for normal gems)
  - 3 unique gems can be equipped at once
  - Total bonus: +18 stamina over non-JCs (3 gems × 6 stamina difference)
- **Enchanting**:
  - **Ring enchants** (Enchanters only): +7.5 stamina or +12 spell damage per ring
  - Total bonus: +15 stamina or +24 spell damage (2 rings)
- **Comparison to Warrior Guide**: Warriors often take Engineering for threat/utility; paladins may prioritize JC/Enchanting for stats

**Content Requirements**:
- Profession comparison table for tanks
- Jewelcrafting: Best JC-only gems for tanks (+18 stamina gems)
- Enchanting: Ring enchant options (+stamina for mitigation, +spell damage for threat)
- Secondary professions: Leatherworking (Nethercobra/Nethercleft leg armor), Alchemy (flask duration, transmutes)
- `.tip` callout: JC + Enchanting gives +33 stamina total over non-crafters

---

## 6. Estimated Complexity by Section

| Section | Complexity | Est. Hours | Notes |
|---------|------------|------------|-------|
| **Introduction** | Simple | 0.5 | Overview, philosophy |
| **Race Selection** | Medium | 2-3 | Racial math, charts |
| **Combat Mechanics** | Complex | 8-10 | 8 subsections, formulas, charts |
| **Stat Priorities** | Complex | 4-5 | Multiple builds, comparative analysis |
| **Combat Rotations** | Medium | 2-3 | AOE, Boss, Mana rotations |
| **Paladin Builds** | Medium | 3-4 | 3 talent specs, comparison table |
| **Consumables** | Medium | 3-4 | TBC consumables, ROI charts |
| **Engineering** | Simple | 1-2 | Goblin vs Gnomish, gear |
| **Gear Optimization** | Complex | 8-10 | 6 gear sets, item research |
| **Enchantments** | Simple | 2-3 | Slot-by-slot enchants |
| **Macros** | Medium | 3-4 | 12+ paladin-specific macros |
| **WeakAuras** | Simple | 1-2 | 7+ WeakAura recommendations |
| **Addons** | Simple | 1 | PallyPower, general addons |
| **Simulators & Tools** | Simple | 1-2 | TBC tools, spreadsheets |
| **Sources & References** | Simple | 1 | Compile research sources |
| **Changelog** | Simple | 0.5 | Template for updates |
| **Chart Integration** | Complex | 6-8 | 5+ Chart.js visualizations |
| **Polish & Testing** | Medium | 3-4 | Proofing, testing, formatting |
| **TOTAL** | — | **50-65 hours** | Full implementation estimate |

---

## 7. Next Steps & Recommendations

### Immediate Actions
1. **Approve this plan** with any requested modifications
2. **Begin Phase 1** (HTML structure and CSS foundation)
3. **Start research tasks** in parallel:
   - Confirm all TBC formulas (Consecration, Holy Shield, Seal of Vengeance, etc.)
   - Gather BiS gear lists for each phase (Pre-raid, T4, T5, T6)
   - Collect consumable cost data
   - Research racial ability values

### Research Priorities (Critical Path)
1. **Spell power coefficients** for all abilities (required for formulas)
2. **Defense/stat rating conversions** (required for stat priority section)
3. **Block cap mechanics** (required for combat table section)
4. **Threat-per-Mana (TPM)** calculations (required for mana management and rotation sections)

### Optional Enhancements (Post-Launch)
- **Interactive Gear Optimizer**: JavaScript tool for comparing gear sets
- **Threat Calculator**: Input stats, output TPS
- **Video Embed**: Link to paladin tanking gameplay/guides (YouTube)
- **Multi-Language Support**: Translate guide to other languages (future)

---

## 8. Risk Assessment & Mitigation

### Risks
1. **Incomplete TBC data**: Some formulas/coefficients may not be publicly documented
   - **Mitigation**: Use private server research, archived forums (Elitist Jerks, Maintankadin), or estimate with disclaimers
2. **Chart.js complexity**: Advanced charts (multi-dataset) may require debugging
   - **Mitigation**: Start with simple bar charts, iterate to complex visualizations
3. **Scope creep**: Guide could expand beyond single-page HTML
   - **Mitigation**: Strict adherence to warrior guide format, use collapsible sections for verbosity
4. **TBC patch variance**: Different TBC patches (2.0 vs 2.4) have mechanical differences
   - **Mitigation**: Specify guide targets 2.4.3 (final TBC patch), note historical changes in changelog

### Success Criteria
- Guide matches warrior guide in quality, depth, and presentation
- All formulas are accurate and sourced
- Charts render correctly and provide actionable insights
- Guide is usable by both new and veteran paladin tanks
- HTML file is under 2MB (single-page, no external dependencies except Chart.js CDN)

---

## Conclusion

This implementation plan provides a comprehensive roadmap for creating a TBC Paladin Tanking Guide that mirrors the depth and quality of the existing Classic Warrior Tanking Guide. The dual-philosophy approach (AOE vs Boss tanking) is woven throughout the stat priorities, rotations, and gear sections, ensuring paladins understand when and how to optimize for each role.

**Estimated Total Effort**: 50-65 hours
**Primary Complexity Areas**: Combat Mechanics, Gear Optimization, Chart Integration
**Unique Paladin Content**: Mana management, spell power scaling, block mechanics, Righteous Fury threat modifier, Righteous Defense taunt, raid utility (blessings/auras)

The guide will serve as the definitive TBC paladin tanking resource, combining mechanical depth, practical optimization, and visual data presentation in a single, accessible HTML document.
