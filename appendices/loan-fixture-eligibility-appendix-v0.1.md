The Beautiful Game

Loan Fixture Eligibility Appendix v0.2

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

The world-level dial is boolean:

`parent_club_restriction = true | false`

A competition-level setting is tri-state:

`parent_club_restriction = inherit | true | false`

`inherit` may be represented by an omitted field or an explicit `inherit` value. It must never be materialised as `false` merely because the field is absent.

Resolution order:

1. an explicit competition value of `true` or `false`;
2. otherwise the world-level value;
3. otherwise the global default, `false`.

The competition-level value therefore overrides the world only when it is explicitly boolean. An unset competition inherits the world.

The global default is permissive so that introducing this Appendix does not retrospectively invalidate existing worlds. A world organiser must positively enable the restriction where desired.

---

3. Eligibility checkpoint

Every fixture has one canonical eligibility checkpoint.

The checkpoint is the fixture lock instant: the authoritative timestamp or turn at which the team sheet becomes final for that fixture. Where a competition does not separately publish a lock instant, the scheduled kickoff timestamp is the checkpoint.

Loan status, Parent Club, Loan Club, loan start and loan end must all be evaluated as at this same checkpoint.

Submission, preset restoration, AI selection and deadline fallback may perform provisional validation earlier, but locking and final match resolution must re-evaluate against the canonical checkpoint. They must not use their own current wall-clock time.

A team sheet accepted provisionally may therefore be rejected or repaired at lock only when the authoritative loan record genuinely changes before the checkpoint. Final match resolution must reproduce the lock determination from the same fixture and loan snapshot.

---

4. Eligibility rule

When the resolved `parent_club_restriction = true`, a player is ineligible for a fixture when all of the following are true at the canonical eligibility checkpoint:

1. the loan record is active;
2. the selected club is the Loan Club; and
3. the opponent is the Parent Club.

The restriction applies whether the Parent Club is home or away.

When the resolved dial is `false`, the loan itself does not prevent the player appearing against the Parent Club. Injury, suspension, registration and other eligibility rules continue to apply independently.

---

5. Enforcement

The same determination must be enforced in every path that can produce a team sheet:

- manager team submission;
- saved presets and restored submissions;
- assistant-manager or AI selection;
- deadline fallback selection;
- fixture locking; and
- final match-resolution validation.

A user-interface warning alone is not sufficient. Invalid selections must be rejected or repaired before the match is resolved.

The lock result must record the resolved rule value, checkpoint, relevant loan record identity and outcome so final resolution can reproduce it exactly.

---

6. Public information

The resolved rule value and its source — competition, world or global default — are public competition information.

Where the restriction applies, the player's availability must state:

`Unavailable — parent club fixture`

The explanation must identify the rule, not imply injury, suspension or manager choice.

---

7. Determinism and audit

The result is deterministic from the fixture, canonical eligibility checkpoint, authoritative loan record and resolved published rule value.

Any rejected or repaired team sheet must retain an auditable reason code:

`parent_club_fixture`

No administrator judgement is permitted at selection or resolution time.

---

8. Relationship to other rules

This Appendix changes fixture eligibility only. It does not alter ownership, wages, loan limits, recall rights, transfer evaluation, promises or development credit.

Suspension and injury rules remain separate. A player may have more than one simultaneous reason for unavailability.

---

Dials

- World-level `parent_club_restriction`: `true | false`
- Competition-level override: `inherit | true | false`
- Global default: `false`
- Canonical checkpoint: fixture lock instant, falling back to scheduled kickoff where no separate lock instant exists

All dials must be published before the relevant competition begins and may not be changed retrospectively for already locked fixtures.
