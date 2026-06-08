# Lead Manager

The **Lead Manager** is the staff-facing CRM pipeline for reviewing, qualifying, and converting inbound leads from every channel in one place.

---

## Where it lives

- **Route**: `/admin/leads`
- **Who can access**: admins and operations staff (see [Dashboard overview](dashboard-overview.md))

---

## Dual admin views

The same person can appear in more than one source table. Operations uses two complementary lenses:

| View | Route | Purpose |
|------|-------|---------|
| **Lead Manager** | `/admin/leads` | Unified pipeline — all origins, full stage workflow, comments, follow-ups |
| **Affiliates Manager** | `/admin/affiliates` | Affiliate-scoped leads, commissions, payouts, and partner leaderboard |

Affiliate-attributed leads appear in **both** views. Converting an affiliate lead from either surface runs a **dual-write**: `admin_convert_affiliate_lead` plus `admin_convert_crm_lead_to_member`.

See [Affiliates Manager](affiliates-manager.md) for commission and payout workflows.

---

## Data model

### `crm_leads` — pipeline identity

One row per contact in the sales pipeline. Stores:

- Contact fields (`full_name`, `email`, `phone`)
- **Stage** (`stage`) — see [Pipeline stages](#pipeline-stages)
- Primary source hint (`source_system`, `source`, `source_record_id`)
- Follow-up dates (`last_contacted_at`, `next_follow_up_at`)
- JSON `metadata` with merged snapshots from source systems

Leads are deduplicated on sync by **normalized email**, or **normalized phone** when email is missing.

### `crm_lead_sources` — linked touchpoints

Each CRM lead can have **multiple** source records (webinar signup + affiliate referral, etc.):

| Field | Meaning |
|-------|---------|
| `source_system` | `ath_leads`, `affiliate_leads`, or `manual_import` |
| `source_record_id` | UUID of the row in the source table |
| `is_primary` | Main touchpoint used for display |
| `metadata` | Snapshot from that source at link time |

Source tables sync into CRM on **insert** and **update**. Staff stage changes can sync back to linked `affiliate_leads.status` when applicable.

### Source tables

- **`ath_leads`** — platform capture (webinars, events, home contact, free course, etc.)
- **`affiliate_leads`** — affiliate program capture

---

## Pipeline stages

| Stage | Kanban group | Meaning |
|-------|--------------|---------|
| `lead` | Intake | New, not yet contacted |
| `first_contact` | First contact | Initial outreach done |
| `first_meeting` | Meetings | First meeting scheduled or held |
| `second_meeting` | Meetings | Second meeting |
| `visit` | Meetings | In-person or deep-dive session |
| `first_follow_up` | Follow-up | First follow-up cycle |
| `second_follow_up` | Follow-up | Second follow-up cycle |
| `ath_member` | Closed | Converted — requires product selection |

Moving to `ath_member` opens the **product conversion** dialog; it does not use a simple stage dropdown.

### CRM stage → affiliate status

When staff change a CRM stage, linked affiliate leads (that are not already `paid`, `invalid`, or `duplicate`) may update automatically:

| CRM stage | Affiliate `status` |
|-----------|-------------------|
| `ath_member` | `paid` |
| `first_contact`, meetings, follow-ups | `contacted` |
| Other | `new` |

---

## Dashboard header

Stat cards summarize the loaded dataset (up to **800** recent rows):

- **Total** — all CRM rows in the current fetch
- Counts per kanban group (intake, first contact, meetings, follow-up, closed)

---

## Working the queue

### Layout modes

| Mode | Behavior |
|------|----------|
| **Stages** | Kanban across pipeline groups; drag to change stage |
| **List** | Tabular view with pagination |

### Search and filters

- **Search** — name, email, phone, stage, source
- **Origin filter** — webinar, event, contact form, free course, affiliate, or other
- **Affiliate filter** — narrow to leads linked to a specific affiliate account

### Multi-origin badge

Leads with more than one linked touchpoint show a **Multi-origin** badge in kanban and list views.

### List pagination

Choose **25**, **50**, or **100** rows per page.

---

## Lead detail

Open a lead from kanban or list to see:

- **Linked touchpoints** — loaded via `get_crm_lead_profile` (live data from `ath_leads` / `affiliate_leads`)
- **Appointments** — GHL calendar bookings from `ath_appointments` and `affiliate_appointments`
- **Activity timeline** — stage changes, conversions, comments, follow-up updates, source sync/link events
- **Comments** — internal notes on `crm_lead_comments`
- **Follow-up dates** — last contacted and next follow-up

From affiliate-origin leads, a link opens [Affiliates Manager](affiliates-manager.md) on that partner’s leads tab.

---

## Deep links

Open Affiliates Manager filtered to one partner’s leads:

```
/admin/affiliates?section=leads&affiliate={affiliate_account_id}
```

From Lead Manager, affiliate-origin rows can surface this link when an affiliate ID is known.

---

## Staff actions

| Action | Behavior |
|--------|----------|
| **Move stage** | Kanban drag or detail dropdown; persisted via `admin_update_crm_lead_stage` |
| **Convert to member** | Select products; calls `admin_convert_crm_lead_to_member` |
| **Add comment** | Stored on `crm_lead_comments` + activity log |
| **Save follow-up dates** | Updates `crm_leads` + activity log |
| **Copy** email or phone from a card |
| **Export** | CSV for current filter (includes stage, source, origin) |

Lead import from this screen is **not** supported.

---

## Webinars Manager integration

In **Admin → Webinars**, each webinar lead row can show **`crm_stage`** — the pipeline stage from `crm_leads` joined via `ath_leads.id`. CSV exports include this column for ops handoff.

See [Webinars & Events](../user-guide/events-webinars.md).

---

## Key RPCs (technical)

| RPC | Purpose |
|-----|---------|
| `admin_update_crm_lead_stage` | Stage change + activity; syncs affiliate status when linked |
| `admin_convert_crm_lead_to_member` | Conversion with product IDs |
| `get_crm_lead_profile` | CRM row, sources (live), appointments, activity |
| `upsert_crm_lead` | Internal sync helper (triggers + staff paths) |
| `link_crm_lead_source` | Idempotent touchpoint link |

Activity event types include `stage_change`, `member_conversion`, `comment_added`, `follow_up_updated`, `source_sync`, and `source_linked`.

---

## Related docs

- [Affiliates Manager](affiliates-manager.md)
- [Webinars & in-person events](../user-guide/events-webinars.md)
- [Affiliate program (member-facing)](../user-guide/affiliates.md)
- [Dashboard overview](dashboard-overview.md)
