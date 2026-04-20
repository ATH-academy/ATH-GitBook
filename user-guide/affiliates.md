# Affiliate program

All Time High Academy includes tools for **affiliates** who promote the academy and track referrals.

---

## Where it lives in the app

| Route | Who uses it |
|-------|-------------|
| `/affiliates` | Public program information page (when linked from marketing). |
| `/affiliate` | **Affiliate dashboard** (requires sign-in). |

The affiliate dashboard is for reviewing leads, sales, and commission status according to the active program rules.

---

## Attribution with `?ref=`

The app can store an affiliate code when someone arrives with a **`?ref=CODE`** query parameter on the URL. That value is kept in the browser for use in checkout or reporting flows later.

**Example:**

```text
https://alltimehigh.academy/?ref=YOUR_CODE
```

<div class="docsify-callout docsify-callout--warning">
<p><strong>Important:</strong> Use only codes assigned to you by the team. Incorrect links will not record commissions.</p>
</div>

---

## Support

For questions about payouts, codes, or marketing assets, contact the team through the channels on [Contact](../support/contact.md).
