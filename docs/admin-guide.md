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

---

## Managing roles (`/admin/roles`)

The registry uses a flexible role-based access control (RBAC) system. Admins
can create custom roles and assign permissions to them.

### Viewing roles

The roles page shows all roles in a table:
- **Name** — the role identifier
- **Description** — what the role is for
- **Permissions** — click to view/edit the permissions assigned to the role
- **Type** — `System` (built-in) or `Custom`

### System roles

Four system roles are created by default:
- `user` — can submit dogs (`dog:create`)
- `member` — can submit and edit kennel dogs (`dog:create`, `dog:edit:own`, `kennel:edit:own`)
- `kennel_owner` — member permissions plus `dog:approve`, `qualification:create`, `queue:view`, `kennel:member:add`, `kennel:member:remove`
- `admin` — all permissions

System role names cannot be changed, but their permissions can be edited.
System roles cannot be deleted.

### Creating a custom role

1. Click **+ Create role**.
2. Enter a name and description.
3. Click **Create role**.
4. Click the permissions count to open the permission editor.
5. Check the permissions you want to assign.

### Editing a role

Click **Edit** on any role to update its name (custom roles only) or description.

### Editing role permissions

Click the permission count (e.g., "5 permissions") to open the permission editor.

Permissions are grouped by category:
- **dogs** — `dog:create`, `dog:edit`, `dog:edit:own`, `dog:delete`, `dog:approve`, `dog:reject`, `dog:transfer`
- **kennels** — `kennel:create`, `kennel:edit`, `kennel:edit:own`, `kennel:delete`, `kennel:approve`, `kennel:reject`, `kennel:member:add`, `kennel:member:remove`
- **qualifications** — `qualification:create`, `qualification:edit`, `qualification:delete`
- **users** — `user:view`, `user:edit`, `user:delete`, `user:approve`, `user:reject`, `user:role:assign`
- **admin** — `queue:view`, `ownership:approve`, `ownership:reject`

Check or uncheck permissions. Changes are saved immediately.

### Deleting a role

Click **Delete** on any custom role. System roles cannot be deleted.

---

## Managing users (`/admin/users`)

The users page lists all registered accounts.

### Filtering users

Use the status dropdown to filter by:
- **All statuses** — show everyone
- **Active** — approved accounts
- **Pending** — awaiting approval
- **Rejected** — accounts that were not approved

### User detail page (`/admin/users/[id]`)

Click a user's email to open their detail page showing:
- Email and status
- Join date
- Assigned roles
- Kennel memberships
- Effective permissions (union of all role permissions)

### Assigning roles to a user

On the user detail page:
1. Select a role from the dropdown.
2. Click **Add role**.

The user now has all permissions from that role.

### Removing a role from a user

Click the **×** button next to any role pill to remove it.

---

## Registry configuration

The registry is configured per-tenant via the database. Configuration includes
the allowed breed list, visual theme, logo, support email, and feature flags.

The frontend reads configuration from `GET /api/config` on startup. All
tenant-specific values come from this endpoint — nothing is hardcoded.

### What is configurable

| Setting | Description | Example |
|---|---|---|
| Breeds | Allowed breed list for dog submissions | `["Vizsla","GSP","GWP","Weimaraner","HWV"]` |
| Theme — primary colour | Main brand colour (CSS variable) | `#2D5016` |
| Theme — accent colour | Secondary brand colour | `#8B6914` |
| Theme — heading font | Font for headings | `Playfair Display` |
| Theme — body font | Font for body text | `Inter` |
| Logo URL | Path or URL to the registry logo | `/logos/hpr.svg` |
| Support email | Contact email shown in the footer | `admin@hprregistry.co.za` |
| Features | Feature flags (on/off toggles) | `{}` |

### Changing configuration

Configuration is stored in the `tenants.config` JSON column in the database.
Changes require a database update (via `seed.sql` or direct SQL) — there is
no admin UI for configuration yet.

To update configuration, edit the tenant's config JSON in `seed.sql` and run
`make db-seed`.

### Breed validation

When a user or kennel owner submits a dog, the breed must be in the registry's
configured breed list. If the registry has no configured breeds (empty list),
any breed is accepted.

---

## Managing kennel members (`/admin/kennels/[id]/members`)

Kennel membership allows multiple users to manage a single kennel's dogs.

### Accessing kennel members

From any kennel profile page, click the **Members** button (visible to admins only).

Or navigate directly to `/admin/kennels/[id]/members`.

### Viewing members

The members table shows:
- User email
- Role within the kennel (e.g., `kennel_owner`, `member`)
- Date joined
- Actions (change role, remove)

### Adding a member

1. Click **+ Add member**.
2. Search for a user by email.
3. Select the user from the search results.
4. Choose a role (e.g., `kennel_owner` or `member`).
5. Click **Add member**.

The user can now manage dogs belonging to this kennel.

### Changing a member's role

Use the role dropdown in the members table to change a user's role within the kennel.

### Removing a member

Click **Remove** to revoke a user's membership in the kennel.
