---
title: Admin guide
nav_order: 6
---

# Admin guide

Admins have full access to the registry. This guide covers the admin-specific
features. Admins can also do everything in the [User guide](user-guide.md) and
[Kennel owner guide](kennel-owner-guide.md).

---

## Admin dashboard (`/admin`)

The dashboard is your starting point. It shows:

- **Pending badge** — a count of all items awaiting approval, linking to the queue
- **Stats** — total dogs, kennels, and breeders in the registry
- **Quick links** — Add dog, Add kennel, Add breeder, Manage qualifications, Approval queue
- **Dog table** — searchable list of all dogs with edit, delete, and pagination

Access the dashboard via the **Admin** link in the top navigation bar.

---

## Adding records

Admin-created records are **immediately approved** — they go live in the registry
without going through the approval queue.

### Add a dog (`/admin/dogs/new`)

Click **+ Add dog** in the header or the quick link on the dashboard.

The dog form is the same as for kennel owners, with one difference: the kennel
suffix field is not restricted — you can assign any kennel as the birth kennel.

After saving, you are redirected to the new dog's profile.

### Add a kennel (`/admin/kennels/new`)

Click **+ Add kennel** on the dashboard.

Fill in name, KUSA number, status, location, and contact details.

### Add a breeder (`/admin/breeders/new`)

Click **+ Add breeder** on the dashboard.

Fill in name, email, phone, and optionally link to a kennel record.

---

## Editing records

Edit buttons appear throughout the registry for admins:

- **Dog profile** — **Edit** button → `/admin/dogs/[id]/edit`
- **Dog profile** — **Assign owner** button → `/admin/dogs/[id]/owner`
- **Kennel profile** — **Edit** button → `/admin/kennels/[id]/edit`
- **Breeder profile** — **Edit** button → `/admin/breeders/[id]/edit`

Admin edits do not go through the approval queue — changes are applied immediately.

---

## Deleting records

A **Delete** button with confirmation appears on:
- Dog rows in the admin dashboard dog table
- Dog, kennel, and breeder profile pages (when accessed as admin)

Deletion is permanent. The confirmation modal requires you to confirm before
the record is removed.

---

## Assigning a dog owner (`/admin/dogs/[id]/owner`)

Use this page to manually link a dog's ownership record to a registered user account.

1. Open the dog's profile.
2. Click **Assign owner**.
3. Search for the user by email address — results appear as you type.
4. Select the user and confirm.

This creates an owner history entry on the dog linking to that user's account.

---

## Managing qualifications (`/admin/qualifications`)

Qualifications are the linked entities that appear as pills on dog profiles
(e.g. JD, CC, CAC).

On the qualifications page you can:
- **Add** a new qualification — name and abbreviation
- **Edit** an existing qualification — inline
- **Delete** a qualification

Qualifications are searchable by members when filling in the dog form.

---

## Approval queue (`/admin/queue`)

All submissions from users and kennel owners, plus new user registrations, appear here.

Access via the pending badge on the dashboard or via the **Approval queue** quick link.

### Dogs tab

Shows dogs submitted by users or kennel owners with `status = pending`.

Each row shows: dog name, breed, submission date.

- **Approve** — dog status becomes `approved`; appears in public search
- **Reject** — opens the rejection reason modal; dog status becomes `rejected`;
  reason is stored and shown on the dog's profile

### Kennels tab

Shows kennel records with `status = pending` (edits submitted by kennel owners).

Each row shows: kennel name, country, submission date.

- **Approve** / **Reject** — same behaviour as dogs

### Ownership requests tab

Shows requests from users to be listed as a dog's owner.

Each row shows: dog name, requesting user's email, optional message, submission date.

- **Approve** — ownership request is accepted; user is linked to the dog
- **Reject** — request is declined with a reason

### Users tab

Shows new account registrations awaiting activation.

Each row shows: email address, sign-up date.

- **Approve** — account status becomes `active`; user can now access the registry
- **Reject** — opens the rejection reason modal; account status becomes `rejected`;
  user sees the `/rejected` page when they sign in

---

## Rejection reason modal

When you click **Reject** on any item, a modal appears:

1. Enter a reason for rejection (required).
2. Click **Reject** to confirm.

The reason is stored on the record and displayed to the relevant user (on the
dog/kennel profile, or on their account page).

---

## Pending badge

The orange badge at the top of the admin dashboard shows the total count of:
- Pending dogs
- Pending kennels
- Pending ownership requests
- Pending user accounts

The badge is a link to `/admin/queue`. It only appears when there is at least
one pending item.
