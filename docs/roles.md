---
title: Role reference
nav_order: 3
---

# Role reference

The registry has four account states and three active roles. This page summarises
what each can and cannot do.

---

## Account states

### Unauthenticated visitor
Not signed in.

- Can view: the landing page (`/`) only
- Cannot view: any registry content
- Can do: click **Sign in** to create an account or log in

### Pending account
Signed in but awaiting admin approval.

- Can view: the `/pending` page only
- Cannot view: any registry content
- Can do: sign out

### Rejected account
Account was not approved.

- Can view: the `/rejected` page only
- Cannot view: any registry content
- Can do: sign out; contact the registry admin

---

## Active roles

### `user` — Standard member

**Browse**
- Search the dog registry at `/dogs`
- View individual dog profiles at `/dogs/[id]`
- View kennel profiles at `/kennels/[id]`
- Browse the kennel list at `/kennels`
- View breeder profiles at `/breeders/[id]`
- Browse the breeder list at `/breeders`

**Submit a dog**
- Click **+ Add dog** in the header to submit a dog to the registry
- The dog is created with `status = pending` and goes to the admin approval queue
- No kennel restriction — submit any dog you have records for

**Ownership requests**
- On any dog profile, submit a "Request ownership" form
- The request is reviewed by an admin
- Approved requests link the dog's owner history to your account

**Cannot**
- Edit dogs or kennels
- Add kennels or breeders
- Access the admin interface

---

### `kennel_owner` — Kennel owner

Everything a `user` can do, plus:

**Dogs**
- Add new dogs via the **+ Add dog** button in the header
  — submits to `/kennel-owner/dogs/new`
  — dog is created with `status = pending` and goes to the admin approval queue
- Edit dogs that belong to their kennel
  — edit button appears on dog profiles for dogs in their kennel
  — submits to `/kennel-owner/dogs/[id]/edit`

**Kennel**
- Edit their own kennel record
  — edit button appears on their kennel profile
  — submits to `/kennel-owner/kennels/[id]/edit`

**Cannot**
- Add or edit dogs belonging to other kennels
- Edit other kennels
- Access the admin interface
- Approve or reject submissions

> **Approval queue:** All kennel_owner submissions (dogs and kennel edits) go into
> a `pending` state and must be approved by an admin before they appear in public
> search results. The dog profile will show a pending banner while awaiting approval.

---

### `admin` — Registry administrator

Full access to all registry functions.

**Browse**
Everything a standard user can browse, plus:

**Admin dashboard** (`/admin`)
- Searchable dog table with edit and delete actions
- Stats: total dogs, kennels, breeders
- Pending items badge linking to the approval queue
- Quick links to add dog/kennel/breeder and manage qualifications

**Dogs**
- Add dogs: `/admin/dogs/new` — immediately `approved`, visible in search
- Edit any dog: `/admin/dogs/[id]/edit`
- Delete any dog (with confirmation)
- Assign owner to a dog: `/admin/dogs/[id]/owner` — search users by email

**Kennels**
- Add kennels: `/admin/kennels/new` — immediately `approved`
- Edit any kennel: `/admin/kennels/[id]/edit`
- Delete any kennel

**Breeders**
- Add breeders: `/admin/breeders/new`
- Edit any breeder: `/admin/breeders/[id]/edit`
- Delete any breeder

**Qualifications**
- Manage the qualifications list at `/admin/qualifications`
- Add, edit, and delete qualification records (name + abbreviation)

**Approval queue** (`/admin/queue`)
Four tabs — each showing pending items with Approve / Reject actions:

| Tab | What's shown |
|---|---|
| **Dogs** | Dogs submitted by users or kennel owners awaiting approval |
| **Kennels** | Kennel edits awaiting approval |
| **Ownership requests** | User requests to be listed as a dog's owner |
| **Users** | New account registrations awaiting approval |

- **Approve**: record becomes `approved` and appears in public search
- **Reject**: opens a reason modal; record kept with `rejected` status; reason stored

---

## Permission matrix

| Action | user | kennel_owner | admin |
|---|:---:|:---:|:---:|
| Browse dogs, kennels, breeders | ✅ | ✅ | ✅ |
| Request dog ownership | ✅ | ✅ | ✅ |
| Add a dog | ✅ (pending) | ✅ (pending) | ✅ (approved) |
| Edit own kennel's dogs | — | ✅ (pending) | — |
| Edit own kennel | — | ✅ (pending) | — |
| Edit any dog | — | — | ✅ |
| Edit any kennel | — | — | ✅ |
| Add/edit breeders | — | — | ✅ |
| Manage qualifications | — | — | ✅ |
| Approve/reject queue | — | — | ✅ |
| Approve/reject users | — | — | ✅ |
| Assign dog owner | — | — | ✅ |
| Delete records | — | — | ✅ |
| Access `/admin` | — | — | ✅ |
