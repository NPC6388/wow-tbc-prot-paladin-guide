# Tankadin — Sixty Upgrades Stat Weights

Custom stat-weight scales for a TBC Protection Paladin, derived from the math in
this repo's guide (`index.html`). **Paste one scale at a time** into Sixty Upgrades
→ your set → *Edit Stat Weights* → *Custom*. Each fenced block below is a complete,
valid weights object.

Reference profile (matches the guide): T4/T5 raid gear, **709 spell power** raid-buffed,
1.80-speed 1H, 1.9× Righteous Fury, level 73 boss. Threat values are anchored to the
guide's TPS-per-point table (`#sp-vs-ap-analysis`); survival values to its mitigation /
combat-table math (`#stat-conversions`, `#block-mechanics`).

> **The two things the linear weights can't see — gate on these first:**
> 1. **Uncrittable** before anything else. Reach 490 Defense skill (raid) / 485 (heroic),
>    or top off with Resilience. Until then, Defense/Resilience are worth far more than any
>    number here.
> 2. **Uncrushable** = 102.4% combined dodge + parry + block + miss with Holy Shield up.
>    Don't let the optimizer gem/enchant you back under this hard cap.

---

## 1. Threat — Single Target (below caps)

Your daily driver until you hit the spell-hit / melee-hit / expertise caps.

```json
{
    "stamina": 0,
    "intellect": 0.1,
    "strength": 0.55,
    "agility": 0.05,
    "dodgeRating": 0,
    "parryRating": 0,
    "defenseRating": 0.04,
    "blockRating": 0.3,
    "blockValue": 0,
    "blockValueBonus": 0,
    "hitRating": 0.85,
    "expertiseRating": 1.1,
    "spellDamage": 1.5,
    "spellHitRating": 1.65,
    "health": 0,
    "resilienceRating": 0,
    "armor": 0,
    "metaSockets": 18,
    "redSockets": 13.5,
    "yellowSockets": 9,
    "blueSockets": 7
}
```

- Spell power is the anchor (1.35 TPS/pt → 1.5). Below their caps, spell hit (≈1.5 TPS)
  and expertise (≈1.0 TPS) are the strongest stats per point.
- `blockRating 0.3`: every block fires a Holy Shield + Blessing of Sanctuary threat event.
- Survival stats are zeroed — use the survival scales for those.

## 2. Threat — Single Target (at caps)

Same scale once you're spell-hit capped (17% / ~215 rating), melee-hit capped
(9%, or 6% w/ 3/3 Precision), and at 26 expertise. Those three drop to zero so the
optimizer stops chasing wasted itemization.

```json
{
    "stamina": 0,
    "intellect": 0.1,
    "strength": 0.55,
    "agility": 0.05,
    "dodgeRating": 0,
    "parryRating": 0,
    "defenseRating": 0.04,
    "blockRating": 0.3,
    "blockValue": 0,
    "blockValueBonus": 0,
    "hitRating": 0,
    "expertiseRating": 0,
    "spellDamage": 1.5,
    "spellHitRating": 0,
    "health": 0,
    "resilienceRating": 0,
    "armor": 0,
    "metaSockets": 18,
    "redSockets": 13.5,
    "yellowSockets": 9,
    "blueSockets": 7
}
```

## 3. Threat — AOE (heroics / trash / add fights)

Spell power is rescaled up because Consecration scales **per target** — it's the runaway
#1, so the red-socket value follows (9 SP × 2.5). Single-target-only stats (melee hit,
expertise, Strength touch just one seal-proc/auto target) fall in relative weight; Block
Rating rises (more attackers → more Holy Shield procs) and Intellect rises slightly
(Consec spam is the real mana sink).

```json
{
    "stamina": 0,
    "intellect": 0.15,
    "strength": 0.4,
    "agility": 0.05,
    "dodgeRating": 0,
    "parryRating": 0,
    "defenseRating": 0.06,
    "blockRating": 0.6,
    "blockValue": 0,
    "blockValueBonus": 0,
    "hitRating": 0.5,
    "expertiseRating": 0.7,
    "spellDamage": 2.5,
    "spellHitRating": 2.2,
    "health": 0,
    "resilienceRating": 0,
    "armor": 0,
    "metaSockets": 18,
    "redSockets": 22.5,
    "yellowSockets": 14,
    "blueSockets": 11
}
```

- Written **below caps**; zero `spellHitRating` / `hitRating` / `expertiseRating` once
  capped, same as scale 2.
- `blockRating 0.6` assumes you're not perma-charge-capped on Holy Shield (8 charges
  w/ Improved HS). On 4+ mobs you can exceed the charges, at which point extra block
  is pure mitigation — but it's still the strongest "defensive" threat stat.

---

## 4. Survival — Reaching / Maintaining Uncrushable

Use this while you're still climbing to (or fighting to hold) the 102.4% cap. Below the
cap, **every** point of avoidance and block deletes a 1.5× crushing blow, so Block Rating
(cheapest per rating) leads, and Dodge/Parry/Defense/Agility carry the crush-removal
premium too.

```json
{
    "stamina": 1,
    "intellect": 0.1,
    "strength": 0.02,
    "agility": 1.45,
    "dodgeRating": 1.76,
    "parryRating": 1.41,
    "defenseRating": 2.0,
    "blockRating": 2.54,
    "blockValue": 0.05,
    "blockValueBonus": 0.05,
    "hitRating": 0.1,
    "expertiseRating": 0.2,
    "spellDamage": 0.3,
    "spellHitRating": 0.1,
    "health": 0.08,
    "resilienceRating": 0.05,
    "armor": 0.06,
    "metaSockets": 18,
    "redSockets": 9,
    "yellowSockets": 9,
    "blueSockets": 12
}
```

- Block 2.54 is the anchor: 0.127% block/rating × ~0.9-hit crush-swing saved is the best
  mitigation-per-rating below the cap. Dodge/Parry get the same crush credit (1.76 / 1.41).
- `resilienceRating 0.05` assumes you're already crit-capped via Defense. **If you're using
  Resilience to *reach* crit immunity, it's near-mandatory — bump it to ~1.5+ until capped**,
  then drop it back.
- Blue is the top socket (Solid +12 stamina). Defense stays strong past 490 skill because
  its avoidance/block portions never cap — only the crit-reduction slice does.

## 5. Survival — Uncrushable / EHP (farm, geared)

Once you're comfortably uncrushable with Holy Shield up, block loses its crush premium
and falls to just block-value mitigation (≈ dodge per rating), while Dodge/Parry keep
full-avoidance value. This is the steady-state geared scale.

```json
{
    "stamina": 1,
    "intellect": 0.1,
    "strength": 0.02,
    "agility": 0.92,
    "dodgeRating": 1.06,
    "parryRating": 0.85,
    "defenseRating": 1.2,
    "blockRating": 1.02,
    "blockValue": 0.05,
    "blockValueBonus": 0.05,
    "hitRating": 0.1,
    "expertiseRating": 0.2,
    "spellDamage": 0.3,
    "spellHitRating": 0.1,
    "health": 0.08,
    "resilienceRating": 0.05,
    "armor": 0.06,
    "metaSockets": 18,
    "redSockets": 9,
    "yellowSockets": 9,
    "blueSockets": 12
}
```

- For spike-damage progression bosses, raise `stamina` to **1.3–1.5** to lean the leftover
  budget toward effective health (the guide's "stamina-vs-spell-power knob").
- Keep an eye on the uncrushable gate: a linear scale will happily trade block away once
  it's "only" worth 1.02 — re-check that you're still ≥102.4% combined after any swap.

---

## How the numbers are derived

**Threat** (anchored to `index.html` `#sp-vs-ap-analysis`, normalized to Spell Power = 1.5):

| Stat | Guide TPS/pt | Weight |
|---|---|---|
| Spell Power | 1.2–1.5 (≈1.35) | 1.5 (anchor) |
| Spell Hit (below cap) | 1.0–2.0 | 1.65 |
| Expertise (below cap) | 0.8–1.2 | 1.1 |
| Melee Hit (below cap) | protects seal procs/autos | 0.85 |
| Strength (= 2 AP) | 0.5–0.7 | 0.55 |

**Survival** (rating costs from `#stat-conversions`; "saved per rating" = damage-per-swing
prevented). Below the uncrushable cap the bottom of the combat table is a 1.5× crush;
at/above the cap it's a 1.0× normal hit:

| Stat | per 1% | saved/rating (below cap) | saved/rating (at cap) |
|---|---|---|---|
| Block | 7.88 | 0.114 (crush→block, ~0.9 saved) | 0.051 (block value only) |
| Dodge | 18.92 | 0.079 (full crush removal) | 0.053 |
| Parry | 23.65 | 0.063 | 0.042 |
| Defense | 2.37/skill | 0.091 (5 benefits) | 0.057 |

Stamina is the survival anchor (1 Sta ≈ 12.8 HP after Sacred Duty + Combat Expertise +
Kings); health = 1/12.8 ≈ 0.08. Armor ≈ 1 physical-EHP per point at raid armor levels,
discounted for the physical-only fraction → ≈0.06.

## Caps & gotchas (the binary stats)

- **Hit / Expertise / Spell Hit** — strong below their caps, **exactly zero above**. Switch
  from threat scale 1 → 2 when you cap them.
- **Defense** — its *crit-reduction* slice is worth ~∞ until 490 skill, then zero; its
  avoidance/block slices never cap. The weights above assume you're already at 490.
- **Resilience** — ~0 once crit-capped by Defense; near-mandatory if it *is* your route to
  crit immunity (PvP gear in heroics). Adjust per gear set.
- **Block Value** — does **not** feed Holy Shield threat in TBC (HS is flat damage + SP
  coefficient only); it's a pure survival stat, hence ~0 on every threat scale.
