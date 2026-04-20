# Integrations

Third-party services integrated with All Time High Academy.

---

## MUX (Video Streaming)

### Overview
MUX provides video hosting, encoding, and streaming for all course videos.

### How It Works

```
Upload Video → MUX Processing → Asset ID Generated
                                      │
User Requests Video → Edge Function → Generate JWT
                                      │
                            MUX Player → Secure Stream
```

### Configuration

**Environment Variables:**
```bash
MUX_SIGNING_KEY_ID=your-key-id
MUX_SIGNING_PRIVATE_KEY=-----BEGIN RSA PRIVATE KEY-----...
```

### JWT Token Generation

```typescript
// Edge function generates signed tokens
import Mux from '@mux/mux-node';

const mux = new Mux();
const token = mux.JWT.signPlaybackId(playbackId, {
  type: 'video',
  expiration: '2h'
});
```

### Video Player

```typescript
// React component
import MuxPlayer from '@mux/mux-player-react';

<MuxPlayer
  playbackId={playbackId}
  tokens={{
    playback: playbackToken,
    thumbnail: thumbnailToken
  }}
/>
```

### Features Used
- Signed URL playback
- Adaptive bitrate streaming
- Thumbnail generation
- Playback analytics

---

## Supabase

### Overview
Supabase provides the complete backend infrastructure.

### Components Used

| Component | Purpose |
|-----------|---------|
| PostgreSQL | Database |
| Auth | Authentication |
| Edge Functions | API endpoints |
| Realtime | WebSocket subscriptions |
| Storage | File storage |

### Database Access

```typescript
// Initialize client
import { createClient } from '@supabase/supabase-js';

const supabase = createClient(
  process.env.VITE_SUPABASE_URL,
  process.env.VITE_SUPABASE_ANON_KEY
);

// Query with RLS
const { data } = await supabase
  .from('courses')
  .select('*')
  .eq('is_published', true);
```

### Authentication

```typescript
// Email/password
await supabase.auth.signInWithPassword({
  email,
  password
});

// OAuth
await supabase.auth.signInWithOAuth({
  provider: 'discord'
});
```

### Edge Functions

```typescript
// Invoke function
const { data } = await supabase.functions.invoke('get-videos', {
  body: { courseId }
});
```

### Realtime

```typescript
// Subscribe to changes
supabase
  .channel('progress')
  .on('postgres_changes', {
    event: 'UPDATE',
    schema: 'public',
    table: 'module_progress'
  }, handleChange)
  .subscribe();
```

---

## Whop

### Overview
Whop handles membership management and payments for subscriptions.

### OAuth Flow

```
User Clicks "Login with Whop"
           │
           ▼
Edge Function: whop-oauth-init
           │
           ▼
Redirect to Whop Authorization
           │
           ▼
User Authorizes
           │
           ▼
Callback to: whop-oauth-callback
           │
           ▼
Store Tokens & User Info
           │
           ▼
Create/Update Supabase User
```

### Configuration

```bash
VITE_WHOP_APP_ID=your-app-id
VITE_WHOP_API_KEY=your-api-key
VITE_WHOP_REDIRECT_URI=https://your-domain/auth/callback
```

### Webhook Events

| Event | Purpose |
|-------|---------|
| membership.created | New subscription |
| membership.updated | Subscription change |
| membership.cancelled | Cancellation |
| payment.succeeded | Payment received |
| payment.failed | Payment failed |

### Membership Sync

```typescript
// Webhook handler syncs membership data
async function handleWebhook(event) {
  switch (event.type) {
    case 'membership.created':
      await syncMembership(event.data);
      break;
    case 'membership.cancelled':
      await cancelMembership(event.data);
      break;
  }
}
```

---

## Discord

### Overview
Discord provides OAuth authentication and community integration.

### OAuth via Supabase

```typescript
// Initiate Discord OAuth
await supabase.auth.signInWithOAuth({
  provider: 'discord',
  options: {
    redirectTo: `${window.location.origin}/auth/discord/callback`
  }
});
```

### User Data Retrieved

| Field | Description |
|-------|-------------|
| id | Discord user ID |
| email | User email |
| username | Discord username |
| avatar | Profile picture URL |

### Community Connection

After OAuth:
1. Store Discord user ID
2. Check community membership
3. Grant community access
4. Display connection status

---

## Stripe

### Overview
Stripe processes credit card payments for subscriptions.

### Integration Points

| Integration | Purpose |
|-------------|---------|
| Checkout | Payment collection |
| Webhooks | Payment events |
| Customer Portal | Subscription management |

### Payment Flow

```
User Selects Plan
       │
       ▼
Create Checkout Session
       │
       ▼
Redirect to Stripe Checkout
       │
       ▼
User Completes Payment
       │
       ▼
Webhook: payment.succeeded
       │
       ▼
Activate Subscription
```

### Configuration

```bash
STRIPE_SECRET_KEY=sk_...
STRIPE_WEBHOOK_SECRET=whsec_...
```

---

## Resend

### Overview
Resend handles transactional email delivery.

### Email Types

| Email Type | Trigger |
|------------|---------|
| Welcome | User registration |
| Verification | Email confirmation |
| Password Reset | Password reset request |
| Notifications | Various platform events |

### Configuration

```bash
RESEND_API_KEY=re_...
```

### Usage

```typescript
import { Resend } from 'resend';

const resend = new Resend(process.env.RESEND_API_KEY);

await resend.emails.send({
  from: 'ATH Academy <noreply@alltimehigh.academy>',
  to: user.email,
  subject: 'Welcome to All Time High Academy',
  html: welcomeTemplate
});
```

---

## CoinGecko (Planned)

### Overview
CoinGecko will provide cryptocurrency price data.

### Planned Features

| Feature | Purpose |
|---------|---------|
| Price Data | Current BTC/crypto prices |
| Historical Data | Price charts |
| Market Cap | Coin rankings |

### API Usage

```typescript
// Example API call
const response = await fetch(
  'https://api.coingecko.com/api/v3/simple/price?ids=bitcoin&vs_currencies=usd'
);
const { bitcoin } = await response.json();
```

---

## Integration Architecture

### Data Flow

```
┌─────────────────────────────────────────────────┐
│                  FRONTEND                        │
│        (React Application)                       │
└────────────────────┬────────────────────────────┘
                     │
        ┌────────────┼────────────┐
        ▼            ▼            ▼
   ┌─────────┐  ┌─────────┐  ┌─────────┐
   │ Supabase│  │   MUX   │  │  Whop   │
   │         │  │         │  │         │
   │ Database│  │ Videos  │  │ Payments│
   │ Auth    │  │ Stream  │  │ Members │
   └─────────┘  └─────────┘  └─────────┘
        │
        ▼
   ┌─────────┐
   │ Discord │
   │         │
   │ OAuth   │
   │Community│
   └─────────┘
```

### Webhook Architecture

```
External Service
       │
       ▼ (webhook)
Supabase Edge Function
       │
       ▼ (validate)
Process Event
       │
       ▼ (update)
Database
       │
       ▼ (notify)
Realtime Subscribers
```

---

## Environment Variables Summary

```bash
# Supabase
VITE_SUPABASE_URL=https://xxx.supabase.co
VITE_SUPABASE_ANON_KEY=eyJ...

# Whop
VITE_WHOP_APP_ID=app_xxx
VITE_WHOP_API_KEY=xxx
VITE_WHOP_REDIRECT_URI=https://your-domain/auth/callback

# MUX (Edge Functions)
MUX_SIGNING_KEY_ID=xxx
MUX_SIGNING_PRIVATE_KEY=-----BEGIN RSA PRIVATE KEY-----...

# Stripe (Edge Functions)
STRIPE_SECRET_KEY=sk_...
STRIPE_WEBHOOK_SECRET=whsec_...

# Resend (Edge Functions)
RESEND_API_KEY=re_...
```

---

## Next Steps

- Review [Security](security.md) practices
- See [API Reference](api-reference.md)
- Understand [Architecture](architecture.md)
