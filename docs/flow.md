---
title: How data flows
nav_order: 3
---

# How data flows through the registry

This page shows how records move through the system from submission to
approval. Each diagram is followed by a plain-English explanation.

---

## 1. Member onboarding

```mermaid
flowchart TD
    A[Visitor lands on site] --> B[Creates account via Sign Up]
    B --> C[Account status: pending]
    C --> D[Sees /pending page]
    D --> E{Admin reviews}
    E -->|Approve| F[Account status: active]
    E -->|Reject| G[Account status: rejected]
    F --> H[Can browse dogs, kennels, breeders]
    F --> I[Can submit dogs and qualifications]
    G --> J[Sees /rejected page on sign-in]
```

Every new account starts as pending. The member sees a waiting page until an
administrator approves their account. Rejected members see a rejection page
when they sign in. Only active members can access the registry.

---

## 2. Dog submission

```mermaid
flowchart TD
    A[Member fills dog form] --> B[Submits dog]
    B --> C[Dog created with status: pending]
    C --> D[Appears in admin approval queue]
    D --> E{Admin reviews}
    E -->|Approve| F[Status: approved]
    E -->|Reject| G[Status: rejected]
    F --> H[Display name computed from qualifications]
    F --> I[Dog visible in search results]
    G --> J[Rejection reason required]
    J --> K[Reason recorded in audit log]
    K --> L[Member sees reason on dog profile]
    K --> M[Member sees reason in account history]
```

Dogs are not visible in search results until approved. On approval, the display
name is computed from any approved qualifications that add a name prefix. On
rejection, the admin must provide a reason, which the submitter can see on the
dog's profile page and in their account history.

---

## 3. Qualification result

```mermaid
flowchart TD
    A[Member opens dog profile] --> B[Clicks Add qualification result]
    B --> C[Selects qualification, fills result]
    C --> D[Uploads certificate]
    D --> E[Submits result]
    E --> F[Result status: pending]
    F --> G[Appears in admin queue — Qualifications tab]
    G --> H[Admin clicks certificate icon]
    H --> I[Certificate viewer modal opens]
    I --> J{Admin reviews certificate}
    J -->|Approve| K[Result status: approved]
    J -->|Reject| L[Rejection reason required]
    K --> M{adds_name_prefix?}
    M -->|Yes| N[Display name updated with prefix]
    M -->|No| O[Result shown on profile only]
    L --> P[Reason recorded in audit log]
    P --> Q[Member sees reason in account history]
```

Certificate upload is optional at submission but required before approval
(admins can override at their discretion). The certificate viewer modal lets
admins view the certificate and approve or reject directly from the modal.
When a qualification with `adds_name_prefix = true` is approved, the dog's
display name updates immediately.

---

## 4. Bulk upload

```mermaid
flowchart TD
    A[Prepare CSV or ZIP] --> B{File type?}
    B -->|CSV| C[Upload CSV via Bulk Upload page]
    B -->|ZIP| D[CSV + certificates in ZIP]
    D --> E[Compress images if needed]
    E --> C
    C --> F[Validation runs on all rows]
    F --> G{Errors?}
    G -->|Hard errors| H[422 — fix and re-upload]
    G -->|Warnings only| I[Job created]
    G -->|Clean| I
    I --> J[Worker processes rows in order]
    J --> K[Kennels]
    K --> L[Breeders]
    L --> M[Dogs]
    M --> N[Qualifications]
    N --> O[Health records]
    O --> P[All records created with status: pending]
    P --> Q[Records appear in approval queue]
    Q --> R[Admin bulk-approves or reviews individually]
```

A single upload can contain mixed record types. The worker processes them in
dependency order so that a kennel is created before the dogs that belong to it.
All records go to the pending queue — bulk upload never bypasses approval. ZIP
files can include certificate images matched to qualification rows by filename.

---

## 5. Display name computation

```mermaid
flowchart LR
    A[Registered name] --> E[Display name]
    B[Approved qualifications] --> C{adds_name_prefix = true?}
    C -->|Yes| D[Ordered by date achieved]
    C -->|No| F[Not included in name]
    D --> E
```

**Example:**

```
Registered name: Kennel Argo
Approved qualifications:
  - HZP (achieved 2021-06-15) — adds_name_prefix = true
  - VGP (achieved 2022-03-20) — adds_name_prefix = true

Display name: HZP-VGP Kennel Argo
```

The display name is computed by the backend, never stored in the database.
Qualification abbreviations are joined with hyphens and ordered by date
achieved (earliest first). The display name appears everywhere: search
results, dog cards, profile headings, and pedigree links.

---

## 6. Data visibility rules

```mermaid
flowchart TD
    subgraph Public
        A[Landing page only]
    end

    subgraph Pending member
        B[/pending page only]
    end

    subgraph Active member
        C[Dog search and profiles]
        D[Kennel profiles]
        E[Breeder profiles]
        F[COI calculator — if permitted]
        G[Own account history]
        H[Submit dogs and qualifications]
    end

    subgraph Kennel owner
        I[Everything above]
        J[Kennel management]
        K[Kennel audit history]
        L[Bulk upload — if permitted]
    end

    subgraph Admin
        M[Everything above]
        N[Approval queue with all tabs]
        O[Full audit log — History tab]
        P[Bulk upload and bulk approve]
        Q[Role and user management]
        R[Certificate viewer]
    end
```

The registry is members-only. Unauthenticated visitors see only the landing
page. Pending members see a waiting page. Active members can browse and submit.
Kennel owners additionally manage their kennel's dogs and see kennel-specific
audit history. Admins have full access to the approval queue, audit log, bulk
operations, and role management. Certificates are visible only to admins in the
approval queue.
