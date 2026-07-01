The Beautiful Game

Match Engine Appendix A — Formation Families, Tactical Styles & Player Roles

An implementation appendix to the Match Engine Constitution v0.6. If Appendix D is the physics, this is where the football starts to look like football. It defines what a manager actually chooses — a shape, a style, and a role for each player — and how those choices become the strengths, routes to goal and matchups that Appendix D resolves.

Status — subordinate to the constitution. Everything here is a dial or a structure to test except the anchors in A.1. The role catalogue, the style list and the matchup values are starting points; whether they produce real football is a question for a hundred thousand simulated seasons, not for reasoning. A scaffold, not a result.

v0.2 note — adds Route to Goal (Central / Balanced / Wide) as a spatial layer distinct from style (A.4), so width becomes its own matchup axis; and caps the player lean at exactly three public archetypes (A.2, A.5), to hold the line against attribute creep.

v0.3 note — guards the Balanced route as robust-not-optimal (A.4), extends the Trade-Off Law's acceptance test to routes (A.6), adds a route-diversity calibration target (A.8), and logs set pieces as a deliberate future omission.

---

A.1 Constitutional Anchors

- No Universal Solution / Formation Diversity — multiple formation families must be able to win titles under capable managers; a dominant family is a bug, and balance is judged at the family level, not the formation label.
- Football Is A Game Of Trade-Offs — every tactical gain must create an exposure somewhere else. This is the generative rule behind No Universal Solution, and in this appendix it is a hard design law (A.6). A style or role that gains pressing, possession, chance creation and solidity at once is, by definition, a bug. (This idea may deserve elevation to a named constitutional principle; offered as a one-line Match Engine v0.7 amendment if wanted. Until then it governs here.)
- Players Matter Most, Managers Matter Too — roles let the right players overperform, within the 70–80 / 20–30 split. A great role choice improves a side; it never rescues poor players.
- Football Before Mathematics — shapes, styles and roles are football concepts a manager recognises, not stat spreadsheets.
- Variance Before Mean — a mastered system is more reliable (Appendix D.7), not simply stronger.
- Reads Ratings, Never Writes Them — roles read a player's Ability and position; they never alter them.

---

A.2 The Single-Rating Constraint (the central design decision)

The Player Rating Constitution gives each player one Ability, derived from market value, plus his real position. There is no hidden array of pace, passing and tackling. Roles must therefore be built on that single number, not on attributes the model does not have — anything else would betray the reality-mirror and turn the game into stat-reading rather than football knowledge.

So a role does not ask "what are this player's thirty attributes?" It asks two things the model does possess:

- Where does his quality land? A role places a player's Ability into a zone of the pitch and a job — defend, control, create, finish — and so into the line-strength-by-third and ControlShare sums that Appendix D consumes. The same 90-rated wide player pushed inside as an Inside Forward pours his quality into central chance creation and finishing; sent to Wing Back, he pours it into the wide defensive and control zones instead. One number, applied in different places, to solve different football problems.
- How well does it fit him? RoleFit (A.5) discounts a player asked to do a job far from his natural position — a winger at wing-back keeps most of his quality, a winger at centre-back keeps little. This is where positional Versatility (a Future Directions item) will eventually pay off: a genuinely versatile player carries a smaller penalty across more roles.

Optionally, and only from public, reality-derived signal, a player may carry a light lean — and exactly three are allowed, ever: Creator, Finisher, All-rounder. Nothing more. The lean is inferred from how real football already describes him (his goal-and-assist shape, his position), it nudges which jobs suit him, and it is never a hidden stat block; the baseline engine works without it. The three-archetype ceiling is deliberate and load-bearing: the moment it grows into ten leans it is halfway back to a thirty-attribute spreadsheet, and the Single-Rating Constraint is lost. Three keeps role variety honest — football knowledge about real players, not numbers the game invented.

---

A.3 Formation Families

Formations are grouped into families by underlying structure, and balance is judged at family level (a constitutional anchor), so tuning never chases 4-3-3 and 4-1-4-1 as if they were different problems.

Starting families:
- Back-Four families and Back-Three / Back-Five families (the defensive base).
- Single-Pivot and Double-Pivot families (how the midfield is anchored).
- Lone-Striker, Two-Striker and Wide-Forward families (the attacking apex).

A formation is a point in this space — 4-2-3-1 is back-four, double-pivot, lone-striker with wide support; 3-5-2 is back-three, double-pivot, two-striker. Each family carries a ShapeWeight, the distribution of player contribution across defence, midfield and attack that Appendix D.3 consumes, and a structural trade-off: a back three adds central defensive mass and wing-back width but thins central midfield unless the pivot compensates; two strikers add presence but cede a midfielder, and so on. The families and their weights are dials; that every family has a built-in give-and-take is not.

---

A.4 Tactical Styles and Routes to Goal

Style is chosen across formations, not within one. Each style is a different answer to the question Appendix D's ControlShare layer poses — how a side turns possession and territory into chances at all. This is why midfield mediates the game: there is more than one route to goal.

Starting styles and their routes:
- Possession — high ControlShare, patient chance volume; exposed to a compact block and to the counter when it loses the ball high.
- Counter / Transition — concedes ControlShare deliberately, converts turnovers into high-value chances; exposed to a side that refuses to over-commit.
- Direct — bypasses midfield control for early, lower-probability chances at higher volume; exposed to strong central defence.
- High Press — manufactures turnovers and territory; exposed to pace in behind and to being played through.
- Low Block — concedes territory to deny space and chance quality; exposed to patience and to set-piece and wide overloads.

Each entry names a gain and an exposure deliberately, because that pairing is the law of A.6. Tempo and intent are sub-dials of style. The catalogue is a dial; that each style buys its strength with a matching vulnerability is not.

Route to Goal — a separate, spatial layer, chosen alongside style rather than within it. Two sides can both play possession yet attack through different space, and that difference is often what really distinguishes real systems — Guardiola's width, Conte's wing-back overloads, Dyche's crossing volume, a classic 4-4-2's wide delivery are not possession-versus-counter distinctions, they are where the attack goes.

- Central — works the middle; beats a stretched or wide-committed defence, struggles against a packed centre.
- Balanced — no spatial bias: robust, not optimal. It carries fewer exposures than Central or Wide, but also less matchup upside — it is rarely badly countered and rarely lands a decisive spatial advantage. The generalist's choice, and deliberately not a free safe default: its weakness is precisely that it cannot exploit a specific opponent the way a committed route can. Robustness is its strength and its ceiling.
- Wide — attacks the flanks and the box from them; beats a compact, narrow centre, struggles against a disciplined wide block and strong full-backs.

Route to Goal carries its own trade-offs under the A.6 law, and it is what finally makes width matter: wing-backs, wide overloads and full-back quality become decisive against the right opponent, and a narrow possession side can be undone by a wide block it would beat through the middle. It interacts with formation family — a back-three / wing-back family is built for Wide, a narrow diamond for Central — so shape and route reinforce or fight each other. The three routes are a deliberate ceiling, like the three leans; the spatial axis must stay legible, not sprawl.

Set pieces — a central, decisive feature of real football — are deliberately not yet a route or a sub-route. They are a known rabbit hole that could quietly swallow the model, and the current structure is clean without them; they are logged in the Future Directions Register for a later, careful pass rather than omitted by oversight.

---

A.5 Player Roles and RoleFit

A role is a job within a shape and style: where a player operates and what he is asked to do. A position offers several roles — a wide attacker may be asked to be a Winger (Attack or Support), an Inside Forward, an Inverted Winger, a Wide Playmaker, a Shadow Striker, or a Wing Back — and each routes his single Ability into a different mix of zone and job.

RoleFit(player, role) = PositionalFit × LeanFit

- PositionalFit discounts distance from the player's natural position(s): 1.00 at home, falling as the role moves away, steeply once it crosses a line (attacker to defender). Versatility raises the floor.
- LeanFit (optional) nudges by the player's public lean — a finisher as a Shadow Striker fits better than as a Wide Playmaker — and sits at 1.00 when no lean is used.

RoleFit feeds the line-strength sum of Appendix D.3; the role's zone decides which thirds and which job (defend / control / create / finish) the player's quality counts toward.

The balance to find by simulation is the one you named: roles loose enough that the same squad can be set up several ways, so 4-4-2, 3-5-2, 4-2-3-1 and 4-3-3 ask players to solve genuinely different problems — but not so loose that every shape collapses into the same output, nor so strict that a manager feels railroaded into one "correct" role per player. PositionalFit steepness is the chief dial here, and it is explicitly a thing to tune, not to derive.

---

A.6 The Matchup Matrix and the Trade-Off Law

The TacticalMatchupFactor that Appendix D.4 consumes is produced here: a matrix of soft counters over families, styles and routes to goal, bounded close to 1 (working band 0.85–1.15) so that no entry is a hard counter and nothing is dominant.

The matrix is built under one law: every strength is entered with its exposure. A style that counters another must itself be counterable; a gain on one axis must cost on another. The acceptance test is blunt — if any single style, route or family shows a positive factor against the whole field, the matrix is broken and must be re-cut. This is the structural cure for "4-2-3-1 syndrome": the disease is not a formation, it is a cell that wins everywhere, and the law forbids that cell from existing.

Concretely, the rock-paper-scissors is many-dimensional rather than a single loop — press beats slow build-up, pace beats a high line, a low block beats the impatient, patience beats the low block — so it cannot be solved, only read. And it is read blind: the opponent's choice is hidden until kickoff (the competitive uncertainty), so the matrix is a game of anticipation, not of looking up the winning cell.

---

A.7 Dials — starting values

All tunable; none a finding.

Dial| Starting value| Governs
Formation families| 3 axes (defence / pivot / apex)| the structural space
ShapeWeight per family| defence/mid/attack split summing to 1| where contribution lands
Style catalogue| 5 styles + tempo sub-dials| routes to goal
Route to Goal| 3 (Central / Balanced / Wide)| the spatial axis; makes width matter
PositionalFit at natural position| 1.00| no penalty when used correctly
PositionalFit off-position floor| ≈ 0.55| how badly a misused player drops
PositionalFit cross-line penalty| steep| attacker-as-defender and the reverse
LeanFit range| 0.92–1.05| effect of a public creator/finisher lean
TacticalMatchupFactor band| 0.85–1.15| counter strength; no hard counters
Matrix acceptance test| no all-conquering cell| the Trade-Off Law, enforced

---

A.8 Calibration Targets

To be met by simulation, not derivation:

- Over many seasons, titles are won from more than one formation family (Formation Diversity).
- No style posts a winning matchup against the whole field (the Trade-Off Law holds in practice).
- A strong squad set up well beats a strong squad set up poorly often enough that roles matter, within the 70–80 / 20–30 split — never so much that tactics outweigh players.
- The same squad can be configured several credible ways, and different opponents reward different configurations (roles are loose enough).
- No single "correct" role emerges for each position regardless of context (roles are not too strict).
- No route to goal becomes universally preferred: Central, Balanced and Wide each produce successful teams in the right contexts. If width quietly becomes the default everyone reaches for, it is the old disease in new clothes.

---

Relationship

Supplies ShapeWeight, the style routes, RoleFit and the TacticalMatchupFactor to Appendix D, which turns them into expected performance and a result. Reads each player's Ability and natural position from the Player Rating Constitution and writes nothing back. Leans on the same reality-mirror as everything else: role variety is football knowledge about real players, never a hidden attribute array the game made up. Where it succeeds, the proof is simple — the football looks like football, and more than one way of playing it can win.
