# TODO: Spell Power Threat Set for Off-Tank / Not Taking Damage

## Concept
When not actively tanking (no incoming damage), ~85% of paladin threat scales with spell power. Mitigation/avoidance stats are wasted. Build a dedicated SP threat set that hits defense cap and crush cap minimums, then stacks spell power in every remaining slot.

## What Needs Work
- The specific gear swap recommendations in `max_threat_no_damage.html` are wrong — need accurate slot-by-slot BiS items for an SP threat set
- Research actual available spell power plate, caster jewelry, SP trinkets, etc. that work for this use case
- Verify defense cap (490) and crush cap (102.4%) can still be met with an SP-heavy loadout

## Constraints (Safety Net)
- 490 Defense — non-negotiable
- 102.4% combined avoidance with Holy Shield — stay uncrushable in case of emergency tanking
- Enough HP to survive a boss swing if MT dies

## Priority Stats (After Caps)
Spell Power > Spell Hit (until capped) > Spell Crit > Int (mana pool, especially important since Spiritual Attunement is offline)

## Context
- This is a third gear set alongside boss mitigation and AOE sets
- Used during off-tank phases where you're building threat without tanking
- See `max_threat_no_damage.html` for the full rotation and mana analysis
