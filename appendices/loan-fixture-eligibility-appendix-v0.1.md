The Beautiful Game

Loan Fixture Eligibility Appendix v0.1

Appendix to the Contracts, Agents, Ambition & Club Attractiveness Constitution v2.1 and the World Constitution v0.3

---

Purpose

This Appendix governs whether a player on loan may appear in a fixture against the club that owns his registration.

The rule is deliberately configurable because real competitions and football jurisdictions do not apply one universal convention.

---

1. Canonical identities

For every active loan the world must retain:

- Player ID
- Parent Club ID — the club that owns the player's registration
- Loan Club ID — the club for which the player is temporarily eligible
- Loan start and end dates or turns
- Loan status

Eligibility must be evaluated from stable IDs, never inferred from club or player display names.

---

2. Parent-club restriction dial

Each world or competition may publish:

`parent_club_restriction = true | false`

The competition-level value overrides the world-level value for fixtures in that competition.

Default: `false`.

The default is permissive so that introducing this Appendix does not retrospectively invalidate existing worlds or competitions. A world organiser must positively enable the restriction where desired.

---

3. Eligibility rule

When `parent_club_restriction = true`, a player is ineligible for a fixture when all of the following are true:

1. the player is currently on loan;
2. the selected club is the Loan Club;
3. the opponent is the Parent Club; and
4. the loan is active at the fixture's eligibility checkpoint.

The restriction applies whether the Parent Club is home or away.

When the dial is `false`, the loan itself does not prevent the player appearing against the Parent Club. Injury, suspension, registration and other eligibility rules continue to apply independently.

---

4. Enforcement

The same determination must be enforced in every path that can produce a team sheet:

- manager team submission;
- saved presets and restored submissions;
- assistant-manager or AI selection;
- deadline fallback selection;
- fixture locking; and
- final match-resolution validation.

A user-interface warning alone is not sufficient. Invalid selections must be rejected or repaired before the match is resolved.

---

5. Public information

The rule value is public competition information.

Where the restriction applies, the player's availability must state:

`Unavailable — parent club fixture`

The explanation must identify the rule, not imply injury, suspension or manager choice.

---

6. Determinism and audit

The result is deterministic from the fixture, active loan record and published rule value.

Any rejected or repaired team sheet must retain an auditable reason code:

`parent_club_fixture`

No administrator judgement is permitted at selection or resolution time.

---

7. Relationship to other rules

This Appendix changes fixture eligibility only. It does not alter ownership, wages, loan limits, recall rights, transfer evaluation, promises or development credit.

Suspension and injury rules remain separate. A player may have more than one simultaneous reason for unavailability.

---

Dials

- World-level `parent_club_restriction`
- Competition-level override
- Default value (`false`)

All dials must be published before the relevant competition begins and may not be changed retrospectively for already locked fixtures.
