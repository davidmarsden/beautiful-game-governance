The Beautiful Game

Match Engine Appendix B — Game States, Match Plans & Substitutions

An implementation appendix to the Match Engine Constitution v0.6. It defines how a manager's prepared intentions execute inside the ninety minutes that Appendices A, C and D resolve: the game states the engine recognises, the plans a manager sets for them, the substitutions he spends, and the deterministic rule that decides which plan fires when several apply at once.

Status — subordinate to the constitution. Everything here is a dial or a structure except the anchors in B.1. The state set, the sub count and the priority order are starting points for simulation, not findings.

---

B.1 Constitutional Anchors

- No Tactical Omniscience, made concrete. A manager decides before kickoff and through pre-defined plans; he does not react with perfect knowledge during play. This is the appendix that turns that principle into machinery, so it is the one most exposed if the principle slips.
- Reward engagement, not presence. In-match skill is anticipation — foreseeing the states a match can reach and preparing for them — never attendance. Being online during a match confers no advantage, by hard rule (B.7). No result turns on who was watching at the time.
- A tactic is a set of plans. A single setup is not a tactic; a tactic answers leading, trailing, late, a man down, extra time. The base plan plus its game-state responses are the unit.
- Deterministic. Triggers are deterministic functions of the match state and the seed; B introduces no new randomness, and the same match reproduces the same plan execution forever.
- Match-layer only. Plans and subs change Appendix D's inputs for the rest of the match; they write nothing back to any reality-synced value.

---

B.2 Game States

At every moment a match has a current game state, computed deterministically from:

- Score — leading or trailing and by how much, or level.
- Time — opening, settled, late, closing; and, in knockout football, extra time.
- Personnel — at full strength, down to ten (or fewer), or facing ten.
- Context — league or knockout, must-win, the tie on a knife-edge.

A state is the set of these that are currently true — "trailing, late, a man down" is one state. Which distinctions the engine draws is a dial; that a match always has a computed state, and that a tactic should answer more than one, is not.

---

B.3 Match Plans

Before kickoff a manager sets a base plan — the shape, style and route of Appendix A — and any number of conditional plans, each a trigger and an action:

- Trigger — a game state ("leading by one or more after the 70th minute").
- Action — a change expressed in Appendix A's vocabulary: shift style or route, adjust tempo, change shape or a role, or make a substitution.

The engine evaluates the match state continuously and fires the matching plan automatically. A manager may set one plan or many; setting none for a state simply continues the base plan, at the cost of not having adapted, never a penalty beyond that.

Plan depth has diminishing returns by design. Sensible responses to the common states — protecting a lead, chasing a deficit, closing out, going a man down — capture almost all the value; obsessively scripting rare states yields little, because they rarely fire. This is deliberate: preparation is rewarded, but micro-scripting is not, so the layer cannot become a clicking treadmill in slow motion. Skill is foreseeing what matters, not enumerating everything.

---

B.4 Substitutions

Substitutions are a limited resource — a capped number across a capped set of windows (a dial; five across three is a sensible start). Spending them is part of the plan.

- A planned substitution is an action inside a match plan (B.3).
- A forced substitution from injury (Appendix C) consumes a substitution and a window like any other. So injuries do not only remove a player — they spend tactical flexibility, which is another way congestion and a thin squad bite, and another reason depth has value.
- A substitution trades along Appendix C's grain: a fresh sub restores fitness but may cost quality (the bench gradient) and pairing cohesion (a less-drilled combination, slightly wider variance). Bringing on fresh legs late is a real decision, not a free upgrade.

A substitution changes Appendix D's line-strength sums for the remainder of the match.

---

B.5 The Priority Hierarchy

When several conditional plans apply at once — leading after seventy minutes and down to ten men — the engine resolves them deterministically, by two published rules in order:

1. Specificity beats generality. A plan whose trigger matches more of the current state wins. A manager who has set a combined "leading and a man down" plan sees it fire ahead of his separate "leading" and "a man down" plans. Foreseeing the combination is rewarded, and it is the manager's own preparation that resolves the conflict, not the engine guessing.

2. Category priority breaks ties. Where two applicable plans are equally specific, the higher-priority category wins, in a published order: personnel state (the numbers on the pitch) over score-and-time state over general phase. Reshaping to eleven-versus-ten is more fundamental than protecting a lead, so absent a combined plan, the personnel plan takes precedence. The category order is a dial; that resolution is deterministic and specificity-first is the structure.

If no conditional plan matches, the base plan continues. Nothing here is decided live; it is all a pre-published rule applied to a computed state, so No Tactical Omniscience holds even at the moment of conflict.

---

B.6 The Familiarity Interaction

A plan's change lands as cleanly as the club knows the destination. Shifting into a shape, style or route the club is familiar with (Appendix C.5) executes smoothly — the system's variance-narrowing carries the transition. Shifting into something the club rarely plays is shaky: the change adds variance rather than control, because the players are improvising a system they have not drilled.

So in-match adaptation is bounded by the repertoire. A manager who wants to shut up shop when leading should have a low block his club actually knows, not one it invents in the 78th minute. This rewards building a repertoire that includes your game-state answers, and it is the same truth as everywhere else in the engine: a club can only reliably do what it has practised.

---

B.7 No Live Intervention

The engine never waits for, accepts, or rewards live input during a match. All changes are the prepared plans of B.3, executed automatically. A manager is free to watch, but watching changes nothing — there is no live lever to pull. This is the hard expression of reward-engagement-not-presence: the entirety of in-match management happens before kickoff, so a manager asleep in another time zone and a manager watching every minute play the identical match. Skill lives in the plan, never in the moment.

---

B.8 Dials — starting values

All tunable; none a finding.

Dial| Starting value| Governs
Substitutions / windows| 5 / 3| the substitution budget
Game-state set| score, time, personnel, context| how finely states are drawn
Priority category order| personnel > score-and-time > phase| tie-breaking between equal-specificity plans
Specificity-first| structural| the primary conflict rule, not a dial
Unfamiliar-shift variance penalty| a dial| how shaky an out-of-repertoire change is
Injury consumes a sub| yes| whether forced changes spend the budget
Plan-depth returns| diminishing| why micro-scripting is not rewarded

---

B.9 Calibration Targets

To be met by simulation, not derivation:

- A manager who prepares game-state responses outperforms one who sets only a base plan — and a manager who is never online during matches is never disadvantaged. The gap is preparation, not presence.
- There is no live lever, and no measurable advantage to watching a match unfold. If one appears, B.7 has been violated.
- Conflicts resolve deterministically and intuitively — the leading-and-a-man-down case lands sensibly, specificity wins, and the same match reproduces the same resolution.
- Substitutions are a meaningful resource: limited, depleted by injury, and the freshness-against-quality trade is real rather than a free upgrade.
- In-repertoire shifts execute cleanly and out-of-repertoire shifts are shaky, so the familiarity interaction holds.
- No single optimal plan-set dominates: different squads and identities want different game-state answers, the same anti-convergence the rest of the engine demands.
- Plan depth shows diminishing returns, so thoroughness is rewarded but micro-scripting is not, and the layer never becomes a clicking treadmill.

---

Relationship

Feeds Appendix D by changing its inputs at each trigger — a substitution re-forms the line-strength sums, a style or route or shape change re-scales the attack-defence interaction — within deterministic resolution and the same seed. Leans on Appendix C: substitutions spend fitness and pairing cohesion, injuries force them, and familiarity governs how cleanly a mid-match shift lands. Speaks Appendix A's language: every plan action is a move in shape, style, route or role. Sits under the constitution's No Tactical Omniscience and reward-engagement-not-presence, and absorbs the conflicting-instruction priority item from the Future Directions Register. With B in place, the four engine appendices are complete: A is the football a club plays, C is how well it knows its players and systems, D is what should and did happen on the day, and B is how a manager's foresight executes within it — all of it prepared, none of it live.
