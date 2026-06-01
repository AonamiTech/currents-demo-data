# 01 — Multi-Source Payment Reconciliation

Dummy feeds for the demo workflow. The three payment-mode settlement reports
(`upi.csv`, `nach.csv`, `neft.csv`) are reconciled against the core-banking
ledger (`cbs_ledger.csv`).

Match key: feed `rrn`/`txn_ref`/`utr` == ledger `ref_no`, with equal `amount`
and a successful feed `status`.

Planted exceptions (5):
- RRN100003 (UPI) — status FAILED
- RRN100004 (UPI) — amount mismatch (feed 750.00 vs ledger 700.00)
- RRN100006 (UPI) — missing from ledger
- RRN200003 (NACH) — status RETURNED
- UTR300003 (NEFT) — amount mismatch (feed 9500.00 vs ledger 9000.00)

Expected result: 9 matched, 5 exceptions.
