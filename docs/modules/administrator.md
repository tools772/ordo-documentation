# Administrator

**Administrator** is Ordo’s own control room. It is **not** a clinic module. Dental staff should not expect to see it, and clinic roles cannot be given these permissions.

If you are a practice user reading this: you can skip the page. Your tools live under [Clinic settings](clinic-settings.md).

If you are Ordo staff (platform admin): this is where you onboard a practice and keep the lights on.

---

## Who can open it

Only **platform administrators**. That is a locked vendor list (Ordo / Perfect Ventures staff), plus any extra emails configured on the server. It is separate from “Owner” at a dental clinic.

A clinic Owner can run Bright Smile. They still cannot open Administrator.

---

## What you will find

The Administrator home has two main areas:

### Admins

Platform-level access: who is allowed to operate this control room, and related allowlist tools.

### Clinics

A directory of practices Ordo serves.

Each clinic row typically shows:

- Practice name
- Location summary
- Clinic admins (the dental office people designated as admins)
- Whether the clinic is **allowed** (active) or **disallowed**

You can search by name, location, or admin email.

**Allow / disallow** is the big switch. Disallowing a clinic is how you take a practice off the product without deleting history. They should not keep working in Actual mode once disallowed.

---

## Adding a clinic

Use **New clinic** (or the equivalent button) and fill in the practice identity: name, location, and who the first clinic admins are.

Until a clinic exists, that practice’s **Clinic settings → Integrations** may show that no clinic is provisioned. Matching and posting in Actual cannot start from a blank onboarding.

---

## Inside one clinic (Ordo staff workspace)

Opening a clinic gives a workspace with tabs such as:

| Tab | Typical use |
| --- | --- |
| **Overview** | Status, allow switch, clinic admins. |
| **Users / team / roles / locations** | Same kinds of controls as clinic settings, from the vendor side (for support). |
| **Integrations** | Help a practice connect Open Dental. |
| **API logs / Audit** | Investigate a failed post without logging in as the coordinator. |
| **Keys / security** | Developer and practice keys, security toggles. Treat as highly sensitive. |

Add a clinic admin when the office manager should be able to invite their own staff later. Clinic admins still cannot see this Administrator module.

---

## Example: onboarding Bright Smile

1. Platform admin creates clinic **Bright Smile Dental**, location Austin.
2. Adds Jennifer Park as a clinic admin and **allows** the clinic.
3. Confirms the Open Dental **developer key** is present on the platform.
4. Jennifer, in Clinic settings, pastes the **customer key**, tests, saves, syncs.
5. Jennifer invites Mike as Reviewer and Sarah remains Owner.
6. They run a week in **Demo**, then switch **Actual** for live EOBs.

If step 2 is skipped, Jennifer may be able to sign in but cannot finish integrations.

---

## What Administrator is not

- Not a place for coordinators to post payments.
- Not a replacement for Clinic settings day to day.
- Not something to screenshot into Slack — keys and allowlists live here.

---

## Related pages

- [Clinic settings](clinic-settings.md)
- [Roles and who can do what](../people/roles.md)
- [Demo vs Actual](../workflows/demo-vs-actual.md)
