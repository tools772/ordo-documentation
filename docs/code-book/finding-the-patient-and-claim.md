---
search:
  exclude: true
---

# Step 2 — Finding the patient and the claim

**The question:** which chart in Open Dental is this, and which of that patient's claims is the remittance paying?

This is two separate jobs. Getting the person right comes first. A claim with the right dollars on the wrong patient is still the wrong post.

---

## What Ordo does

### 1. Fetch from Open Dental

Nothing happens until someone ticks patients and clicks **Fetch Open Dental**. For each EOB patient Ordo looks for the chart:

1. If the patient is **already linked** to an Open Dental chart, use that chart.
2. Otherwise search by **last + first name**, then by **last name only**. The first search that returns anyone wins.

For each chart found, Ordo pulls all of that patient's claims, the procedures on each claim, the insurance plan, carrier and provider. It keeps this copy so you can review without hammering Open Dental.

### 2. When the name doesn't find the chart — "Find possible patients"

Remittance names and chart names often disagree (married names, nicknames, hyphens, typos). On the Open Dental tab, **Find possible patients** tries these searches in order:

1. Date of birth + name
2. Date of birth only
3. Full name
4. Last name only
5. First and last swapped
6. Repaired names (for EOBs that split a two-word first name wrongly)

Each chart it finds gets points:

| Signal | Points |
| --- | --- |
| Date of birth exact | 50 |
| First name exact / close (80%+ similar) | 20 / 10 |
| Last name exact / close (80%+ similar) | 20 / 10 |
| Subscriber ID | 25 |
| Phone | 25 |
| Email | 25 |
| Address similar (70%+) | 10 |
| First and last look swapped | 5 |

A chart is only **shown** if the date of birth, subscriber ID, phone or email matched, or **both** first and last names matched. A sibling who only shares the surname is never offered. Nothing is linked until a person confirms the chart.

### 3. Which charts a claim is allowed to match

Before scoring any claim, Ordo decides which charts are even eligible:

- **Exact:** the linked chart; a chart whose subscriber ID matches; or a chart with the same last name and a first name at least 85% similar.
- **Close:** same last name and a first name at least 70% similar. Used only if there is no exact chart.

If nobody is eligible, Ordo shows **no candidates** rather than dumping the whole practice into the list. Claims from different family members are never mixed in one list.

### 4. Score each claim

Every Open Dental claim for the eligible chart gets up to 100 points:

| Signal | Points | Earned when |
| --- | --- | --- |
| Patient ID | 30 | The EOB's member ID or the linked chart points at this claim's patient |
| Date of service | 20 | Same calendar day |
| Patient name | 15 | Scaled by name similarity |
| Payer | 10 | Scaled by carrier name similarity |
| Provider | 10 | Scaled by provider name similarity |
| Procedure codes | 10 | Share of EOB codes found on the claim |
| Money adds up | 5 | All lines matched and totals agree within 1 cent |

- **90 or more** → high confidence. **75–89** → medium. Below 75 → low.
- The best **high-confidence** claim with no hard mismatch is **recommended** and pre-selected.

**Hard mismatches** force low confidence and block **Approve**, whatever the score:

- The member ID or linked chart points to a **different patient**.
- The **date of service differs**.
- **None** of the EOB's procedure codes are on the claim.
- The **payer** is very different (under 40% similar) — unless the name, date and every code match, in which case it is only noted.

### 5. Pair the procedure lines

For each EOB line Ordo takes the first unused Open Dental procedure with the **same code on the same day**, then the same code on any day of that claim.

Procedures on the Open Dental claim that are **not on the remittance** are listed as "Open Dental only". What happens to them at posting is on [the next page](approving-and-posting.md).

### 6. Link the chart

When a claim is recommended, Ordo links that EOB patient to the chart automatically, so the next fetch goes straight to it.

---

## Real cases

!!! example "A two-word first name split in half"
    **What happened.** The remittance printed a patient with a two-word first name (think "Mary Ann Lopez") as first name "Mary", last name "Ann Lopez". Open Dental search found nobody. Even after Mike linked the right chart by hand, claim matching wanted an exact surname and still showed **No match**.

    **What Ordo does now.** Ordo repairs mis-split names, both when reading the EOB and when searching Open Dental. Once a chart is linked, that chart is used for fetching and for matching. The name score uses whichever is better: the split name, or the whole name with spaces removed.

!!! example "A Cigna remittance for a claim filed under MetLife"
    **What happened.** Cigna's layout always says "Cigna Dental" at the top. The clinic's Open Dental stored that plan's carrier as MetLife. Ordo blocked a correct match as a payer mismatch.

    **What Ordo does now.** A payer name difference is only a note when everything else is strong: name at least 85% similar, same date of service, every code on the claim. A different date, zero shared codes, or a different patient still blocks.

!!! example "Two siblings on one parent's policy"
    **What happened.** A Delta check paid for two children covered by their mother. Both share her subscriber ID. Ordo identified patients by ID alone and merged the children into one patient.

    **What Ordo does now.** Patients are identified by ID **plus** name (see [Reading the EOB](reading-the-eob.md#3-decide-who-each-patient-is)). The **Family** tab shows everyone on one policy, and siblings merged before the fix were split back apart.

!!! tip "Safeguard — right dollars, wrong visit"
    **The situation.** Maria had two cleanings, June 12 and December 4. The EOB is for June. The December claim has the same code and nearly the same dollars.

    **What Ordo does.** A different date of service is a hard mismatch. The December claim cannot be approved for the June remittance, no matter how close the money is.

---

## What Ordo does not do yet

!!! warning "Known gaps"
    - **Tooth numbers are not used to pair lines.** If one claim has the same code twice (two fillings, `D2391` on #3 and #14), lines pair in the order they appear. The amounts can land on the wrong tooth.
    - **Code substitutions do not pair.** If the payer paid a different code than was billed (an alternate benefit, say billed `D2740`, paid as `D2750`), that line shows as not matched.
    - **Primary vs secondary claims are not told apart.** A secondary EOB can be scored against the primary claim in Open Dental. Check the claim type before approving a secondary.
    - **The chart link is automatic** when a claim is recommended. If the recommendation was wrong, unlink and pick the right chart on the Open Dental tab.
    - **A family member's claim can score high** if the real patient's claim is missing from Open Dental and the sibling had the same codes the same day. The name lowers the score but never blocks on its own.

---

## Questions for your team

!!! question "Have you seen something different?"
    1. How often is the remittance name different from the chart name? What are the usual reasons — married names, nicknames, hyphens, middle names?
    2. Do you have families where **two children were seen the same day for the same procedures** on the same policy?
    3. When a payer pays a **different code** than you billed (downgrade or alternate benefit), how do you post it in Open Dental today?
    4. Do you post **secondary** insurance EOBs through Ordo? Should Ordo look only at secondary claims for those?
    5. Do you ever split one visit across **two claims** in Open Dental, so the remittance pays parts of both?
    6. Would you rather Ordo **ask** before linking a chart, even when it is confident?

---

[← 1. Reading the EOB](reading-the-eob.md) · [The codebook](index.md) · [Next: 3–4. Approving and posting →](approving-and-posting.md)
