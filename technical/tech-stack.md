# Tech Stack

Detailed breakdown of technologies used in All Time High Academy.

---

## Frontend Stack

### Core Framework

| Technology | Version | Purpose |
|------------|---------|---------|
| React | 19.1.0 | UI framework |
| TypeScript | 5.8+ | Type safety |
| Vite | 5.4+ | Build tool |

### Styling

| Technology | Version | Purpose |
|------------|---------|---------|
| TailwindCSS | 3.4+ | Utility-first CSS |
| shadcn/ui | Latest | Component library |
| Radix UI | Various | Accessible primitives |

### State & Data

| Technology | Version | Purpose |
|------------|---------|---------|
| React Query | 5.83.0 | Server state |
| React Hook Form | Latest | Form management |
| Zod | Latest | Schema validation |

### Routing

| Technology | Version | Purpose |
|------------|---------|---------|
| React Router | 7.6+ | Client-side routing |

### UI Enhancements

| Technology | Purpose |
|------------|---------|
| Framer Motion | Animations |
| Lucide React | Icons |
| Recharts | Charts |
| Sonner | Toast notifications |

---

## Backend Stack

### Database & Auth

| Technology | Purpose |
|------------|---------|
| Supabase | Backend-as-a-Service |
| PostgreSQL 15+ | Relational database |
| Supabase Auth | Authentication |
| Row-Level Security | Data access control |

### Serverless Functions

| Technology | Purpose |
|------------|---------|
| Supabase Edge Functions | API endpoints |
| Deno | Runtime environment |

### Realtime

| Technology | Purpose |
|------------|---------|
| Supabase Realtime | WebSocket subscriptions |

---

## External Services

### Video

| Service | Purpose |
|---------|---------|
| MUX | Video hosting & streaming |
| YouTube | Fallback video hosting |

### Payments

| Service | Purpose |
|---------|---------|
| Stripe | Credit card processing |
| Whop | Membership management |

### Authentication

| Service | Purpose |
|---------|---------|
| Discord OAuth | Social login |
| Whop OAuth | Membership login |

### Email

| Service | Purpose |
|---------|---------|
| Resend | Transactional email |

---

## Infrastructure

### Hosting

| Service | Purpose |
|---------|---------|
| Vercel | Frontend hosting |
| Supabase Cloud | Backend hosting |

### CDN

| Service | Purpose |
|---------|---------|
| Vercel Edge Network | Static assets |
| MUX CDN | Video delivery |

---

## Development Tools

### Build & Development

| Tool | Purpose |
|------|---------|
| Vite | Development server & bundler |
| ESLint | Code linting |
| Prettier | Code formatting |
| TypeScript | Type checking |

### Testing

| Tool | Purpose |
|------|---------|
| Vitest | Unit testing |
| Testing Library | Component testing |
| MSW | API mocking |

### Version Control

| Tool | Purpose |
|------|---------|
| Git | Source control |
| GitHub | Repository hosting |
| Husky | Git hooks |

---

## Package Dependencies

### Production Dependencies

```json
{
  "react": "^19.1.0",
  "react-dom": "^19.1.0",
  "react-router": "^7.6.0",
  "@tanstack/react-query": "^5.83.0",
  "@supabase/supabase-js": "^2.x",
  "tailwindcss": "^3.4.x",
  "@radix-ui/react-*": "various",
  "framer-motion": "^11.x",
  "lucide-react": "latest",
  "zod": "^3.x",
  "react-hook-form": "^7.x",
  "recharts": "^2.x",
  "@mux/mux-player-react": "latest",
  "react-i18next": "^14.x",
  "i18next": "^23.x"
}
```

### Development Dependencies

```json
{
  "typescript": "^5.8.x",
  "vite": "^5.4.x",
  "vitest": "^1.x",
  "@testing-library/react": "latest",
  "eslint": "^9.x",
  "prettier": "^3.x",
  "husky": "latest"
}
```

---

## Configuration Files

### TypeScript

```typescript
// tsconfig.json highlights
{
  "compilerOptions": {
    "strict": true,
    "target": "ESNext",
    "module": "ESNext",
    "moduleResolution": "bundler",
    "jsx": "react-jsx"
  }
}
```

### Vite

```typescript
// vite.config.ts highlights
{
  plugins: [react()],
  build: {
    target: 'esnext'
  }
}
```

### Tailwind

```javascript
// tailwind.config.js highlights
{
  content: ['./src/**/*.{ts,tsx}'],
  theme: {
    extend: {
      // Custom theme extensions
    }
  }
}
```

---

## API Patterns

### Supabase Client Usage

```typescript
// Initialize client
import { createClient } from '@supabase/supabase-js';

const supabase = createClient(
  process.env.VITE_SUPABASE_URL,
  process.env.VITE_SUPABASE_ANON_KEY
);

// Query example
const { data, error } = await supabase
  .from('courses')
  .select(`
    *,
    modules (*)
  `)
  .eq('is_published', true);
```

### React Query Pattern

```typescript
// Query hook example
export function useCourses() {
  return useQuery({
    queryKey: ['courses'],
    queryFn: () => coursesService.getCourses(),
    staleTime: 5 * 60 * 1000 // 5 minutes
  });
}
```

### Form Pattern

```typescript
// Form with validation
const schema = z.object({
  email: z.string().email(),
  password: z.string().min(8)
});

const form = useForm<FormData>({
  resolver: zodResolver(schema)
});
```

---

## Environment Variables

### Required Variables

```bash
VITE_SUPABASE_URL=your-supabase-url
VITE_SUPABASE_ANON_KEY=your-anon-key
VITE_WHOP_APP_ID=your-whop-app-id
VITE_WHOP_API_KEY=your-whop-api-key
VITE_WHOP_REDIRECT_URI=your-redirect-uri
VITE_APP_URL=your-app-url
VITE_APP_NAME=All Time High Academy
NODE_ENV=development|production
```

### MUX Variables (Edge Functions)

```bash
MUX_SIGNING_KEY_ID=your-mux-key-id
MUX_SIGNING_PRIVATE_KEY=your-mux-private-key
```

---

## Browser Support

### Supported Browsers

| Browser | Version |
|---------|---------|
| Chrome | Last 2 versions |
| Firefox | Last 2 versions |
| Safari | Last 2 versions |
| Edge | Last 2 versions |

### Mobile

| Platform | Support |
|----------|---------|
| iOS Safari | Supported |
| Android Chrome | Supported |
| PWA | Planned |

---

## Performance Targets

### Core Web Vitals

| Metric | Target |
|--------|--------|
| LCP | < 2.5s |
| FID | < 100ms |
| CLS | < 0.1 |

### Bundle Size

| Aspect | Target |
|--------|--------|
| Initial JS | < 200KB gzipped |
| CSS | < 50KB gzipped |

---

## Next Steps

- Understand [Integrations](integrations.md)
- Review [Security](security.md) practices
- See [API Reference](api-reference.md)
