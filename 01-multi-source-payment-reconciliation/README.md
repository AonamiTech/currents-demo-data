# 01 — Multi-Source Payment Reconciliation

Three downloads (1 sheet + 2 JSON). The two JSON feed files are reconciled
against the core-banking ledger (`cbs_ledger.csv`):

- `cbs_ledger.csv`      — core-banking ledger (CSV)        → Read Sheet File
- `feeds_upi_nach.json` — UPI + NACH settlement feed (JSON) → Read JSON File
- `feeds_neft_rtgs.json`— NEFT + RTGS settlement feed (JSON)→ Read JSON File

Match key: feed `rrn`/`txn_ref`/`utr` == ledger `ref_no`, with equal `amount`
and a successful feed `status`. Each row carries a `mode` for readability; the
workflow's Code node detects the source from the key columns regardless.

Planted exceptions (6):
- RRN100003 (UPI)  — status FAILED
- RRN100004 (UPI)  — amount mismatch (feed 750.00 vs ledger 700.00)
- RRN100006 (UPI)  — missing from ledger
- RRN200003 (NACH) — status RETURNED
- UTR300003 (NEFT) — amount mismatch (feed 9500 vs ledger 9000)
- RTGS400003 (RTGS) — status PENDING

Expected result: 11 matched, 6 exceptions.
