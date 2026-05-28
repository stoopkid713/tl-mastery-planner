# Throne & Liberty — Weapon Mastery Planner

Interactive calculator for planning weapon mastery progression in **Throne & Liberty**.

**Live tool:** https://stoopkid713.github.io/tl-mastery-planner/

## What it does

- **My Setup** — toggle the 6 mastery buff sources (Amatori, Pal Synergy, Guild Blessing, Mastery Report, Golden Apple Pie, Black Anvil) and see live stats: total mastery %, token efficiency %, XP per token, multiplier vs bare.
- **Weapon Planner** — set weekly token burn and per-weapon current/target levels; see XP needed and weeks to complete at both your current buff stack and a full stack.
- **Session Calc** — input tokens to burn + starting level → levels gained, with a comparison table across 5 buff scenarios.
- **Lookup Table** — full L0–L200 per-level XP, cumulative XP, and XP-to-max.

## Model

The XP curve is a **quartic polynomial** fitted to 23 measured data points from in-game screenshots across 5 anchor zones (L50–54, L80–84, L100–103, L130–134, L170–174). Max residual: **±0.077%** across all measured points. The curve is weapon-type independent.

- Cost at L200: **19,253,922 XP**
- Total XP to take a weapon from 0 → 200: **1,186,206,907 XP**
- Base XP per base token (no buffs): **638.7** (derived from 31,935 base XP / 50 base tokens, Mutant Slaughterer dataset)

## Formulas

```
Mastery XP   = Base_Mob_XP × (1 + Total_Mastery_Bonus%)
Tokens/kill  ≈ floor(Base_Tokens / (1 + Efficiency%))
XP per token = 638.7 × (1 + mastery%) × (1 + efficiency%)
```

## Run locally

```bash
python -m http.server 7772 --directory .
# then visit http://localhost:7772
```

Single-file static site — no build step, just HTML + Chart.js from CDN.
