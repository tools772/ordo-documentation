# Clinic settings

**Clinic settings** is the practice office: who works here, what they are allowed to do, how Ordo talks to Open Dental, and the logs you open when something needs explaining.

Open it from the sidebar: **Clinic settings**. You need a role that can view clinic settings. Changing team, roles, or the Open Dental connection needs **Manage team and roles**.

If you do not see this item, your role is view-or-work only (for example Viewer or Reviewer). Ask an Owner or Admin.

The **top header** shows the clinic and location you are in. If you have more than one site, click that pill to switch. Owners and Admins can also open **Manage or add locations** from that menu.

---

## The tabs

| Tab | What it is for |
| --- | --- |
| **Users** | People, roles, and locations for this practice. |
| **Integrations** | Connect and test Open Dental; sync the replica. |
| **API Logs** | Technical diary of Open Dental calls. |
| **Audit** | Who uploaded, approved, rejected, posted. |
| **Profile** | Your own name and display preferences (including theme). |
| **Notifications** | How you want to be notified (for example extraction finished). |

The Users tab also contains **roles** and **locations** for people who can manage the team.

---

## Users, roles, and locations

### Users

Each person has a name, email, role, active/inactive flag, and optional **locations**.

**Example — grant access to someone who already signed up**

1. Priya signs up on Ordo with `priya@brightsmile.com`. She sees **Waiting for access**.
2. Sarah (Owner) opens **Clinic settings → Users** and invites that same email: `Priya Nair`, role **Reviewer**, location **Main Street**.
3. Priya taps **I've been added — check again** (or signs out and in). She can now review and approve matches. She cannot post and cannot invite others.

You can also add an email before they sign up. They will get in on first sign-in.

Deactivating someone keeps the history (audit still shows their name) but they cannot open Ordo until you set them Active again. Do not recycle logins.

The last **Owner** cannot be demoted. That protects you from locking the practice out.

### Roles

Built-in starting points:

| Role | In one sentence |
| --- | --- |
| **Owner** | Full clinic access. Last owner stays an owner. |
| **Admin** | Run the practice: upload, review, post, manage the team. |
| **Reviewer** | Review EOBs and approve/reject matches. Cannot post or manage settings. |
| **Viewer** | Read dashboard, patients, and reports. |

You can **clone** a role and tick different permissions (for example an “Insurance poster” who can post but cannot invite users). Details and a permission table: [Roles and who can do what](../people/roles.md).

### Locations

Multi-site practices can list locations (Main Street, North Clinic) and map users to them. A user with no locations may still be practice-wide depending on how your clinic was set up — if a new hire “cannot see files,” check location mapping before assuming the role is wrong.

---

## Integrations (Open Dental)

This is how Ordo learns your charts and how it posts.

Typical pieces:

- Connection name
- Open Dental API URL (usually the standard Open Dental API address)
- **Customer key** (your practice’s key — treat it like a password)
- Environment (for example test vs production, as labeled on screen)
- **Test connection**
- **Save**
- **Sync** (refresh Ordo’s copy of patients/claims)

A **developer key** is held by Ordo (platform). The practice provides the **customer key**. If Test stays disabled, either the developer key is missing (Ordo staff) or no customer key has been entered yet.

**Save** and **Test** are separate. You can **Save** the customer key even if Test has not succeeded yet — for example the key is not registered in Open Dental yet. Ordo stores the key and reminds you to Test when it is registered. Fetch and Post still need a working connection, so Test (and then Sync) before live posting.

**Example — first-time connect**

1. Jennifer opens **Integrations**.
2. She pastes the customer key Open Dental support provided.
3. She **Saves**. Toast: keys saved (even if Test is still pending).
4. When the key is live in Open Dental, she clicks **Test**. Success toast: Ordo can reach Open Dental.
5. She clicks **Sync** and waits. Status shows last sync time and how many patients/claims were stored.

Until this is connected, **Fetch Open Dental** in Actual mode cannot load live charts. Demo uses sample data and does not need a real key.

!!! warning "Keys are secrets"
    Do not paste customer keys into email, chat, or screenshots. If a key leaked, rotate it in Open Dental and save the new one here.

---

## API Logs

Each call to Open Dental can appear here: test connection, sync, fetch, post. If Test fails, open API Logs (or the error card on the integrations panel) and look at the latest row. The message is often enough for Ordo support without sending screenshots of patient names.

The list is **paginated** (default 25 rows). You can search, filter to **success** or **failed**, and page through older calls. Expand a row for the endpoint and status code.

How to read the **status code** (400, 401, 429, …) and the posting refusals Open Dental sends: [Open Dental errors](../errors/open-dental.md).

Most coordinators will never need this tab. Office managers use it with support on the phone. Copy the error text (not patient names) into an email to **[help@perfect.ventures](mailto:help@perfect.ventures)**.

---

## Audit

This is the human history:

- Who uploaded which file
- Who approved or rejected a match
- Who posted
- Who changed settings, when that is logged

Filter by event type (for example Payment Posted, Claim Approved, EOB Uploaded), by EOB, and by date range. Search and page through results the same way as API Logs.

**Example.** The dentist asks “who posted Maria Santos?” Jennifer opens **Audit**, filters to **Payment Posted**, searches the time window, and sees Jennifer Park posted at 2:14 p.m. after Mike approved at 2:09 p.m.

Prefer Audit over API Logs when the question is about *people*. Prefer API Logs when the question is about *the wire to Open Dental*.

---

## Profile and notifications

- **Profile** — your display name, theme (light/dark).
- **Notifications** — opt in to notices such as “extraction finished” or “extraction failed,” depending on what is enabled for your practice.

---

## If the page says no clinic is provisioned

Integrations may show that this practice is not set up yet. That is Ordo onboarding — not something a Reviewer can fix. Ask your office manager to email **[help@perfect.ventures](mailto:help@perfect.ventures)**.

---

## Related pages

- [Roles and who can do what](../people/roles.md)
- [Demo vs Actual](../workflows/demo-vs-actual.md)
- [What each operation does](../workflows/operations.md)
- [Open Dental errors](../errors/open-dental.md)
