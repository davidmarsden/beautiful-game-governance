# The Beautiful Game — Alpha Rulebook v0.1

This is the player-facing rulebook for the **current controlled-alpha game**.

It describes what managers can actually use now, plus a small number of known alpha limitations that materially affect play. It does **not** treat future constitutional systems as if they are already implemented.

The constitutions remain the design authority. Where the implementation has not yet caught up with an amended constitutional rule, this rulebook says so explicitly.

---

## 1. The World

The Beautiful Game currently runs as one persistent shared world containing:

- **80 clubs**;
- **4 divisions**;
- **20 clubs in each division**.

Every club and player exists once in the shared world. Manager decisions, transfers, results and history persist from one matchday to the next.

There are no duplicate copies of the same world for different managers.

---

## 2. Managers and Clubs

A human manager controls one appointed club.

The Manager Portal is private to that appointment. Your team selections, transfer actions and club information are scoped to your own club unless the information is deliberately public.

The controlled alpha begins with a small invited group of human managers. Clubs without human managers continue to exist in the same canonical world.

---

## 3. Squads

Every club has two separate ownership cohorts:

- **First-team squad: maximum 25 players**;
- **Youth squad: maximum 25 players**.

A player aged **21 or under at the start of the season** is youth-eligible for that season. If he turns 22 during the season, he remains youth-eligible until the next season boundary.

The two caps are independent. An empty youth place cannot be used to sign a 26th first-team player, and an empty first-team place cannot be used to sign a 26th youth player.

A transfer that would breach either squad cap must not complete.

---

## 4. Players and Real-World Data

TBG uses real footballers.

Real-world information supplies the governed player data used by the game, including identity, position and published player ratings.

A player's **in-game club ownership is independent of his real-world club**. A real-world transfer does not automatically move him between TBG clubs.

Published player updates are applied through the governed Player Updates / New Players process rather than by silently changing the live world.

---

## 5. Player Ratings

The match engine uses the canonical ratings published for each player.

Player ratings are governed outside the match engine. A great or terrible TBG match does not rewrite a player's underlying real-world-derived Ability.

Match performance ratings describe how a player performed in that match; they are not permanent Ability changes.

---

## 6. Matchdays

Matchdays are centrally scheduled for the shared world.

Before the deadline, managers can submit their team and available tactical choices through the Manager Portal.

When the matchday runs:

- the same canonical world is advanced for every club;
- each manager's submission applies only to the correct club and fixture;
- the engine produces results, commentary/replay information and player performances;
- tables and history are updated from the canonical result.

Managers do not gain an advantage by being online while the match is resolving.

---

## 7. Missing or Invalid Matchday Submissions

The world must still advance if a manager misses a deadline or submits an invalid XI.

TBG therefore uses a deterministic fallback rather than abandoning the fixture or requiring an administrator to improvise a team.

This is an alpha safety feature as well as a gameplay rule: one manager's missed submission cannot block the entire shared world.

---

## 8. Fitness, Morale and Availability

The live matchday state includes player condition and availability information such as:

- fitness;
- morale;
- injuries;
- suspensions.

These states can affect selection and match performance.

They are game-world match states. They do not change the player's underlying real-world-derived Ability.

---

## 9. Transfers Between Clubs

The current transfer market supports manager-to-manager negotiation.

Managers can use the live market to:

- list players;
- make offers;
- counter offers;
- decline offers;
- withdraw offers;
- reach an agreement;
- allow an agreed deal to pass through its binding/settlement process.

Completed transfer history is recorded and presented to managers.

The transfer system is designed so that settlement changes the relevant club/player/financial state together rather than partially completing a deal.

---

## 10. Free Agents and External Players

Managers can search for and acquire eligible free agents.

The game also has a governed route for acquiring eligible real players who exist in the wider player registry but are not yet owned inside the canonical world.

Identity checks prevent the same real footballer being introduced twice under duplicate records.

---

## 11. Contracts and Renewals

The alpha includes the contract lifecycle required to keep squads viable, including player contracts, expiries and renewals.

Incoming transfers, renewals and free-agent acquisitions must respect the club's current wage affordability rules.

The richer constitutional system of agents, player ambitions, promises and competing career choices is **not yet part of the current alpha game**.

---

## 12. Club Finance

Each club currently has a minimal canonical financial model containing:

- cash balance;
- wage bill;
- wage budget;
- wage headroom.

Transfer cash moves with successful settlement.

A club cannot complete a deal it cannot afford. An unaffordable deal must fail without partially changing ownership, contracts or cash.

This is deliberately a minimal alpha economy. Sponsorship, richer revenue modelling, FFP sanctions, Board Backing and the wider constitutional finance system are later development.

---

## 13. The World Feed

The shared world includes **World Feed v0**.

It supports:

- manager posts;
- comments;
- system-generated world events;
- administration/moderation.

The World Feed is a community and presentation layer. It does not directly alter the canonical match simulation or its checksum.

This is not yet the full constitutional media system. Automated journalism, press conferences and transfer-rumour mechanics remain future work.

---

## 14. Results, Tables, Replay and History

Managers can see the canonical outputs of played matchdays, including the current league picture and historical match information.

The production alpha has canonical results, tables, archives, replay/presentation data and player-performance ratings.

The world is persistent: completed matchdays become part of its history rather than being discarded after each turn.

---

## 15. Promotion and Relegation — Known Alpha Gap

The constitutional target is now:

- **1st–3rd:** automatic promotion from Divisions 2–4;
- **4th–7th:** promotion playoffs;
- **playoff winner:** fourth promoted club;
- **bottom four:** automatic relegation from Divisions 1–3.

The current rollover engine can move four clubs automatically and **does not yet implement the playoff stage**.

Therefore the season-end movement mechanism is a known implementation gap and must be brought into line with the World Constitution before it is treated as the final competition rule.

---

## 16. Cups — Not Yet Part of the Controlled Alpha Core

The wider TBG design includes cup competitions.

They are not part of the current production-proven controlled-alpha core and should not be assumed available merely because they appear in the constitutional design.

---

## 17. Loans and Multi-Club Deals

Straight transfers and the core exchange path are available at alpha entry.

First-class loans, automatic loan returns and broader three-or-more-club transaction support are scheduled to be exercised and developed during the controlled alpha.

Until those paths are declared production-ready, managers should not treat them as ordinary supported transfer mechanisms.

---

## 18. What Is Not Yet Implemented

The following constitutional systems are part of the intended game but are **not current alpha rules**:

- Board Objectives and Contract Objectives;
- Board Confidence and the full sack race;
- Board Backing;
- manager Professionalism scoring;
- Away Mode and the Warning → Caretaker → Removal participation ladder;
- enforced 72-hour transfer-response obligations;
- Knowledge Regions and deeper scouting uncertainty;
- autonomous player career decisions between competing clubs;
- Recruitment Windows;
- agents and player promises;
- the full young-player development and Development Levy system;
- the constitutional transfer-fee ceiling;
- the wider FFP regime and its transfer/wage/points sanctions;
- automated world journalism and press conferences;
- transfer rumours;
- emergent manager-style labels and the deeper career/reputation model.

These belong to the constitutional destination and development roadmap, not to the current player-facing alpha rules.

---

## 19. Alpha Principle

The controlled alpha exists to prove that multiple human managers can safely operate different clubs in the same persistent world.

The priorities are therefore:

1. correct club and manager identity;
2. reliable team submission and scheduled matchdays;
3. recoverable canonical world state;
4. safe transfers and finance;
5. governed player updates;
6. clear results, history and manager-facing presentation;
7. real human testing before adding unnecessary system breadth.

---

## 20. Conduct

Compete hard and negotiate hard, but treat the people playing the game with respect.

No multi-accounting, collusion, deliberate exploitation of technical faults, dishonesty or abuse.

**Fun. Friendship. Fair play. While attempting to utterly destroy your rivals on the pitch.**

---

## The Simple Rule

If this Alpha Rulebook says a feature exists, a manager should be able to use or encounter it in the current game.

If it exists only in a constitution or roadmap, it is part of the game TBG is building — not something an alpha tester should go looking for today.
