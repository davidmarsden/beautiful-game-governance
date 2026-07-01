The Beautiful Game

Match Engine Constitution v0.3

The football layer. Every other constitution exists to create the players, clubs, managers, money, information and decisions. This one determines what happens when two teams walk onto the pitch — and it is the only system in the project where genuine variance is allowed to live. Most of this document is about keeping that variance honest.

---

Purpose

To create believable football in which recruitment, squad-building, tactical planning and match management all matter, and in which no single formation, tactic or style is ever universally optimal. The objective is not perfect realism. It is football that rewards good decisions over many seasons.

---

Design Philosophy

Better players usually win. Better managers consistently outperform the level their players alone would suggest. Neither player quality nor tactics should ever dominate completely. The engine exists to test plans, not to validate formulas — its job is to discover whether a manager's plan survives contact with the opposition.

---

Constitutional Principles

No Universal Solution — no formation, tactic or style may hold a permanent advantage independent of context. Every approach must have strengths and weaknesses; one that is strong in one situation must be vulnerable in another. A dominant formation is a constitutional failure.

Context Matters — effectiveness depends on player quality, form, tactical suitability, the opposition's choices, match circumstances, familiarity and cohesion. No tactical choice can be judged in isolation.

Players Matter Most — recruitment is the foundation. Across a large sample the stronger squad wins; tactics never overwhelm quality. A great manager can improve a team, but cannot turn poor players into champions indefinitely.

Managers Matter Too — the right formation, style and selection for a given opponent produces real overperformance. The gap must be meaningful, and never decisive on its own. As a calibration anchor, squad quality should explain the large majority of long-run performance — on the order of 70–80% — and management the remainder, 20–30%: enough that a brilliant manager overachieves and a poor one underachieves, but neither ever escapes the squad he has assembled. The exact split is a dial, and the framework already leans this way.

No Tactical Omniscience — a manager decides before kickoff and through pre-defined match plans; he does not react with perfect knowledge as play unfolds. The plan is set, and the engine executes it. This keeps the game free of any live-management advantage — no result turns on who happened to be online at eight in the evening — and it is the same principle that lets match plans run automatically (Part 6). Reward engagement, not presence, holds on the pitch as everywhere else.

Football Before Mathematics — managers should think in football concepts — shape, pressing, mentality, balance, familiarity, cohesion — that are visible and understandable. Success should come from understanding football, not from reverse-engineering formulas.

Mastery Versus Flexibility — repeated use of a system builds familiarity that sharpens its execution but narrows adaptability. Constant tinkering builds nothing. A manager must balance mastering a system against staying flexible.

Continuity Versus Renewal — a settled squad develops cohesion; heavy turnover costs it. Keeping a team and rebuilding one can both be correct. Continuity should matter and perpetual churn should carry a price, but neither should dominate.

Uncertainty Belongs On The Pitch — ratings, scouting and contracts are deterministic. The match is the one place variance lives, and it comes from two sources: the competitive uncertainty of not knowing the opponent's plan in advance — manager versus manager, the project's core uncertainty — and the genuine sporting variance of the ball not always going in. Only the second is chance. Over a season the better teams rise; in a single match anything remains possible. The purpose of variance is to make football, not chaos.

Honest, Auditable Variance — the engine computes an expected performance both managers can see after the match, and variance is the transparent gap between the expected and the realised: you can outplay your expected goals and lose, exactly as in real football. Every fixture resolves from its inputs and a match seed, so the same inputs and seed always produce the same match — but the seed is published only after the fixture, never before. A result can always be audited, and never foreseen.

The Engine Reads Ratings, Never Writes Them — a match is played with what a player is, and never changes what he is. The engine reads Effective Match Rating; it never alters Ability, Form or market value, which are reality-synced (Player Rating Constitution). This single rule protects the entire model the rest of the project rests on.

On-Pitch Causes Only — a result is produced by football: selection, shape, tactics, fitness, morale, familiarity, cohesion, home advantage. It is never produced by media, press stances, Professionalism, Fan or Board Confidence, or money. Those are consequences of results, never inputs. Money reaches the pitch only through the squad it has already built — it raises the odds, never buys the day.

---

PART 1 — WHAT THE ENGINE READS

The only inputs to a result are footballing:

- Player quality — the Effective Match Rating (Ability + Form × 0.5) of each selected player, by position and role.
- Formation, style and tactics — shape and instructions, drawn from formation families and styles (Part 5).
- Match-layer states — fitness, morale, Tactical Familiarity and Squad Cohesion (Part 3).
- Home advantage — bounded and justified (Part 2).
- Manager preparation — selection quality and opponent-appropriate choices, including pre-set match plans (Part 6).

Explicitly not inputs: media, Professionalism, confidence, money. They sit downstream of results, never upstream.

---

PART 2 — HOW A MATCH RESOLVES

The model is transparent. All coefficients are dials.

Line strength by third — for each third (defence, midfield, attack):
LineStrength = Σ ( EffectiveMatchRating × RoleFit × Fitness × MoraleMod ) × FamiliarityMod, shaped by formation, its variance narrowed by CohesionMod.

Tactical interaction — each side's effective attack is set against the other's effective defence, modified by a published matrix of soft counters over formation families and styles (Part 5), in which no entry is dominant.

Expected performance —
ExpChances(A) = Tempo × EffAttack(A) ÷ ( EffAttack(A) + EffDefence(B) )
ExpGoals(A) = ExpChances(A) × ConversionRate( attacker quality vs keeper and defence ) × HomeFactor(if A at home)

Home advantage is not a magic number. It is anchored to three football causes: familiarity with the home pitch and surroundings; crowd influence, drawn from the club's organic stadium and fanbase size rather than volatile confidence, so it cannot spiral with results; and the travelling burden on the away side. Future formulas must trace to these anchors.

Resolution by seed — actual chances and conversions are drawn around the expected values using the fixture's match seed, with variance bounded by a dial and narrowed by the cohesion of each side. The expected figures and the seed are published after the match; the realised figures are the result. Same inputs, same seed, same match — but never visible before kickoff.

Over one match the gap between expected and realised can hand the game to the weaker side. Over a season, expected performance dominates and the table tells the truth.

---

PART 3 — MATCH-LAYER STATES

These states live entirely inside the match engine. None of them ever touches a reality-synced value.

Fitness — depletes with minutes, recovers with rest. Low fitness reduces contribution and raises injury risk. Managed through rotation and depth.

Morale — driven by football causes only: results, run of form, playing time, and fairness of rotation. A small, bounded, mean-reverting modifier — enough for momentum or a slump, never a spiral. It is deliberately not driven by off-pitch information: a player unsettled by transfer rumours (Information §3.5) carries that into the contract room, not onto the pitch. That link is a realism dial left off, to keep the wall between information and results intact.

Tactical Familiarity — a state attached to a club's use of a specific formation-and-style combination. It grows through repeated use and decays when the system is abandoned. High familiarity sharpens execution of that system but narrows adaptability — a mastered side plays its way beautifully, yet is more disrupted by a well-chosen counter or a forced change. This is the answer to "pick the perfect tactic every match": constant switching never accumulates familiarity, so it underperforms a mastered system, and many formations can coexist because each club masters its own. Growth and decay rates are dials.

Squad Cohesion — a state attached to the players, distinct from Familiarity. It grows from shared appearances and long-term partnerships and falls after major turnover. It improves morale stability and tactical execution, and narrows performance variance — a settled side has fewer bad days, which in the model literally tightens the band the seed can draw within. Familiarity is about the system; Cohesion is about the players. A manager may keep the XI but change system, or keep the system but rotate heavily — two independent levers — which is what makes both the settled team and the rebuild defensible choices.

Momentum — within-match swing; its detailed treatment is a dial for later.

Injuries — arise mainly from fatigue, rewarding rotation and depth. An in-game injury is an availability state only; it never alters a player's reality-synced Ability or value, and on return he is exactly as good as reality says. Real-world injuries apply too, via the Player Rating freeze. Injury frequency is a dial, and may be set to zero for a pure reality-mirror in which only real injuries remove a player. This is the one accepted, bounded divergence from reality, and it is the manager's to plan around.

The boundary, restated: fitness, morale, familiarity, cohesion, momentum and in-game injury are match-layer states. Ability, Form and value are reality. The first set never writes to the second.

---

PART 4 — WHAT THE ENGINE WRITES

- Score and match events.
- Match performance ratings — a per-player mark for how he played on the day, a descriptive output for the news layer (Information Part 2). It is not Form, and never feeds back into the reality-synced ratings.
- State updates — fitness, morale, familiarity, cohesion, momentum, injuries.

Results then feed the world: standings drive promotion and relegation (World) and the evaluation of every Contract Objective (World §7); they move Board Confidence and the sack race (Manager Career §5), Board Backing (Scouting & Finance §8), and Fan and Board Confidence (Information).

Results never feed Ability, Form, or market value. This is the wall the whole project leans on, and the match engine is where it is most tempting to breach and most important to hold.

---

PART 5 — THE TACTICAL METAGAME

The tactical layer must be understandable but never solvable.

- Formation families and styles — formations are grouped into families, and styles (pressing, possession, direct, counter-attacking, and so on) are chosen across them. The soft-counter matrix operates over families and styles, and no entry is strictly dominant.
- Trade-offs and soft counters — styles answer one another: a high press squeezes slow build-up but is exposed to pace and directness; possession control frustrates a deep block but can be frustrated by it in turn.
- Player-role fit — a system needs the players for it; the right idea with the wrong personnel underperforms.
- Hidden choices — neither manager sees the other's selection or setup in advance. This is the competitive uncertainty, alive inside the match.
- No win-button — no setting wins regardless of opponent or squad. Reading the matchup is the skill.

Formation Diversity is the test of balance: not that every formation wins equally often, but that multiple formations can win championships under capable managers. If only one consistently succeeds, the system has failed. The specific dimensions, instructions and matrix values are dials and future detail; this document fixes only that they must trade off, must depend on personnel, and must never resolve into a dominant solution.

---

PART 6 — MATCH PLANS AND SUBSTITUTIONS (future)

Managers may define conditional match instructions, substitutions and game-state responses — what to change when leading, chasing, a man down, or running out of time. These are executed automatically by the engine when their conditions are met. Because they are set in advance and run by the engine, a manager need not be present during a match — consistent with No Tactical Omniscience and with rewarding engagement, not presence (Information §1.1). The detail is for a later version; this document fixes that the layer exists and runs automatically.

---

PART 7 — WHERE THE GAME IS WON

Manager skill is expressed through selection, shape and tactics, opponent-specific preparation, pre-set match plans, and rotation that manages fitness, morale, familiarity and cohesion across a congested calendar — all resting on the squad the recruitment, contract and finance game has already built. The engine rewards every one of these, and rewards football knowledge above all. In any single match the seed can humble anyone; across a season, the manager who reads the game better wins more. That is the whole point.

---

Relationship to Other Constitutions

Reads Effective Match Rating, and so Ability and Form, from the Player Rating Constitution — and never writes back. Fields squads bound by the registration and squad rules of the World Constitution, with ownership settled there. Takes its players from the recruitment, contract and finance game that builds them. Sends results into the standings that drive promotion and relegation (World), Contract Objectives (World §7), the sack race and Board Confidence (Manager Career §5), Board Backing (Scouting & Finance §8), and Fan and Board Confidence (Information). Supplies match reports and per-match performance ratings to the news layer (Information Part 2), which narrates them and never adjudicates them. Honours, throughout, the reality-mirror the whole project is built on.

---

Golden Rule

The manager's job is to build a team and choose a plan. The engine's job is to discover whether that plan survives contact with the opposition. A match is played with what a player is, and never changes what he is. The better squad, better prepared and better read, wins more often across a season — but on any given day the engine tells you what you deserved and the seed tells you what you got. Uncertainty comes from the manager across from you, and from the honest bounce of the ball — never from a hidden hand, and never from anything that happened off the pitch.
