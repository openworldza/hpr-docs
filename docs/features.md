---
title: Features
nav_order: 2
---

# Features

The HPR Registry is a verified pedigree database for Hunt, Point, Retrieve
breeds in South Africa. It tracks bloodlines, qualification results, health
records, and kennel histories in a single moderated system. Every account, dog,
and result is reviewed before it goes live.

---

## Core features

### Verified pedigrees

Full bloodline tracking with sire and dam linking. Multiple registration numbers
supported — KUSA, FCI, AKC, and any other registry. Every dog profile shows its
ancestry as clickable links — follow the line back through generations. When a
parent is not yet in the registry, free-text entry is accepted and the birth
kennel is notified to review and link the record.

### Qualification results

Field test and working ability results submitted by members, verified by
administrators. Each result goes through an approval workflow with certificate
upload and review. Approved qualifications appear on the dog's profile and
(when configured) prefix the dog's display name.

### Health records

Standardised health data per dog: hips, eyes, elbows, and DNA results.
Supported grading schemes include BVA, OFA, FCI, PennHIP (hips), ECVO, OFA,
CERF (eyes), plus elbow scores and flexible DNA results that can be configured
per breed.

### COI calculator

Projected coefficient of inbreeding for any prospective breeding pair. Uses
Wright's path coefficient method across all registered ancestors. Returns the
COI percentage, pedigree completeness, generations analysed, and a list of
common ancestors sorted by contribution.

### Kennel records

Breeder profiles linked to kennels, dogs produced, kennel membership, and full
kennel history. Kennel owners manage their own dogs and breeders. Each kennel
profile tracks founding date, location, contact details, and a history of dogs
registered through the kennel.

### Bulk import

CSV and ZIP upload for large datasets. A single file can contain kennels,
breeders, dogs, qualification results, and health records — the system processes
them in dependency order. ZIP uploads can include certificate files (PDF, JPEG,
PNG, WebP) matched to qualification rows by filename. Maximum 1,000 rows per
upload, 50 MB ZIP limit. See the [image optimisation guide](admin-guide.md#optimising-images-for-upload)
for tips on keeping file sizes within limits.

### Audit trail

Every approval and rejection is recorded with who acted, when, and why. Admins
see the full history in the approval queue. Members see their own submission
outcomes on their account history page. Kennel owners see the audit trail for
their kennel and its dogs.

### Members only

The registry is moderated. Every new account must be approved by an
administrator before the member can access dog records, submit data, or search
the registry. Unauthenticated visitors see the landing page only.

### Multi-tenant

The platform is white-label and configurable per breed club. Each tenant has
its own breed list, health tests, club affiliations, visual theme (colours,
fonts, logo), support contact, and feature flags. All tenant-specific values
are stored in the database — nothing is hardcoded.

---

## Supported qualifications

### KUSA — Kennel Union of Southern Africa

**Schedule 5C(4) — Field tests:**

| Qualification | Abbreviation | Result format |
|---|---|---|
| SA-Derby Test | SA-D | Grade: Prize 1, Prize 2, Prize 3 |
| SA-Novice Test | SA-N | Grade: Prize 1, Prize 2, Prize 3 |
| SA-Older Dog Elite Test | SA-AZP | Grade: Prize 1, Prize 2, Prize 3 |

**Schedule 5C(6) — Shooting and Retrieving ratings:**

| Qualification | Abbreviation | Result format |
|---|---|---|
| Novice Shooting Dog | NSD | Pass/Fail |
| Shooting Dog | SD | Pass/Fail |
| Shooting Dog Excellent | SDX | Pass/Fail |
| Novice Retrieving Dog | NRD | Pass/Fail |
| Retrieving Dog | RD | Pass/Fail |
| Retrieving Dog Excellent | RDX | Pass/Fail |

### JGHV — Jagdgebrauchshundverband

| Qualification | Abbreviation | Result format |
|---|---|---|
| Verbandsjugendprufung | VJP | Score + Grade (Prize I/II/III) |
| Herbstzuchtprufung | HZP | Score + Grade (Prize I/II/III) |
| Verbandsgebrauchsprufung | VGP | Score + Grade (Prize I/II/III/Pass/Fail) |
| Bringtreueprufung | BGVP | Score + Grade (Prize I/II/III) |
| Armbruster Zuchtprufung | AZP | Score + Grade (Prize I/II/III) |

All KUSA and JGHV qualifications above add a prefix to the dog's display name
when approved.

---

## Supported breeds

- Hungarian Vizsla
- Hungarian Wirehaired Vizsla
- German Shorthaired Pointer
- German Wirehaired Pointer
- Weimaraner

The breed list is configurable per tenant. Breed clubs adopting the platform
can set their own list.

---

## Health tests supported

| Test | Grading schemes |
|---|---|
| Hips | BVA, OFA, FCI, PennHIP |
| Eyes | ECVO, OFA, CERF |
| Elbows | Standard grading |
| DNA | Flexible per breed — results stored as key-value pairs |

Health tests are configured per tenant. Breed clubs can define which tests are
standard for their breeds.

---

## Technical details

- 50 MB maximum ZIP size for bulk uploads
- 10 MB maximum per individual certificate upload
- 5 MB maximum per dog photo upload
- Certificates are stored for admin verification only — never displayed publicly
- All data protected by row-level security in the database
- Authentication via industry-standard JWT with provider abstraction
