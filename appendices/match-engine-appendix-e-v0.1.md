# The Beautiful Game — Match Engine Appendix E

## Player Match-Performance Ratings

**Version:** 0.1  
**Status:** Adopted implementation baseline  
**Parent authority:** Match Engine Constitution v0.3  
**Related authority:** Player Rating Constitution v1.1; Information, Media & Communication Constitution v1.2

---

## 1. Purpose

This appendix governs the deterministic post-match rating assigned to each player who participates in a resolved match.

A match-performance rating is a descriptive output. It reports how well a player performed in that match. It is not the player's Ability, Form, Potential, Reputation or Effective Match Rating, and it must not feed back into those reality-synchronised ratings merely because it was produced.

The model must be reproducible from the official event stream, resolved line-up state and constitutional match inputs.

---

## 2. Core principles

1. Every eligible player begins from a neutral rating of **6.0**.
2. Ratings are determined by realised contribution, not reputation.
3. Ability and Form establish expectation; they do not directly award a high match rating.
4. Contributions must be interpreted by the player's resolved positional role.
5. The match result may influence ratings only modestly.
6. Decisive match context may influence ratings only modestly.
7. Missing evidence must never be converted into a zero-valued performance.
8. Every published rating must retain an auditable component breakdown.
9. The final rating is bounded from **1.0 to 10.0** and rounded to one decimal place.
10. Calibration weights are explicit dials and must not be hidden in presentation code.

---

## 3. Rating bands

| Rating | Meaning |
|---|---|
| 9.0–10.0 | Exceptional; match-defining |
| 8.0–8.9 | Outstanding |
| 7.0–7.9 | Clearly good |
| 6.0–6.9 | Ordinary to solid |
| 5.0–5.9 | Below par |
| 4.0–4.9 | Poor |
| 1.0–3.9 | Disastrous |

These descriptions are presentational guidance, not separate formula inputs.

---

## 4. Constitutional formula

The version 0.1 rating is:

```text
RawRating =
  6.0
  + EventImpact
  + RoleContribution
  + AboveExpectation
  + MatchContext
  + TeamResult
  + Discipline

FinalRating = round(clamp(RawRating, 1.0, 10.0), 1)
```

Component bounds:

| Component | Minimum | Maximum |
|---|---:|---:|
| EventImpact | -2.00 | +2.50 |
| RoleContribution | -1.00 | +1.00 |
| AboveExpectation | -0.75 | +0.75 |
| MatchContext | -0.25 | +0.25 |
| TeamResult | -0.25 | +0.25 |
| Discipline | -1.25 | 0.00 |

The implementation may internally separate chance, possession and defensive contributions, but their published combined role contribution must respect the stated bound.

---

## 5. Eligibility and minutes

- A player who plays fewer than 10 minutes and records no meaningful event receives `null`, not 6.0.
- A meaningful event includes a goal, assist, major chance, penalty involvement, card, dismissal or injury event attributable to that player.
- A player who plays fewer than 10 minutes but records a meaningful event is eligible for a rating.
- A player who plays 10 minutes or more is eligible.
- An unused substitute receives no rating.
- Minutes played must come from the official resolved line-up state.

A `null` rating means insufficient match evidence. It does not mean a rating of zero.

---

## 6. Event-impact baseline weights

The following are version 0.1 calibration baselines:

| Event | Baseline effect |
|---|---:|
| Open-play goal | +1.15 |
| Penalty goal | +0.70 |
| Assist | +0.70 |
| Shot on target | +0.08 |
| Shot off target | -0.05 |
| Major chance missed | -0.40 |
| Penalty missed or saved | -0.80 |
| Penalty saved by goalkeeper | +1.25 |
| Ordinary goalkeeper save | +0.14, capped within role contribution |
| Ordinary foul | -0.04 |
| Penalty conceded | -0.65 |
| Yellow card | -0.15 |
| Straight red card | -1.25 |

These values are calibration dials. Changes require an appendix version change or an explicitly recorded calibration amendment.

Duplicate representations of the same football act must not be counted twice. In particular, the linked penalty-attempt and penalty-goal events represent one scored penalty outcome.

---

## 7. Role interpretation

### 7.1 Goalkeepers

Goalkeepers may receive credit for saves inferred from official opposition shots on target that do not become goals, and explicit penalty saves. Goals conceded must not by themselves force a poor rating where the event evidence shows strong goalkeeping contribution.

### 7.2 Defenders

Defenders receive bounded credit for defensive outcome contribution, including clean-sheet contribution where richer defensive events are not yet available. Goals conceded may apply a small bounded reduction. Penalties conceded and dismissals are separately penalised.

### 7.3 Midfielders

Midfield contribution should reward creation, assists, useful shot involvement, possession influence and defensive work where represented in the official event stream. Version 0.1 may use a conservative proxy until richer possession events exist.

### 7.4 Attackers

Attacking contribution should reward goals, assists, chances and useful shot involvement, while penalising major chances and penalties missed.

### 7.5 Unknown roles

An unknown role must not prevent a rating. The engine must use common event impact and omit unsupported role-specific adjustments rather than guessing a role.

---

## 8. Above-expectation adjustment

The engine may compare realised contribution against a bounded expectation derived from:

- effective player quality;
- role suitability;
- minutes played;
- team-strength context;
- opponent strength.

This adjustment must be capped at ±0.75.

The purpose is to recognise performance relative to the task faced. It must not become a hidden conversion of Ability into the match rating. A high-quality player with little positive contribution may receive an ordinary or poor rating; a weaker player who performs exceptionally may receive a high rating.

---

## 9. Match context

Match-state context is bounded at ±0.25.

A goal that improves the scoring side's result state may receive a modest bonus. A late decisive action may receive a slightly larger bonus than an early one. Context must never outweigh the underlying football contribution.

---

## 10. Team-result adjustment

Baseline result adjustments are:

| Result | Adjustment |
|---|---:|
| Win | +0.15 |
| Draw | 0.00 |
| Defeat | -0.15 |

An unexpected win by a materially weaker team may add up to +0.10. An unexpected defeat by a materially stronger team may subtract up to -0.10. The total TeamResult component remains bounded at ±0.25.

No blanket team-result rule may erase an outstanding individual performance in defeat or manufacture an outstanding performance in victory.

---

## 11. Public result contract

The resolved public match result must expose player ratings by side and may expose Player of the Match.

Minimum player-rating row:

```json
{
  "player_id": "tbg-player-id",
  "side": "home",
  "minutes_played": 90,
  "role": "midfielder",
  "rating": 8.2,
  "components": {
    "baseline": 6.0,
    "event_impact": 0.45,
    "role_contribution": 0.74,
    "above_expectation": 0.58,
    "match_context": 0.10,
    "team_result": 0.15,
    "discipline": -0.15
  },
  "highlights": [
    "1 assist",
    "booked"
  ]
}
```

For an ineligible short cameo, `rating` and `components` must be `null` and `highlights` may be empty.

Player of the Match is the highest eligible rating. Deterministic tie-breakers must be applied in this order:

1. higher rating;
2. more minutes played;
3. canonical player ID lexical order.

---

## 12. Determinism and auditability

Given the same constitutional contract, official event stream, line-up state and seed-resolved match result, the performance-rating output must be identical.

The rating module must not use:

- presentation-layer text parsing;
- external live data fetched after match resolution;
- random numbers independent of the match seed;
- manager-facing reputation;
- media narrative;
- hidden manual overrides.

All component values must be retained in the engine result or an equivalent audit record.

---

## 13. Calibration obligations

Before version 1.0, calibration should test at least:

- average starter rating and distribution;
- proportion of ratings above 7.0, 8.0 and 9.0;
- Player of the Match positional distribution;
- ratings in wins, draws and defeats;
- goalkeeper ratings in high-save defeats;
- striker ratings after goals combined with major misses;
- defender ratings in clean sheets with low involvement;
- red-card and penalty-error tails;
- short substitute eligibility;
- elite-versus-weaker-player above-expectation behaviour.

The intended broad centre is approximately 6.2–6.5 for eligible players. Ratings above 9.0 should be rare and evidence-led.

---

## 14. Future enrichment

Later versions may add explicit calibrated weights for:

- tackles, interceptions and blocks;
- aerial and ground duels;
- pressures and recoveries;
- progressive passes and carries;
- possession losses and dangerous turnovers;
- errors leading to shots or goals;
- per-player expected goals and expected assists;
- goalkeeper post-shot expected goals;
- off-ball space creation and chance prevention.

Absence of these events in version 0.1 must not be disguised through invented statistics.
