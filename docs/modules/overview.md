# What is a module?

A **module** is one section of Ordo — a room with a job. The left sidebar lists the rooms your role can enter. This page is the floor plan. Each module has its own longer page with examples.

---

## Why the product is split this way

Insurance posting is a pipeline:

**File arrives → people are read off the page → someone matches them to the chart → someone posts → someone checks the numbers later.**

Each module is one stage of that pipeline (plus settings and help):

```
  Upload PDF          Find a person         Check the books
       │                    │                      │
       ▼                    ▼                      ▼
 EOB Dashboard  ←──  Patients list  ──→  Reports
       │
       ▼
  Open one file
  (EOB Review / Open Dental / Audit)
       │
       ▼
  Clinic settings (people, Open Dental connection)
```

You do not have to visit every room every day. Many coordinators live in **EOB Dashboard**. The office manager dips into **Reports** on Friday. The owner opens **Clinic settings** when a new hire starts.

---

## The sidebar, group by group

### Modules (daily work)

| Menu label | Job in one sentence | Typical visitor |
| --- | --- | --- |
| **EOB Dashboard** | Inbox of remittance files. | Everyone who posts or reviews. |
| **Patients** | All extracted people, across files. | “Where is this patient?” questions. |
| **Reports** | Uploaded / posted / failed, with filters. | Office manager, owner. |
| **Docs** | Short in-app articles, plus a link here. | Anyone. |

### Practice

| Menu label | Job in one sentence | Typical visitor |
| --- | --- | --- |
| **Clinic settings** | Team, roles, locations, Open Dental connection, logs. | Owner, clinic admin. |

### Ordo (vendor)

| Menu label | Job in one sentence | Typical visitor |
| --- | --- | --- |
| **Administrator** | Onboard clinics, allow access, platform keys. | Ordo staff only. |

If **Administrator** is missing for you, that is correct. It is not a clinic role.

---

## Example: who uses which rooms at Bright Smile

Bright Smile Dental has four people in the demo story:

| Person | Role | Modules they live in |
| --- | --- | --- |
| **Sarah Chen** | Owner | Everything clinic-side. She sets roles, glances at Reports on Monday, rarely posts. |
| **Jennifer Park** | Admin | Dashboard (upload + post), Clinic settings (invite staff), Reports. |
| **Mike Johnson** | Reviewer | Dashboard and the Open Dental tab. He approves and rejects. He cannot post and cannot change settings. |
| **Alex Rivera** | Viewer | Dashboard, Patients, Reports — read only. Useful for a new hire shadowing, or an accountant who should not click Post. |

If Alex opens an EOB, he can read Maria Santos’s lines. He will not see **Post payment**. That is the product working as designed, not a broken button.

---

## What “you cannot see this” usually means

Three common reasons:

1. **Role.** Your permission set does not include that module or button. Ask an Owner or Admin to change your role — do not try to “fix” the screen.
2. **Mode.** In Demo you are often signed in as a Viewer. Switch to Actual (with a live account) for real posting, or ask for a role that can post.
3. **No clinic yet.** Integrations and some settings stay empty until an Administrator has added the practice.

---

## Related pages

- [EOB Dashboard](eob-dashboard.md)
- [Inside an EOB](working-an-eob.md)
- [Patients](patients.md)
- [Reports](reports.md)
- [Clinic settings](clinic-settings.md)
- [Administrator](administrator.md)
- [Roles and who can do what](../people/roles.md)
