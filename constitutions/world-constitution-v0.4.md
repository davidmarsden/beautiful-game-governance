The Beautiful Game

World Constitution v0.4

The backbone. It defines the world-level rules and delegates the specialised systems to the constitutions built on top of it.

---

Purpose

To create a realistic, competitive and sustainable football management world where managers build clubs over many seasons using football knowledge, strategic planning and negotiation. The game prioritises realism, fairness, community and long-term engagement.

---

The Constitutional Set

This document is the parent. Nine constitutions now divide the rules, with a tenth document parking what is deliberately deferred; each owns its domain and the others defer to it:

- World Constitution (this) — the world, clubs, managers, ownership, squads, contract administration and objectives, sanctions, governance, conduct. Defers the detail of manager employment to the Manager Career Constitution.
- Player Rating Constitution — Ability, Potential, Form, Reputation, and the formulas that produce them.
- Youth Discovery & Recruitment Constitution — scouting, Knowledge Regions, the Clarity Factor, discovery, recruitment windows, Building Credit, the Development Levy. Supersedes the former Draft.
- Contracts, Agents, Ambition & Club Attractiveness Constitution — contract terms, agents, player preferences, club attractiveness, manager reputation, promises, transfer evaluation.
- Transfer Mechanics Appendix — the deterministic formulas behind contract evaluation, attractiveness, promises and force-majeure.
- Scouting & Finance Constitution — revenue, wages and the ExpectedWage curve, transfers and the fee ceiling, FFP, the scouting economy, and Board Backing.
- Information, Media & Communication Constitution — professionalism and responsiveness, world news and press, transfer rumours, journalists, and the Records Ledger.
- Manager Career, Participation & Governance Constitution — the manager lifecycle, manager value and approaches, Board Confidence and the sack race, participation and the caretaker, career and legacy, and the amendment process.
- Match Engine Constitution — what happens on the pitch: the expected-performance model, match-layer states, the tactical metagame, and the one place genuine sporting variance lives.
- Future Directions Register — a non-binding home for deferred ideas, kept short and current.

Where any document conflicts with this one on a world-level rule, this one governs; on a specialised rule, the specialised document governs.

---

1. The World

Single Shared Universe — there is one game world. Every club, player, finance and competition exists within it. History is permanent. No duplicate worlds; no resets except in exceptional, published circumstances. (If the model proves successful, it may be replicated as a separate world; "one world" means one shared universe per world, never duplicates within it.)

League Structure — four divisions, twenty clubs each, eighty clubs in the canonical world.

Promotion and Relegation — between each adjacent pair of divisions, four clubs move in each direction at season end. In Divisions 2–4, the top three clubs are promoted automatically. Clubs finishing 4th–7th enter promotion playoffs for the fourth promotion place. In Divisions 1–3, the bottom four clubs are relegated automatically. Division 1 has no promotion and Division 4 has no relegation.

The world size and movement counts are constitutional structural dials and may be amended through governance. The canonical implementation must not silently substitute a different competition format.

Competitions — League Championship, National Cup, League Cup, Youth Cup; optional future continental and international competitions.

Cadence — two league turns per week; cup ties on other days. A full league season runs roughly a third of a calendar year, so history and legacy accrue over many seasons.

---

2. Clubs

Real-world clubs are preferred. Each inherits name, badge, stadium, nation and historical reputation, and retains its identity through manager changes.

Every club has reputation, fanbase, financial strength and facilities. These drive player attraction, sponsorship, revenue and youth development — their economic detail lives in the Scouting & Finance Constitution. A club's only structural money advantage is its larger organic economy (stadium, fanbase, history); there are no unequal owners (see §5).

---

3. Managers

One-Club Rule — a manager controls one club. No multi-accounting, no shared ownership.

Managers accumulate reputation, Building Credit and tenure over a career. Reputation is defined in the Contracts Constitution; Building Credit and tenure in the Youth Discovery Constitution. This document defines only the contractual and dismissal framework within which managers operate (§7, §8).

---

4. Players and the Reality Mirror

Real players are the foundation of the world. Their ratings, ageing, development and retirement are defined in the Player Rating Constitution and mirror real-world football. Their entry into the world and allocation to clubs are defined in the Youth Discovery & Recruitment Constitution.

This document owns one thing about players: their ownership.

---

5. Ownership

In-world ownership is authoritative and overrides reality. A player belongs to the club that owns him in the game world, regardless of his real-world club. Real-world transfers never move a player between in-world clubs; only in-world transfers, free moves and expiries do.

Reality governs the player's qualities (Ability, value, position, real-world retirement); the world governs who owns him. A real-world retirement removes the player from the active world; a real-world transfer changes nothing about his in-world ownership.

There are no unequal owners. Every club's board is equally supportive and rewards its manager purely on earned merit relative to expectation (Scouting & Finance §8). This is the one place the game deliberately departs from reality, because real ownership inequality would let money override skill.

---

6. Squads and Registration

The canonical squad model uses two independent ownership cohorts:

- First-team squad: maximum 25 players.
- Youth squad: maximum 25 players.

Youth eligibility is fixed for the season. A player aged 21 or under at the season start is youth-eligible for that season and remains in the youth cohort until the next season boundary, even if he turns 22 during the season. A player who is not youth-eligible counts towards the first-team limit.

A club may therefore own no more than 50 players across the two cohorts. Space in one cohort cannot be used to exceed the cap in the other.

Competition registration rules may sit inside these ownership limits, but they must never permit a club to bypass the 25/25 ownership caps.

Loans, when implemented, must respect the ownership and registration model defined here and any additional limits published in the relevant transfer rules.

Anti-hoarding rests on these limits together with the player-choice, development-pathway and Development-Levy mechanisms of the Youth Discovery Constitution. The former Draft is retired: talent allocation is governed entirely by the Youth Discovery & Recruitment Constitution.

---

7. Contracts and Objectives

Every player holds an active contract or is a free agent. Every manager holds a contract with his club. Contract terms (wage, length, clauses, bonuses) and their negotiation are defined in the Contracts Constitution; this document administers their existence, expiry and registration.

Contract Objective (the dependency Scouting & Finance §8 relies on)

At signing or renewal, the board and manager agree a public Contract Objective for the term — drawn from a published ladder matched to the club's Expected Finish: avoid relegation, consolidate, top half, promotion, title challenge, or a specified trophy. The objective is fixed for the term and public, and is set deterministically (the board offers an objective consistent with the club's level; no administrator chooses it).

Delivery against the objective feeds Board Backing (Scouting & Finance §8) and dismissal and reappointment (§8 below).

---

8. Dismissal and Reappointment

Relegation = dismissal: any relegation place results in automatic dismissal at season end. Under the canonical four-division structure, this means finishing in the bottom four of Divisions 1–3. Division 4 has no relegation.

The full machinery of manager employment — the three exit routes (relegation, lost confidence, abandonment), the Board Confidence sack race, mid-contract triggers, manager consent, compensation and approaches, the caretaker, and the reappointment priority order — is defined in the Manager Career, Participation & Governance Constitution. This section states the structural rule and defers to that document for all detail.

---

9. Finance, Transfers and Sanctions

The financial economy — revenue, wages, transfer budgets, the ExpectedWage curve, the scouting economy and Board Backing — is defined in the Scouting & Finance Constitution. Transfer evaluation and contracts are defined in the Contracts Constitution and its Appendix.

This document holds the regulatory machinery:

- Transfer regulations — cash is the dominant mechanism; swaps are uncommon. No transfer fee may exceed the published market-value ceiling (Scouting & Finance §3).
- Financial Fair Play sanctions — when a club breaches the limits set in Scouting & Finance §6, escalating, published, deterministic sanctions apply: transfer restrictions, then wage restrictions, then points deductions. The trigger is the formula; no discretion.

---

10. The Match Engine

The match engine should reward intelligent management — formation, tactics, squad balance, fitness, morale and preparation all matter — while remaining understandable but never fully solvable. The best team does not always win; the best managers win more often across many seasons.

A distinction the rest of the project depends on: ratings and recruitment are strictly deterministic and carry no hidden randomness, because their uncertainty is meant to be competitive, not stochastic. The match engine is the one system where genuine sporting variance is appropriate — real football matches are unpredictable. The two are distinct systems. The match engine's detailed rules are defined in the Match Engine Constitution.

---

11. Governance

All rules are public; all major changes are documented. Managers may appeal administrative decisions through a published process. Managers elect a Community Council that advises on rule changes; final authority rests with game administration — but administration is bound by the published rules and cannot override a deterministic outcome. The objective is legitimacy: a trusted system outlasts an efficient one nobody believes in.

---

12. Code of Conduct

Managers are expected to show respect, honesty, sportsmanship and competitive integrity. The goal is hard competition within a healthy community.

Fun. Friendship. Fair play. While attempting to utterly destroy your rivals on the pitch.

---

Golden Rule

One world, one history, equal boards, public rules. Clubs differ in size and wealth, never in the support or the standards applied to them. Managers win by understanding football and people better than their rivals, over many seasons — never by privilege, hidden information, or the size of an owner's chequebook.
