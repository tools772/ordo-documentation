# Ordo Help

Ordo is a **payment operations** tool for dental practices. It takes the insurance payment document you already receive — the **EOB** — and helps your team post that payment into **Open Dental** without retyping every line by hand.

This site is written for the people who actually do the work: office managers, insurance coordinators, billing staff, and practice owners. You do not need to be a programmer to use it.

---

## The problem Ordo is solving

After a patient visit, the practice sends a claim to the insurance company. Days or weeks later, the insurance company sends back an **Explanation of Benefits (EOB)** — a PDF that says, for each procedure, how much they are paying.

Someone then has to:

1. Open that PDF.
2. Find the matching patient and claim in Open Dental.
3. Type the paid amounts onto the right procedure lines.
4. Repeat for every patient on the remittance.

That work is slow, easy to mistype, and hard to audit later. Ordo is the inbox, reviewer, and posting desk for that job.

---

## What Ordo does — and what it does not do

| Ordo **does** | Ordo **does not** |
| --- | --- |
| Read the EOB PDF and pull out patients, claims, and procedure amounts | Replace Open Dental as your practice management system |
| Show you the Open Dental claim it thinks is the right match | Automatically write money into Open Dental without a person clicking **Post payment** |
| Let a reviewer approve the match, then a poster write the payment | Decide medical necessity or change what the insurance paid |
| Keep a log of who uploaded, approved, rejected, or posted | File the original claim with the payer |

The golden rule: **nothing is written to Open Dental until someone with the right role clicks Post payment.** Approve is a confirmation, not a post.

---

## A 30-second picture of the day

Imagine Bright Smile Dental. Jennifer (office manager) uploads this week's Cigna remittance. Ordo reads the PDF and lists every patient on it. Mike (insurance coordinator) opens Maria Santos, fetches her Open Dental chart, checks that the cleaning and exam lines match, and approves. Jennifer then posts. Open Dental now shows the insurance paid amount. Reports later show how many files were posted that week.

That same path is described step by step in [Post a payment](workflows/posting-a-payment.md) and as a story in [A typical Monday morning](examples/typical-morning.md).

---

## The modules (the left-hand menu)

Ordo is organized into **modules**. A module is simply a section of the product — like a room in an office. You only see the rooms your role is allowed to enter.

| Module | What it is for |
| --- | --- |
| **EOB Dashboard** | The file inbox. Upload remittances, see their status, open a file to work it. |
| **Patients** | Find a person across all files without opening the EOB first. |
| **Reports** | Counts and dollars for operations: uploaded, posted, failed, by carrier. |
| **Docs** | Short in-app help, plus a link to this longer site. |
| **Clinic settings** | Your practice: people, roles, locations, Open Dental connection, logs. |

Start with [What is a module?](modules/overview.md) if you want a map before diving in.

---

## Two modes: Demo and Actual

| Mode | Use it when | What happens |
| --- | --- | --- |
| **Demo** | Training, screenshots, “show me how this works” | Sample data only. Nothing touches your live charts. |
| **Actual** | Real work for the practice | Live files, live patients, live Open Dental (when connected). |

Switching is in the sidebar (and on the sign-in screen). Details: [Demo vs Actual](workflows/demo-vs-actual.md).

---

## How to use this site

- New to Ordo? Read [First day with Ordo](getting-started.md).
- Stuck on a word like “EOB” or “CDT”? Open the [Word list](glossary.md).
- Looking for a screen? Use the **Modules** tab.
- Looking for a procedure (“how do I post?”)? Use the **How to** tab.
- Prefer stories? Use the **Examples** tab.
- An error on screen? Use the **Errors** tab — what it means, what to try, and when to contact Ordo. Open Dental API numbers (400, 401, …) have their own page: [Open Dental errors](errors/open-dental.md).
- Want every button explained, including which **status** it changes? [What each operation does](workflows/operations.md) and [Statuses](workflows/statuses.md).

There is a search box at the top of every page. Try typing a button name, such as **Approve match** or **Fetch Open Dental**.
