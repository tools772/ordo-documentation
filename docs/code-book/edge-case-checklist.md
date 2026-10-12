---
search:
  exclude: true
---

# Edge-case checklist

Go through this list with whoever posts insurance at your office. It should take about 20 minutes.

For each row, mark **Seen it** if this happens at your office. Then look at the Ordo column:

- **Handled** — Ordo has a rule (and usually an automatic test) for it.
- **Partly** — Ordo catches it but a person has to finish the job.
- **Not yet** — Ordo does not handle it. Tell us how often you see it; that decides what we build next.

Anything you see that is **not on this list** is the most valuable thing you can send us.

---

## Reading the remittance

| Situation | Ordo | Details |
| --- | --- | --- |
| A claim continues onto the next page | Handled | [Reading the EOB](reading-the-eob.md#real-cases) |
| The same code, tooth and date legitimately appears twice | Handled (Cigna); check other payers | [Reading the EOB](reading-the-eob.md#real-cases) |
| Several patients on one check | Handled for most layouts; **Not yet** for one-claim layouts | [Known gaps](reading-the-eob.md#what-ordo-does-not-do-yet) |
| Siblings on one parent's policy | Handled | [Finding the patient](finding-the-patient-and-claim.md#real-cases) |
| Father and son with the same name (Jr / Sr) | Handled | [Reading the EOB](reading-the-eob.md#3-decide-who-each-patient-is) |
| Paid amount printed only on a total row | Handled (Ameritas) | [Reading the EOB](reading-the-eob.md#real-cases) |
| Check date or number printed without labels | Handled (Delta Washington) | [Reading the EOB](reading-the-eob.md#real-cases) |
| Remittance with no payment date (all denied) | Handled | [Approving and posting](approving-and-posting.md#which-date-becomes-the-check-date) |
| Denied or $0 lines | Handled — kept and shown | |
| Allowance applied entirely to deductible | Handled (United Concordia A1) | |
| A deposit slip uploaded instead of the remittance | Handled — clear message | |
| Scanned paper or a phone photo | Handled when legible | [Supported formats](../workflows/supported-formats.md) |
| "Other insurance paid" column on the remittance | **Not yet** | |
| Same remittance uploaded twice | **Not yet** | |
| Totals on the remittance do not add up | Partly — lowers confidence, no warning yet | |
| A payer or layout not on the supported list | **Not yet** — tell us which | [Supported formats](../workflows/supported-formats.md) |

## Finding the patient and claim

| Situation | Ordo | Details |
| --- | --- | --- |
| Remittance name differs from the chart (married name, nickname, hyphen) | Partly — **Find possible patients** suggests charts | [Finding the patient](finding-the-patient-and-claim.md#2-when-the-name-doesnt-find-the-chart-find-possible-patients) |
| A two-word first name split wrongly | Handled | [Finding the patient](finding-the-patient-and-claim.md#real-cases) |
| Payer on the remittance differs from the carrier in Open Dental | Handled when everything else matches | [Finding the patient](finding-the-patient-and-claim.md#real-cases) |
| Two visits with the same codes, different dates | Handled — different date blocks approval | |
| Same code twice on one claim (two teeth) | **Not yet** — pairs in order, ignores tooth | [Known gaps](finding-the-patient-and-claim.md#what-ordo-does-not-do-yet) |
| Payer paid a different code than billed | **Not yet** — line shows unmatched | |
| Secondary EOB vs primary claim in Open Dental | **Not yet** — check claim type yourself | |
| Claim not yet entered in Open Dental | Partly — shows No match; enter it, then fetch | |
| One visit split across two Open Dental claims | **Not yet** | |

## Posting to Open Dental

| Situation | Ordo | Details |
| --- | --- | --- |
| Payment already entered by hand | Handled — **Already Posted** if amounts match, review if not | [Approving and posting](approving-and-posting.md#real-cases) |
| Open Dental claim edited after approval | Handled — **Needs review** | |
| Procedure on the claim but not on the remittance ($0) | Handled — Received at $0 with a note | |
| Procedure on the claim but not on the remittance (has money) | Partly — stops for you to fix in Open Dental | |
| Connection drops while creating the check | Handled — never retried automatically | |
| Write-offs and adjustments | **Not yet** — post in Open Dental | [Known gaps](approving-and-posting.md#what-ordo-does-not-do-yet) |
| One deposit line per remittance (not per claim) | **Not yet** | |
| Supplemental payment on an already-received claim | **Not yet** — ends in review | |
| Recoupment / negative line / take-back | **Not yet** | |
| Corrected or reissued remittance | **Not yet** | |

## Checking the money

| Situation | Ordo | Details |
| --- | --- | --- |
| Dual insurance — primary and secondary each paid part | Handled | [Checking the money](checking-the-money.md#4-dual-insurance) |
| No fee schedule for the payer | Partly — sent to fee-schedule review | |
| Frequency limit denial | Partly — recognised from remark wording | |
| Downgrade / alternate benefit | Partly — recognised from remark wording | |
| Annual maximum reached | Partly — recognised from remark wording | |
| Waiting period, missing tooth, age limit, exclusion | **Not yet** | |
| Posted amount in Open Dental differs from the remittance | Handled — internal posting review | |

## Corrections

| Situation | Ordo | Details |
| --- | --- | --- |
| Fix a typo before approval | Handled — audit-logged | [Corrections](corrections-and-safety.md) |
| Fix an amount after approval | Handled — approval is cleared, approve again | |
| Fix something after posting | By design: fix in Open Dental; Ordo locks the claim | |
| Re-read a file after a reader fix | Handled until something is approved or posted | |

---

## Send us what you found

Email **[help@perfect.ventures](mailto:help@perfect.ventures)** with:

1. The rows you marked **Seen it** next to a **Not yet** or **Partly**, and roughly how often (weekly, monthly, rarely).
2. Anything you see that is not on this list.
3. An **EOB ID** from Ordo for each example, if it is in Ordo. No patient names or member IDs in the email, please.

---

[← 6. Corrections and safety](corrections-and-safety.md) · [Back to the codebook](index.md)
