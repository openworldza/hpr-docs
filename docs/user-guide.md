---
title: User guide
nav_order: 4
---

# User guide

This guide covers what a standard member (`user` role) can do in the registry.
For account creation and the approval process see [Getting started](getting-started.md).

---

## Submitting a dog

Any active member can submit a dog to the registry. Click **+ Add dog** in the
top navigation bar (visible once your account is approved).

### What to fill in

**Identity section:**
- **Registered name** (required) — the name without qualification prefixes
- **Sex** — Male or Female
- **Breed** (required) — from the registry's configured breed list

**Details section:**
- **Date of birth** — must not be in the future
- **Colour** (required)
- **Country of origin** — searchable dropdown
- **Chip ID** — microchip number (displayed in monospace)
- **KUSA number** — registration number (displayed in monospace)

**Birth kennel and breeder:**
- **Birth kennel** — searchable lookup; you can also create a new kennel
- **Breeder** — this field only appears after you select a birth kennel
  - If the kennel lists breeders publicly: shows a dropdown of that kennel's breeders
  - Always includes "Other / not listed" option
  - If the kennel does not list breeders: only shows "Other / not listed"
  - Selecting "Other / not listed" notifies the birth kennel to review

**Parentage:**
- **Sire** — search for male dogs in the registry
- **Dam** — search for female dogs in the registry
- Both fields always allow free text entry as a fallback
- If you enter a parent as free text: the birth kennel is notified to review
  and link the parent to a registry record
- Free text entry never blocks submission

**Health records (mandatory):**
- Standard health tests are configured per registry (e.g. Hips, Eyes)
- For each test you must either:
  - Enter a result, OR
  - Check "Not tested"
- The form cannot be submitted if any test has neither a result nor "Not tested"

**Photo:**
- Upload a photo of your dog (JPEG, PNG, or WebP, max 5MB)
- Optional — can be added after submission

**Qualifications (optional):**
- Add known qualifications at submission time
- Each qualification goes to the approval queue
- Certificate upload is optional at submission but required before approval
- Qualifications can also be added to the dog profile after approval

**Clubs and organisations:**
- Dropdown of known clubs/organisations
- Multiple entries allowed
- "Other" option for clubs not in the list

### After submission

Your dog is created with **status = pending** and goes to the admin approval queue.
It will not appear in search results until an admin approves it.

On the dog's profile page you will see:
> *This record is pending admin approval.*

Once approved the banner disappears and the dog appears in search results.
If rejected, the rejection reason will be shown on the profile.

Check the dog's profile page to see its current status — there is no automatic
notification when your submission is reviewed.

---

## Searching dogs

Navigate to **Dogs** in the top navigation bar (or go to `/dogs`).

**Important:** The search page starts empty — no dogs are shown until you type
a search query. This is intentional design for performance and usability.

The search page lets you:

- **Search by name** — type part of a dog's name in the search box
  - Searches both registered name and display name (which includes qualification prefixes)
  - Also searches by chip ID and registration number
- **Filter by breed** — select from the breed dropdown
- **Filter by sex** — select Male or Female

Results update as you change filters. Results are paginated (20 per page).
Only approved dogs appear in search results.

---

## Dog profiles

Click any dog in the search results to open its profile.

### Display name vs registered name

Every dog has a **display name** that includes earned qualification prefixes.
For example, a dog named "Kennel von Haus Example" with approved VGP and HZP
qualifications appears as "VGP-HZP Kennel von Haus Example" everywhere in the
registry — search results, cards, and the profile heading.

The **registered name** (the name without prefixes) is shown below the heading
when it differs from the display name.

Only approved qualifications marked as "adds to name" contribute to the prefix.
Pending or rejected qualifications do not affect the display name.

### Profile sections

| Section | Details |
|---|---|
| Display name | The dog's name with qualification prefixes (H1 heading) |
| Registered name | Shown below the heading if different from display name |
| Status | Breed, sex, age — compact info strip |
| Photo | Dog image (if uploaded) |
| Qualifications | Earned qualifications grouped by organisation, near the top |
| Health records | Hip and eye scores — mandatory section |
| Details | Date of birth, country of origin, chip ID, KUSA number |
| Parentage | Sire and dam — clickable links if in registry, or text if unlinked |
| Breeder | Breeder name — clickable link if in the registry |
| Kennel | Current kennel — clickable link |
| Clubs & organisations | Membership records |
| History | Owner history, kennel history, name history (collapsible) |

**Unlinked parents:** If a parent was entered as free text (not linked to a
registered dog), it shows in muted italic text with a note that it is unlinked.

---

## Submitting a qualification result

You can add qualification results to any dog in the registry.

### Steps

1. Open the dog's profile page.
2. Click **Add qualification result**.
3. Select the qualification from the grouped dropdown (organised by issuing organisation).
4. Fill in the result fields:
   - Fields shown depend on the qualification type (score, grade, pass/fail)
   - **Date achieved** (required)
   - **Judge** (optional)
   - **Location** (optional)
   - **Notes** (optional)
5. Upload a certificate (optional now, but required before admin approval).
6. Click **Submit**.

### About certificates

Certificates are used for admin verification only. They are **never shown publicly**
on dog profiles. Upload your certificate to help the admin approve your result
quickly — you can upload it at submission or add it later while the result is pending.

### What happens after submission

- The result is created with **status = pending**
- It appears on the dog's profile with a pending badge (visible to you and admins)
- An admin reviews and approves or rejects
- On approval:
  - The result appears publicly on the dog's profile (without certificate)
  - If the qualification adds to the dog's name, the display name updates immediately

---

### Requesting ownership

If you are the owner of a dog in the registry and it is not yet associated with
your account, you can submit an ownership request from the dog's profile page.

1. Open the dog's profile.
2. Click **Request ownership**.
3. Optionally add a message giving context for your request.
4. Click **Submit request**.

The request is sent to an admin for review. You will see a confirmation message
on the page. The admin can approve or reject the request from the approval queue.

---

## COI calculator

The **Coefficient of Inbreeding (COI)** calculator lets you assess genetic
diversity before committing to a breeding. It computes the probability that
two alleles in the offspring are identical by descent.

### How to access it

If you have the `coi:calculate` permission (granted to kennel owners and admins
by default), you will see **COI Calculator** in the navigation menu.

Click it to open the calculator at `/coi`.

### How to use it

1. In the **Sire (Male)** field, search for the prospective sire by name.
2. In the **Dam (Female)** field, search for the prospective dam by name.
3. Click **Calculate COI**.
4. The system displays:
   - **COI percentage** — the main result, with a classification badge (Low, Moderate, High, Very High)
   - **Progress bar** — visual reference showing half-sibling (6.25%), first cousin (12.5%), and full sibling (25%) markers
   - **Completeness percentage** — how much of the pedigree tree is known
   - **Generations deep** — how many generations the calculation spans
   - **Common ancestors** — shared ancestors sorted by contribution, showing the number of paths via sire and dam

### What completeness means

The calculator can only consider ancestors that are registered in the system.
If large portions of the pedigree are unknown (parents entered as free text
rather than linked to registry dogs), the completeness percentage will be low.
A low completeness means the calculated COI is likely an underestimate — the
true COI may be higher because untracked lineage could contain shared ancestors.

### Interpreting results

| COI | Interpretation |
|---|---|
| 0% | No common ancestors found in known pedigree |
| < 5% | Generally considered acceptable |
| 5–10% | Moderate inbreeding — worth reviewing |
| > 10% | High inbreeding — review carefully |
| 25% | Equivalent to full-sibling mating |

These are guidelines, not rules. Breed-specific norms and the completeness
of the pedigree should factor into your assessment.

---

## Kennel profiles

Navigate to **Kennels** in the top navigation bar (or go to `/kennels`).

- Search kennels by name
- Click a kennel card to open its profile
- A kennel profile shows name, KUSA number, status (active/inactive), location,
  contact details, and the founding date

---

## Breeder profiles

Navigate to **Breeders** in the top navigation bar (or go to `/breeders`).

- Search breeders by name
- Click a breeder card to open their profile
- A breeder profile shows name, contact details, and linked kennel

---

## Account settings

Click the **account button** (your avatar) in the top-right corner to:

- View your account
- Sign out

Role upgrades (e.g. from `user` to `kennel_owner`) are handled by the registry
administrator — contact them if you need your role changed.
