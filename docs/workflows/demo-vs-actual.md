# Demo vs Actual

Ordo has two **app modes**. They look similar on purpose, so training feels like the real product. They are not the same world.

You can switch in the **sidebar** (bottom) and on the **sign-in** screen.

| | **Demo** | **Actual** |
| --- | --- | --- |
| Data | Sample practice (Bright Smile–style fake charts and files) | Your live practice |
| Open Dental | Simulated / sample | Real connection when configured |
| Post payment | Practice click; does not write your production charts | Writes `InsPayAmt` to Open Dental |
| Who you are | Typically a sample Viewer unless you use a live login | Your real user and role |
| Use it for | Training, screenshots, “show the dentist” | Monday morning posting |

---

## Demo — the safe sandbox

Choose Demo when you want to click without fear.

- Sample EOBs and patients already exist, so you may not need to upload.
- Demo sign-in does not require your production password.
- The demo identity is **read-oriented** (Viewer): you can tour Dashboard, Patients, and Reports. Posting buttons may be hidden. That is so a first-day user cannot think they posted live money.
- Switching into Demo stores a local “I am practicing” flag on that computer.

**Example.** Sarah walks a new hire through Maria Santos. She switches to **Demo**, opens the sample Cigna file, and narrates Fetch → Open Dental → Audit. No real patient data is on the projector.

---

## Actual — live work

Choose Actual when the PDF in your hand is a real remittance.

- Sign in with email and password, or an email one-time code.
- You only see modules your **role** allows.
- Upload, fetch, approve, and post talk to live storage and, when connected, live Open Dental.
- Treat everything as **patient payment information**. Do not screenshot full EOBs into chat.

**Example.** Jennifer switches to **Actual** at 8:05 a.m., uploads the real Cigna PDF, and posts after Mike reviews. If she had stayed in Demo, that PDF would never have entered the live inbox.

---

## How to switch without getting confused

1. Look at the sidebar label: it says **Demo** or **Actual**.
2. If you are about to upload a **real** EOB, it must say **Actual**.
3. If you are training, it must say **Demo**.
4. After switching, you should see a confirmation toast. Lists will reload. A file that exists only in Actual will not appear in Demo, and vice versa.

!!! danger "The mix-up to avoid"
    Uploading a real patient EOB while still in Demo (or into a training discussion) is how real names end up in the wrong place. Check the sidebar **before** you drop the PDF.

---

## “HIPAA-ready” on the sidebar

The sidebar notes that data is encrypted at rest and in transit. That is a **product control**, not a legal stamp that your office is “done” with HIPAA. Live patient EOBs are still sensitive. Follow your practice’s policies: who may sign in, which computers are used, and when to use Actual.

Until your practice has officially gone live with Ordo, prefer Demo or synthetic (fake) files.

---

## Related pages

- [Sign in](../people/signing-in.md)
- [First day with Ordo](../getting-started.md)
- [Clinic settings](../modules/clinic-settings.md)
