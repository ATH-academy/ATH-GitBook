# Security

Security practices and implementations in All Time High Academy.

---

## Overview

Security is a core priority for All Time High Academy. This document outlines the security measures implemented across the platform.

---

## Authentication

### Multi-Method Authentication

| Method | Provider | Security |
|--------|----------|----------|
| Email/Password | Supabase Auth | Bcrypt hashing |
| Discord OAuth | Supabase + Discord | OAuth 2.0 |
| Whop OAuth | Edge Functions | OAuth 2.0 |

### Password Security

- Minimum 8 characters
- Bcrypt hashing (industry standard)
- Password reset via email
- No plain-text storage

### OAuth Security

- State parameter for CSRF protection
- Secure token storage
- Token expiration handling
- Refresh token rotation

### Session Management

- JWT-based sessions
- Automatic token refresh
- Secure cookie storage
- Session timeout policies

---

## Authorization

### Role-Based Access Control (RBAC)

| Role | Access Level |
|------|--------------|
| Student | Own data only |
| Instructor | Own data only |
| Admin | Full access |

### Row-Level Security (RLS)

All database tables enforce RLS:

```sql
-- Example: Users can only see their own enrollments
CREATE POLICY "Users can view own enrollments"
ON enrollments FOR SELECT
USING (auth.uid() = user_id);

-- Admins can view all enrollments
CREATE POLICY "Admins can view all enrollments"
ON enrollments FOR SELECT
USING (public.is_admin());
```

### Admin Detection

```sql
CREATE FUNCTION public.is_admin(p_user_id UUID DEFAULT auth.uid())
RETURNS BOOLEAN
LANGUAGE plpgsql
SECURITY DEFINER
AS $$
BEGIN
  RETURN EXISTS (
    SELECT 1 FROM public.users
    WHERE id = p_user_id AND role = 'admin'
  );
END;
$$;
```

---

## Data Protection

### Data Encryption

| Data Type | Protection |
|-----------|------------|
| Passwords | Bcrypt hashing |
| Tokens | Encrypted at rest |
| PII | Database encryption |
| Transit | TLS 1.3 |

### Secure Data Access

- All API calls over HTTPS
- Database connections encrypted
- Edge functions use secure environment
- No sensitive data in logs

### Data Isolation

- User data segregated by user ID
- RLS enforces isolation
- No cross-tenant data access
- Admin actions logged

---

## Video Security

### MUX Signed URLs

Videos are protected with signed JWT tokens:

```typescript
// Token generation with expiration
const token = mux.JWT.signPlaybackId(playbackId, {
  type: 'video',
  expiration: '2h' // 2-hour expiration
});
```

### Access Control

1. User requests video
2. Edge function verifies enrollment
3. If authorized, generate signed token
4. Token expires after 2 hours
5. Prevents unauthorized sharing

### Protection Measures

- No direct video URLs exposed
- Tokens are user-specific
- Expiration prevents long-term access
- Enrollment verified on each request

---

## API Security

### Supabase Edge Functions

- Run in isolated Deno environment
- No direct database access to users
- Environment variables for secrets
- Request validation

### SECURITY DEFINER Functions

For admin operations:

```sql
CREATE FUNCTION admin_function()
RETURNS void
LANGUAGE plpgsql
SECURITY DEFINER
SET search_path = public, pg_temp
AS $$
BEGIN
  -- Function only runs with elevated privileges
  -- if caller passes is_admin() check
END;
$$;
```

### Input Validation

- Zod schemas for frontend validation
- Database constraints for backend
- Edge function parameter validation
- SQL injection prevention via ORM

---

## Infrastructure Security

### Hosting Security

| Provider | Security Features |
|----------|-------------------|
| Vercel | DDoS protection, SSL |
| Supabase | SOC 2 compliant, encryption |
| MUX | CDN security, signed URLs |

### Environment Variables

- Never committed to repository
- Stored in platform secrets
- Different values per environment
- Regular rotation policy

### Network Security

- HTTPS only
- HSTS enabled
- Secure headers configured
- CORS properly configured

---

## Compliance

### Data Privacy

- GDPR awareness
- Data minimization
- User data access rights
- Deletion capabilities

### Best Practices

| Practice | Implementation |
|----------|----------------|
| Least Privilege | RLS policies |
| Defense in Depth | Multiple security layers |
| Audit Trail | Action logging |
| Regular Updates | Dependency updates |

---

## Security Headers

### Configured Headers

| Header | Value |
|--------|-------|
| X-Content-Type-Options | nosniff |
| X-Frame-Options | DENY |
| X-XSS-Protection | 1; mode=block |
| Referrer-Policy | strict-origin-when-cross-origin |
| Content-Security-Policy | Configured per needs |

---

## Threat Mitigation

### XSS Prevention

- React's built-in escaping
- No dangerouslySetInnerHTML
- Content Security Policy
- Input sanitization

### CSRF Prevention

- OAuth state parameter
- SameSite cookies
- Origin validation

### SQL Injection Prevention

- Supabase client parameterized queries
- No raw SQL from user input
- ORM protection

### Rate Limiting

- Supabase built-in limits
- Edge function timeout
- API rate limits

---

## Incident Response

### Monitoring

- Error logging
- Unusual activity detection
- Authentication failures

### Response Plan

1. Detect: Monitor for anomalies
2. Assess: Evaluate severity
3. Contain: Limit damage
4. Eradicate: Remove threat
5. Recover: Restore service
6. Review: Post-incident analysis

---

## Security Checklist

### Development

- [ ] Environment variables secured
- [ ] No secrets in code
- [ ] Dependencies updated
- [ ] Input validation implemented
- [ ] RLS policies tested

### Deployment

- [ ] HTTPS configured
- [ ] Security headers set
- [ ] Error pages don't leak info
- [ ] Logs don't contain PII
- [ ] Admin access limited

### Ongoing

- [ ] Regular security reviews
- [ ] Dependency updates
- [ ] Access audit
- [ ] Backup verification

---

## Reporting Security Issues

If you discover a security vulnerability:

1. Do not disclose publicly
2. Email security@alltimehigh.academy
3. Include detailed description
4. We'll respond within 48 hours
5. Coordinated disclosure after fix

---

## Next Steps

- Review [API Reference](api-reference.md)
- Understand [Architecture](architecture.md)
- See [Integrations](integrations.md)
