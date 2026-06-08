# Portfolio Tracker

Connect **on-chain wallet addresses** to see holdings, total value, profit & loss, and allocation — all in one place on your dashboard. Tracking is **read-only**: you enter a public address; the platform never asks for private keys or seed phrases.

Data is provided by [CoinStats](https://coinstats.app/) via the platform’s secure backend.

---

## Access

| Requirement | Details |
|-------------|---------|
| **Route** | [`/dashboard/portfolio`](https://alltimehigh.academy/dashboard/portfolio) |
| **Membership** | Active subscription (same as the main dashboard) |
| **Languages** | English and Spanish (UI follows your dashboard language) |

<div class="docsify-callout docsify-callout--info">
<p><strong>Navigation note:</strong> The Portfolio tab may be hidden from the main dashboard tab bar while the feature is rolled out. Use the direct URL above to open the tracker.</p>
</div>

---

## What you can do

| Capability | Description |
|------------|-------------|
| **Multi-wallet** | Connect up to **5** wallets per account |
| **Multi-chain** | Choose a supported blockchain/network when adding each address |
| **Summary metrics** | Total value, all-time P&L, unrealized P&L, and asset count |
| **Allocation heatmap** | Tile size = portfolio weight; color = 24h price change |
| **Holdings table** | Per-asset amount, price, USD value, allocation %, and 24h change |
| **Wallet management** | Optional labels, sync status, remove wallets |
| **Refresh** | Manually reload balances and summary data |

### Not included (yet)

The following are **not** part of the current release and may appear in future updates:

- Centralized exchange connections (e.g. Binance, Coinbase API)
- WalletConnect or browser-wallet signing
- Historical portfolio performance charts
- Automated price or take-profit alerts tied to holdings

See [Coming Soon](../roadmap/coming-soon.md) for planned enhancements.

---

## Getting started

### 1. Open the Portfolio Tracker

1. Sign in with an active membership.
2. Go to **`/dashboard/portfolio`** (or use a Portfolio link from the dashboard when visible).

### 2. Connect your first wallet

1. Click **Add wallet** (or **Connect your first wallet** on the empty state).
2. Complete the short onboarding (read-only security, multi-chain support, P&L overview).
3. On the connect step:
   - **Blockchain** — select the network that matches your address (e.g. Ethereum, Solana).
   - **Wallet address** — paste your **public** address only.
   - **Label (optional)** — e.g. “Main ETH wallet” for easier identification.
4. Click **Connect wallet**.

After a successful connection, CoinStats syncs on-chain balances. Holdings and P&L may take a short time to appear.

### 3. Add more wallets (optional)

Repeat **Add wallet** until you reach the **5-wallet limit**. Each wallet is tracked separately and rolled up in your combined summary.

---

## Understanding the screen

### Connected wallets

Each row shows:

- **Label** (or “Unnamed wallet” if you skipped the label)
- **Truncated address** for quick identification
- **Sync status**:
  - **Synced** — data is up to date
  - **Syncing…** — import in progress
  - **Sync error** — see [Troubleshooting](#troubleshooting) below

Use the remove control to disconnect a wallet (you’ll be asked to confirm).

### Summary cards

| Card | Meaning |
|------|---------|
| **Total value** | Combined USD value across all connected wallets |
| **All-time P&L** | Realized + unrealized performance vs. cost basis (with % badge) |
| **Unrealized P&L** | Open position gain/loss (with % badge) |
| **Assets** | Number of distinct tokens/coins reported |

### Allocation heatmap

- **Larger tiles** — higher share of total portfolio value.
- **Green tint** — positive 24h change; **red tint** — negative 24h change.
- Hover or focus a tile for symbol, value, allocation %, and 24h %.

### Holdings table

Columns: **Asset**, **Allocation**, **Amount**, **Price**, **Value**, **24h**.

If the table is empty but wallets show as synced, wait a moment and use **Refresh** — sync can still be finishing.

---

## Refresh and data freshness

- Use **Refresh** in the header to reload wallet list and summary.
- Summary data is cached briefly on the server (about **5 minutes**) to respect API limits and keep the page fast.
- Supported blockchain list is cached longer (about **24 hours**).

---

## Security and privacy

- **Read-only** — Only public addresses are stored and queried.
- **No keys** — Never paste a seed phrase or private key. Legitimate tracking only needs a public address.
- **Your account** — Wallets are tied to your academy user; other members cannot see your addresses or balances.
- **Removal** — Deleting a wallet removes it from your account and stops future sync for that address.

<div class="docsify-callout docsify-callout--warning">
<p><strong>Educational use:</strong> Balances and P&L are for personal tracking and learning. They are not tax, legal, or investment advice. Verify important figures independently.</p>
</div>

---

## Troubleshooting

### Wallet stuck on “Syncing…”

- New wallets often need a few minutes for CoinStats to index on-chain data.
- Click **Refresh** after waiting.
- If it persists, remove the wallet and add it again with the correct **blockchain** and **address**.

### “Sync error” on a wallet

- Confirm the address matches the selected network (e.g. don’t use an EVM address on Solana).
- Remove and reconnect the wallet.
- Use **Refresh** on the summary section.

### “Could not load portfolio data”

- Check your connection and try **Try again**.
- If you see a **rate limit** message, wait a few minutes — the data provider throttles heavy usage; partial data may still show.

### Banner: “Data refresh temporarily limited”

- Too many requests to CoinStats in a short window.
- Wait and use **Try refreshing** on the banner; totals may still be visible.

### Wrong or missing tokens

- Some chains, tokens, or DeFi positions may not be fully represented in CoinStats.
- Small or new tokens can lag behind major assets.
- This is a limitation of the upstream provider, not your wallet connection.

### Cannot add another wallet

- The limit is **5 wallets** per user. Remove an unused wallet to add a different one.

### I don’t see a Portfolio tab

- Open **`/dashboard/portfolio`** directly while the tab is hidden during rollout.
- Ensure your subscription is active (same requirement as the full dashboard).

---

## Related pages

- [Dashboard Features](dashboard.md) — overview, calculator, and other tools
- [Troubleshooting](../support/troubleshooting.md) — general platform issues
- [FAQ](../support/faq.md)
- [Coming Soon](../roadmap/coming-soon.md) — price alerts and other planned tools
