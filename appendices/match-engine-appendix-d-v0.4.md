The Beautiful Game

Match Engine Appendix D — Variance, Seed & Expected Performance

An implementation appendix to the Match Engine Constitution v0.6. It defines the spine of the engine: how team strength becomes an expected performance, how a seed turns that into a result, and how within-match momentum moves it about. Appendices A, B and C all feed or modulate the numbers defined here.

Status — subordinate to the constitution. Everything in this document is a dial except the anchors in D.1, which it may never contradict. The starting values below are sensible guesses, not findings; the curve shapes, coefficients and variance band can only be settled by simulation and playtest. This is a scaffold to test against, not a result.

v0.2 note — familiarity now narrows variance alongside cohesion (D.7), so a mastered system feels reliable, not merely sharp.

v0.3 note — narrowing split started more aggressively at cohesion 0.80 / familiarity 0.20 (D.10); a championship-floor calibration target added (D.11); and the open question of what ExpGoals represents flagged (D.5).

v0.4 note — the ExpGoals design note now logs a likely destination and a discipline: deserved performance probably decomposes into more than xG, but any such dimension becomes narrative before it becomes mechanics (D.5). The championship-floor target is sharpened into an ecosystem-usage target (D.11).

---

D.1 Constitutional Anchors

This appendix exists to serve these, and is wrong wherever it departs from them:

- Honest, Auditable Variance / You Deserved X, You Got Y — the engine computes and publishes an expected performance; the result is the transparent gap from it.
- Deterministic But Never Previewable — the match resolves from its inputs and a seed; the seed is published after the fixture, never before.
- Variance Before Mean — organisation narrows the spread of outcomes; it does not inflate the average. Cohesion makes a side reliable, not stronger.
- Calibration Anchor — squad quality should explain roughly 70–80% of long-run performance, management 20–30%.
- Two Sources Of Uncertainty — the opponent's hidden choices (handled upstream) and the honest bounce (the seed). Nothing else is chance.
- Reads Ratings, Never Writes Them; On-Pitch Causes Only — the engine consumes Effective Match Rating and never alters it, and takes only footballing inputs.

---

D.2 Inputs

D consumes, and does not redefine:

- EffectiveMatchRating(player) = Ability + Form × 0.5 — from the Player Rating Constitution.
- The selected XI, its formation and the role each player is asked to fill.
- TacticalMatchupFactor and the formation's shape weights — from Appendix A.
- The state modifiers Fitness, Morale, Familiarity, and the dispersion-narrowing effect of Cohesion — from Appendix C.
- Home advantage, from its three anchors (home familiarity, crowd from organic stadium and fanbase size, away travel burden).
- Tempo and attacking intent, from the chosen style.

---

D.3 Team Strength By Third

For each side and each third (defence, midfield, attack):

LineStrength(third) = [ Σ over players in that third of EMR(p) × RoleFit(p) × FitnessMod(p) × MoraleMod(p) ] × FamiliarityMod(side) × ShapeWeight(third)

RoleFit, FitnessMod, MoraleMod and FamiliarityMod are produced by Appendix C and A; their working ranges (D.10) are reproduced only so the strength figures here land sensibly.

---

D.4 Tactical Interaction

Midfield mediates the game:

ControlShare(A) = MidStrength(A) ÷ ( MidStrength(A) + MidStrength(B) )

Each side's effective attack and the opponent's defence are scaled by the matchup:

EffAttack(A) = AttackStrength(A) × TacticalMatchupFactor(styleA vs styleB) × Tempo(A)
EffDefence(B) = DefenceStrength(B) × TacticalMatchupFactor(styleB vs styleA)

TacticalMatchupFactor comes from Appendix A and is bounded close to 1 (working band 0.85–1.15) so that no style is a dominant counter — the No Universal Solution anchor expressed as a numerical ceiling.

---

D.5 Expected Performance — the xG-like spine

ExpChances(A) = BaseChances × Tempo(A) × ControlShare(A) × [ EffAttack(A) ÷ ( EffAttack(A) + EffDefence(B) ) ]

ExpGoals(A) = ExpChances(A) × ConversionRate(A) × HomeFactor(if A at home)

ConversionRate(A) rises with attacker quality relative to the opposing keeper and defence, around a low base (a chance is usually missed). ExpGoals(A) and ExpGoals(B) are the figures published to both managers after the match — the "what you deserved." BaseChances and ConversionRate are calibrated so average ExpGoals per side sits in a realistic range and so the squad-quality terms carry 70–80% of the variation across matches (D.1, D.10).

Design note (open) — this model treats ExpGoals as the deserved score: the result is a noisy version of it. That is simple, elegant and auditable, and it is the right place to start. But it collapses everything into one number, and football is messier: a side with 65% possession and xG 2.1 can lose 1–0 to a low-block counter that posted 1.2 and executed perfectly. The xG model calls that underperformance and luck; the football manager calls it a plan well carried out. Both are partly right.

The likely destination is not to dethrone xG but to surround it. Deserved performance probably decomposes into a small set of dimensions — Territorial Control, Chance Quality, Tactical Execution, Expected Goals — with xG remaining king, because goals are what is real, while the others let the match acknowledge a plan well executed.

The discipline that keeps this from becoming a trap: any such dimension becomes narrative before it becomes mechanics. Tactical Execution should first be something the news layer says — "Southall lost the xG battle 1.8–1.2 but executed their low-block counter exceptionally well" — and only later, if ever, earn mechanical weight. Football Manager's recurring error was turning every interesting story into another hidden number; here, a story stays a story until there is a proven reason to give it force. Not now, then — but logged, with its direction and its guard rail, so it is neither mistaken for settled nor allowed to creep in as a silent modifier.

---

D.6 The Seed

MatchSeed = a published hash of ( fixture id, season, round, date ). One seed per fixture, fixed when the fixture is scheduled.

- It seeds a published pseudo-random generator; the algorithm is documented, so any result can be recomputed and audited.
- It is never exposed before kickoff and is published only after the match. Reproducibility is for verification, not prediction (Deterministic But Never Previewable).
- There is no re-roll. The same inputs and the same seed reproduce the same match exactly, forever.

---

D.7 Resolution — turning ExpGoals into a score

Realised goals for each side are drawn around its ExpGoals using the seeded generator. The mean of the draw is ExpGoals; the spread is what cohesion controls.

Use a dispersion parameter φ on the goal draw (φ = 1 is Poisson, the chance-by-chance baseline):

φ(side) = φ_max − ( φ_max − φ_min ) × Narrowing(side)
Narrowing(side) = w_cohesion × CohesionNarrowing(side) + w_familiarity × FamiliarityNarrowing(side)

Two settled things narrow the band, for the same football reason — practice breeds reliability. Cohesion, players who know each other, is the larger term and is almost purely variance: a cohesive side barely plays better on average, it just stops suffering the 0–4 disaster. Familiarity, a system the club has mastered, is the smaller term but a real one: a long-run 4-3-3 is executed slightly better (its small mean lift via FamiliarityMod, D.3) and, more importantly, more reliably. So a low-cohesion side in a newly adopted system draws with φ above 1 (over-dispersed — volatile, prone to the thrashing and the collapse), while a settled side playing a mastered system draws with φ well below 1 (under-dispersed — fewer disasters and fewer flukes). The mean barely moves. This is Variance Before Mean made literal: organisation narrows the band the seed draws within, cohesion doing most of the narrowing and familiarity the rest.

A single master scalar, the Upset Factor, multiplies dispersion globally and is the chief knob for "how often does the better team win?" Set it high and the table is chaos; set it to zero and ExpGoals is destiny and football dies. It is tuned to the 70–80 / 20–30 anchor.

Because realised differs from expected, the side with the lower ExpGoals can win on the day — bounded by the band, and washed out over a season, where ExpGoals dominates and the table tells the truth.

---

D.8 Momentum — within the match

Within the simulated match, events move momentum: a goal lifts the scoring side's chance rate for a decaying window, and concedes the mirror to the other. It is a bounded, mean-reverting modifier on ExpChances during the run of play, drawn on the same seed.

- It is capped, so a lead compounds a little but never snowballs.
- Cohesion damps the downswing — a settled side is less likely to fall apart after conceding, the within-match face of Variance Before Mean.
- It lives only inside the match. It writes to no state afterward except through the result itself, which feeds morale via Appendix C. Momentum is texture, never a second engine.

---

D.9 Outputs

- ExpGoals(A) and ExpGoals(B) — published; the deserved performance.
- The realised score and the event sequence.
- The seed — published after the match, for audit.
- Per-player match performance ratings — derived from each player's contribution relative to his own expected contribution. These are descriptive, for the news layer (Information Part 2). They are not Form and never write back to any reality-synced value.
- The deserved-versus-got summary: ExpGoals beside the score, the post-match truth a manager can argue with honestly.

---

D.10 Dials — starting values

All are tunable; none is a finding.

Dial| Starting value| Governs
BaseChances| ≈ 11 per side| overall chance volume
ConversionRate base| ≈ 0.10 per chance| scoring level
ConversionRate quality span| ×0.6 to ×1.6| how much attacker quality matters
HomeFactor| ≈ 1.08| home advantage size
TacticalMatchupFactor band| 0.85–1.15| counter strength (A owns the matrix)
RoleFit range| 0.70–1.00| penalty for misused players
FitnessMod range| 0.60–1.00| effect of tiredness (C owns the curve)
MoraleMod range| 0.90–1.10| effect of morale (C owns the curve)
FamiliarityMod range| 0.97–1.06| small mean lift of system mastery (C owns the curve)
φ_max / φ_min| 1.40 / 0.70| dispersion at zero / high settledness
w_cohesion / w_familiarity| 0.80 / 0.20| how the two split the narrowing of φ
Upset Factor| 1.00| master variance scalar
Momentum boost / decay| +8% / halves per ~10 min| within-match swing size and persistence

---

D.11 Calibration Targets

What the tuning is aiming at, to be hit by simulation rather than derivation:

- Average goals per side land in a realistic range.
- Squad quality explains roughly 70–80% of long-run performance; management 20–30%.
- A clearly stronger side wins the single match often but far from always; evenly matched sides produce a healthy share of draws and upsets.
- Upsets occur and are memorable, but do not dominate a season.
- Cohesion is measurable: among sides of equal ExpGoals, the more cohesive show lower result variance.
- No formation family, once Appendix A is in, wins a disproportionate share of titles (the Formation Diversity test).
- And the floor matters more than the ceiling. The real test is not whether a family still wins the odd title on squad quality alone, but whether intelligent managers still choose to explore it at all. Balance fails at the bottom first: once managers believe a family is worse, experimentation stops, the metagame narrows, and eventually trading itself converges as every squad chases the same template. That is the true story of 4-2-3-1 — not that it was unbeatable, but that managers came to believe everything else was worse. So the target is usage, not trophies: every formation family should stay attractive enough that capable managers keep trying it. A family nobody plays has already failed, however many titles it could in theory still win.

---

Relationship

Consumes the tactical matchup and shape weights of Appendix A, the state curves of Appendix C, and Effective Match Rating from the Player Rating Constitution. Produces the results that drive standings, Contract Objectives, the sack race, Board Backing and Fan and Board Confidence, the runs that the Information Records Ledger remembers, and the match reports the news layer narrates. It writes nothing back to Ability, Form or value. It is, in the end, only the honest machinery behind a single line of the constitution: the engine tells you what you deserved, and the seed tells you what you got.
