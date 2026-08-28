# Roles and who can do what

A **role** is a nametag that turns modules and buttons on or off. Two people can work the same EOB and see different buttons. That is intentional.

Owners and Admins manage roles in **Clinic settings → Users** (roles panel).

---

## The four starter roles

| Role | Meant for | Can post? | Can invite staff? |
| --- | --- | --- | --- |
| **Owner** | Practice owner / responsible party | Yes | Yes |
| **Admin** | Office manager who runs posting day to day | Yes | Yes |
| **Reviewer** | Insurance coordinator who checks matches | No | No |
| **Viewer** | Shadow, accountant, dentist who only looks | No | No |

The **Owner** role is a system role. You cannot delete it, and the last remaining owner cannot be demoted.

Admins start with the same clinic abilities as owners in the default setup (upload, review, post, manage team). You can narrow an Admin clone later if you want.

---

## Permission catalog (clinic)

Grouped the way the product labels them.

### View

| Permission | What it unlocks |
| --- | --- |
| EOB dashboard | See the inbox and open files |
| Patients | See the cross-file patient list |
| Reports | See Reports |
| Clinic settings | Open practice settings (read) |

### Work

| Permission | What it unlocks |
| --- | --- |
| Upload EOBs | Drop new remittance files |
| Archive | Archive or restore EOBs and patients |
| Edit extracted data | Correct names, lines, amounts Ordo read |
| Approve match | Confirm the Open Dental claim |
| Reject match | Discard a candidate without posting |
| Post payment | Write `InsPayAmt` to Open Dental |

### Clinic admin

| Permission | What it unlocks |
| --- | --- |
| Manage team and roles | Create roles, invite users, edit locations, manage the Open Dental connection |

---

## What each starter role can do

| Ability | Owner | Admin | Reviewer | Viewer |
| --- | --- | --- | --- | --- |
| See dashboard, patients | Yes | Yes | Yes | Yes |
| See reports | Yes | Yes | No* | Yes |
| Upload / archive / edit | Yes | Yes | Edit only | No |
| Approve / reject match | Yes | Yes | Yes | No |
| Post payment | Yes | Yes | No | No |
| Manage team | Yes | Yes | No | No |

\*Default Reviewer does **not** include Reports. If your coordinators should see the scoreboard, clone Reviewer and tick **Reports**.

Default Reviewer **does** include edit, approve, and reject, and **does not** include upload, archive, or post.

---

## Bright Smile stories

### Mike (Reviewer) — “I cannot post”

Mike opens Maria Santos, fetches, approves. **Post payment** is missing. Jennifer (Admin) opens the same patient and posts. This is the two-person control Bright Smile wanted.

If the office later decides Mike should post, Sarah clones Reviewer, names it **Poster**, ticks **Post payment** (and maybe **Upload EOBs**), and assigns Mike that role. No software developer is required.

### Alex (Viewer) — “I only wanted to watch”

Alex can open Reports for the owner meeting. He cannot archive a file, cannot approve, cannot post. If a button is missing, he should not hunt for a bug.

### Priya — custom “Insurance poster”

Sarah wants someone who can upload and post but **cannot** invite users or change roles:

1. Clone **Admin**.
2. Untick **Manage team and roles**.
3. Save as **Insurance poster**.
4. Assign Priya.

Priya still sees Clinic settings if View settings is ticked, but she cannot rewrite the team.

---

## Locations and roles together

A user can be Admin and still “see nothing” if they are mapped to **North Clinic** and today’s files belong to **Main Street**, depending on how your practice uses locations. When access looks random, check **location mapping** before changing roles.

---

## Related pages

- [Clinic settings](../modules/clinic-settings.md)
- [Post a payment](../workflows/posting-a-payment.md)
