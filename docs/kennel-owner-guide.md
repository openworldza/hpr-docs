---
title: Kennel owner guide
nav_order: 5
---

# Kennel owner guide

This guide covers what a kennel owner (`kennel_owner` role) can do in the registry.
Kennel owners can do everything a standard user can do — see [User guide](user-guide.md)
for browsing, searching, and ownership requests.

Your account must be a member of at least one kennel before kennel-owner features
are available. An admin adds you as a member via the kennel's member management page.

---

## Adding a dog

Click **+ Add dog** in the top navigation bar. This opens the dog submission form.

### The dog form

Fill in as many fields as you can. Required fields are marked — colour is mandatory.

**Section 1 — Identity**
- Registered name
- Kennel suffix — your kennel is pre-selected; you cannot submit dogs for other kennels
- Sex (Male / Female)

**Section 2 — Details**
- Breed (from the registry's configured breed list)
- Colour *(required)*
- Date of birth
- Country of origin
- Chip ID
- KUSA registration number
- Image URL — a direct link to a photo of the dog

**Section 3 — Breeder & initial owner**
- Breeder — search by name (looks up registry breeders) or type free text
- Owner name and contact at time of registration

**Section 4 — Parentage**
- Sire — search the dog registry or enter free text if not in the registry
  (sire field shows male dogs; dogs with no sex recorded also appear)
- Dam — same as sire but filtered to female dogs

**Section 5 — Health records**
- Hips: score and scheme (repeatable)
- Eyes: score and scheme (repeatable)

**Section 6 — Clubs & organisations**
- Organisation name and membership number (repeatable)
- Record NFTA membership here

**Section 7 — Qualifications**
- Searchable lookup — type to search the qualifications list
- Selected qualifications appear as pills (showing the abbreviation)

### After submission

Your dog is created with **status = pending**. It will not appear in public
search results until an admin approves it.

On the dog's profile page you will see a pending banner:
> *This record is pending admin approval.*

Once approved the banner disappears and the dog appears in search results.
If rejected, a rejection reason will be shown on the profile.

---

## Editing a dog

The **Edit** button appears on the profile page of any dog that belongs to your kennel.

- Click **Edit** to open the edit form (same layout as the add form)
- Make your changes and click **Save**
- The edit goes back into **pending** status and must be re-approved

---

## Editing your kennel

Open your kennel's profile page. If this is your linked kennel, an **Edit** button
will appear.

The kennel form covers:

**Section 1 — Identity**
- Kennel name
- KUSA registration number
- Status (active / inactive)
- Founded date
- **Logo** — upload your kennel's logo (JPEG, PNG, WebP, or SVG, max 2MB)

**Section 2 — Breeder visibility**
- **List breeders publicly** toggle
  - When **on**: this kennel's breeders appear in the breeder dropdown when
    someone registers a dog with this kennel as the birth kennel
  - When **off**: breeders are internal only; submitters see "Other / not listed"
    and you will be notified to review and link the correct breeder

**Section 3 — Location**
- Country — searchable dropdown (ISO countries)
- Province — SA provinces dropdown when South Africa is selected; free text otherwise

**Section 4 — Contact**
- Email, phone, website

**Section 5 — Notes**

Changes go to **pending** status and must be approved by an admin.

---

## Managing breeders

A kennel can have multiple breeders. Breeders are the individuals who bred
specific dogs — they may or may not be kennel owners.

### Adding a breeder

1. Navigate to your kennel's profile.
2. Click **Manage breeders**.
3. Click **+ Add breeder**.
4. Enter the breeder's name and contact details.
5. Optionally link to a registered user account.

### Breeder visibility

Whether your breeders appear publicly depends on your kennel's **List breeders publicly** setting:

- **On**: Breeders appear on your kennel's public profile and in the breeder
  dropdown when registering dogs bred at this kennel
- **Off**: Breeders are internal only — visible to you and admins but not on
  the public profile or in dropdowns

### What happens when someone submits without a linked breeder

If someone submits a dog with your kennel as the birth kennel and selects
"Other / not listed" for the breeder, you will be notified to:

1. Review the submission
2. Link the correct breeder from your kennel's breeder list

This ensures breeder records stay accurate even when the submitter doesn't know
which breeder to select.

---

## Notifications you may receive

As a kennel owner, you are notified when:

- A dog is submitted with your kennel as the birth kennel and **breeder = "Other / not listed"**
  — review and link the correct breeder
- A dog is submitted with a **free-text parent** that might match a dog in your kennel
  — review and link the parent to the correct registry record
- A new kennel member is added or removed (by an admin)

Notifications help you keep kennel records accurate without having to monitor
every submission manually.

---

## What happens to pending records

| Event | What you see | What visitors see |
|---|---|---|
| Submitted | Pending banner on profile | Dog not in search results |
| Approved | No banner | Dog in search results |
| Rejected | Rejection reason banner | Dog not in search results |

An admin reviews all pending submissions in the approval queue. There is no
automatic notification when a submission is approved or rejected — check the
dog's profile page to see its current status.

---

## Kennel membership

A kennel can have multiple members. Each member can add and edit dogs for
the kennel, subject to admin approval.

### How membership works

- An admin assigns users to kennels via the **Manage members** page.
- Each membership has a role (e.g., `kennel_owner` or `member`).
- Members with the appropriate permissions can:
  - Add dogs to the kennel
  - Edit dogs belonging to the kennel
  - Edit the kennel's details

### What members can do

| Action | kennel_owner | member |
|---|:---:|:---:|
| Add dogs to kennel (`dog:create`) | ✅ | ✅ |
| Edit kennel dogs (`dog:edit:own`) | ✅ | ✅ |
| Edit kennel details (`kennel:edit:own`) | ✅ | ✅ |
| Approve own-kennel dogs (`dog:approve`) | ✅ | — |
| Add/remove kennel members | ✅ | — |

All non-admin submissions go to the approval queue.

### Owner vs member

- **kennel_owner** — full kennel management including `dog:approve` for own kennel,
  `qualification:create`, `queue:view`, and the ability to add/remove kennel members.
- **member** — can add and edit dogs and edit the kennel record, but cannot approve
  submissions or manage other members.

The specific permissions for each role can be customised by an admin.

### Multiple kennels

A user can be a member of multiple kennels. When adding a dog, you select
which kennel the dog belongs to from a dropdown of your kennel memberships.

### Becoming a member

Kennel membership is managed by admins. If you should be a member of a kennel
but don't see it in your list, contact the registry admin.

### Viewing your memberships

Your kennel memberships are shown on your user profile (accessible to admins).
The **Edit** button will appear on kennel profiles for any kennel you are
a member of with the appropriate permissions.
