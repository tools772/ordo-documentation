# First day with Ordo

This page is the orientation. After you finish it, you should be able to sign in, find the inbox, open a sample file, and know which buttons are safe to click.

---

## 1. Sign in

Go to **[app.useordo.ai](https://app.useordo.ai)** (or the address your practice was given).

On the sign-in screen you will see two modes:

- **Demo** — practice with sample data. Safe. Nothing is written to your real Open Dental.
- **Actual** — your live practice. Use this only when you are ready to work real EOBs.

For a first day, choose **Demo**. Then either:

- Click **Enter Demo Mode** (no real password needed in Demo), or
- In Actual, sign in with **Continue with Google**, or with username/email and password.

More detail: [Sign in](people/signing-in.md).

---

## 2. Look around the screen

The **top header** shows the clinic name and location you are working in. If you belong to more than one site, click that pill to switch. On the live production site a blue **Production** bar sits above the page.

The **left sidebar** is the building directory. From top to bottom you will typically see:

1. **Ordo** (the logo) — you are in payment operations.
2. **Modules** — EOB Dashboard, Patients, **Appointments** (if Ordo has turned it on for your clinic), and a collapsible **Analytics** group (Posting Analytics, Payment Analytics, Fee Analysis, Analytics AI).
3. **Practice** — Clinic settings (if your role can open it).
4. **Help & docs** — a link to this site, plus **help@perfect.ventures** if you need to raise an issue.
5. **App mode** — Demo or Actual toggle, plus a HIPAA-ready note.

If a module is missing, that is normal. Your **role** hides what you are not allowed to use. A Viewer will not see posting buttons. An insurance reviewer may not see Clinic settings. See [Roles and who can do what](people/roles.md).

---

## 3. Open the EOB Dashboard

This is the inbox. Each row is one uploaded remittance file, not one patient.

You will see:

- How many files were uploaded today
- How many still need a person to look at them
- How many payments have been posted
- Files that failed to read

Under the summary is the **file list**. You can search by file name, filter by status (Uploaded, Extracting, Extracted, Failed, Archived), and filter by **uploaded date** (today, last 7 days, last 30 days, this month). Files waiting for confirmation show a **Confirm layout** badge (usually under Active / Uploaded — there is no separate Confirm layout tab).

If your role allows it, there is an **Upload EOBs** button. Prefer **Detect & upload**, then **Process EOB** when Ordo shows the detected payer. Demo may already have sample files so you can skip uploading.

Each row also has a menu with **Download EOB**. That downloads the original PDF (or image) you uploaded — useful when you want to compare what Ordo read against the paper.

Upload accepts **PDF**, **JPG**, and **PNG** (up to 50 MB). Ordo auto-detects the remittance layout — Cigna, MetLife, Guardian, several Delta forms, Premera, Aetna Medicare, and others. The full list: [What files and layouts Ordo reads](workflows/supported-formats.md).

---

## 4. Open one file

Click a row. You land on that remittance’s patient list.

Do this in order the first time:

1. Tick the checkbox next to one patient (or a few).
2. Click **Fetch Open Dental**. Wait for **Fetching from Open Dental…** to finish. This loads matching chart data so the Open Dental tab is not empty.
3. Click the patient name. A **Workflow guide** button on the page explains which actions are allowed at each status.
4. Look at the four tabs:
   - **EOB Review** — what Ordo read from the PDF.
   - **Payment Analysis** — did insurance pay the contracted fee? (You can skip this on day one.)
   - **Open Dental** — the claim Ordo thinks is the match, line by line.
   - **Audit** — the individual checks (name, date of service, procedure codes, amounts).

!!! warning "Opening a patient before Fetch"
    If you open a patient **before** clicking Fetch Open Dental, you will only see the EOB side. That is expected, not a bug. Go back, select the patient, fetch, then open again.

---

## 5. Learn the two “commit” buttons

On the Open Dental tab you will eventually see:

| Button | What it means in plain language | Writes to Open Dental? |
| --- | --- | --- |
| **Approve match** | “Yes, this is the right claim.” | No |
| **Post payment** | “Write the insurance paid amounts now.” | Yes (Actual mode only, when connected) |
| **Reject match** | “This is the wrong claim. Throw this match away.” | No |

**Post payment** stays off until the match is approved. That is on purpose: two steps, two chances to stop.

In Demo, posting is simulated. In Actual, posting writes `InsPayAmt` (the plan covered amount from the EOB) onto the Open Dental procedure lines.

Walk through a full example: [Post a payment](workflows/posting-a-payment.md).

---

## 6. Peek at Patients and Analytics

- **Patients** is the same extracted people, but across every file. Use it when someone asks “where is Maria Santos?” and you do not remember which PDF she was on. Click a row to open her detail page, including **EOB History** if she appears on more than one remittance.
- **Analytics → Posting Analytics** is the operations scoreboard (it used to be called Reports). Click **Load overview**, then filter by uploaded date and by which EOBs you care about. Archived files are left out.
- **Analytics → Payment Analytics** shows where insurance paid less than your contract. Your office manager usually owns this. More: [Analytics](modules/analytics.md).

---

## 7. What not to do on day one

- Do not switch to **Actual** and upload a **real** patient EOB unless your practice has already gone live with Ordo. Until then, use Demo or synthetic (fake) files.
- Do not click **Post payment** on a claim you have not read. Approve is cheap; posting is the real write.
- Do not assume a green “Match” on every line means the *patient* is correct. Always glance at the Audit tab if something feels off.

---

## A first-day checklist

Copy this and tick it off:

- [ ] I can sign in (Demo is fine).
- [ ] I can find **EOB Dashboard** in the sidebar.
- [ ] I can open a file and see a list of patients.
- [ ] I know I must **Fetch Open Dental** before the Open Dental tab has live chart data.
- [ ] I know **Approve match** does not post, and **Post payment** does.
- [ ] I know my role may hide some buttons, and that is expected.
- [ ] I know to email **help@perfect.ventures** if I am stuck.

When you are ready, read [What is a module?](modules/overview.md) or jump straight into [Inside an EOB](modules/working-an-eob.md). For a full button catalog, see [What each operation does](workflows/operations.md). Stuck? Email **[help@perfect.ventures](mailto:help@perfect.ventures)**.
