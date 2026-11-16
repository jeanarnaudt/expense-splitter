# ADR-002: Store a $0.00 share as a split row

Status: Accepted
Date: 2026-11-14
Issue: #7

## Context
In an exact split, a member can owe $0.00 (e.g. Jake drove, so
passengers split the gas). We must decide whether that member is
stored in the split with a zero amount, or treated as excluded.

## Options
A. Keep the member in the split with owed_minor = 0.
B. Treat the member as excluded (no split row).

## Decision
Option A.

## Consequences
+ The expense shows that Jake was considered and deliberately
  charged nothing, which is more accurate than "not involved".
+ Matches the sample data, so the seed loads without conversion.
- The split calculator must allow 0 for exact splits, while
  shares splits still require weights > 0 (see #5).
