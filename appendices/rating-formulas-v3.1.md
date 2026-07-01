The Beautiful Game

Rating Formulas v3.1

Companion to the Player Rating Constitution v0.4

---

Purpose

The Player Rating Constitution defines four player attributes: Ability, Potential, Form, Reputation.

This document provides the published formulas required to calculate each from public football data.

«Any two independent managers should be able to calculate identical ratings from identical inputs.»

No administrator interpretation is permitted. All values are deterministic. All calculations are reproducible. All formula constants are public.

---

Constitutional Boundary

Player ratings describe footballers. They do not determine match outcomes.

Match outcomes are governed separately by team selection, tactical decisions, squad balance, fitness, morale, chemistry and Match Engine mechanics.

A manager who recruits stronger players gains an advantage. A manager who deploys them intelligently gains a further advantage. The scouting game and the match game are distinct systems.

---

Description and Projection (revised)

Three of the four attributes are purely descriptive of present reality:

- Ability, Form and Reputation describe a player's current football standing using public information. They do not forecast future performance, transfers, market value or success.

Potential is the single forward-looking attribute — but it is not a forecast of an outcome either:

- Potential publishes the deterministic ENVELOPE of plausible career ceilings implied by today's public data. It updates as that data changes.
- Where inside the envelope a player ultimately lands is never forecast by the game. That judgement belongs to managers.

The game provides information and a bounded projection. Managers provide the prediction.

(This replaces the earlier "Ratings Are Descriptive, Not Predictive" wording, which read as denying the forward projection that Potential's Centre formula plainly performs.)

---

PART 1 — POTENTIAL

Purpose

Potential defines a published range of plausible career ceilings — a deterministic envelope derived from public information, not a prediction and not a hidden rating.

The game publishes the range. Managers estimate the destination.

---

Potential Regime

Potential is determined by the first matching rule.

Rule 1 — Veteran: Age ≥ 30 → Peak: X
Rule 2 — Post-Peak: Age ≥ 26 AND Peak Ability > Current Ability + 3 → Peak: X
Rule 3 — Mature: Age 26–29 → Ability ±1
Rule 4 — Late Development: Age 24–25 → Ability ±2
Rule 5 — Developing: Age 16–23 → Forward Projection

Peak Display

Peak = Highest Recorded Ability. Peak is a permanent career record; once achieved it never decreases. A Peak display reflects historical achievement, not future projection.

---

Forward Projection (Ages 16–23)

Band Structure

Potential Band = [Centre − Width, Centre + Width]

Subject to:

Lower Bound ≥ Ability
Upper Bound ≤ 100

A young player's band may never fall below current Ability.

Centre Formula

Centre = Ability + (PeakGain × TrajectoryFactor)

PeakGain

Age| PeakGain
16| 16
17| 14
18| 12
19| 10
20| 8
21| 6
22| 4
23| 3

TrajectoryFactor

TrajectoryFactor = clamp(1.0 + ValueGrowthModifier + PrecocityModifier, 0.5, 1.5)

Value Growth Modifier (market value change over previous 12 months)

Growth| Modifier
>100%| +0.40
+50% to +100%| +0.20
−25% to +50%| 0
−50% to −25%| −0.20
< −50%| −0.30

Precocity Modifier

Typical Ability benchmark:

Age| Typical Ability
16| 48
17| 52
18| 56
19| 60
20| 63
21| 66
22| 69
23| 72

Gap = Ability − Typical Ability(age)

Gap| Modifier
≥ +8| +0.30
+3 to +7| +0.15
−2 to +2| 0
−7 to −3| −0.10
≤ −8| −0.20

Potential Width

Age| Width
16| ±15
17| ±14
18| ±12
19| ±10
20| ±8
21| ±6
22| ±5
23| ±4

---

PART 2 — FORM

Purpose

Form measures recent real-world performance relative to expectation. Form is temporary; Ability is persistent. A sustained improvement first appears as Form; if it lasts long enough to lift market value, it becomes Ability. The same performance is never rewarded twice.

Scale: −5 to +5.

Actual Output (across the current refresh window)

- Forwards / Attacking Midfielders: Goals + Assists per 90
- Midfielders: Goals + Assists per 90
- Defenders: Clean Sheet Rate + ((Goals + Assists per 90) × 0.5)
- Goalkeepers: Clean Sheet Rate

Expected Output (by Current Ability and position)

Ability| Forward| Midfield| Defence
100| 1.10| 0.60| 0.55
90| 0.85| 0.45| 0.45
80| 0.55| 0.30| 0.38
70| 0.35| 0.18| 0.30
60| 0.20| 0.10| 0.22

Intermediate values are interpolated linearly.

Expected Floor

Expected = max(Expected, 0.10)

This protects against extreme volatility among very low-rated players. No upper bound is required: the table already peaks at 1.10 (a forward at Ability 100), and Ability cannot exceed 100, so Expected can never exceed 1.10. (The earlier explicit ceiling never bound and has been removed.)

Form Formula

FormRaw = 5 × ((Actual − Expected) ÷ Expected) × LeagueWeight × MinutesConfidence

Form = clamp(round(FormRaw), −5, +5)

League Weights

Tier| Weight
S| 1.00
A| 0.85
B| 0.70
C| 0.55
D| 0.40

Minutes Confidence

Minutes Played ÷ Maximum Window Minutes, capped at 1.0.

Maximum Window Minutes = Club Competitive Fixtures × 90.

Match Impact

Effective Match Rating = Ability + (Form × 0.5). Ability remains dominant; Form remains meaningful.

---

PART 3 — REPUTATION

Purpose

Reputation measures accumulated football stature — achievement, recognition, status. It does not measure current footballing quality.

CareerStature = Highest Recorded Ability. Permanent; it never decreases. (This is the same recorded figure used for Peak Display in Part 1.)

CapsScore

Caps| Score
0| 0
1–10| 20
11–25| 40
26–50| 60
51–80| 78
81–120| 90
120+| 100

Reputation Formula

Reputation = round(20 + (0.56 × CareerStature) + (0.24 × CapsScore))

Capped at 100. Because the Ability floor is 40, the practical Reputation floor is about 42.

Future Extension

Future versions may incorporate career longevity. The prototype deliberately avoids variables that cannot be reproduced consistently.

Relationship to Profile

Profile may be derived directly from Reputation and public prominence indicators. No separate or hidden reputation system exists.

---

Result

All four player attributes are fully reproducible.

Attribute| Derived From
Ability| Market Value → Ability Curve
Potential| Forward Projection or Peak Display
Form| Relative performance vs Expected Output
Reputation| CareerStature + International Caps

No administrator interpretation. No hidden ratings. No hidden modifiers.

---

Golden Rule

A manager should be able to inspect any player and independently reproduce every published attribute.

If a rating cannot be derived from public data and published formulas, the system has failed.
