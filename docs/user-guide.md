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

| Field | Required? | Notes |
|---|---|---|
| Registered name | Yes | Name without kennel prefix/suffix |
| Breed | Yes | Vizsla, GSP, GWP, Weimaraner, or HWV |
| Colour | Yes | |
| Sex | No | Male or Female |
| Kennel suffix | No | The kennel prefix in the registered name, if any |
| Date of birth | No | Must not be in the future |
| Country of origin | No | |
| Chip ID | No | Microchip number |
| KUSA number | No | |
| Image URL | No | Direct link to a photo |
| Sire / Dam | No | Search the registry, or type a name if not listed |
| Breeder | No | Search the registry, or type a name |
| Owner name | No | Name of the owner at time of registration |
| Health records | No | Hips and eyes — score and scheme (repeatable) |
| Clubs & organisations | No | Organisation name and membership number (repeatable) |
| Qualifications | No | Searchable lookup — earned qualifications |

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

The search page lets you:

- **Search by name** — type part of a dog's registered name in the search box
- **Filter by breed** — select from the breed dropdown
- **Filter by sex** — select Male or Female

Results update as you change filters. Results are paginated (20 per page).
Only approved dogs appear in search results.

---

## Dog profiles

Click any dog in the search results to open its profile.

A dog profile shows:

| Section | Details |
|---|---|
| Identity | Registered name, kennel suffix, sex |
| Details | Breed, colour, date of birth, age, country of origin, chip ID, KUSA number |
| Image | Photo (if one has been added) |
| Parentage | Sire and dam — clickable links if they are in the registry |
| Breeder | Breeder name — clickable link if in the registry |
| Kennel | Current kennel — clickable link |
| Owner history | Recorded ownership history with dates |
| Health records | Hip and eye scores |
| Qualifications | Earned qualifications shown as pills (abbreviation) |
| Clubs & organisations | Membership records including NFTA |
| Kennel history | Previous kennels the dog has been registered with |

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
