The Beautiful Game

Match Engine Appendix C — Match-Layer State Dynamics

An implementation appendix to the Match Engine Constitution v0.6. It defines the curves behind the states a match leaves on a club: how fit a player is, how settled the squad is, how well the club knows its system, how morale moves, and when fatigue becomes injury. Appendix D consumes these as the modifiers and the dispersion-narrowing it resolves a match with; Appendix A's line-strength sums lean on them.

Status — subordinate to the constitution. Everything here is a dial except the anchors in C.1. Uniquely among the appendices, C is written to a brief that already exists: Stress Test 2 specified four requirements and their degeneracy boundaries, and each curve below is shaped to hit them. The numbers remain starting values for simulation, not findings.

---

C.1 Constitutional Anchors

- Variance Before Mean, correctly applied. The earned states — cohesion and familiarity — express mainly as reliability: they narrow the band the seed draws within (D.7), they do not inflate the average. Fitness is different: it is not a benefit but a cost a manager spends and recovers, so it legitimately gates the mean (a tired player is worse), without being an advantage that stacks. Morale is a small, bounded mean modifier plus a stabiliser. This split is the whole reason C does not contradict the constitution.
- Match-layer only. Every state here is match-layer and writes nothing back to Ability, Form or market value. An injury is availability, never quality.
- No hidden anti-dominance. Fatigue and injury are transparent, fatigue-driven and seeded — a tiring side fades because it is tired, never because it was winning.
- Diminishing returns. Cohesion and familiarity both pay strongly early and flatten high (the constitution's Diminishing Returns), so settledness is worth pursuing and never worth hoarding.
- The Stress Test 2 brief. The four requirements — fitness meaningful but recoverable, injuries fatigue-driven not a lottery, rotation costing cohesion with a familiarity cushion, and depth mattering without being season-ending — are the targets C.9 is measured against.

---

C.2 Fitness (and Sharpness)

Each player carries Fitness on 0–100. A full match costs it; rest restores it.

Fitness −= MatchCost × (minutes ÷ 90); Fitness += Recovery × days_rest

FitnessMod(Fitness) maps it to the multiplier Appendix D.3 applies to a player's contribution — full near 100, falling to a floor (D.10) as a player tires. The cost and recovery are set so an ever-present player drifts down meaningfully across a six-match block and a single match's rest materially restores him: the rotation game lives between those two facts. Too shallow a cost and the best XI plays every game; too steep and quality is never on the pitch by midweek. Recovery may slow with age (a reality-synced input read, never written).

Sharpness is the mirror: a player starved of minutes loses a little edge, a small mean penalty recovered by playing. It is bounded and minor, but it is the reason a manager cannot simply bench everyone forever — over-resting has its own small cost, which keeps rotate-everything honest.

---

C.3 Morale

Team Morale on 0–100, baseline in the middle, moved only by football: results relative to expectation, run of form, and playing-time fairness. It is explicitly not moved by transfer rumours or any off-pitch information (the constitution's wall).

- It is bounded and mean-reverting — it drifts back to baseline over time, so a bad week dips it and a good week lifts it, but nothing spirals. This is where "runs end naturally" lives on the morale side.
- Cohesion damps the downswing: a settled side falls less far after a defeat and is harder to send into freefall.
- A playing-time term tracks fairness — a fringe player who never appears, or a starter benched without rotation, loses a little morale — which gives rotation a human cost on both extremes.

MoraleMod(Morale) is the small multiplier of D.3 (a tight band around 1.0). Small on purpose: morale is texture and momentum, never a lever that decides matches on its own.

---

C.4 Squad Cohesion

Cohesion is the relationship between players, accumulated from playing together. It is held at the level of combinations — pairings and units — and a given XI's cohesion is the aggregate of its players' shared history.

- It grows per shared start, with diminishing returns: the first dozen games a partnership plays together matter far more than the fiftieth.
- It decays slowly when players are apart and is lost when a player leaves — so heavy turnover, or constant rotation, fields lower-cohesion XIs.
- Its main effect is CohesionNarrowing, the larger (0.80) term that narrows dispersion in D.7: a settled side has fewer disasters and fewer flukes, not a higher average. It also lends a little tactical-execution and the morale-damping of C.3.

This is what makes a rotated XI not merely weaker but more erratic, and it is the cost side of the rotation trade-off. It is also the natural socket for the future Partnerships idea: a pairing-level refinement of exactly this accumulator.

---

C.5 Tactical Familiarity

Familiarity is the relationship between the club and a system — a formation-style-route package — and it is a club-level asset, not a player state. Each package the club plays carries its own score on 0–100.

- It grows per use of that package, with diminishing returns, and decays slowly when the package is set aside — slowly enough that a club keeps a repertoire rather than losing a system overnight.
- It persists through manager changes: a new manager inherits the club's repertoire and only lets it fade if he plays something else.
- It has two effects, matching the constitution's intent: a small mean lift (FamiliarityMod, D.3, a tight band) and, more importantly, a variance narrowing (FamiliarityNarrowing, the smaller 0.20 term in D.7).

The familiarity cushion is the crucial interaction Stress Test 2 demanded. Because familiarity is a property of the club's mastery of the system, not of which eleven play it, its narrowing applies to any XI fielding that package. So when rotation drops a lineup's cohesion, the club's system familiarity offsets part of the widened dispersion — and the offset scales with how mastered the system is. A club deep in its system rotates safely; a club mid-transition cannot. That is the entire reason cohesion and familiarity are two states and not one.

---

C.6 Injuries

Injuries arise mainly from fatigue, so that managing minutes is managing risk.

InjuryChance(appearance) = Baseline + FatigueMultiplier × (1 − Fitness/100), resolved on the match seed

- Fatigue-driven — a fresh player carries only the baseline; a spent one carries much more. The risk is therefore managed, not suffered: it is the consequence that makes rotation matter, not a die roll that punishes at random.
- Availability-only — an injury removes a player for a seeded duration and never touches his reality-synced Ability or value; he returns exactly as good as reality says. Real-world injuries apply too, via the Player Rating freeze; both sources are availability, both nothing more.
- Seeded and transparent — the same inputs and seed reproduce the same injury, so nothing is rigged and a winning side is never secretly broken.
- Frequency is a dial, and may be set to zero for a pure reality-mirror in which only real injuries remove a player.

Severity follows a distribution from knocks to longer lay-offs (a dial). Its bite scales with depth: an injury to a one-deep position forces a weak deputy, which is how the calendar gives squad-building its value (Stress Test 2).

---

C.7 The Handoff

C produces, and D and A consume:

- FitnessMod, MoraleMod, FamiliarityMod — the mean modifiers in the line-strength sums (A.3, D.3).
- CohesionNarrowing and FamiliarityNarrowing — the two terms that set the dispersion φ (D.7), split 0.80 / 0.20.
- Injury availability events — removing players for a duration, never altering their quality.

C reads minutes, results and lineups from the match record and Ability and age from the Player Rating Constitution. It writes to none of them.

---

C.8 Dials — starting values

All tunable; none a finding.

Dial| Starting value| Governs
MatchCost (per 90)| ≈ 35 fitness| how fast a starter tires
Recovery (per day rest)| ≈ 9 fitness| how fast he comes back
FitnessMod floor| ≈ 0.60| worst-case tired contribution
Sharpness penalty / floor| small / ≈ 0.95| cost of being under-played
Morale band (MoraleMod)| 0.90–1.10| how much morale can swing a side
Morale reversion| toward baseline each week| why nothing spirals
Cohesion growth per shared start| diminishing toward a cap| how fast a unit gels
Cohesion decay (apart / on exit)| slow / lost on transfer| the cost of churn
Familiarity growth per use| diminishing toward a cap| how fast a system is learned
Familiarity decay (unused)| slow| why a repertoire survives a change
Narrowing split (cohesion / familiarity)| 0.80 / 0.20| from D.7
Injury baseline / fatigue multiplier| low / the larger term| fresh risk vs tired risk
Injury frequency| a master scalar (0 = reality-mirror)| how much congestion bites
Injury severity| knock-to-layoff distribution| how long a player is lost

---

C.9 Calibration Targets

Measured against the Stress Test 2 brief, by simulation:

- An ever-present player is meaningfully tired by the back of a six-match block, and one match's rest materially restores him. Rotation is worthwhile; quality still reaches the pitch.
- Injuries are visibly fatigue-driven, always availability-only, and frequent enough that running one XI through a congested block is a real gamble — without becoming a lottery that decides seasons by luck.
- Rotation costs cohesion-variance; familiarity offsets part of it; and the offset scales with system mastery, so a well-drilled club rotates more safely than an unsettled one. Selective rotation beats both never-rotate and rotate-everything.
- A thin squad pays a real congestion tax, and depth has competitive value — but no single fatigue injury is season-ending.
- Cohesion and familiarity both show clear diminishing returns: settledness is richly rewarded early and barely at the margin, so trading and tactical change stay alive.
- Morale moves a bad week without spiralling, and no state ever acts as a hidden anti-dominance mechanic.

---

Relationship

Feeds Appendix D the mean modifiers (FitnessMod, MoraleMod, FamiliarityMod) and the two dispersion-narrowing terms (CohesionNarrowing, FamiliarityNarrowing), and feeds the availability events that injuries create; supplies the same modifiers to Appendix A's line-strength sums. Reads minutes, results, lineups, Ability and age from the match record and the Player Rating Constitution, and writes nothing back to any reality-synced value. Leaves the obvious socket for the future Partnerships system as a pairing-level refinement of Cohesion. With C in place, the three engine appendices close the loop: A asks what football a club is trying to play, C asks how well it knows its players and systems, and D asks what should have happened and what actually did.
