# OTC Desk KYC

The **OTC Desk KYC** module is the staff workflow for reviewing customer identity submissions and documents for OTC eligibility.

---

## Where it lives

- **Route**: `/admin/otc-kyc`
- **Who can access**: staff roles (admins + operations)

---

## What staff can see

Staff review KYC submissions with:

- **Customer identity**: name and email (from the user profile)
- **Submission metadata**: structured info captured during onboarding (stored as `metadata`)
- **Review notes**: internal-only notes written by staff
- **Timeline**: created/submitted/reviewed timestamps
- **Documents**: uploaded files linked to the submission

Documents are stored in Supabase Storage (bucket: `kyc-docs`). The admin UI generates **signed download URLs** so staff can securely view files without making the bucket public.

---

## Status lifecycle

Each submission has a `status`:

| Status | Meaning |
|--------|---------|
| `draft` | Customer started but hasn’t submitted |
| `submitted` | Ready for staff review |
| `needs_changes` | Staff requests corrections or additional documents |
| `approved` | KYC accepted |
| `rejected` | KYC rejected |

Typical flow:

`submitted` → `approved` (or `needs_changes` / `rejected`)

---

## Staff workflow

1. **Filter** by status (default: `submitted`).
2. **Search** by email, name, status, or submission id.
3. Open a submission and review:
   - metadata
   - uploaded documents
   - any prior review notes
4. Update:
   - **status**
   - optional **review notes**

---

## Security and access notes

- Access to submissions is protected by database policies (staff only).
- Documents remain private in Storage; staff download access is time-limited via signed URLs.

---

## Related docs

- [Admin dashboard overview](dashboard-overview.md)

