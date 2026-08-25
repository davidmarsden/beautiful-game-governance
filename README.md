# The Beautiful Game — Governance

This repository is the design authority for **The Beautiful Game**.

It contains the constitutions, appendices, calibration briefs, stress tests and future-direction notes that define how the simulation should behave.

The engine must implement these documents. If code and governance disagree, governance wins until the constitution is amended.

## Player-facing documents

Three documents deliberately separate **the game that exists now**, **the game being built**, and **how TBG's public player ratings are produced and maintained**:

- [`docs/alpha-rulebook-v0.1.md`](docs/alpha-rulebook-v0.1.md) — the current controlled-alpha rulebook. A feature belongs here only when managers can actually use or encounter it now, or when a known implementation gap materially affects current play.
- [`docs/road-ahead.md`](docs/road-ahead.md) — a non-binding, player-friendly overview of the deeper constitutional destination. Inclusion here does not mean a feature is implemented or promise a release date.
- [`docs/how-ratings-work.md`](docs/how-ratings-work.md) — a player-friendly explanation of The Pink Final, historical Transfermarkt/SoccerWiki/SMW calibration, the current Transfermarkt-derived live rating pipeline, and the governed Ratings Updates / New Players lifecycle.

This distinction prevents constitutional ambition from being presented to testers as current functionality and keeps the provenance of public TBG ratings understandable without requiring managers to read calibration code.

## Structure

```text
/constitutions
/appendices
/registers
/tests-and-calibration
/docs
```

## Versioning principle

Each constitution keeps its own version number. Engine releases should declare which governance versions they are compatible with.

Player-facing rulebooks are also versioned because they describe a particular implementation boundary.

## First development rule

A behaviour is valid only if it is specified in governance, derived from governance, or explicitly marked as a temporary implementation assumption.

A feature is advertised as **current gameplay** only when the live implementation actually supports it.
