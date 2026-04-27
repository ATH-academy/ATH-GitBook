# Lead Manager

The **Lead Manager** is the staff-facing pipeline for reviewing and organizing inbound leads across multiple sources in one place.

---

## Where it lives

- **Route**: `/admin/leads`
- **Who can access**: staff roles (admins + operations)

---

## What it aggregates

Leads are unified into a single table called `crm_leads`, which can be populated from multiple systems:

- `ath_leads` (platform lead capture, e.g. webinar/event signups, home contact, free course, etc.)
- `affiliate_leads` (affiliate program lead capture)
- `manual_import` (staff-added records; optional)

Each CRM row keeps the best available **name**, **email**, **phone**, and a JSON `metadata` payload with source details.

---

## Pipeline stages

The pipeline stage is stored on each lead as `stage`:

| Stage | Meaning |
|------|---------|
| `lead` | New lead (not yet qualified) |
| `qualified` | Reviewed and qualified for follow-up |
| `ath_member` | Converted to member/customer |

Operators typically move leads through these stages as outreach progresses.

---

## Dedupe behavior (high level)

When syncing from source tables into `crm_leads`, the system attempts a best-effort merge:

1. Prefer matching by **normalized email** (lowercased/trimmed).
2. If no email exists, fall back to **normalized phone** (digits only).

This keeps a single “canonical” lead record even if the same person opts in via different forms.

---

## Common lead origins

The UI recognizes common origin keys such as:

- `webinar`
- `evento`
- `home-contact`
- `free_course`

For webinars/events, the lead metadata can include a snapshot title or landing path so staff can quickly identify the campaign the lead came from.

---

## Staff actions

Typical operator workflow:

- **Search and filter** leads by name/email/phone/source.
- **Update stage** as the lead progresses (lead → qualified → member).
- **Export to CSV** for reporting or external outreach tooling.

---

## Related docs

- [Webinars & in-person events](../user-guide/events-webinars.md)
- [Affiliate program](../user-guide/affiliates.md)

