# Affiliates manager

The **Affiliates** admin section is the staff console for affiliate program leads, commission rules, monthly payouts, and withdrawal history.

---

## Where it lives

- **Route**: `/admin/affiliates`
- **Who can access**: admins and operations staff (see [Dashboard overview](dashboard-overview.md))

---

## At-a-glance metrics

The header shows three counters derived from `affiliate_leads`:

| Metric | Meaning |
|--------|---------|
| Total leads | All affiliate-attributed leads |
| New / under review | Leads not yet marked paid |
| Marked paid | Leads converted to paid sales |

---

## Commission settings

Staff can expand **commission settings** to maintain catalog and tier rules in USD.

### Products (`affiliate_products`)

Per active product, configure:

| Field | Purpose |
|-------|---------|
| `commission_type` | `percent`, `fixed_usd`, or `tiered_lifetime` |
| `commission_percent` | Percent of `price_usd` when type is percent |
| `commission_fixed_usd` | Flat commission when type is fixed |
| `counts_toward_tier` | Whether the sale advances the affiliate lifetime tier counter |
| `tier_scope` | Scope key for tiered lifetime products (default `high_ticket`) |

### Tier ladder (`affiliate_commission_tiers`)

For `tiered_lifetime` products, tiers are keyed by **scope** and **client index** (with optional **terminal** rows). Staff can edit tier **amount_usd** values inline.

The admin UI **previews** commission lines with the same logic as the database RPC `admin_convert_affiliate_lead` before marking a lead paid.

---

## Leads tab

### Leaderboard

Rank affiliates by paid leads, sales volume, and commission for:

- **Global** (all time)
- **Monthly** or **yearly** (with year and, for monthly, month selectors)

Show **Top 10**, **Top 25**, or **Top 50**. Copy affiliate IDs from the table when needed.

### Lead pipeline

Affiliate leads use `affiliate_leads.status`:

| Status | Typical use |
|--------|-------------|
| `new` | Just captured |
| `contacted` | Outreach in progress |
| `paid` | Sale recorded and commission generated |
| `invalid` | Not a valid referral |
| `duplicate` | Duplicate of an existing lead |

**Views**

- **Global** vs **per-affiliate** (sidebar picker when per-affiliate is selected)
- **Stages** (kanban) vs **list**

**Search** matches lead name, email, phone, country, notes, and affiliate email.

### Marking a lead paid

1. Open a lead and choose one or more **products** (`affiliate_lead_products`).
2. Review the commission breakdown (percent, fixed, or tiered lines).
3. Confirm **Mark paid** — the app calls `admin_convert_affiliate_lead` with the selected product IDs and persists sale and commission amounts on the lead.

Staff can also update status directly (for example mark **Invalid**) without converting.

---

## Payouts tab

Monthly commission **referrals** (`affiliate_referrals`) are grouped by affiliate and calendar month.

| Referral status | Meaning |
|-----------------|---------|
| `pending` | Awaiting approval |
| `approved` | Eligible for withdrawal |
| `payout` | Included in a created withdraw |
| `paid` | Paid out |
| `cancelled` | Voided |

**Workflow**

1. Select **year** and **month**.
2. Pick an affiliate from the sidebar (approved / payout / paid counts and totals).
3. Review **payment preferences** from `affiliate_accounts` (read-only — affiliates configure these in `/affiliate`).
4. Use **Create withdraw** to call `create_affiliate_monthly_payout` for approved items in that month (requires a configured payout method on the affiliate account).

---

## Withdrawals tab

Browse **`affiliate_payouts`** withdrawal history by year and month. Filter by affiliate and export rows for reporting (amount, currency, method, status, payment date, and reference).

---

## Related docs

- [Affiliate program (member-facing)](../user-guide/affiliates.md)
- [Lead Manager](lead-manager.md) — unified CRM pipeline (`crm_leads`)
- [Dashboard overview](dashboard-overview.md)
