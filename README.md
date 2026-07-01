# The Beautiful Game — Governance

This repository is the design authority for **The Beautiful Game**.

It contains the constitutions, appendices, calibration briefs, stress tests and future-direction notes that define how the simulation should behave.

The engine must implement these documents. If code and governance disagree, governance wins until the constitution is amended.

## Structure

```text
/constitutions
/appendices
/registers
/tests-and-calibration
```

## Versioning principle

Each constitution keeps its own version number. Engine releases should declare which governance versions they are compatible with.

## First development rule

A behaviour is valid only if it is specified in governance, derived from governance, or explicitly marked as a temporary implementation assumption.
