# VERA Build — Demo Output

**Engine:** VERA Build — *Automated Repayment Plan Boarding*
**Input:** A synthetic prior-servicer transfer report (S2MR format) listing multiple loans.
**Task:** Extract a clean, board-ready repayment plan for loan 0080012301.

> All data is fully synthetic. See `/demo-documents/DEMO_S2MR_Transfer_Report.pdf` for the input.

---

## Result — Board-Ready Repayment Plan, Loan 0080012301

| Field | Value | Source |
|---|---|---|
| Loan Number | 0080012301 | header line |
| Plan Type | 26 — Repayment Plan | "26 REPAYMENT PLAN" |
| Principal Balance | $97,214.40 | "PRINCIPAL BALANCE 97,214.40" |
| Plan Create Date | 08/22/25 | "A 08/22/25" |
| Total Repay Amount | $6,842.40 | "REPAY TOTAL 6,842.40" |
| Number of Payments | 6 | "CNT 6" |
| Monthly Payment | $1,140.40 | every due-amount line |

### Payment Schedule
| # | Due Date | Amount |
|---|---|---|
| 1 | 09/01/25 | $1,140.40 |
| 2 | 10/01/25 | $1,140.40 |
| 3 | 11/01/25 | $1,140.40 |
| 4 | 12/01/25 | $1,140.40 |
| 5 | 01/01/26 | $1,140.40 |
| 6 | 02/01/26 | $1,140.40 |

### Flagged for Review (the judgment layer)
1. **First payment received date vs. scheduled due date** — received 09/10/25, scheduled 09/01/25. Normal (late payment), but confirm which date should board.
2. **Prior completed modification present** — a prior non-HAMP mod exists; confirm this repayment plan is the active workout.
3. **Arrears ledger not shown** — confirm the arrears detail matches the $6,842.40 total before boarding.

---

**Why this matters:** A simple extraction tool would just copy the numbers. VERA Build
extracts the plan AND applies the judgment a senior associate would — flagging the
received-vs-due date nuance, the prior mod, and the missing arrears detail. That reasoning
is the difference between automation and expertise.
