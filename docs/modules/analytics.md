# Analytics

**Analytics** is the collapsible group in the sidebar, under **Modules**. It holds four pages that answer “how is the work going?” and “is insurance paying what they owe us?”

| Menu label | Question it answers | Longer page |
| --- | --- | --- |
| **Posting Analytics** | How many remittances did we upload, post, or fail? Which claims in Open Dental still have no payment posted? | [Posting Analytics](posting-analytics.md) |
| **Payment Analytics** | Did the insurance company pay the contracted fee — on this week’s EOBs, and on past claims in Open Dental? | [Payment Analytics](payment-analytics.md) |
| **Fee Analysis** | What does each insurer (and our office UCR) pay for a CDT code on a given date? | [Fee Analysis](fee-analysis.md) |
| **Analytics AI** | Ask any of the above in plain English. | [Analytics AI](#analytics-ai) below |

The old **Reports** page now lives at **Posting Analytics → Overview**. Old bookmarks to Reports still work; they open that tab.

**Nothing on these pages writes to Open Dental.** Analytics reads Ordo’s EOBs, Ordo’s copy of Open Dental, and your clinic’s fee schedules. It never posts, adjusts, or changes a claim.

---

## Who can see it

| Permission (as labelled in the role editor) | What it unlocks |
| --- | --- |
| **View analytics** | Posting Analytics, Payment Analytics, and Fee Analysis. |
| **Analytics AI chat** | The Analytics AI page. |

Owners, Admins, and Viewers have both by default. The default **Reviewer** does not — clone the role and tick them if your coordinators need analytics. See [Roles and who can do what](../people/roles.md).

---

## Pages stay idle until you ask

Analytics pages do not crunch numbers the moment you open them. You see a card such as **Overview is idle** or **Results stay idle**, with a button to load or run. That keeps tab switching fast and stops a big practice from waiting on numbers nobody asked for.

- **Load …** / **Load saved results** — show the last saved result.
- **Run analysis** — calculate again with the current filters.

---

## Fetch first, then analyze

Two tabs work with past claims straight from Open Dental rather than with uploaded EOBs:

- **Payment Analytics → Historical Analysis** — were past claims paid at the contracted fee?
- **Posting Analytics → Missing Posting** — which sent or received claims still have no insurance payment posted?

Both use the same two steps:

1. **1. Fetch data** — you ask Ordo to pull claims from Open Dental for a date range. This creates a **fetch job**. The job runs in the background, so you can leave the page.
2. **2. Analyze** — pick a finished fetch job and click **Run analysis**. Ordo works on that saved copy (a snapshot), not on live Open Dental, so the numbers do not shift while you read them.

### Fetch job statuses

| Status | Meaning |
| --- | --- |
| **Queued** | Waiting to start. |
| **Fetching** | Pulling claims from Open Dental now. |
| **Complete** | Every date in the range was fetched. Ready to analyze. |
| **Partially complete** | Some dates failed. You can analyze what arrived, or retry the failed dates. |
| **Failed** | Nothing usable arrived. Check the Open Dental connection, then retry. |

### Good to know

- **Historical and Missing Posting jobs are separate.** A job fetched for one tab never shows up in the other, because each pulls different claims.
- **Asking twice is safe.** If an identical job is already running, Ordo joins it instead of starting another. If an identical job already finished, Ordo fetches it again so you get fresh data. Archived jobs are never reused.
- **Old jobs tidy themselves up.** Finished fetch jobs and past analysis runs are removed automatically after **90 days**. Fetch again if you need an older range.

---

## Analytics AI

Open **Analytics AI** in the sidebar and type a question, for example:

- *Show MetLife underpayments from Open Dental for the last 30 days*
- *Summarize posting metrics for this month*
- *List underpayment work items that need review*

Ordo runs the same tools the other Analytics pages use — Historical Analysis, the remittance underpayment queue, or posting metrics — and then summarizes the **real results**. Small tags under each answer show which tools ran. The numbers come from your data, not from the AI guessing.

Click **New chat** to start over. If you see “You don’t have the Analytics AI permission,” ask an Owner to tick **Analytics AI chat** on your role.

!!! tip "Treat AI answers as a starting point"
    If a number matters (for an appeal or the owner huddle), open the matching page — Payment Analytics or Posting Analytics — and check the lines there.

---

## Related pages

- [Posting Analytics](posting-analytics.md)
- [Payment Analytics](payment-analytics.md)
- [Fee Analysis](fee-analysis.md)
- [Payment Analysis inside an EOB](../workflows/payment-analysis.md)
- [Fee schedules and date maps](../workflows/fee-schedules.md)
