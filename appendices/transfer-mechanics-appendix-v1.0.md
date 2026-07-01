The Beautiful Game

Transfer Mechanics Appendix v1.0

Appendix to the Contracts, Agents, Ambition & Club Attractiveness Constitution v2.1

---

Purpose

Supplies the formulas the Contracts Constitution defers to it: the five Club Attractiveness factors, the deterministic offer-evaluation formula, the promise thresholds, and the force-majeure rules.

Conventions

- Every score is 0–100 unless stated.
- Public inputs are public; player preference exact values are the deliberate exception (Part 2).
- Every calculation is deterministic and reproducible from the underlying values: no randomness, no administrator judgement.
- All constants are tunable DIALS.

Changes to v1.0: preference-weight generation made explicitly deterministic and non-hand-set while remaining hidden (2.2); a concrete ExpectedGain formula now closes the Development Reputation dependency (1.3); the Contract Review minimum gains a market-value floor (Part 3); "randomness" corrected to "uncertainty" (Part 5).

---

PART 1 — CLUB ATTRACTIVENESS FACTORS

Each 0–100, from public data.

1.1 Sporting Prestige = 0.35×Division + 0.25×Position + 0.20×RecentFinishes + 0.15×Trophies + 0.05×Continental.
Division = 100 − (Tier − 1) × 20. Position = 100 × (ClubsPerDivision − LeaguePosition) ÷ (ClubsPerDivision − 1). RecentFinishes = mean over 3 seasons of 100 × (TotalClubs − PyramidRank) ÷ (TotalClubs − 1). Trophies = Σ over 5 seasons of TrophyWeight × 0.8^(seasons ago), normalised (league 100, national cup 60, league cup 30). Continental = 50 qualification + 10 per knockout round, capped 100.

1.2 Financial Strength = 0.40×Revenue + 0.30×BudgetHeadroom + 0.30×FinancialStability.
Revenue via a logarithmic curve relative to the world's highest. BudgetHeadroom = remaining ÷ total wage budget × 100. FinancialStability from World Constitution data.

1.3 Development Reputation

DevelopmentReputation = 0.35×YouthProgression + 0.25×SuccessfulSales + 0.25×GraduatesAtHigherLevels + 0.15×DevelopmentPromiseFulfilment.

YouthProgression measures whether a club's young players BEAT their projected development. For each under-21 player owned at least one season:

- ExpectedGain — now defined (closing the prior dependency):

  ExpectedCeiling C = Ability_at_acquisition + PeakGain(age) × TrajectoryFactor   (the Potential Centre at acquisition, per the Player Rating Constitution)

  ExpectedGain = (C − Ability_at_acquisition) × (min(age + SeasonsOwned, PeakAge) − age) ÷ (PeakAge − age),  for age < PeakAge; otherwise 0.

  PeakAge = 26 (dial). This is the share of a player's projected rise to his ceiling that a typical development would deliver over the seasons the club held him.

- ActualGain = real-world Ability change while owned.
- OverGain = ActualGain − ExpectedGain.

YouthProgression = clamp(50 + k × mean(OverGain), 0, 100).

A club scores ~50 for a prospect who merely follows his projected curve, and climbs only by owning players who exceed projection. Because ratings are reality-synced and clubs cannot cause development, this correctly rewards selection and judgement — backing under-rated risers — not raw possession of talent.

(SuccessfulSales = Development Levy events generated, scaled. GraduatesAtHigherLevels = former under-21 players now at a higher division or Ability than when sold. DevelopmentPromiseFulfilment = % of development promises kept.)

1.4 Stability = 0.40×Tenure + 0.20×Ownership + 0.20×FinancialStability + 0.20×Consistency.
Tenure = min(100, ManagerTenureSeasons × 20). Consistency = 100 − scaled std-dev of Pyramid Rank over 5 seasons.

1.5 Playing Opportunity (player- and position-specific)
PositionalCompetition = squad players in the player's position with Ability ≥ (player Ability − 3).

Competition| Role| Score
0| Guaranteed Starter| 100
1| First Choice| 80
2| Rotation| 55
3| Squad Player| 30
4+| Fringe| 10

TacticalFit modifier ±10. Clamped 0–100.

---

PART 2 — TRANSFER EVALUATION (scouted preference bands)

A player scores every offer across nine Offer Dimensions, weighted by his preferences, and chooses the highest qualifying one.

2.1 Offer Dimensions (each 0–100)

Wage = clamp(50 × OfferedWage ÷ ExpectedWage, 0, 100). ContractSecurity = clamp(20 × min(Length,5) + bonuses, 0, 100). PlayingOpportunity = Part 1.5. SportingPrestige = 1.1. Development = 1.3. Stability = 1.4. ManagerReputation = manager's score. HomeRegion = 100 same region / 60 neighbouring / 20 otherwise. Loyalty = 100 current club / 0 otherwise.

2.2 Preference Weights — scouted bands

Each player has TRUE, FIXED, HIDDEN weights across the nine dimensions (normalised to sum to 1). Public is a BAND for each: a category and range (e.g. Wage Priority: High (60–80)).

True Weight Generation (deterministic, committed, never hand-set)

The true weights are generated at the player's entry from public player data (age, career stage, home region, career history) and a fixed, published archetype ruleset, combined with a per-player personality component committed at entry. The generation is rule-based and auditable, so weights are provably never hand-set or adjusted by administrators — there is no admin discretion over personalities. The committed component is not published during play, so the exact weights cannot be recomputed by managers; only the public band is shown.

This is deliberate. If weights were derived only from public data and public rules with nothing withheld, they would be fully reverse-engineerable, and the band system — and v0.2's solvability fix — would unravel. The committed component is fixed once at entry (a personality, not a die roll); it never changes during play and introduces no gameplay randomness. The result satisfies both requirements at once: not hand-set, and not solvable.

Personal Estimate

Personal Band = [True − h, True + h] ∩ Public Band, where h = (Public Band Width × ClarityFactor) ÷ 2.

ClarityFactor is the same value used for Potential (Youth Discovery §5): max(0.40, RegionFactor × ScoutingFactor). The personal band always contains the true value, lies within the public band, and is never narrower than 40% of the public width. The true weight is never pinned exactly.

2.3 Agent Modifier (fully public)

The agent archetype multiplies its focus dimensions' weights (Financial Maximiser → Wage ×1.3; Career Builder → SportingPrestige, ManagerReputation ×1.2; Loyalty Focused → Loyalty, Stability ×1.3; Development Focused → Development, PlayingOpportunity ×1.3; Prestige Focused → SportingPrestige ×1.4), then re-normalises. Agents shift emphasis but cannot override a near-zero weight. Only the player's own weights are banded.

2.4 Promise Integration

PromiseBoost(applied) = BasePromiseBoost × CredibilityFactor.
CredibilityFactor = clamp(0.2 + 0.8 × (0.5×FulfilmentRate + 0.5×Stability) ÷ 100, 0.2, 1.0). New managers start at FulfilmentRate 70. BasePromiseBoost: First-Team +20 PlayingOpportunity; Development +15 Development; Promotion/Trophy +15 SportingPrestige.

2.5 Offer Score and Choice

OfferScore = Σ (Weight_d × DimensionScore_d) → 0–100.

The GAME computes each player's OfferScore from his TRUE weights, deterministically, accepts only offers ≥ the Acceptance Floor (prototype 40), and picks the highest. Tie-break: higher Wage → higher SportingPrestige → current club → lowest club ID. A MANAGER computes only an ESTIMATED OfferScore RANGE, knowing preferences as bands, and so cannot calculate the exact minimum winning offer.

2.6 Worked Example

A 21-year-old winger, Ability 72. Public bands: Playing Time High, Development Very High, Wage Medium. Agent: Development-Focused.

Offer A (big club): Wage 90, PlayingOpportunity 30, SportingPrestige 95, Development 50, Stability 85.
Offer B (development club): Wage 55, PlayingOpportunity 100, Development 85, plus credible First-Team and Development promises from a Youth-Developer manager (Credibility 0.84 → Development ≈ 98).

On true weights the game scores B ≈ 82, A ≈ 55 — the development club wins despite less money and prestige. Neither bidder knew this in advance: each saw only the bands, read tightly or loosely by his scouting of the player's region. The manager who knew the region read the priorities well and bid confidently on a pathway; the big club guessed and lost. No one could have computed the exact winning offer beforehand.

---

PART 3 — PROMISES

Each promise is evaluated at season end as Kept, Broken, or Void.

Promise| Kept if…
First-Team Football| started ≥ 50% of league matches AND played ≥ 60% of league minutes
Positional Role| ≥ 70% of minutes in the promised position
Development Pathway| Ability rose ≥ 2 over the season (under-21s: did not fall)
Promotion Challenge| promoted OR within the promotion zone + 2 places
Trophy Ambition| won a trophy OR reached a final
Contract Review| a good-faith renegotiation offer was made by the promised date (see below)

Contract Review — good-faith standard

A Contract Review promise is Kept only if the offer meets all published minimums:

- Wage ≥ the player's current wage, AND
- Wage ≥ 80% of his current ExpectedWage, AND
- Term ≥ 2 seasons.

The second condition is essential for a breakout star: matching his old bargain wage no longer discharges the promise once his market value has risen. An offer failing any minimum counts as Broken.

Fulfilment Rate = Kept ÷ (Kept + Broken); Void excluded. Feeds Manager Reputation and the Credibility Factor.

---

PART 4 — FORCE-MAJEURE

A promise is Void — no reputation effect — when failure was outside the manager's control:

- Injury — the player missed ≥ 40% of available minutes through injury (voids First-Team, Positional, Development).
- Suspension — minutes lost to the player's own bans are excluded before the threshold test.
- Severe loss of Form — Form ≤ −4 across the window; a justified benching does not break a starter promise.
- Declined review — the player rejected a good-faith review offer (one meeting all Part 3 minimums) that was actually made → Contract Review counts as Kept. A declined sub-standard offer does not qualify.
- Mid-term dismissal — a promise is assessed only over the seasons the manager was in post.

Force-majeure protects correct football decisions; a manager is never punished for benching an injured or out-of-form player.

---

PART 5 — THE PERSUASION GAME

The skill of recruitment lives in four layers:

- Reading the player. Preferences are public only as bands; exact weights are scouted, narrowed by Knowledge Regions and scouting exactly as Potential is. Understanding people is a scouted skill, not a lookup.
- Sealed-bid competition. Recruitment Windows resolve blind: you know the player's bands, not your rivals' offers.
- Constrained trade-offs. Promising playing time means benching someone; a high wage spends budget needed elsewhere.
- Promise-credibility management. Promises are discounted by your record; breaking them cheapens every future promise.

Two non-stochastic uncertainties drive the game: Potential (unknowable because future) and Preferences (unknowable-in-detail because scouted) — both public bands narrowed by judgement, never reduced to certainty. The uncertainty comes from other managers, not dice. Reproducibility is fully preserved.

---

Dials

Factor weights (1.1–1.4) · YouthProgression scaling k · PeakAge (1.3) · role thresholds (1.5) · ExpectedWage curve · Acceptance Floor · agent factors · BasePromiseBoost · Credibility floor and blend · promise thresholds · Contract Review minimums (wage ≥ current, wage ≥ 80% ExpectedWage, term ≥ 2) · force-majeure percentages · public preference band widths · preference Clarity floor (0.40) · archetype ruleset and committed-component scheme (2.2).

---

Relationship

Implements the Contracts, Agents, Ambition & Club Attractiveness Constitution. Draws Ability, Potential, Form and Reputation from the Player Rating Constitution; Pyramid Rank, the Development Levy, sealed-bid Recruitment Windows and the Clarity Factor from the Youth Discovery & Recruitment Constitution; finances, ownership and tenure from the World Constitution. The ExpectedWage curve (referenced in 2.1 and Part 3) is defined in the forthcoming Scouting & Finance Constitution.
