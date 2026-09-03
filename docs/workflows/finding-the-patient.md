# Finding the patient in Open Dental

Names on an EOB and names in Open Dental often disagree. Insurance may print a nickname, misspell a last name, or use the name on the ID card. Open Dental may have an abbreviated first name, a maiden name, or a typo from registration.

You should **not** have to rewrite the EOB name just to find the chart. Ordo suggests possible Open Dental patients; **you** pick the right one.

This is **who is this person?** Claim matching (which visit to post) still happens after **Fetch Open Dental**. See [Matching and remarks](matching-and-remarks.md).

---

## Where you do it

Open a patient (from **Patients** or from inside an EOB) → **Open Dental** tab → **Find possible patients**.

Nothing is linked until you click **Select patient**. A high-ranked card is a suggestion, not a decision.

---

## What Ordo looks up

It uses what is already on the extracted patient:

| Field | Used? |
| --- | --- |
| First name, last name | Yes |
| Date of birth | Yes, when present — this is the strongest rescue when names differ |
| Subscriber ID | Yes, when scoring charts already returned |
| Phone, email, address | Only if those values exist (EOBs usually do not include them) |

Ordo does **not** send names to an outside matching service. Search stays inside Open Dental and Ordo.

---

## How search works

Open Dental’s API is not a fuzzy name engine. A search for `Smith` will not return `Smyth`. Ordo therefore runs several lookups and **combines** the people it gets back (same Open Dental ID only once):

1. **Name + date of birth**
2. **Date of birth only** — finds the chart even when the first or last name is wrong in either system
3. **First + last name**
4. **Last name only** — then Ordo scores first names locally (John vs Johnathan)
5. **First and last swapped** — in case the names were reversed

It then ranks the combined list. Similar first names (John / Johnathan) and similar last names (Smith / Smyth) are scored **after** Open Dental returns rows. Date of birth is how misspelled last names still appear.

Weak hits are dropped (same last name, completely different first name, no matching DOB or subscriber ID).

---

## What you see

Each remaining person is a **card**, not an automatic link:

- Name and Open Dental ID
- Date of birth (and a masked phone when the chart has one)
- **Strongest suggestion** or **Possible match**
- **Why this was suggested** (for example: DOB matches, first name is similar, last name matches)

If several charts look plausible, **all of them** are listed. You choose.

**Example.** The EOB says **Jonathan Smith**, DOB March 12, 1985. Open Dental has **John Smith** on that date (registration used a short name). Ordo lists John Smith as a strong suggestion and any other charts with that DOB as possible matches. You select the correct Open Dental ID. You do not edit the EOB name first.

---

## Select, unlink, or search yourself

| Action | What it does |
| --- | --- |
| **Select patient** | Links this EOB person to that Open Dental ID. Posting then uses that chart. |
| **Unlink** | Clears the link so you can pick again. |
| **None of these are the correct patient** | Opens a **manual search**: first name, last name, date of birth, or Open Dental ID (PatNum). |
| **Find possible patients** | Runs the suggestion search again. |

Manual search uses the same Open Dental lookup the rest of Ordo uses. Phone and email are **not** searchable in the Open Dental API; use name, DOB, or ID.

---

## No candidates vs Open Dental is down

These are not the same:

| Message | Meaning |
| --- | --- |
| **No candidates found** | Lookups ran. Nobody looked plausible. Try manual search, or confirm the patient exists in Open Dental. |
| **Unable to search Open Dental** | The connection failed. This is **not** “the patient does not exist.” Fix the connection, then search again. |

Ordo will not invent a chart and will not create a new Open Dental patient from the EOB.

---

## What this does not do

- It does not silently pick the top-ranked person when more than one chart looks plausible.
- It does not change the name stored in Open Dental.
- It does not replace **Fetch Open Dental** (that step still loads claims for posting).
- It does not mean every misspelling will appear. Without a date of birth, a badly misspelled last name may still need **manual search** (try an alternate spelling or the Open Dental ID).

---

## Related pages

- [Matching and remarks](matching-and-remarks.md)
- [Patients](../modules/patients.md)
- [Inside an EOB](../modules/working-an-eob.md)
- [When something looks wrong](../examples/when-things-go-wrong.md)
