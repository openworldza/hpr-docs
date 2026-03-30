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

Qualifications represent tests, titles, and certifications that dogs can earn.
They are organised by **organisation** (e.g. JGHV, KUSA) and appear on dog profiles.

### Organisation management

Organisations issue qualifications. Each organisation has:
- Name and abbreviation
- Country
- Website
- Description
- Logo (optional)

### Qualification configuration

Each qualification has:
- **Name** — full name (e.g. "Verbandsjugendprüfung")
- **Abbreviation** — short code shown on dog profiles (e.g. "VJP")
- **Organisation** — which organisation issues it
- **Result type** — configure which fields appear on the result form:
  - **Has score** — numeric score input
  - **Has grade** — grade dropdown or free text
  - **Is pass/fail** — toggle for pass/fail results
  - **Grade options** — predefined grades (if set, shows dropdown; otherwise free text)
- **Adds to name** toggle:
  - When **on**: the abbreviation is prepended to the dog's display name when approved
  - When **off**: the qualification appears on the profile but doesn't affect the name
  - Field tests like VGP, HZP typically add to name; health tests typically do not

### Dog display name

A dog's **display name** is computed from their registered name plus approved
qualification prefixes. For example:

- Registered name: "Kennel von Haus Example"
- Approved qualifications with adds_name_prefix: VGP (achieved 2024-01), HZP (achieved 2023-06)
- Display name: "HZP-VGP Kennel von Haus Example" (ordered by date achieved)

The display name appears everywhere: search results, cards, profile heading, pedigree links.
The registered name is never modified in the database.

### Seeded qualifications

The following qualifications are pre-configured in the registry.

#### JGHV — Jagdgebrauchshundverband

All JGHV qualifications have a numeric score and a grade. All add a name prefix
when approved (e.g. "VGP-HZP Kennel von Haus Example").

| Name | Abbreviation | Type | Grades |
|------|-------------|------|--------|
| Verbandsjugendprüfung | VJP | Field test | Prize I, Prize II, Prize III |
| Herbstzuchtprüfung | HZP | Field test | Prize I, Prize II, Prize III |
| Verbandsgebrauchsprüfung | VGP | Field test | Prize I, Prize II, Prize III, Pass, Fail |
| Bringtreueprüfung | BGVP | Field test | Prize I, Prize II, Prize III |
| Armbruster Zuchtprüfung | AZP | Working ability | Prize I, Prize II, Prize III |

#### KUSA — Kennel Union of Southern Africa

Based on KUSA Schedule 5C(4) and Schedule 5C(6). All add a name prefix when approved.

| Name | Abbreviation | Type | Result format |
|------|-------------|------|---------------|
| SA-Derby Test | SA-D | Field test | Grade: Prize 1, Prize 2, Prize 3 |
| SA-Novice Test | SA-N | Field test | Grade: Prize 1, Prize 2, Prize 3 |
| SA-Older Dog Elite Test | SA-AZP | Working ability | Grade: Prize 1, Prize 2, Prize 3 |
| Novice Shooting Dog | NSD | Working ability | Pass/Fail |
| Shooting Dog | SD | Working ability | Pass/Fail |
| Shooting Dog Excellent | SDX | Working ability | Pass/Fail |
| Novice Retrieving Dog | NRD | Working ability | Pass/Fail |
| Retrieving Dog | RD | Working ability | Pass/Fail |
| Retrieving Dog Excellent | RDX | Working ability | Pass/Fail |

#### VDD — Verein Deutsch-Drahthaar

| Name | Abbreviation | Type | Result format |
|------|-------------|------|---------------|
| VDD Natural Ability | VDD-NA | Field test | Pass/Fail |

VDD-NA does **not** add a name prefix.

### Certificate handling

Certificates are uploaded by users when submitting qualification results.
They are used for **admin verification only** and are **never shown publicly**.

- View certificates inline in the approval queue (thumbnail or PDF link)
- Certificates are required before approval (but you can approve without at your discretion)
- After approval, the certificate is retained for records but not visible on dog profiles

---

## Approval queue (`/admin/queue`)

All submissions from users and kennel owners, plus new user registrations, appear here.

Access via the pending badge on the dashboard or via the **Approval queue** quick link.

The queue has six tabs: **Dogs**, **Qualifications**, **Health**, **Kennels**, **Breeders**, **Users**, plus a **History** tab for the audit log.

### Dogs tab

Shows dogs submitted by users or kennel owners with `status = pending`.

Each row shows: dog display name, breed, submitter, submission date.
- Unlinked parent indicator if a parent was entered as free text
- Quick link to full profile

- **Approve** — dog status becomes `approved`; display name is computed and the
  dog appears in public search
- **Reject** — opens the rejection reason modal; dog status becomes `rejected`;
  reason is stored and shown on the dog's profile

### Qualifications tab

Shows qualification results submitted by users awaiting verification.

Each row shows:
- Dog display name (clickable link to profile)
- Qualification (organisation + name)
- Grade/score
- Submitted by
- Submission date
- **Certificate column** — document icon if a certificate is uploaded, muted
  "No certificate" text if not

**Certificate viewer:**
Click the document icon in the certificate column to open the **certificate
viewer modal**. The modal displays the certificate inline (image preview or
PDF via iframe). From the modal you can **Approve** or **Reject** the result
directly — no need to close the modal and use the row buttons.

Certificates are visible **only** in the admin queue. They are never shown
publicly on dog profiles.

**Approving:**
- If certificate present: approve directly (from the row or from the certificate viewer modal)
- If no certificate: a warning appears, but you can still approve at your discretion

**Display name update:**
When you approve a qualification that has **adds_name_prefix = true**, the dog's
display name updates immediately to include the qualification abbreviation as a prefix.

### Health tab

Shows health record submissions awaiting approval.

Each row shows: dog display name, test type (Hips, Eyes, etc.), result, submitter, date.

- **Approve** / **Reject** — same behaviour as other tabs

### Kennels tab

Shows kennel records with `status = pending` (edits submitted by kennel owners).

Each row shows: kennel name, country, submission date.

- **Approve** / **Reject** — same behaviour as dogs

### Breeders tab

Shows breeder records with `status = pending`.

Each row shows: breeder name, linked kennel (if any), submission date.

- **Approve** / **Reject** — same behaviour as dogs

### Users tab

Shows new account registrations awaiting activation.

Each row shows: email address, sign-up date.

- **Approve** — account status becomes `active`; user can now access the registry
- **Reject** — opens the rejection reason modal; account status becomes `rejected`;
  user sees the `/rejected` page when they sign in

---

## Bulk approve

You can approve multiple pending records at once from any queue tab.

### Selecting records

- Each row has a **checkbox** on the left
- Check individual rows, or use the **"Select all N pending"** shortcut at the
  top of the tab to select every pending record of that type
- The bulk action bar appears at the bottom when at least one row is selected,
  showing the count of selected items

### Approving

1. Select the records you want to approve.
2. Click **Approve selected** in the bulk action bar.
3. A confirmation modal appears — type **APPROVE** (exact, case-sensitive) to confirm.
4. Click **Confirm**.

The system processes each record individually. If some records fail (e.g. a
qualification missing a certificate when override is not allowed), those failures
are reported per-record and the successful approvals are not rolled back.

**Missing certificate warning:** When bulk-approving qualifications, the modal
shows a count of results that have no certificate attached. You can proceed at
your discretion.

---

## Certificate viewer

The certificate viewer modal is available from the Qualifications tab in the
approval queue. It lets you review a certificate without leaving the queue.

### How to use it

1. In the Qualifications tab, find a row with a certificate (document icon in
   the certificate column).
2. Click the document icon.
3. The modal opens with the certificate displayed inline:
   - **Images** (JPEG, PNG, WebP) — shown as a preview image
   - **PDFs** — displayed in an embedded iframe
4. From the modal footer, click **Approve** or **Reject**.

Approving or rejecting from the modal has the same effect as using the row
buttons — the result updates, the audit log is written, and the modal closes.

---

## Rejection reasons

A reason is **required** for every rejection. The reason must be at least 10
characters long.

When you click **Reject** on any item (from a queue row or from the certificate
viewer modal), a modal appears:

1. Enter a clear reason for rejection (minimum 10 characters).
2. Click **Reject** to confirm.

The reason is:
- Stored in the **approval audit log** (see below)
- Visible to the member who submitted the record (on their account history page
  and on the dog/kennel profile)
- Expandable in the audit log History tab

---

## Approval audit log

Every approve and reject action is recorded in the audit log. The log captures
who acted, what they acted on, when, and (for rejections) why.

### History tab

The **History** tab in the approval queue shows the full audit trail. It is the
sixth tab, after Users.

**Columns:** date, entity type, entity name, action (approved/rejected),
acted by, submitted by, reason (expandable for rejections).

**Filters:**
- **Type** — filter by entity type (dog, kennel, qualification, health, breeder, user)
- **Action** — filter by action (approved, rejected)

Results are paginated. Dates are shown as relative time with the full timestamp
in a tooltip on hover.

### Where else audit data appears

- **Member account history** (`/account/history`) — members see their own
  submission results (approved/rejected with reasons)
- **Kennel audit section** — on each kennel profile, a collapsible History section
  shows audit entries for that kennel and its dogs (visible to kennel owners and admins)

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
- **breeding** — `coi:calculate`
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
| Breeds | Allowed breed list for dog submissions | `["Hungarian Vizsla","German Shorthaired Pointer","German Wirehaired Pointer","Weimaraner","Hungarian Wirehaired Vizsla"]` |
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

---

## Bulk upload (CSV and ZIP import)

Bulk upload allows admins and kennel owners to import multiple records at once
using a CSV file or a ZIP file containing a CSV and certificate files. All
imported records go through the same approval queue as individual submissions.

### Getting started

1. Navigate to the **Bulk Upload** page (Admin sidebar > Registry > Bulk upload).
2. Download a template for the record type you want to import (dogs, kennels,
   breeders, qualifications, or health records).
3. Fill in the template with your data. You can mix multiple types in one file
   by using the `type` column.
4. Upload the CSV file (or a ZIP — see below). The system validates every row
   before creating any records.
5. If there are errors, fix them and re-upload. Warnings (e.g., ambiguous name
   matches) do not block the upload.
6. Track progress on the job status section of the page.

### CSV format

Every CSV file must have a `type` column. Valid types: `dog`, `kennel`,
`breeder`, `qualification`, `health`. Each type has its own required columns:

- **Dogs**: registered_name, breed, sex (M/F), dob (YYYY-MM-DD)
- **Kennels**: name
- **Breeders**: first_name, last_name
- **Qualifications**: dog_name or chip_id, qualification_abbreviation,
  organisation_abbreviation, date_achieved
- **Health records**: dog_name or chip_id, test_name (Hips/Eyes), result

### ZIP upload (with certificates)

To include certificate files with qualification records, upload a ZIP file
instead of a plain CSV:

1. Prepare your CSV as normal.
2. Add a `certificate_filename` column to qualification rows — set it to the
   filename of the certificate (e.g., `argo_vgp_2024.pdf`).
3. Place the CSV and all certificate files in a ZIP archive. The CSV should
   be named `bulk.csv` (preferred) or any `.csv` file in the ZIP root.
4. Certificate files can be PDF, JPEG, PNG, or WebP.
5. Upload the ZIP file on the Bulk Upload page.

The system extracts the certificates, uploads them to storage, and links them
to the corresponding qualification rows. Filenames are matched
case-insensitively. If a `certificate_filename` refers to a file not found in
the ZIP, the row proceeds with a warning (no certificate attached).

### Limits

| Limit | CSV | ZIP |
|---|---|---|
| Maximum file size | 5 MB | 50 MB |
| Maximum rows | 1,000 | 1,000 |
| Maximum certificate files | n/a | 500 |

### Processing order

The bulk worker processes rows in a fixed order to respect dependencies:
kennels, then breeders, then dogs, then qualifications, then health records.
This means a single upload can create a kennel, its breeders, dogs belonging
to that kennel, and qualification results for those dogs — all in one file.

### Permissions

| Permission | Admin | Kennel owner |
|---|:---:|:---:|
| Dogs | yes | yes |
| Kennels | yes | |
| Breeders | yes | yes |
| Qualifications | yes | yes |
| Health records | yes | yes |

Rows for types the uploader lacks permission for will be flagged as errors
during validation. The Bulk Upload page and sidebar link are only visible if
you have at least one `bulk:upload:*` permission.

### Job status and history

Each upload creates a job. The Bulk Upload page shows your recent jobs with
their status:

- **Pending** — queued for processing
- **Processing** — rows being imported (progress count updates)
- **Complete** — all rows processed (some may have failed individually)
- **Failed** — unrecoverable error (e.g., invalid CSV)

Click a job to see per-row detail including any errors or warnings.
Qualification rows show whether a certificate was attached.

### Optimising images for upload

Large certificate files slow down uploads and can push ZIP files past the 50 MB
limit. Optimise your files before uploading.

**Target file sizes:**

| File type | Target | Notes |
|---|---|---|
| Certificate scan (PDF) | Under 500 KB | Export at 150 DPI not 300 |
| Certificate photo (JPEG) | 200-400 KB | 70-75% quality |
| Certificate photo (PNG) | Under 1 MB | Convert to JPEG if larger |

**Recommended free tools:**

- **Squoosh** (squoosh.app) — browser-based, no install, drag and drop, works
  on any OS. Recommended.
- **TinyPNG** (tinypng.com) — free up to 20 images at a time
- **macOS Preview** — File > Export > adjust JPEG quality to 60-70%
- **Windows Paint** — File > Save As > JPEG

**PDF certificates:**
Scan or export at 150 DPI. Most scanner apps (Adobe Scan, Microsoft Lens,
Apple Notes) have a resolution setting. 150 DPI is perfectly readable on
screen and keeps PDFs under 500 KB.

**What not to do:**

- Do not upload raw camera files (.heic, .raw, .tiff) — convert to JPEG first
- Do not scan at 600 DPI — unnecessary and produces huge files
- Do not include dog photos in bulk upload ZIPs — certificates only

**Quick rule of thumb:** If all certificates are under 500 KB, you can fit
100 certificates in a 50 MB ZIP with room to spare.
