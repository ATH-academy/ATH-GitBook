# Admin dashboard overview

The admin dashboard is a **tab-based** console at `/admin/:tab`. What you see depends on your **role** (full admin, operations, or Discord-linked moderator).

---

## How to access

1. Sign in with a staff account.
2. Go to **`/admin`** — you are redirected to the default section for your role.

---

## Sections (implemented in the app)

### Learning

| Tab | Purpose |
|-----|---------|
| **Learning progress** | Track student progress and completion. |
| **Quiz progress** | Quiz performance across learners. |
| **Quiz manager** | Create and maintain question banks. |
| **Certification review** | Certification queue; approve or reject candidates. |

### Operations

| Tab | Purpose |
|-----|---------|
| **Live streaming** | Manage live streams and publishing status. |
| **Live sessions** | Cohort session calendar and timelines. |
| **Webinar/Event** | Webinar and in-person event landings, countdowns, and lead exports. |
| **Attendance** | Attendance stats and records. |
| **Leads** | Unified `crm_leads` pipeline: stages, kanban/list views, filters, and export. See [Lead Manager](lead-manager.md). |

### Marketing and community

| Tab | Purpose |
|-----|---------|
| **Affiliates** | Affiliate leads, commission rules, monthly withdrawals, and history. See [Affiliates Manager](affiliates-manager.md). |
| **External invites** | External onboarding links and promotional invites (e.g. Whop). |

### OTC Desk

| Tab | Purpose |
|-----|---------|
| **KYC** | Review customer submissions and documents. See [OTC Desk KYC](otc-kyc.md). |
| **Operations** | OTC trade operations (coming soon). |

Customers complete verification at **`/kyc`**. See [OTC Desk KYC (customer)](../user-guide/kyc-onboarding.md).

---

## Restricted roles

- **Discord moderator:** usually **Live streaming** only, or other sections agreed with the team.
- **Operations:** focused on **Webinars**, **Live streaming**, **Leads**, **Affiliates**, and **OTC Desk KYC** (per configuration).

Ask a team admin if you need additional access.

---

## Related documentation

- [Certification review](certification-review.md)
- [Quiz management](quiz-management.md)
- [Content management](content-management.md) (course catalog may be managed outside these screens)
