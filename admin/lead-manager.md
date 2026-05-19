# Lead Manager

The **Lead Manager** is the staff-facing pipeline for reviewing and organizing inbound leads across multiple sources in one place.

---

## Where it lives

- **Route**: `/admin/leads`
- **Who can access**: admins and operations staff

---

## What it aggregates

Leads are unified into a single table called `crm_leads`, which can be populated from multiple systems:

- `ath_leads` (platform lead capture, e.g. webinar/event signups, home contact, free course, etc.)
- `affiliate_leads` (affiliate program lead capture)
- `manual_import` (staff-added records; optional)

Each CRM row keeps the best available **name**, **email**, **phone**, and a JSON `metadata` payload with source details. The admin UI loads the most recent **800** rows ordered by `created_at`.

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

## Dashboard header

Four stat cards summarize the loaded dataset:

- **Total** — all CRM rows in the current fetch
- **Leads** — count in stage `lead`
- **Qualified** — count in stage `qualified`
- **ATH members** — count in stage `ath_member`

---

## Working the queue

### Stage tabs

Filter the main workspace by stage. Tabs show live counts: **Leads**, **Qualified**, **ATH members**, and **All**.

### Layout modes

| Mode | Behavior |
|------|----------|
| **Stages** | Kanban board (`CrmLeadsKanban`) across all stages; search and origin filters still apply |
| **List** | Tabular view for the active stage tab with pagination |

### Search and filters

- **Search** — name, email, phone, `stage`, `source_system`, and `source`
- **Origin filter** — webinar, event, contact form, free course, or other (derived from the `source` field)

### List pagination

In list mode, choose **25**, **50**, or **100** rows per page. The footer shows the visible range and total matching rows.

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
- `other` (anything else)

For webinars and events, cards can show extra detail from `metadata` (for example `webinar_title_snapshot`, `landing_path`, or `webinar_id` captured at signup).

---

## Staff actions

Typical operator workflow:

- **Move stage** — drag on the kanban or update in list view (optimistic UI with server persistence on `crm_leads.stage`)
- **Copy** email or phone from a card
- **Export (Excel columns)** — CSV with name, phone, and email for the active stage tab (Spanish or English headers based on UI language)
- **Export (full)** — CSV of the current filtered set including `created_at`, contact fields, `stage`, `source_system`, and `source`

Lead import from this screen is **not** supported; the manager is export- and stage-update-focused.

---

## Related docs

- [Webinars & in-person events](../user-guide/events-webinars.md)
- [Affiliate program](../user-guide/affiliates.md)
- [Affiliates manager](affiliates-manager.md)
