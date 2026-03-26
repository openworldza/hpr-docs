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

## RBAC — permission-based access control

Access is controlled by **permissions**, not role names directly. Users are assigned
one or more roles, and each role carries a set of permissions. Admins can create
custom roles and tune permissions at any time via `/admin/roles`.

The four **system roles** (`admin`, `kennel_owner`, `member`, `user`) are created at
setup and cannot be deleted. Their permissions can still be edited by an admin.

### Kennel membership

Users can be added as members of individual kennels. Each kennel membership carries
its own role (and that role's permissions), scoped to that kennel only.

For example, a user might have the global `user` role but also be a `member` of
Kennel A — giving them `dog:edit:own` and `kennel:edit:own` for Kennel A only.

---

## Full permission list

### Dogs

| Permission | Description |
|---|---|
| `dog:create` | Submit a dog for registration |
| `dog:edit` | Edit any dog record |
| `dog:edit:own` | Edit dogs in own kennel |
| `dog:delete` | Delete a dog record |
| `dog:approve` | Approve a pending dog submission |
| `dog:reject` | Reject a pending dog submission |
| `dog:transfer` | Transfer dog ownership |

### Kennels

| Permission | Description |
|---|---|
| `kennel:create` | Register a new kennel |
| `kennel:edit` | Edit any kennel record |
| `kennel:edit:own` | Edit own kennel record |
| `kennel:delete` | Delete a kennel record |
| `kennel:approve` | Approve a pending kennel |
| `kennel:reject` | Reject a pending kennel |
| `kennel:member:add` | Add a member to a kennel |
| `kennel:member:remove` | Remove a member from a kennel |

### Qualifications

| Permission | Description |
|---|---|
| `qualification:create` | Create a qualification definition |
| `qualification:edit` | Edit a qualification definition |
| `qualification:delete` | Delete a qualification definition |
| `qualification:result:submit` | Submit a qualification result for a dog |
| `qualification:result:approve` | Approve a pending qualification result |
| `qualification:result:reject` | Reject a pending qualification result |

### Organisations

| Permission | Description |
|---|---|
| `organisation:create` | Create an organisation |
| `organisation:edit` | Edit an organisation |
| `organisation:delete` | Delete an organisation |

### Users

| Permission | Description |
|---|---|
| `user:view` | View user list |
| `user:edit` | Edit a user account |
| `user:delete` | Delete a user account |
| `user:approve` | Approve a pending user account |
| `user:reject` | Reject a pending user account |
| `user:role:assign` | Assign roles to users |

### Admin

| Permission | Description |
|---|---|
| `queue:view` | View the approval queue (all tabs: Users, Dogs, Kennels, Qualifications, Ownership) |
| `ownership:approve` | Approve an ownership transfer request |
| `ownership:reject` | Reject an ownership transfer request |

---

## Default role → permission matrix

| Permission | user | member | kennel_owner | admin |
|---|:---:|:---:|:---:|:---:|
| `dog:create` | ✅ | ✅ | ✅ | ✅ |
| `dog:edit` | — | — | — | ✅ |
| `dog:edit:own` | — | ✅ | ✅ | ✅ |
| `dog:delete` | — | — | — | ✅ |
| `dog:approve` | — | — | ✅ | ✅ |
| `dog:reject` | — | — | — | ✅ |
| `dog:transfer` | — | — | — | ✅ |
| `kennel:create` | — | — | — | ✅ |
| `kennel:edit` | — | — | — | ✅ |
| `kennel:edit:own` | — | ✅ | ✅ | ✅ |
| `kennel:delete` | — | — | — | ✅ |
| `kennel:approve` | — | — | — | ✅ |
| `kennel:reject` | — | — | — | ✅ |
| `kennel:member:add` | — | — | ✅ | ✅ |
| `kennel:member:remove` | — | — | ✅ | ✅ |
| `qualification:create` | — | — | ✅ | ✅ |
| `qualification:edit` | — | — | — | ✅ |
| `qualification:delete` | — | — | — | ✅ |
| `user:view` | — | — | — | ✅ |
| `user:edit` | — | — | — | ✅ |
| `user:delete` | — | — | — | ✅ |
| `user:approve` | — | — | — | ✅ |
| `user:reject` | — | — | — | ✅ |
| `user:role:assign` | — | — | — | ✅ |
| `queue:view` | — | — | ✅ | ✅ |
| `ownership:approve` | — | — | — | ✅ |
| `ownership:reject` | — | — | — | ✅ |

---

## How permissions are resolved

1. **Global permissions** come from the user's assigned roles (via `user_roles`).
2. **Kennel-scoped permissions** come from kennel memberships (via `kennel_members`).
3. A user can perform an action if they have the relevant permission from either source.
4. Permissions are cached for 5 minutes — changes take up to 5 minutes to take effect.

Example: A user with the `user` role (global) and `member` membership in "Sunset Kennels"
can submit dogs (`dog:create` from their global role) and edit dogs belonging to
Sunset Kennels (`dog:edit:own` from their kennel-scoped membership).

### Custom roles

Admins can create custom roles with any combination of permissions via `/admin/roles`.
This allows fine-grained access control — for example, a "moderator" role that
can approve dogs but cannot manage users.

See [Admin guide — Managing roles](admin-guide.md#managing-roles-adminroles)
for instructions.
