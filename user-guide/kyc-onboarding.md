# OTC Desk KYC (customer)

The **`/kyc`** route is the signed-in customer workflow for OTC Desk identity verification. It explains what is required, collects personal data and documents, and shows submission status after review.

---

## Where it lives

| Route | Who uses it |
|-------|-------------|
| `/kyc` | Signed-in academy members completing OTC Desk KYC |

The page is wrapped in the standard academy layout (title, description, and SEO metadata). A WhatsApp floating button is available for help during verification.

---

## Access

- You must be **signed in** to open `/kyc`.
- If you are not authenticated, the app redirects you to login before the KYC flow loads.

---

## First visit: onboarding

Before the main form, the app may show a short **onboarding** experience:

1. **Intro** — what KYC is, why it is required, privacy expectations, and that verification is typically one-time.
2. **Documents** — which files to prepare (government ID and proof of address).

You can continue through both screens or **skip** the intro. Completion is remembered for the current browser session (`sessionStorage` key `ath_kyc_onboarding_done`), so a refresh in the same tab does not repeat onboarding until the session ends.

---

## Verification flow

After onboarding, **`KycPageContent`** runs the multi-step flow:

| Step | Purpose |
|------|---------|
| Personal data | Name, date of birth, address, and related fields stored on the submission `metadata` |
| ID documents | Upload front and back of government ID (`id_front`, `id_back`) |
| Proof of address | Upload proof-of-address document (`proof_of_address`) |
| Submitted | Confirmation and read-only status after the customer submits |

The UI creates or resumes an **open submission** (draft) and advances steps in order. When everything is complete, the customer submits for staff review.

---

## Submission status (customer view)

Each submission has a `status`. From the customer side you typically see:

| Status | Meaning |
|--------|---------|
| `draft` | Started but not submitted |
| `submitted` | With the operations team for review |
| `needs_changes` | Staff requested corrections or additional documents |
| `approved` | KYC accepted |
| `rejected` | KYC rejected |

Uploaded files are stored privately (Supabase Storage bucket `kyc-docs`); only authorized staff can download them for review.

---

## Getting help

Use the on-page **WhatsApp** prompt if you need assistance while completing verification.

---

## Related docs

- [OTC Desk KYC (staff review)](../admin/otc-kyc.md)
- [Admin dashboard overview](../admin/dashboard-overview.md)
- [Contact](../support/contact.md)
