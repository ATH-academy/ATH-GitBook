# All Time High Academy

<div class="docsify-callout docsify-callout--success">
<p><strong>Crypto education built for real outcomes</strong> — structured courses, certifications, community, and tooling in one place.</p>
</div>

---

## What this site is

This GitBook space documents **how the product works today**: learning paths, memberships, certifications, public pages (webinars, events, kids), and the admin tooling staff use to run the academy.

| If you want to… | Start here |
|-----------------|------------|
| Get productive fast | [Quick Start](welcome/quick-start.md) |
| See routes & features | [Platform Overview](welcome/platform-overview.md) |
| Compare plans | [Plan Comparison](membership/plan-comparison.md) |
| Ship docs to GitBook | [Publishing on GitBook](reference/gitbook-setup.md) |

---

## Highlights

### Learning & proof

- Hierarchical **courses** with modules, video (MUX), and sequential unlocks.
- **Quizzes** with retries and score tracking.
- **Certification tracks** (ATH-CCP, ATH-CDS, ATH-CMA) with admin review where applicable.

### Community & growth

- **Discord** integration for members.
- **Webinars** (`/webinar`) and **in-person events** (`/evento`) with dedicated landings.
- **Affiliate** panel (`/affiliate`) and `?ref=` attribution for partners.

### Product surface

- **Bilingual** UI (English / Spanish).
- **Dashboard** with progress, calculators, and certification status.
- **ATH Kids** landing at `/kids`.
- Marketing landings such as **`/go`** (contact / acquisition) and **`/altura`** (institutional vs personal paths).

---

## Membership at a glance

| Plan | Best for |
|------|----------|
| **Free** | Exploring intro content |
| **Community** | Full course access + Discord |
| **VIP** | Deeper support and sessions |
| **Concierge** | Highest-touch guidance |

Exact pricing and entitlements live in-app on [Pricing](https://alltimehigh.academy/pricing) and in [Choosing Your Plan](getting-started/choosing-plan.md).

---

## Help

- [FAQ](support/faq.md) · [Troubleshooting](support/troubleshooting.md) · [Contact](support/contact.md)
- [Changelog](CHANGELOG.md) for **documentation** updates (not the application release notes).

---

## GitHub Pages (Docsify)

This repository ships a static documentation shell (`index.html`, `404.html`, `sidebar.md`, `.nojekyll`) powered by [Docsify](https://docsify.js.org/). You can host it **only on GitHub** with no build step.

**Recommended (fixes many “404” cases): GitHub Actions**

1. Push `main` including `.github/workflows/pages.yml`.
2. **Settings → Pages → Build and deployment → Source:** **GitHub Actions** (not “Deploy from a branch” unless you know that path works for this org).
3. Open the **Actions** tab and confirm the **Deploy GitHub Pages** workflow run succeeds (approve it once if the org asks).
4. The site URL is **https://ath-academy.github.io/ATH-GitBook/** — use hash routes such as `/#/welcome/quick-start`.

**Alternative:** **Settings → Pages →** Source **Deploy from a branch**, branch **main**, folder **/** (root).

If the root URL still returns **404**, the Pages source is usually wrong, the workflow has not run yet, or an org policy blocks Pages—use Actions + a green workflow run as the checklist.

Keep **`sidebar.md`** in sync with **`SUMMARY.md`** when you add or rename pages so GitBook and GitHub Pages stay aligned.

---

*All Time High Academy — documentation aligned with the live platform.*
