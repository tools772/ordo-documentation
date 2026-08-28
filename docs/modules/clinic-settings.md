# Clinic settings

**Clinic settings** is the practice office: who works here, what they are allowed to do, how Ordo talks to Open Dental, and the logs you open when something needs explaining.

Open it from the sidebar: **Clinic settings**. You need a role that can view clinic settings. Changing team, roles, or the Open Dental connection needs **Manage team and roles**.

If you do not see this item, your role is view-or-work only (for example Viewer or Reviewer). Ask an Owner or Admin.

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

**Example — invite a new coordinator**

1. Sarah (Owner) opens **Clinic settings → Users**.
2. She clicks to add a person: `Priya Nair`, `priya@brightsmile.com`, role **Reviewer**, location **Main Street**.
3. Priya can now review and approve matches. She cannot post and cannot invite others.

Deactivating someone keeps the history (audit still shows their name) but they should no longer work in the product. Do not recycle logins.

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

**Example — first-time connect**

1. Jennifer opens **Integrations**.
2. She pastes the customer key Open Dental support provided.
3. She clicks **Test**. Success toast: Ordo can reach Open Dental.
4. She **Saves**.
5. She clicks **Sync** and waits. Status shows last sync time and how many patients/claims were stored.

Until this is connected, **Fetch Open Dental** in Actual mode cannot load live charts. Demo uses sample data and does not need a real key.

!!! warning "Keys are secrets"
    Do not paste customer keys into email, chat, or screenshots. If a key leaked, rotate it in Open Dental and save the new one here.

---

## API Logs

Each call to Open Dental can appear here: test connection, sync, fetch, post. If Test fails, open API Logs (or the error card on the integrations panel) and look at the latest row. The message is often enough for Ordo support without sending screenshots of patient names.

Most coordinators will never need this tab. Office managers use it with support on the phone.

---

## Audit

This is the human history:

- Who uploaded which file
- Who approved or rejected a match
- Who posted
- Who changed settings, when that is logged

**Example.** The dentist asks “who posted Maria Santos?” Jennifer opens **Audit**, searches the time window, and sees Jennifer Park posted at 2:14 p.m. after Mike approved at 2:09 p.m.

Prefer Audit over API Logs when the question is about *people*. Prefer API Logs when the question is about *the wire to Open Dental*.

---

## Profile and notifications

- **Profile** — your display name, theme (light/dark).
- **Notifications** — opt in to notices such as “extraction finished” or “extraction failed,” depending on what is enabled for your practice.

---

## If the page says no clinic is provisioned

Integrations may show that this practice is not set up yet. That is Ordo onboarding — not something a Reviewer can fix. Ask your office manager to contact Ordo support.

---

## Related pages

- [Roles and who can do what](../people/roles.md)
- [Demo vs Actual](../workflows/demo-vs-actual.md)
