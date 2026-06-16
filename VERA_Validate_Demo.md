# VERA Validate — Demo Output

**Engine:** VERA Validate — *Exception Detection & Pre-Boarding QC*
**Task:** Compare a loan's boarded data against its source documents and flag discrepancies before boarding.

> All data is fully synthetic. Source documents in `/demo-documents`.

---

## Test 1 — Clean loan (control test)
All seven fields matched the source. **Verdict: CLEAR TO BOARD.**
Purpose: proves VERA does not raise false alarms on clean data.

---

## Test 2 — Real documents, terms match
Input: a Fannie Mae investor approval letter (prose format) + an internal underwriting
worksheet (table format) for the same loan.

VERA extracted terms from both, cited each source line, and confirmed they matched —
**including correctly recognizing that "three and seven-eighths percent" equals "3.875%"**
across the two different formats. **Verdict: CLEAR.**

Purpose: proves VERA reads real document formats and understands meaning, not just text.

---

## Test 3 — Real documents, planted errors
Same loan, but the worksheet contained four transposition/entry errors.

| Field | Investor Letter (truth) | Worksheet | Result |
|---|---|---|---|
| Interest rate | 3.875% | 3.785% | FAIL |
| Total trial payment | $1,913.82 | $1,931.82 | FAIL ($18.00 higher) |
| First payment due | 09/01/2026 | 09/15/2026 | FAIL |
| Payment due date | 1st of month | 15th of month | FAIL |
| UPB | $284,915.44 | $284,951.44 | FAIL ($36.00 higher) |

**Verdict: HOLD — EXCEPTIONS FOUND.**

VERA caught every error, calculated the exact dollar variance on the financial fields, and
cascaded the due-date error to flag the recurring due date as well.

Purpose: proves VERA catches the exact transposition errors that cause borrower harm —
misapplied payments, wrong due dates, incorrect balances.
