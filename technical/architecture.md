# Architecture Overview

Technical architecture of All Time High Academy.

---

## System Architecture

### High-Level Overview

```
┌─────────────────────────────────────────────────────────────┐
│                         USERS                                │
│    (Web Browser / Mobile Browser / PWA)                      │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                     VERCEL EDGE                              │
│    (CDN, Static Assets, Serverless Functions)                │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                   REACT APPLICATION                          │
│    (SPA, Client-Side Rendering, React Router)                │
└─────────────────────────────────────────────────────────────┘
                              │
          ┌───────────────────┼───────────────────┐
          ▼                   ▼                   ▼
┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐
│    SUPABASE     │ │      MUX        │ │   THIRD-PARTY   │
│   (Backend)     │ │    (Video)      │ │   (Payments)    │
│                 │ │                 │ │                 │
│ - PostgreSQL    │ │ - Video CDN    │ │ - Stripe        │
│ - Auth          │ │ - Streaming    │ │ - Whop          │
│ - Edge Funcs    │ │ - JWT Tokens   │ │                 │
│ - Realtime      │ │                 │ │                 │
└─────────────────┘ └─────────────────┘ └─────────────────┘
```

---

## Core Components

### Frontend

| Component | Technology |
|-----------|------------|
| Framework | React 19 |
| Language | TypeScript 5.8+ |
| Build Tool | Vite 5.4+ |
| Styling | TailwindCSS 3.4+ |
| Components | shadcn/ui (Radix) |
| Routing | React Router 7.6+ |
| State | React Query + Context |
| Forms | React Hook Form + Zod |

### Backend

| Component | Technology |
|-----------|------------|
| Database | PostgreSQL 15+ (Supabase) |
| Auth | Supabase Auth |
| API | Supabase Edge Functions |
| Realtime | Supabase Realtime |
| Storage | Supabase Storage |

### External Services

| Service | Purpose |
|---------|---------|
| Vercel | Hosting & CDN |
| MUX | Video streaming |
| Stripe | Payments |
| Whop | Memberships |
| Discord | OAuth & Community |
| Resend | Email |

---

## Data Flow

### Authentication Flow

```
User → Login Page → Choose Auth Method
                          │
        ┌─────────────────┼─────────────────┐
        ▼                 ▼                 ▼
    Email/Pass       Discord OAuth     Whop OAuth
        │                 │                 │
        ▼                 ▼                 ▼
    Supabase         Supabase          Edge Function
      Auth           Discord            Whop API
        │             Provider              │
        └─────────────────┼─────────────────┘
                          ▼
                    JWT Token
                          │
                          ▼
                    Client State
                          │
                          ▼
                   Protected Routes
```

### Course Access Flow

```
User → Course Page → Check Enrollment
                           │
            ┌──────────────┼──────────────┐
            ▼              ▼              ▼
      Not Enrolled    Free Course    Enrolled
            │              │              │
            ▼              ▼              ▼
      Show Upgrade    Grant Access   Grant Access
         Options           │              │
                           ▼              ▼
                    Load Modules    Load Modules
                           │              │
                           ▼              ▼
                    Check Lock      Check Lock
                       Status          Status
                           │              │
                           ▼              ▼
                    Render Content  Render Content
```

### Video Playback Flow

```
User → Video Module → Request Playback
                           │
                           ▼
              Edge Function (get-videos)
                           │
                           ▼
              Verify User Enrollment
                           │
              ┌────────────┼────────────┐
              ▼            ▼            ▼
           No Access   Free Module  Has Access
              │            │            │
              ▼            ▼            ▼
           Return       Generate     Generate
            403        Signed JWT   Signed JWT
                           │            │
                           └─────┬──────┘
                                 ▼
                          MUX Player
                                 │
                                 ▼
                        Secure Video Stream
```

---

## Database Architecture

### Core Tables

```
┌──────────────────┐     ┌──────────────────┐
│      users       │     │    categories    │
├──────────────────┤     ├──────────────────┤
│ id (FK auth.users)│    │ id               │
│ email            │     │ name             │
│ username         │     │ slug             │
│ role             │     │ icon             │
│ discord_user_id  │     └──────────────────┘
└──────────────────┘              │
         │                        │
         │         ┌──────────────┘
         │         │
         ▼         ▼
┌──────────────────┐     ┌──────────────────┐
│    enrollments   │◄────│     courses      │
├──────────────────┤     ├──────────────────┤
│ id               │     │ id               │
│ user_id          │     │ title, slug      │
│ course_id        │     │ category_id      │
│ progress_%       │     │ instructor_id    │
│ status           │     │ access_level     │
└──────────────────┘     └──────────────────┘
         │                        │
         │                        │
         ▼                        ▼
┌──────────────────┐     ┌──────────────────┐
│ module_progress  │◄────│     modules      │
├──────────────────┤     ├──────────────────┤
│ id               │     │ id               │
│ enrollment_id    │     │ course_id        │
│ module_id        │     │ parent_id        │
│ is_completed     │     │ type             │
│ quiz_score       │     │ mux_asset_id     │
└──────────────────┘     └──────────────────┘
                                  │
                                  ▼
                         ┌──────────────────┐
                         │  module_quizzes  │
                         ├──────────────────┤
                         │ id               │
                         │ module_id        │
                         │ passing_score    │
                         └──────────────────┘
```

### Security Model

All tables use Row-Level Security (RLS):
- Users can only access their own data
- Admins have full access
- Public content available to all
- Published content filtered by access level

---

## Frontend Architecture

### Directory Structure

```
src/
├── features/           # Feature-based modules
│   ├── auth/          # Authentication
│   ├── courses/       # Course management
│   ├── dashboard/     # User dashboard
│   ├── admin/         # Admin panel
│   └── home/          # Landing page
├── shared/            # Shared utilities
│   ├── components/    # UI components
│   ├── services/      # API services
│   └── hooks/         # Custom hooks
├── providers/         # Context providers
├── lib/              # Libraries
│   ├── supabase/     # Supabase client
│   ├── whop/         # Whop OAuth
│   └── i18n/         # Internationalization
└── pages/            # Page components
```

### State Management

| State Type | Solution |
|------------|----------|
| Server State | React Query |
| Auth State | React Context |
| UI State | React Context |
| Form State | React Hook Form |
| Local State | useState |

---

## API Architecture

### Supabase Client

```typescript
// Direct database queries
const { data } = await supabase
  .from('courses')
  .select('*')
  .eq('is_published', true);

// Edge Functions
const { data } = await supabase.functions.invoke('quiz', {
  body: { quizId, answers }
});

// Realtime subscriptions
supabase
  .channel('progress')
  .on('postgres_changes', handler)
  .subscribe();
```

### Edge Functions

| Function | Purpose |
|----------|---------|
| get-videos | Generate MUX JWT tokens |
| quiz | Process quiz submissions |
| progress | Track module progress |
| whop-oauth-* | Whop authentication |

---

## Deployment Architecture

### Vercel Deployment

```
GitHub Push
     │
     ▼
Vercel Build
     │
     ├── Build React App
     ├── Generate Static Assets
     └── Deploy to Edge
     │
     ▼
Global CDN Distribution
```

### Supabase Deployment

```
Local Development
     │
     ▼
Migration Files
     │
     ▼
supabase db push
     │
     ▼
Production Database
```

---

## Caching Strategy

### Frontend Caching

| Data Type | Strategy | TTL |
|-----------|----------|-----|
| Course List | Stale-while-revalidate | 5 min |
| User Progress | Real-time invalidation | N/A |
| Static Assets | CDN Cache | Long |

### Backend Caching

| Data Type | Strategy |
|-----------|----------|
| Database Queries | PostgreSQL query cache |
| Edge Functions | Stateless |
| Video Tokens | JWT expiration |

---

## Performance Considerations

### Frontend

- Code splitting by route
- Lazy loading for components
- Image optimization
- Font subsetting

### Backend

- Database indexes
- Connection pooling
- RLS policy optimization
- Edge function cold starts

### Video

- Adaptive bitrate streaming
- CDN distribution
- Signed URLs for security

---

## Monitoring & Observability

### Current

| Aspect | Tool |
|--------|------|
| Error Tracking | Console logging |
| Performance | Vercel Analytics |
| Database | Supabase Dashboard |

### Planned

- Sentry for error tracking
- Custom analytics dashboard
- Performance monitoring

---

## Next Steps

- Review [Tech Stack](tech-stack.md) details
- Understand [Integrations](integrations.md)
- Learn about [Security](security.md)
