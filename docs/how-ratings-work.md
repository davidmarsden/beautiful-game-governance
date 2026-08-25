# The Beautiful Game — How Ratings Work

This is the player-facing explanation of where TBG player ratings come from, how **The Pink Final** fits into the system, and how ratings and new players are updated over time.

The short version is simple:

**TBG ratings are our own ratings.** They are produced by a governed, deterministic TBG model. External football data and legacy rating datasets helped us build, calibrate and validate that model, but TBG does not simply copy another site's or game's rating.

---

## The Pink Final

**The Pink Final (TPF)** is TBG's public player and ratings layer.

It presents the governed player database that feeds The Beautiful Game: player identity, football information and the published TBG rating used by the game.

The Pink Final and TBG therefore describe the same player universe from two different angles:

- **The Pink Final** makes the player database and ratings visible;
- **The Beautiful Game** uses those published players and ratings inside the persistent multiplayer world.

---

## 1. Building Our Own Rating Scale

TBG did not begin by inventing an arbitrary 1–100 number for every footballer.

During development we compared large numbers of real players against established football datasets and rating systems to understand how a useful football-management rating scale should be distributed.

Historical development, calibration and validation used or explored:

- **Transfermarkt-derived data**;
- **SoccerWiki** ratings;
- **Soccer Manager / SMW-derived** rating datasets;
- **API-Football** real-world football data during development and experimentation;
- TBG's own football hierarchy and calibration targets.

API-Football was useful during development as a structured real-world football-data source, but it did **not** become an input to the final published TBG rating model.

These comparisons helped us test questions such as:

- what rating range should describe an elite player?
- how far apart should regular starters at different competitive levels be?
- how should established players compare with emerging young players?
- does the resulting player population look plausible across clubs, leagues, ages and positions?

The purpose was calibration: to establish and test **TBG's own scale**, not to reproduce any one external source.

---

## 2. What Is Historical and What Is Live?

This distinction matters.

**SoccerWiki and SMW-derived datasets are legacy calibration and validation sources. API-Football was explored during development. None of them is an active input to current TBG ratings, player eligibility, database refreshes or publication.**

They remain useful historical evidence because they show how the model and data architecture were tested and can help reproduce earlier development work.

The current live pipeline instead starts from **Transfermarkt-derived player data** and passes that evidence through TBG's own governed model.

---

## 3. The Live Rating Pipeline

The governed player-rating publication path is:

1. **Transfermarkt-derived player data**;
2. **TBG Ability Curve / rating model**;
3. **published Veteran Reality Adjustment for qualifying high-rated older players**;
4. **publication eligibility checks**;
5. **player pools and initial squads**;
6. **published player database and The Pink Final**.

This separation is deliberate.

Transfermarkt-derived information supplies evidence about the real football world. The TBG formula turns the relevant inputs into a TBG rating. The published database is therefore a TBG interpretation of that evidence, not a Transfermarkt rating in different clothes.

The Veteran Reality Adjustment is not a hidden administrator tweak. Player Rating Constitution v1.2 publishes the exact qualifying ages, rating threshold, elite-competition classification, market-value threshold and penalties. Given the same source data, another manager can reproduce the same final Ability.

No other undocumented post-model boost or adjustment belongs in the canonical publication path. If the rating formula changes, that change must first be governed and published.

---

## 4. What Transfermarkt Is Used For

Transfermarkt-derived data is an important part of the current player-data pipeline.

Depending on the available source record, it can help TBG maintain information such as:

- player identity;
- age and date of birth;
- position;
- real-world club information;
- market-value evidence and its source date;
- the wider real-player universe from which new TBG players can emerge.

A real-world club transfer does **not** automatically transfer the player between TBG clubs. TBG ownership remains part of the canonical game world.

Likewise, Transfermarkt market value is evidence used within the wider data/rating process; it is not itself the player's TBG Ability rating.

If the current live source is temporarily unavailable, TBG should continue using the last successfully published player-database edition rather than publishing a partial, guessed or manually patched refresh. A source outage should create information lag, not arbitrary rating change.

---

## 5. Deterministic and Reproducible

TBG's publication pipeline is designed to be deterministic.

Given the same governed source edition, rating-model version and inputs, the same publication process should produce the same result.

Player-change provenance can record information such as:

- Transfermarkt source and scrape timestamp;
- Transfermarkt market-value determination date;
- TBG rating-model version;
- deterministic rating-input explanation;
- player-database edition generation time.

The aim is that a rating change can be explained and reproduced rather than quietly hand-edited into the live world.

---

## 6. Ratings Updates

TBG does not need to silently overwrite the live player universe whenever source data changes.

The data pipeline rebuilds the published player database and compares the new edition with the previous published edition.

Meaningful differences can enter the governed player-change lifecycle and then be presented to managers through **Ratings Updates**.

That gives the game a visible publication boundary: managers can see that a player's published TBG rating changed rather than discovering an unexplained number change somewhere in the squad screen.

A player's TBG match performances do not directly rewrite this underlying rating. Match-performance ratings describe how he played in TBG; underlying Ability remains tied to the governed real-world rating process.

---

## 7. New Players

The same lifecycle also supports **New Players**.

As real football produces new relevant players, the wider registry and refreshed source data can identify footballers who are not yet part of the published TBG player database.

Identity resolution is important here: the system must avoid introducing two records for the same real person simply because names, clubs or source identifiers differ.

Once an eligible new player has passed the governed publication process, he can be released into the TBG player universe through the manager-facing New Players flow rather than appearing by an unexplained manual edit.

---

## 8. Why We Do It This Way

The goal is not to claim that one formula can settle every football argument.

The goal is to make TBG's judgement **consistent, transparent and governable**.

External sources give us evidence and useful comparison points. Historical SoccerWiki and SMW data helped us calibrate and validate the scale. API-Football helped us explore structured football data during development. Transfermarkt-derived data remains part of the live evidence pipeline. But the final published number is TBG's own governed interpretation.

**The Pink Final is our interpretation of the evidence.**

That rating is then used consistently by The Beautiful Game until a later governed publication changes it.

---

## The Simple Rule

If you see a TBG rating in The Pink Final or the Manager Portal, it is a **TBG rating**.

It may be informed by real-world evidence and by a calibration history that used external datasets, but it is not simply copied from Transfermarkt, SoccerWiki, Soccer Manager or API-Football.
