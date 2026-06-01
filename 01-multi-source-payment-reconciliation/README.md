# 01 — Multi-Source Payment Reconciliation

Dummy feeds for the demo workflow. Four payment-mode reports are reconciled
against the core-banking ledger (`cbs_ledger.csv`):

- `upi.csv`  — UPI settlement report (CSV)   → Read Sheet File
- `nach.csv` — NACH settlement report (CSV)  → Read Sheet File
- `neft.json` — NEFT feed (JSON)             → Read JSON File
- `rtgs.json` — RTGS feed (JSON)             → Read JSON File

Match key: feed `rrn`/`txn_ref`/`utr` == ledger `ref_no`, with equal `amount`
and a successful feed `status`.

Planted exceptions (6):
- RRN100003 (UPI)  — status FAILED
- RRN100004 (UPI)  — amount mismatch (feed 750.00 vs ledger 700.00)
- RRN100006 (UPI)  — missing from ledger
- RRN200003 (NACH) — status RETURNED
- UTR300003 (NEFT) — amount mismatch (feed 9500 vs ledger 9000)
- RTGS400003 (RTGS) — status PENDING

Expected result: 11 matched, 6 exceptions.
