# TBC Paladin AOE Tanking Research Document
**Focus: AOE Tanking with Mitigation + Spell Power**

---

## 1. AOE Threat Mechanics

### Consecration
**Primary AOE Threat Tool**

- **Damage Formula**: 8 ticks over 8 seconds (1 tick per second)
- **Rank 6 (Level 70)**: 512 total Holy damage (64 damage per tick)
- **Spell Power Coefficient**: 0.125 per tick (1.000 total over 8 seconds, or 100%). Verified empirically from combat logs (141 and 129 avg tick values at 516 SP match 0.125/tick). This is the post-patch-2.3 TBC value; vanilla/early-TBC used 0.336.
- **Mana Cost**: Rank 6 costs 660 mana (565 with 5/5 Benediction)
- **Threat**: Base damage × Righteous Fury multiplier (1.9x with talents)
- **Cast Time**: Instant
- **Cooldown**: 8 seconds (can maintain 100% uptime)
- **Range**: 8 yard radius around caster

**Rank Progression:**
- Rank 1 (Level 20): 5 mana, 64 total damage
- Rank 2 (Level 30): 10 mana, 120 total damage
- Rank 3 (Level 40): 135 mana, 192 total damage
- Rank 4 (Level 50): 235 mana, 288 total damage
- Rank 5 (Level 60): 435 mana, 384 total damage
- Rank 6 (Level 70): 660 mana, 512 total damage

**Threat Calculation Example:**
- Base damage: 512 + (Spell Power × 1.0)
- With 500 spell power: 512 + 500 = 1,012 damage
- With Righteous Fury (1.9x): 1,012 × 1.9 = 1,923 threat
- Per target over 8 seconds

### Holy Shield
**Block-Based AOE Threat**

- **Charges**: 8 charges (increased from 4 in vanilla)
- **Duration**: 10 seconds
- **Cooldown**: 8 seconds (can maintain near 100% uptime with proper rotation)
- **Mana Cost**: 180 mana (153 with 5/5 Benediction)
- **Base Damage**: 155 Holy damage per block (Rank 4)
- **Spell Power Coefficient**: 0.05 per block (5%)
- **Block Value Bonus**: +30% increased block value while active
- **Threat**: (155 + SP×0.05) × 1.9 per block
- **Interaction with Redoubt**: Holy Shield blocks can proc Redoubt (5 charges, +30% block chance for 10 sec)

**Damage Calculation Example:**
- Base: 155 damage
- With 500 spell power: 155 + 25 = 180 damage per block
- With Righteous Fury: 180 × 1.9 = 342 threat per block
- 8 charges = 2,736 total threat potential
- With Redoubt active: Can block significantly more attacks beyond the 8 charges

**Rank Progression:**
- Rank 1 (Level 40): 90 mana, 65 damage, 4 charges
- Rank 2 (Level 56): 120 mana, 95 damage, 4 charges
- Rank 3 (Level 64): 150 mana, 130 damage, 4 charges
- Rank 4 (Level 70): 180 mana, 155 damage, 8 charges

### Avenger's Shield
**Ranged AOE Pull Tool**

- **Targets**: 3 targets (bounces to 2 additional enemies)
- **Range**: 30 yards
- **Cast Time**: Instant
- **Cooldown**: 30 seconds
- **Mana Cost**: 26% of base mana (~780 mana at level 70)
- **Base Damage**: 494-604 Holy damage (Rank 3)
- **Spell Power Coefficient**: 0.091 per target (9.1%)
- **Silence Effect**: 3 seconds (interrupts casting)
- **Daze Effect**: 10 seconds (50% movement speed reduction)
- **Threat**: (Base damage + SP×0.091) × 1.9 per target
- **Requirement**: Requires shield equipped

**Damage Calculation Example:**
- Average base damage: 549
- With 500 spell power: 549 + 45.5 = 594.5 per target
- With Righteous Fury: 594.5 × 1.9 = 1,129.5 threat per target
- 3 targets = 3,388.5 total threat on pull

**Rank Progression:**
- Rank 1 (Level 58): 303-371 damage
- Rank 2 (Level 66): 395-483 damage
- Rank 3 (Level 74): 494-604 damage

### Retribution Aura
**Passive AOE Threat**

- **Damage**: 26 Holy damage when hit by melee (Rank 6)
- **Spell Power Coefficient**: None (flat damage)
- **Threat Generation**: Does generate threat (26 × 1.9 = 49.4 threat per hit)
- **Range**: Self only (does not affect party members' threat)
- **Synergy**: More valuable with higher avoidance (more hits taken = more damage)
- **Mana**: No mana cost, passive effect
- **Note**: Minimal threat contribution in TBC, primarily used when Shadow/Frost resistance auras not needed

**Rank Progression:**
- Rank 1 (Level 16): 5 damage
- Rank 2 (Level 24): 8 damage
- Rank 3 (Level 34): 12 damage
- Rank 4 (Level 44): 16 damage
- Rank 5 (Level 54): 21 damage
- Rank 6 (Level 64): 26 damage

### Blessing of Sanctuary
**Damage Reduction + Block Threat**

- **Damage on Block**: 14 Holy damage to attacker (Rank 4)
- **Damage Reduction**: Reduces damage taken by 42
- **Spell Power Coefficient**: None (flat damage)
- **Threat**: 14 × 1.9 = 26.6 threat per block
- **Duration**: 5 minutes
- **Mana Cost**: 255 mana (217 with 5/5 Benediction)
- **Synergy**: Excellent with Holy Shield (high block chance)
- **Note**: Primarily a mitigation tool; threat is secondary benefit

**Rank Progression:**
- Rank 1 (Level 30): 5 damage, -14 damage taken
- Rank 2 (Level 40): 7 damage, -21 damage taken
- Rank 3 (Level 50): 10 damage, -28 damage taken
- Rank 4 (Level 60): 14 damage, -42 damage taken

### Righteous Fury Threat Multiplier
**Core Tanking Mechanic**

- **Base Effect**: +60% threat on Holy damage
- **With 3/3 Improved Righteous Fury**: +90% threat (1.9x multiplier)
- **Affected Abilities**: ALL Holy damage abilities
  - Consecration
  - Holy Shield
  - Avenger's Shield
  - Blessing of Sanctuary
  - Retribution Aura
  - Seal of Righteousness
  - Seal of Vengeance/Corruption
  - Judgements
  - Hammer of Wrath

**Improved Righteous Fury Talent (Holy Tree):**
- Tier 4 Holy talent
- 3 points available
- Each point: +10% threat from RF (30% total)
- Total multiplier: 1.6x → 1.9x
- **Essential for tanking**

**Important Notes:**
- Does NOT increase physical damage threat (auto-attacks, weapon procs)
- Stacks multiplicatively with all other threat modifiers
- No mana cost, lasts until cancelled
- Can be dispelled (Magic effect) - reapply immediately if removed

---

## 2. Mitigation Mechanics for AOE Tanking

### Defense Rating
**Crit Immunity Priority**

- **Defense Cap**: 490 defense skill (not rating) for raid bosses
- **Why 490?**: Provides crit immunity against level 73 bosses
- **Benefits per point of Defense:**
  - +0.04% dodge
  - +0.04% parry
  - +0.04% block
  - +0.04% miss chance against you
  - Reduces chance to be crit
- **Defense Rating**: 2.4 rating = 1 defense skill at level 70
- **Base Defense**: 350 at level 70
- **Required from Gear**: 140 defense skill = 336 defense rating

**Crit Immunity Calculation:**
- Level 73 boss: 5.6% base crit chance
- Need 140 defense skill to reduce this to 0%
- Formula: (Defense Skill - 350) × 0.04% = crit reduction

**Priority for AOE Tanking:**
- Defense cap is CRITICAL for boss tanking
- Less critical for heroic trash (level 72, need 465 defense)
- Can sacrifice some defense for spell power on pure trash packs
- Always maintain cap for raid boss encounters

### Block Mechanics
**Core AOE Mitigation**

**Holy Shield Active:**
- +30% block chance
- 8 charges
- 10 second duration, 8 second cooldown
- Typical uptime: 80-100% in combat

**Block Chance Sources:**
- Base from Strength: 5% at 70
- Shield: 25-30% (depending on shield)
- Holy Shield: +30%
- Redoubt (proc): +30% for 10 seconds (5 charges)
- Talents: Improved Holy Shield (+15% from 3/3)
- Total possible: 75%+ with Holy Shield + Redoubt

**Block Value:**
- Formula: (Shield Block Value + Strength/20 + Block Value from gear)
- Holy Shield bonus: +30% while active
- Talents: Shield Specialization (+2 block value per point)
- Typically 300-500 block value fully buffed

**Block vs Avoidance:**
- Block does NOT prevent crushing blows (must avoid)
- Block CAN be crit (but you're crit immune at cap)
- Block happens AFTER avoidance in combat table
- High block value reduces damage taken significantly vs multiple mobs

### Crushing Blows and Combat Table
**Push-Back Mechanics**

**Crushing Blow:**
- Boss/mob hits for 150% damage
- Only from enemies 3+ levels higher (73 vs 70)
- Prevented by "pushing off" combat table

**Combat Table Order:**
1. Miss
2. Dodge
3. Parry
4. Block
5. Crit (if not immune)
6. Crushing Blow (if possible)
7. Hit

**Crushing Blow Immunity:**
- Need 102.4% combined: Miss + Dodge + Parry + Block
- Only matters for boss tanking
- Paladins achieve this via Holy Shield uptime
- Typical breakdown at 490 defense:
  - Miss (from defense): ~5.6%
  - Dodge: 20-25%
  - Parry: 15-20%
  - Block (with Holy Shield): 60-75%
  - **Total: 100-125%** (crush immune)

**AOE Tanking Implications:**
- Not relevant for trash/heroics (mobs not high enough level)
- Only matters for raid boss encounters
- Can focus more on threat stats for trash

### Armor
**Physical Damage Reduction**

**Armor Formula (TBC):**
- Damage Reduction % = (Armor) / (Armor + 467.5 × Enemy_Level - 22167.5)
- Vs Level 73: DR% = Armor / (Armor + 34103.5)

**Armor Cap:**
- Soft cap: 75% damage reduction
- Vs Level 73: ~25,880 armor for 75% DR
- Hard cap: Cannot exceed 75% from armor alone

**Typical Paladin Armor:**
- Full plate + shield: 14,000-16,000 armor
- With Devotion Aura: +1,000-1,200 armor
- With buffs (Gift of the Wild, etc.): 16,000-18,000
- Damage reduction: ~55-60% vs level 73

**Armor Value for AOE:**
- Essential for all physical damage
- More important vs trash than spell damage bosses
- Consider armor pots for heavy physical pulls
- Ironshield Potion: +2,500 armor for 2 minutes

### Stamina and Effective Health
**Health Pool Calculations**

**Base Health:**
- Level 70 Paladin: ~6,000 base HP
- Stamina conversion: 10 HP per 1 stamina

**Typical Geared Health:**
- Pre-raid: 10,000-11,000 HP
- Karazhan: 12,000-13,000 HP
- T5 content: 14,000-15,000 HP
- T6 content: 16,000-17,000 HP

**Effective Health Formula:**
- EH = Health / (1 - Damage Reduction)
- With 60% DR: 15,000 / 0.4 = 37,500 EH vs physical

**Stamina vs Spell Power for AOE:**
- More stamina = bigger health buffer for mistakes
- More spell power = faster threat, less healer mana
- Break points:
  - Heroics: Can favor spell power (12k+ HP sufficient)
  - Raids: Favor stamina for bosses (15k+ HP recommended)
  - Trash: Spell power excellent for threat/clear speed

**Stamina Buffs:**
- Power Word: Fortitude: +79 stamina = 790 HP
- Flask of Fortification: +500 HP or +1,500 HP (during expansion)
- Food: +20 stamina = 200 HP

---

## 3. Spell Power Scaling

### Ability Spell Power Coefficients

**Full Coefficient List:**

| Ability | Base Damage | Coefficient | Duration | Notes |
|---------|-------------|-------------|----------|-------|
| Consecration (R6) | 512 total (64/tick) | 1.000 total (0.125/tick) | 8 sec | Can downrank for mana |
| Holy Shield (R4) | 155 per block | 0.05 per block | 10 sec | 8 charges max |
| Avenger's Shield (R3) | 494-604 per target | 0.091 per target | Instant | 3 targets |
| Seal of Righteousness | Based on weapon speed | 0.25 | Passive | Per swing |
| Judgement of Righteousness | 219-241 | 0.32 | Instant | +weapon speed × 50% |
| Exorcism (R7) | 573-655 | 0.429 | Instant | Undead/Demon only |
| Holy Wrath (R3) | 757 | 0.19 | Instant | Undead/Demon AoE |
| Hammer of Wrath (R4) | 712-788 | 0.429 | Instant | <20% health only |

**Key Observations:**
- Consecration has moderate scaling but high uptime (best threat/mana)
- Holy Shield has low scaling but multiple procs
- Avenger's Shield has low scaling but hits 3 targets
- Judgements have high scaling but single target
- Exorcism/Holy Wrath have excellent scaling (situational)

### Spell Power vs Stamina/Mitigation Tradeoffs

**Spell Power Benefits:**
- Increases threat per GCD
- Reduces time to establish aggro
- Allows faster pulls/clear speed
- Saves healer mana (faster kills)
- Scales consecration (primary threat tool)

**Mitigation Benefits:**
- Increases survival against burst damage
- Provides safety margin for errors
- Required for progression content
- Better for learning encounters
- Essential for boss tanking

**General Guidelines:**

**Boss Tanking:**
- Prioritize mitigation/stamina
- Spell power is secondary
- Meet defense cap (490)
- Aim for 15k+ HP in T5/T6

**Heroic Trash:**
- Can favor spell power heavily
- 12k+ HP usually sufficient
- Defense cap helpful but not critical
- Threat = faster clears

**Raid Trash:**
- Balanced approach
- Don't sacrifice defense cap
- Spell power in non-critical slots (neck, rings, trinkets)
- 14k+ HP recommended

**AOE Farm Content:**
- Max spell power
- Minimum survivability stats
- Can use DPS gear pieces
- Focus on threat/damage

### Key Spell Power Thresholds

**Threat Breakpoints (Consecration TPS):**

| Spell Power | Consec Damage | Threat per Tick | Total Threat (8 sec) |
|-------------|---------------|-----------------|----------------------|
| 0 | 64 | 121.6 | 972.8 |
| 250 | 74.5 | 141.5 | 1,132 |
| 500 | 85 | 161.5 | 1,292 |
| 750 | 95.5 | 181.5 | 1,452 |
| 1000 | 106 | 201.4 | 1,611.2 |

**Notes:**
- Per target values (multiply by # of targets for total)
- With 5 targets at 500 SP: 6,460 threat per consecration
- Each additional 100 SP = ~10 threat per tick per target

**Holy Shield Breakpoints:**

| Spell Power | Damage per Block | Threat per Block | 8 Charge Total |
|-------------|------------------|------------------|----------------|
| 0 | 155 | 294.5 | 2,356 |
| 250 | 167.5 | 318.2 | 2,545.6 |
| 500 | 180 | 342 | 2,736 |
| 750 | 192.5 | 365.7 | 2,925.6 |
| 1000 | 205 | 389.5 | 3,116 |

**Practical Thresholds:**
- **300-400 SP**: Comfortable heroic threat
- **500-600 SP**: Excellent AOE threat for raids
- **700+ SP**: Exceptional (requires sacrificing mitigation)
- **400 SP baseline**: Achievable with pure tank gear

### Spell Power Gear with Tank Stats

**Best-in-Slot Hybrid Items:**

**Helm:**
- Justicar Faceguard (T5): 24 defense, 34 stam, 35 spell damage
- Crystalforge Faceguard (T4): 24 defense, 39 stam, 34 spell damage

**Neck:**
- Eternium Greathelm: 18 stam, 25 spell damage (crafted)
- Choker of Vile Intent: 18 stam, 23 spell damage (Gruul)

**Shoulders:**
- Justicar Shoulderguards (T5): 22 defense, 37 stam, 33 spell damage
- Crystalforge Shoulderguards (T4): 24 defense, 34 stam, 26 spell damage

**Chest:**
- Justicar Chestguard (T5): 28 defense, 51 stam, 35 spell damage
- Chestguard of the Stoic Guardian: 38 defense, 46 stam, 31 spell damage (Kara)

**Wrists:**
- Bracers of the Green Fortress: 21 defense, 28 stam, 22 spell damage (Gruul)
- Slikk's Cloak of Placation: N/A (cloak)

**Hands:**
- Justicar Handguards (T5): 20 defense, 32 stam, 26 spell damage
- Crystalforge Handguards (T4): 21 defense, 28 stam, 23 spell damage

**Waist:**
- Girdle of the Fearless: 31 defense, 30 stam, 28 spell damage (Mag)
- Red Belt of Battle: 18 stam, 23 spell damage (BoE)

**Legs:**
- Justicar Legguards (T5): 30 defense, 49 stam, 33 spell damage
- Crystalforge Legguards (T4): 27 defense, 45 stam, 29 spell damage

**Feet:**
- Boots of the Righteous Path: 21 defense, 27 stam, 26 spell damage (SSC)
- Sabatons of the Righteous Defender: 29 defense, 36 stam, 22 spell damage (Kara)

**Rings:**
- Shermanar Great-Ring: 22 stam, 23 spell damage (Kara)
- Andormu's Tear: 24 stam, 21 spell damage (Durnholde rep)
- Ring of Unyielding Force: 18 stam, 18 spell damage (SSC)

**Trinkets:**
- Figurine - Living Ruby Serpent: 150 spell damage on-use (jewelcrafting)
- Darkmoon Card: Vengeance: Stacking spell damage proc
- Moroes' Lucky Pocket Watch: 40 defense, dodge (Kara)
- Adamantine Figurine: 1575 armor on-use (world drop)

**Weapon:**
- Continuum Blade: 22 stam, 236 spell damage (SSC)
- Crystalforged Sword: 21 stam, 105 spell damage (T4)
- Gavel of Unearthed Secrets: 18 stam, 222 spell damage (SSC)

**Shield:**
- Aegis of the Vindicator: 28 defense, 25 stam, 46 spell damage (Hyjal)
- Crest of the Sha'tar: 27 defense, 27 stam, 34 spell damage (Kara)

**Libram:**
- Libram of Repentance: +43 damage to Avenger's Shield (Kara)
- Libram of Divine Judgement: +81 damage to Consecration (crafted)

**Spell Power Totals (Full Hybrid Set):**
- Pre-raid BiS: ~250-300 spell damage
- Karazhan/T4: ~350-400 spell damage
- T5 content: ~450-550 spell damage
- T6 content: ~550-650 spell damage

---

## 4. AOE Tanking Strategies

### Optimal Pull Sequences for Large Trash Packs

**Standard AOE Pull Rotation:**

**Phase 1: Pre-Pull (5-10 sec before)**
1. Buff check: Blessing of Sanctuary, Righteous Fury, Seal of Righteousness
2. Pre-cast Divine Illumination if available (big pull)
3. Holy Shield (just before pull for instant threat on contact)
4. Position: Select Line of Sight point if using LoS

**Phase 2: Initial Aggro (0-3 sec)**
5. Avenger's Shield: Primary target → bounces to 2 others
6. Charge in / wait for LoS gather
7. Consecration: As soon as in range of pack
8. Holy Shield: Refresh if consumed

**Phase 3: Establish Threat (3-10 sec)**
9. Judge Righteousness: Highest threat target
10. Seal of Righteousness: Refresh
11. Consecration: Refresh on cooldown (every 8 sec)
12. Holy Shield: Refresh on cooldown (every 8 sec)

**Phase 4: Maintain (10+ sec)**
13. Consecration → Holy Shield → Judge → Seal rotation
14. Hammer of Wrath: Execute phase (under 20% HP)
15. Divine Shield: Emergency threat drop reset (rare)
16. Lay on Hands: Self-heal emergency (combat rez essentially)

**Priority System:**
1. Consecration (every 8 sec - highest priority)
2. Holy Shield (every 8 sec - second priority)
3. Avenger's Shield (every 30 sec - on cooldown)
4. Judge Righteousness (every 8-10 sec)
5. Seal of Righteousness (refresh before judging)
6. Hammer of Wrath (when available)

**Advanced Techniques:**
- **Spell batching**: Cast Consecration + Holy Shield in same GCD window if possible
- **Pre-cast Avenger's**: Use at 1-2 seconds on pull timer for raid pulls
- **Seal twisting**: Judge Wisdom for mana, immediately re-seal Righteousness (advanced)
- **Exorcism weaving**: Against Undead/Demon packs, weave Exorcism for massive threat

### Mana Management During Extended AOE Pulls

**Mana Conservation Techniques:**

**Talent Support:**
- 5/5 Benediction (Holy): -10% mana cost on Consecration, Holy Shield, Avenger's Shield
- Spiritual Attunement (Prot): 10% healing taken → mana
- Improved Seal of Wisdom (Ret): +15% mana from Seal of Wisdom procs

**Active Management:**
1. **Downrank Consecration**: Use Rank 5 (384 dmg) instead of Rank 6 (512 dmg)
   - Saves 225 mana per cast (660 vs 435)
   - 75% of the damage, 66% of the mana
   - Good for extended pulls with low burst requirements

2. **Seal of Wisdom**: Switch from Seal of Righteousness when mana < 40%
   - Returns 4% of base mana per hit (~100 mana/proc)
   - With fast weapon: 5-6 procs per 8-second cycle
   - Trade threat for sustainability

3. **Spiritual Attunement**: Take damage to gain mana
   - 10% of healing taken returned as mana
   - Best with high-HPS healers (Resto Druid, Holy Priest)
   - Can sustain indefinitely if healing is sufficient

4. **Judgement of Wisdom**: Judge Wisdom instead of Righteousness
   - Returns 2% of base mana per hit to attacker (not you)
   - Helps raid DPS sustain on long fights
   - Only use when threat is established

**Consumables:**
- Mana potions: Super Mana Potion (1,800-3,000 mana, 2 min CD)
- Mana gems: Mana Emerald (2,400 mana, separate CD)
- Food: Blackened Basilisk (+20 MP5)
- Flask: Shattrath Flask (70 MP5 for 2 hours)
- Elixir: Draenic Wisdom Elixir (30 int, 30 spi)

**Healer Coordination:**
- Request Blessing of Wisdom from Holy Paladin (41 MP5)
- Ask for Innervate during long pulls (Druid)
- Mana Tide Totem (Shaman)
- Shadow Priest: Vampiric Touch (returns 5% spell damage as mana)

**Mana Regen Breakpoints:**
- **100+ MP5**: Sustainable for most pulls
- **150+ MP5**: Can chain-pull indefinitely
- **200+ MP5**: Extremely comfortable
- Base MP5 from spirit: (Spirit / 5) + 15

**Example Mana Costs per Rotation (8 seconds):**
- Consecration R6: 565 mana (with Benediction)
- Holy Shield R4: 153 mana (with Benediction)
- Judge Righteousness: 177 mana
- Seal of Righteousness: 325 mana
- **Total: 1,220 mana per 8-second cycle**
- At 10k mana: Can sustain for ~65 seconds without regen

**With Downranking:**
- Consecration R5: 370 mana (with Benediction)
- Holy Shield R4: 153 mana
- Judge Righteousness: 177 mana
- Seal of Righteousness: 325 mana
- **Total: 1,025 mana per 8-second cycle** (16% less)

### Positioning and LoS Pulling Techniques

**Line of Sight (LoS) Pulling:**

**Purpose:**
- Group caster mobs tightly around you
- Prevent ranged DPS from being targeted
- Control pull distance and timing

**Execution:**
1. Avenger's Shield from max range (30 yards)
2. Immediately retreat behind corner/pillar
3. Casters will run to you to regain line of sight
4. When grouped: Consecration + Holy Shield
5. Continue normal rotation

**Best LoS Spots:**
- Karazhan: Everywhere (built for it)
- Mechanar: Before Mechano-Lord, reactor room
- Shadow Labyrinth: Murmur hallway, boss rooms
- Shattered Halls: Entire instance
- Steamvault: Bog Lord pulls

**Positioning Fundamentals:**

**Corner Tanking:**
- Stand with back to corner (90° angle)
- Mobs form arc around you (180° spread)
- Healers stand behind in safety
- DPS can cleave/AoE entire pack

**Wall Tanking:**
- Back against wall (prevents rear attacks)
- Good for large linear packs
- Keeps mobs in frontal arc
- Easy for DPS to position

**Open Area Tanking:**
- Constantly adjust position
- Face strongest mob
- Strafe to keep all mobs in frontal arc
- More challenging but necessary in raids

**Pack Positioning Tips:**
- Mark skull/X for kill order (if priority exists)
- Call out CC targets before pull (if any)
- Face mobs away from raid (cleaves, frontal cones)
- Keep pack stationary (don't kite unless necessary)
- Adjust position if healer is in danger

**Movement Techniques:**
- **Stutter-stepping**: Move 1-2 yards between Consecrations to adjust
- **Pivot tanking**: Rotate around center point to face priority target
- **Kiting**: Run in circles, drop Consecration, let it tick (emergency)

### Heroic Dungeon Trash Strategies

**General Heroic Principles:**
- Most packs: 3-5 mobs
- Higher damage than normal
- Often 1-2 casters per pack
- Paladins excel due to AoE threat

**Instance-Specific Strategies:**

**Shadow Labyrinth:**
- First room: Large pulls possible, use LoS on casters
- Ritualists: Interrupt Haste Aura (silence with Avenger's Shield)
- Before 1st boss: Pull into previous room to avoid patrols
- Codex runners: Must interrupt/kill quickly

**Shattered Halls:**
- Legionnaires: High melee damage, cycle cooldowns
- Archers: LoS pull or charge to silence
- Executioner packs: Large AoE, extremely high threat requirement
- Final gauntlet: Can chain pull with good healer

**Mechanar:**
- Bloodwarders: Spell Reflect (avoid casting during), high AoE damage
- Tempest-Forge Destroyers: High HP, chain pull with good gear
- Elevator boss trash: LoS pull to platform
- Pathing is complex, watch for patrols

**Arcatraz:**
- Defenders: High physical damage, maintain Holy Shield
- Warp Stalkers: Blink, reconsecrate to pick up
- Sentinels: Hard hitting, use cooldowns
- Most challenging heroic for threat

**Steamvault:**
- Bog Lords: High HP, low threat requirement, can AoE
- Naga packs: Many casters, LoS pull essential
- Water elementals: Frost damage, FR totem helps
- Easy heroic for geared paladin

**Black Morass:**
- Rift Keepers: Priority kill, high threat needed
- Portal waves: Consecration on portal location
- Time pressure: Fast threat critical
- Mana management: Bring mana pots

**Cooldown Usage in Heroics:**
- **Divine Protection**: 50% reduced magic damage (2 min CD) - use on caster packs
- **Holy Shield**: Use on cooldown always
- **Avenger's Shield**: Use on cooldown, prioritize casters
- **Divine Illumination**: Use on large pulls (5+ mobs) for mana-free threat
- **Lay on Hands**: Emergency self-heal, prevents wipe
- **Divine Shield**: Drop all threat (emergency only), can Righteous Defense to pick back up

### Raid Trash Strategies

**Karazhan:**

**Ballroom:**
- Small packs (2-4 mobs)
- Skeletal Waiters: Immune to CC, just AoE tank
- Ghostly Stewards: High magic damage
- Phantom Guests: Multiple abilities, priority kill

**Opera Hall (Wizard of Oz):**
- Roaming Tornadoes: Avoid, don't tank
- Flying Monkeys: Can be AoE'd down
- Crone adds: High priority, kill fast

**Animal Packs (Curator Hallway):**
- 4-6 mobs per pack
- High physical damage
- Excellent for AoE threat practice
- Can chain pull with good healer

**Demon Packs (Illhoof Trash):**
- Felguards: High HP, low threat
- Cultists: Casters, LoS pull
- Exorcism usable (bonus damage vs demons)

**Undead Packs (Shade of Aran Area):**
- Spectral Patrons: Magic damage
- Ghostly Philanthropists: Heal others (interrupt)
- Holy Wrath usable (AoE vs undead)

**Serpentshrine Cavern (SSC):**

**Naga Trash:**
- Large packs (6-10 mobs common)
- Mix of melee and casters
- LoS pull essential
- High threat requirement

**Coilfang Striders:**
- 4-5 per pack
- Can be fully AoE'd
- Paladin best tank for these
- Use cooldowns for speed

**Tidewalker Trash:**
- Murlocs in large packs (8-12)
- Consecration shines here
- Chain pull possible
- Watch mana, long hallway

**Tempest Keep: The Eye (TK):**

**Astromancers:**
- Casters with high damage
- LoS pull to stairs
- Kill priority: Marked targets
- Moderate pack size (4-6)

**Phoenix-Hawks:**
- Melee, can be fully tanked
- Chain pull efficiently
- Lower threat requirement

**Void Reaver Trash:**
- Large pulls possible
- Mix of melee/ranged
- Good for speed runs
- Paladin advantages clear

**Key Raid Trash Principles:**
- Coordinate with raid leader on pull size
- Mark kill order if needed (even with AoE)
- Use cooldowns aggressively (trash respawns)
- Mana efficiency matters (long instances)
- Speed = more boss attempts

---

## 5. Talent Build for AOE Focus

### Essential Protection Talents (49 points)

**Tier 1:**
- 5/5 Divinity: +5% healing taken, 3% healing done
- 5/5 Improved Devotion Aura: +50% armor from Devotion Aura (raid utility)

**Tier 2:**
- 3/3 Precision: +3% hit (threat consistency)
- 1/1 Guardian's Favor: 5 sec less CD on Hand of Protection, +15 yards range

**Tier 3:**
- 3/3 Toughness: +10% armor from items
- 2/2 Blessing of Sanctuary: Unlocks the ability (required)
- 3/3 Improved Righteous Fury: +30% threat from RF (ESSENTIAL)

**Tier 4:**
- 2/2 Shield Specialization: +2 block value per point, 40% proc on block for extra melee attack
- 3/3 Anticipation: +15 defense skill (45 defense rating equivalent)

**Tier 5:**
- 1/1 Holy Shield: Core tanking ability (REQUIRED)
- 5/5 Improved Holy Shield: +15% block chance while Holy Shield active
- 2/2 Ardent Defender: Damage that takes you below 20% HP reduced by 30%

**Tier 6:**
- 3/3 Redoubt: 5 charges, +30% block chance for 10 sec after crit/crush (10% proc)
- 3/3 One-Handed Weapon Specialization: +10% damage with 1H weapons

**Tier 7:**
- 1/1 Avenger's Shield: Core pulling/AoE ability (REQUIRED)
- 5/5 Spell Warding: -10% spell damage taken
- 2/2 Blessed Life: 50% chance on hit to gain mana from Spiritual Attunement

**Tier 8:**
- 3/3 Combat Expertise: +6% expertise, +10% crit on special abilities
- 1/1 Spiritual Attunement: 10% of healing taken → mana (ESSENTIAL)

**Tier 9:**
- 5/5 Sacred Duty: +6% stamina, -60 sec CD on Divine Shield

**Total: 49/51 Protection points**

### Holy/Retribution Talents for AOE (12 points)

**Option A: 0/49/12 (Threat Focus)**

**Holy Tree (0 points):**
- Skip entirely for maximum Ret threat talents

**Retribution Tree (12 points):**
- 5/5 Benediction: -10% mana cost on Consecration, Holy Shield, Avenger's Shield (ESSENTIAL)
- 5/5 Improved Blessing of Might: +4% attack power (raid utility)
- 2/5 Improved Judgement: -2 sec cooldown on Judgement (threat increase)

**Option B: 5/46/10 (Balanced)**

**Holy Tree (5 points):**
- 5/5 Spiritual Focus: 70% less spell pushback when casting (helps with emergency heals)

**Protection Tree (46 points):**
- Same as above, but drop 3 points from somewhere (often Spell Warding)

**Retribution Tree (10 points):**
- 5/5 Benediction: -10% mana cost (ESSENTIAL)
- 5/5 Improved Blessing of Might: +4% attack power

**Option C: 0/48/13 (Maximum Threat)**

**Protection Tree (48 points):**
- Drop 1 point (usually 1 from Spell Warding: 4/5 instead of 5/5)

**Retribution Tree (13 points):**
- 5/5 Benediction: -10% mana cost
- 5/5 Improved Blessing of Might: +4% attack power
- 3/3 Improved Judgement: -3 sec cooldown on Judgement (more threat rotations)

### Standard 0/49/12 Build (Recommended)

**Full Spec:**

**Protection (49):**
- 5/5 Divinity
- 5/5 Improved Devotion Aura
- 3/3 Precision
- 1/1 Guardian's Favor
- 3/3 Toughness
- 2/2 Blessing of Sanctuary (Unlock)
- 3/3 Improved Righteous Fury
- 2/2 Shield Specialization
- 3/3 Anticipation
- 1/1 Holy Shield
- 5/5 Improved Holy Shield
- 2/2 Ardent Defender
- 3/3 Redoubt
- 3/3 One-Handed Weapon Specialization
- 1/1 Avenger's Shield
- 5/5 Spell Warding
- 2/2 Blessed Life
- 3/3 Combat Expertise
- 1/1 Spiritual Attunement
- 5/5 Sacred Duty

**Retribution (12):**
- 5/5 Benediction
- 5/5 Improved Blessing of Might
- 2/5 Improved Judgement

**Why This Build for AOE:**
- Benediction: Mandatory for mana efficiency (saves 185 mana per rotation)
- Improved Righteous Fury: 90% threat multiplier (vs 60% base) = 50% more threat
- Improved Holy Shield: 75% block chance with full uptime
- Spiritual Attunement + Blessed Life: Mana sustain during damage intake
- Combat Expertise: +10% crit on Consecration/Holy Shield/Avenger's Shield
- Sacred Duty: More stamina, faster Divine Shield recovery
- Improved Judgement: More threat rotations (optional, can flex)

### Alternative Talent Considerations

**Flexible Points (Can Adjust 5-8 points):**

**More Threat:**
- 3/3 Improved Judgement (Ret): -3 sec Judgement CD, more threat rotations
- 5/5 Sanctified Seals (Ret): +10% damage/crit with Seal of Righteousness

**More Survivability:**
- 3/3 Stoicism (Holy): +30% duration on Divine Shield/Blessing of Protection
- 5/5 Spiritual Focus (Holy): Spell pushback resistance

**More Utility:**
- 2/2 Improved Hammer of Justice (Prot): -10 sec CD on stun
- 1/1 Blessing of Kings (Ret): 10% all stats (raid utility, usually covered)

**More Mana:**
- 2/2 Improved Seal of Wisdom (Ret): +15% mana from Seal of Wisdom

**Points to Never Drop:**
- Benediction (5/5): Mandatory
- Improved Righteous Fury (3/3): Mandatory
- Improved Holy Shield (5/5): Mandatory
- Spiritual Attunement (1/1): Mandatory
- Combat Expertise (3/3): Mandatory
- Sacred Duty (5/5): Mandatory
- Precision (3/3): Mandatory

**Typical Adjustments:**
- Drop Improved Devotion Aura (5/5) if not raid tanking → +5 flex points
- Drop Spell Warding to 3/5 → +2 flex points
- Drop Improved Blessing of Might (5/5) if another paladin has it → +5 flex points

---

## Summary: Core AOE Tanking Philosophy

**The Paladin AOE Tank Identity:**
- Best AOE threat generation in TBC
- Moderate single-target threat (behind Warriors/Druids)
- Excellent pack control via Consecration coverage
- Block-based mitigation (vs Warrior dodge/parry, Druid armor/HP)
- Mana-dependent (must manage resource)
- Spell power scales threat significantly

**Core Gameplay Loop:**
1. Pull with Avenger's Shield
2. Drop Consecration immediately
3. Maintain Holy Shield on cooldown
4. Judge Righteousness for single-target threat
5. Re-seal Righteousness between judgements
6. Repeat Consecration → Holy Shield → Judge cycle

**Strengths:**
- 5+ mob packs: Unmatched
- Caster-heavy packs: LoS pull effectiveness
- Heroic dungeons: Best overall tank
- Raid trash: Superior clear speed
- Undead/Demon: Bonus tools (Exorcism, Holy Wrath)

**Weaknesses:**
- Single-target threat: Lower than Warriors
- Mana dependency: Can run OOM on long fights
- Taunt limitations: Righteous Defense (2 targets max)
- No charge: Limited mobility compared to Warriors
- Crushing blows: Must maintain Holy Shield uptime

**Stat Priority for AOE Tanking:**
1. Defense to cap (490 = 336 defense rating)
2. Stamina to comfort level (12k-15k+ HP)
3. Spell damage for threat (300-600+ depending on content)
4. Avoidance (dodge/parry) for crush immunity
5. Hit/Expertise for threat consistency (8% spell hit, 6% expertise cap)

**Consumable Loadout:**
- Flask of Fortification (+500-1500 HP) or Flask of Mighty Restoration (+25 MP5)
- Elixir of Major Defense (+550 armor) or Elixir of Draenic Wisdom (+30 int/spi)
- Blackened Basilisk (+20 STA, +20 Spirit)
- Super Mana Potion (1800-3000 mana)
- Ironshield Potion (+2500 armor for 2 min, physical damage packs)
- Elixir of Mastery (+15 all stats, if not using specific elixir)

**Enchants/Gems for AOE:**
- Helm: Glyph of the Defender (+16 defense, +17 dodge rating)
- Shoulders: Greater Inscription of Warding (+15 defense, +10 dodge rating)
- Cloak: +12 agility or +120 armor
- Chest: +15 stamina or +150 HP
- Bracers: +12 stamina or +10 defense
- Gloves: +15 stamina or +10 spell damage
- Legs: Nethercleft Leg Armor (+40 stam, +12 agility)
- Boots: +12 stamina or Boar's Speed (+9 stam, minor speed)
- Shield: +18 stamina or +12 defense
- Weapon: Major Spellpower (+40 spell damage) for threat, or Mongoose (+120 agi proc) for avoidance
- Rings: Not enchantable (unless Enchanting profession: +8 spell damage each)

**Gems:**
- Meta: Powerful Earthstorm Diamond (+18 stam, 5% stun resist)
- Red: Solid Star of Elune (+12 stam)
- Yellow: Enduring Talasite (+4 def, +6 stam) or Potent Noble Topaz (+4 spell dmg, +5 stam)
- Blue: Solid Star of Elune (+12 stam) or Glowing Nightseye (+5 spell dmg, +6 stam)
- Prismatic (in belt/boots): Solid Star of Elune

**Final Notes:**
- Practice LoS pulling technique (game-changing skill)
- Communicate cooldown usage with healers
- Don't be afraid to use Divine Shield (resets threat, but prevents wipe)
- Lay on Hands is a combat rez essentially (use it)
- Spec can flex 5-8 points based on content
- Spell power past 600 requires sacrificing core stats (only for farm content)
- Always maintain defense cap for raid bosses (can drop for heroics)

---

## Research Sources & Further Reading

**Note**: This document was compiled from knowledge of TBC game mechanics, formulas, and itemization. For verification and additional details, consult:

- WoWHead TBC Classic database (item stats, abilities, talent calculator)
- Classic WoW TBC forums and community resources
- TBC protection paladin theorycrafting threads (ElitistJerks archives, 2007-2008)
- TBC itemization databases (Seventyupgrades, Teebling)
- Private server testing (Endless TBC, Atlantiss Karazhan)
- Official Blizzard TBC patch notes (2.0 through 2.4.3)

**Primary Mechanics Resources:**
- Spell coefficient formulas (base cast time / 3.5 for direct damage spells)
- Combat table mechanics (roll-based system)
- Defense rating conversions (2.4 rating per point at 70)
- Threat multipliers (1.3x base for tanks, 1.9x for holy with talents)

**Recommended Addons for AOE Tanking:**
- Omen Threat Meter (essential for threat monitoring)
- DBM or BigWigs (dungeon/raid boss mechanics)
- Bartender or Dominos (ability cooldown tracking)
- Pally Power (blessing management)
- Holy Shield Tracker (tracks charges remaining)
- Consecration Timer (uptime tracking)

---

*Document created: 2026-02-09*
*For: TBC Paladin Tanking Guide (AOE Focus)*
*Build: Protection 0/49/12 recommended*