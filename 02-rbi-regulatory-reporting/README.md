# 02 — RBI Regulatory Reporting

`cbs_period_data.csv` — a month's core-banking GL balances exported from CBS.
The workflow aggregates these into regulatory metrics:

- BSR — total deposits / advances
- Form A (CRR) — cash reserve ÷ deposits (expected ≥ 4%)
- SFR (SLR) — SLR investments ÷ deposits (expected ≥ 18%)
- CD ratio — advances ÷ deposits (flagged above 90%)

This dataset is intentionally anomalous: cash 35,000 ÷ deposits 1,000,000 = 3.5%
CRR, which is below 4% → the Anomalies? check trips, routing the run through the
Reviewer Check approval before Senior Sign-off.
