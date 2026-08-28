# A typical Monday morning

A story of one remittance through Ordo. The numbers are realistic but fictional. Use it as a picture of “what good looks like,” then follow the click-by-click version in [Post a payment](../workflows/posting-a-payment.md).

---

## 7:45 a.m. — The PDF arrives

Cigna’s weekly remittance lands in Jennifer Park’s inbox: `Cigna_Remit_Aug24.pdf`. Three patients are on it, including **Maria Santos** (exam + cleaning, plan covered $142.00).

Jennifer makes coffee, opens Ordo, and glances at the sidebar: **Actual**. Not Demo. These are real patients.

---

## 7:52 a.m. — The inbox

She opens **EOB Dashboard**. Last week’s files are **Posted**. She clicks **Upload EOBs**, drops the PDF, and waits. Status moves Extracting → **Extracted**. The row shows 3 patients, 3 claims, 8 procedures.

She does not post yet. She messages Mike: “Cigna is in the inbox.”

---

## 8:10 a.m. — Fetch, don’t guess

Mike opens the file, ticks all three patients, clicks **Fetch Open Dental**. He starts with Maria.

- **EOB Review:** Maria Santos, June 12, D0150 $42, D1110 $100.
- **Open Dental:** recommended claim **18421**, same date, both codes **Match**.
- **Audit:** all signals pass.

He types a line remark on the cleaning: `Cigna paid $100`. He clicks **Approve match**. He does not have **Post payment** — by design.

James Lee’s recommended claim is last year’s visit. Mike picks the June claim from the candidate list, checks Audit, approves.

The third patient is **Needs review**: two people named Patel with overlapping dates. Mike opens Audit, rejects the wrong candidate, and leaves a payment remark: `Two Patels — confirmed DOB with front desk`. He will come back after Jennifer checks the chart.

---

## 8:40 a.m. — Post the easy ones

Jennifer filters the file to **Approved**, opens Maria, clicks **Post payment**. Confirmation with a claim payment number. Same for James.

Patel is still waiting. They will not rush a hard mismatch.

---

## 9:00 a.m. — Someone asks at the desk

Maria is at the front desk: “Did Cigna pay my cleaning?” Alex (Viewer) is covering phones. He does not know the file name. He opens **Patients**, types `Santos`, sees **Posted**, and can tell Maria yes — without having a Post button he could click by accident.

---

## 12:30 p.m. — The leftover

Front desk confirms Patel’s date of birth. Mike fetches again, selects the correct claim, approves. Jennifer posts.

The file’s patients are all **Posted**. Jennifer leaves it in Active until Friday in case Cigna sends a correction. Next week she may **Archive** it so it stops cluttering the inbox. Reports will still have counted it while it was active; after archive it drops out of Reports — so she archives *after* the owner has seen Friday’s numbers, not before.

---

## Friday 4:00 p.m. — Reports

Sarah opens **Reports**, last 7 days, all EOBs. Posted count includes Monday’s Cigna. Failed jobs is zero. She does not need to open Maria’s claim unless a dollar looks wrong.

---

## What to copy from this story

1. Check **Actual** before uploading real PDFs.
2. Fetch before opening patients.
3. Approve and post can be two people.
4. Stop on hard mismatch / two similar names.
5. Patients module is for “where is this person?”
6. Reports is for the week, not for arguing with a patient at the window.

---

## Related pages

- [Post a payment](../workflows/posting-a-payment.md)
- [When something looks wrong](when-things-go-wrong.md)
- [Roles and who can do what](../people/roles.md)
