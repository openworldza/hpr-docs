---
title: Kennel owner guide
nav_order: 5
---

# Kennel owner guide

This guide covers what a kennel owner (`kennel_owner` role) can do in the registry.
Kennel owners can do everything a standard user can do — see [User guide](user-guide.md)
for browsing, searching, and ownership requests.

Your account must be linked to a kennel record before kennel-owner features are
available. Contact the registry admin if you have been given the `kennel_owner` role
but your kennel is not yet linked.

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
- Breed (Vizsla, GSP, GWP, Weimaraner, or HWV)
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

**Section 2 — Location**
- Country — searchable dropdown (ISO countries)
- Province — SA provinces dropdown when South Africa is selected; free text otherwise

**Section 3 — Contact**
- Email, phone, website

**Section 4 — Notes**

Changes go to **pending** status and must be approved by an admin.

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
