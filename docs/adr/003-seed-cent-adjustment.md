# ADR-003: Load seeded splits that are off by a cent

Status: Accepted
Date: 2026-11-14
Issue: #9

## Context
Due to rounding, some splits may be off by $0.01 from the expense
total. We must decide whether the seed loader fixes these
automatically or refuses to load them.

## Options
A. Fix it automatically. Adjust the last share so the sum is exact,
   and log a message saying it was adjusted.
B. Refuse to load it. Stop with an error so you notice and fix the
   data by hand.

## Decision
Option A, limited to differences of at most 1 minor unit
(1 cent, or ¥1). Any larger difference stops the load with an error.

## Consequences
+ Guest mode always loads; a 1-cent rounding difference never
  breaks the demo.
+ Every stored expense satisfies sum(shares) == total, so balances
  stay zero-sum (#18).
- A real data error could be hidden, which is why auto-fix is
  limited to 1 minor unit and anything larger stops the load.
- The last member absorbs the adjusted cent; the log line records
  which expense was changed.
