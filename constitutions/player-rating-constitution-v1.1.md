The Beautiful Game

Player Rating Constitution v1.1

Canonical document. Supersedes Player Rating Constitution v0.4 and Rating Formulas v3.1, consolidating the attribute definitions and their formulas into one place.

---

Design Philosophy

Player ratings must be:

- Transparent
- Deterministic
- Predictable
- Reproducible

Managers should never need to guess how ratings are calculated. Every rating must be independently verifiable using publicly available data and published formulas.

The competitive advantage comes from understanding football better than rival managers — not from understanding hidden game mechanics.

«Any two independent managers should be able to calculate identical ratings from identical inputs.»

---

Core Principles

1. Real Football Drives Everything

In-game activity never affects player ratings. Ratings are derived exclusively from real-world football data. Managers are rewarded for watching football, scouting talent, identifying trends and predicting development. The game rewards football knowledge, not game knowledge.

2. The Market Is The Best Judge

Football's transfer market already aggregates ability, form, reputation, age, potential, contract status, injury history and demand. No single public metric is perfect, but market value is the best available consensus estimate of a player's current standing. Transfermarkt market value is therefore the primary rating input.

3. Deliberate Information Lag

Ratings update on a fixed published schedule — prototype: monthly; full release: fortnightly or monthly. The gap between real-world developments and rating updates creates the scouting game. Managers who identify emerging talent before a refresh gain an advantage.

---

Constitutional Boundary

Player ratings describe footballers. They do not determine match outcomes.

Match outcomes are governed separately by team selection, tactical decisions, squad balance, fitness, morale, chemistry and Match Engine mechanics. A manager who recruits stronger players gains an advantage; a manager who deploys them intelligently gains a further advantage. The scouting game and the match game are distinct systems.

---

Description and Projection

Three of the four attributes are purely descriptive of present reality:

- Ability, Form and Reputation describe a player's current football standing from public information. They do not forecast future performance, transfers, market value or success.

Potential is the single forward-looking attribute — but it is not a forecast of an outcome:

- Potential publishes the deterministic ENVELOPE of plausible career ceilings implied by today's public data, and updates as that data changes.
- Where inside the envelope a player ultimately lands is never forecast by the game. That judgement belongs to managers.

The game provides information and a bounded projection. Managers provide the prediction.

---

The Four Attributes

Attribute| Question Answered
Ability| How good is this player right now?
Potential| How good could this player become?
Form| How well is this player performing right now?
Reputation| How respected is this player within football?

Each serves a distinct purpose. No attribute duplicates another.

---

ABILITY

Ability represents current footballing level. Scale 1–100. It is derived from current market value via the published Ability Curve, and is the single most important determinant of long-term player quality.

Ability Bands

Rating| Meaning
95–100| Generational
90–94| World Class
80–89| Elite
70–79| Established Top Division
60–69| Strong Professional
50–59| Squad Player
40–49| Prospect / Fringe
Below 40| Development Player

Ability Curve — Market Value Anchors

Market Value| Ability
€250m| 99
€200m| 97
€150m| 95
€120m| 93
€80m| 90
€50m| 86
€30m| 83
€20m| 80
€12m| 77
€7m| 74
€4m| 71
€2m| 68
€1m| 64
€500k| 60
€200k| 55
€75k| 50
€25k| 45
Below €25k| 40 (floor)

Interpolation (continuous, logarithmic — removes rating cliffs):

Ability = A_low + (A_high − A_low) × (ln V − ln V_low) ÷ (ln V_high − ln V_low)

Rounded to the nearest integer.

Worked check: €19m falls between €12m (77) and €20m (80) → ≈ 80. A €13m player ≈ 78. Value moves within an old "band" now move the rating.

The anchor table is published and version-controlled. Changes require public notice.

---

POTENTIAL

Potential defines a published range of plausible career ceilings — a deterministic envelope derived from public information. The game publishes the range; managers estimate the destination.

The game stores no landing point within the band. Because Ability tracks real football, where a player ultimately lands is produced by reality, not held by the system — unlike a player's preferences, which are a committed personality the game does hold (Contracts §3). Potential is therefore purely informational: a published envelope and nothing more, never a hidden forecast the game is keeping to itself.

Potential Regime

Potential is determined by the first matching rule.

Rule 1 — Veteran: Age ≥ 30 → Peak: X
Rule 2 — Post-Peak: Age ≥ 26 AND Peak Ability > Current Ability + 3 → Peak: X
Rule 3 — Mature: Age 26–29 → Ability ±1
Rule 4 — Late Development: Age 24–25 → Ability ±2
Rule 5 — Developing: Age 16–23 → Forward Projection

A player aged 25 or under always keeps a forward-looking projection and is never written off by a temporary slump. The post-peak override (Rule 2) catches genuine decline from age 26 and takes precedence over the mature bands.

Peak Display

Peak = Highest Recorded Ability. Permanent; once achieved it never decreases. A Peak display reflects historical achievement, not future projection.

Forward Projection (Ages 16–23)

Potential Band = [Centre − Width, Centre + Width]

Subject to: Lower Bound ≥ Ability, Upper Bound ≤ 100. A young player's band may never fall below current Ability.

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

TrajectoryFactor = clamp(1.0 + ValueGrowthModifier + PrecocityModifier, 0.5, 1.5)

Value Growth Modifier (market value change over previous 12 months)

Growth| Modifier
>100%| +0.40
+50% to +100%| +0.20
−25% to +50%| 0
−50% to −25%| −0.20
< −50%| −0.30

Precocity Modifier — Typical Ability benchmark

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

Worked example: 17-year-old, Ability 70, value up 60%. PeakGain 14; ValueGrowth +0.20; Gap = 70 − 52 = +18 → +0.30; TrajectoryFactor = clamp(1.50) = 1.50; Centre = 70 + 21 = 91; Width ±14 → 77–100.

---

FORM

Form measures recent real-world performance relative to expectation. Form is temporary; Ability is persistent. A sustained improvement first appears as Form; if it lasts long enough to lift market value, it becomes Ability. The same performance is never rewarded twice. Scale −5 to +5.

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

Intermediate values interpolated linearly.

Expected Floor: Expected = max(Expected, 0.10). This protects against extreme volatility among very low-rated players. No upper bound is required — the table peaks at 1.10 and Ability cannot exceed 100.

Form Formula

FormRaw = 5 × ((Actual − Expected) ÷ Expected) × LeagueWeight × MinutesConfidence

Form = clamp(round(FormRaw), −5, +5)

Ratio normalisation makes Form position- and ability-neutral: zero output maps toward −5, double the expected output toward +5, matching expectation gives 0.

League Weights

Tier| Weight
S| 1.00
A| 0.85
B| 0.70
C| 0.55
D| 0.40

Minutes Confidence = Minutes Played ÷ Maximum Window Minutes, capped at 1.0, where Maximum Window Minutes = Club Competitive Fixtures × 90.

Match Impact: Effective Match Rating = Ability + (Form × 0.5). Ability remains dominant; Form remains meaningful.

Worked example: forward, Ability 80, Expected 0.55, Tier S, full minutes, Actual 0.99 → FormRaw = 5 × (0.44 ÷ 0.55) = 4.0 → Form +4 → Effective Match Rating 82.

---

REPUTATION

Reputation measures accumulated football stature — achievement, recognition, status. It does not measure current footballing quality. Scale 1–100.

CareerStature = Highest Recorded Ability. Permanent; it never decreases. (This is the same recorded figure used for Peak Display.)

CapsScore

Caps| Score
0| 0
1–10| 20
11–25| 40
26–50| 60
51–80| 78
81–120| 90
120+| 100

Reputation = round(20 + (0.56 × CareerStature) + (0.24 × CapsScore))

Capped at 100. The coefficients are set so a maximum player (CareerStature 100, CapsScore 100) scores exactly 100. Because the Ability floor is 40, the practical Reputation floor is about 42 — the intercept of 20 is not a reachable value.

Reputation changes slowly, because CareerStature only ratchets upward and caps only accumulate. It influences player ambition, transfer attractiveness, wage expectations, fan interest and sponsorship value, and does not affect match performance.

Worked example: peaked at Ability 86, 70 caps (CapsScore 78) → round(20 + 48.16 + 18.72) = 87.

Future Extension: later versions may incorporate career longevity once reliable data exists. The prototype deliberately avoids variables that cannot be reproduced consistently.

Relationship to Profile: the Youth Discovery Constitution's Profile indicator may be derived directly from Reputation and public prominence data. No separate or hidden reputation system exists.

---

Rating Refreshes

Ratings refresh only on scheduled update days. No manual editing. No hidden boosts. No subjective intervention. Every manager can independently verify every rating change.

---

Exceptional Cases

Long-Term Injury — Ability frozen at pre-injury level; low minutes do not tank it. Form adjusted separately. Player marked Injured.

Retirement — mirrors real football. The game never decides retirement; players retire only when they retire in reality. On retirement the player is removed from active circulation.

Retirement Risk Indicator — advisory flag only. Age 30+ Low, 33+ Moderate, 36+ High. Informational; it never affects retirement outcomes.

New Database Entrants — initial Ability derived from market value via the Ability Curve; Potential generated immediately under the Potential Regime.

Position Changes — player reassessed under the new positional profile.

Missing Data — player marked Estimated until sufficient data exists.

---

Golden Rule

A manager should be able to inspect any player and understand exactly why he holds his current ratings, and independently reproduce every published attribute.

If an explanation requires administrator interpretation, the system has failed. If two independent managers cannot reproduce the same rating from the published rules, the system has failed.
