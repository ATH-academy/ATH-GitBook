# API Reference

API endpoints and database functions for All Time High Academy.

---

## Overview

All Time High Academy uses Supabase as its backend, providing:
- Direct database access via Supabase client
- Edge Functions for complex operations
- RPC functions for admin operations

---

## Authentication

### Supabase Auth

```typescript
// Sign up
const { data, error } = await supabase.auth.signUp({
  email: 'user@example.com',
  password: 'password'
});

// Sign in
const { data, error } = await supabase.auth.signInWithPassword({
  email: 'user@example.com',
  password: 'password'
});

// Sign out
await supabase.auth.signOut();

// Get current user
const { data: { user } } = await supabase.auth.getUser();

// Get session
const { data: { session } } = await supabase.auth.getSession();
```

### OAuth

```typescript
// Discord
await supabase.auth.signInWithOAuth({
  provider: 'discord',
  options: {
    redirectTo: `${window.location.origin}/auth/discord/callback`
  }
});
```

---

## Database Tables

### users

```typescript
interface User {
  id: string;          // UUID, FK to auth.users
  email: string;
  username: string | null;
  full_name: string | null;
  avatar_url: string | null;
  bio: string | null;
  role: 'student' | 'instructor' | 'admin';
  is_active: boolean;
  discord_user_id: string | null;
  created_at: string;
  updated_at: string;
}
```

### courses

```typescript
interface Course {
  id: string;
  title: string;
  slug: string;
  description: string | null;
  category_id: string | null;
  instructor_id: string | null;
  level: 'beginner' | 'intermediate' | 'advanced';
  access_level: 'free' | 'premium' | 'vip' | 'whale';
  price: number | null;
  currency: string;
  is_published: boolean;
  status: 'draft' | 'published' | 'archived';
  featured: boolean;
  rating: number | null;
  enrollment_count: number;
  mux_intro_video_id: string | null;
  youtube_intro_video_id: string | null;
  created_at: string;
  updated_at: string;
}
```

### modules

```typescript
interface Module {
  id: string;
  course_id: string;
  parent_id: string | null;
  title: string;
  slug: string;
  description: string | null;
  content: string | null;
  type: 'standard' | 'video' | 'quiz' | 'assignment' | 'text' | 'live' | 'download';
  position: number;
  level: number;
  path: string | null;
  access_level: 'free' | 'premium' | 'vip' | 'whale';
  is_published: boolean;
  is_locked: boolean;
  mux_asset_id: string | null;
  mux_playback_id: string | null;
  youtube_video_id: string | null;
  video_url: string | null;
  duration_seconds: number | null;
  created_at: string;
  updated_at: string;
}
```

### enrollments

```typescript
interface Enrollment {
  id: string;
  user_id: string;
  course_id: string;
  enrolled_at: string;
  status: 'active' | 'completed' | 'paused' | 'cancelled';
  progress_percentage: number;
  completed_modules: number;
  total_modules: number;
  last_accessed_at: string | null;
  completed_at: string | null;
  access_level: 'free' | 'premium' | 'vip' | 'whale';
}
```

### module_progress

```typescript
interface ModuleProgress {
  id: string;
  user_id: string;
  module_id: string;
  enrollment_id: string | null;
  status: 'not_started' | 'in_progress' | 'completed' | 'skipped' | 'locked';
  is_completed: boolean;
  progress_percentage: number;
  started_at: string | null;
  completed_at: string | null;
  time_spent: number;
  quiz_attempts: number;
  best_quiz_score: number | null;
  last_quiz_score: number | null;
  quiz_passed: boolean;
}
```

---

## Query Examples

### Get Courses

```typescript
// All published courses
const { data: courses } = await supabase
  .from('courses')
  .select('*')
  .eq('is_published', true)
  .eq('status', 'published')
  .order('created_at', { ascending: false });

// Course with modules
const { data: course } = await supabase
  .from('courses')
  .select(`
    *,
    modules (
      id, title, type, position,
      is_published, access_level
    )
  `)
  .eq('slug', courseSlug)
  .single();
```

### Get User Enrollments

```typescript
const { data: enrollments } = await supabase
  .from('enrollments')
  .select(`
    *,
    courses (id, title, slug)
  `)
  .eq('user_id', userId);
```

### Get Module Progress

```typescript
const { data: progress } = await supabase
  .from('module_progress')
  .select('*')
  .eq('enrollment_id', enrollmentId);
```

---

## Edge Functions

### get-videos

**Purpose:** Generate signed MUX playback tokens

**Endpoint:** `/functions/v1/get-videos`

**Request:**
```typescript
{
  course_id?: string;
}
```

**Response:**
```typescript
{
  videos: Array<{
    module_id: string;
    playbackId: string;
    token: string;
    module_type: string;
  }>;
  live: Array<...>;
  other: Array<...>;
}
```

### quiz

**Purpose:** Fetch quiz and submit answers

**Endpoint:** `/functions/v1/quiz`

**GET (Fetch Quiz):**
```typescript
// Request
{ quiz_id: string; language?: 'en' | 'es' }

// Response
{
  quiz: {
    id: string;
    title: string;
    passing_score: number;
    questions: Array<{
      id: string;
      prompt: string;
      options: Array<{
        id: string;
        label: string;
        text: string;
      }>;
    }>;
  };
}
```

**POST (Submit Answers):**
```typescript
// Request
{
  quiz_id: string;
  answers: Array<{
    question_id: string;
    option_id: string;
  }>;
}

// Response
{
  score: number;
  passed: boolean;
  correct_count: number;
  total_questions: number;
  results: Array<{
    question_id: string;
    selected_option_id: string;
    correct_option_id: string;
    is_correct: boolean;
  }>;
}
```

### progress

**Purpose:** Track module progress

**Endpoint:** `/functions/v1/progress`

**GET:**
```typescript
// Request
{ course_id: string }

// Response
{
  progress: Array<{
    module_id: string;
    is_completed: boolean;
    status: string;
    progress_percentage: number;
    is_locked: boolean;
    locked_reason: string | null;
  }>;
}
```

**POST (Toggle Completion):**
```typescript
// Request
{
  module_id: string;
  is_completed: boolean;
}

// Response
{
  success: boolean;
  progress: {...};
}
```

---

## Admin RPC Functions

### Quiz Management

```typescript
// Get global settings
const { data } = await supabase.rpc('admin_get_quiz_global_settings');

// Update global settings
await supabase.rpc('admin_update_quiz_global_settings', {
  p_settings: { passing_score: 70, max_attempts: 3 }
});

// Get quiz with questions
const { data } = await supabase.rpc('admin_get_quiz_detail', {
  p_quiz_id: quizId
});

// Upsert question
await supabase.rpc('admin_upsert_quiz_question', {
  p_quiz_id: quizId,
  p_question: { prompt: '...', position: 1 }
});

// Upsert option
await supabase.rpc('admin_upsert_quiz_option', {
  p_question_id: questionId,
  p_option: { label: 'A', text: '...', is_correct: true }
});
```

### User Management

```typescript
// List students
const { data } = await supabase.rpc('admin_list_students');

// Get quiz progress
const { data } = await supabase.rpc('admin_get_quiz_progress');
```

### Role Management

```typescript
// Check if admin
const { data: isAdmin } = await supabase.rpc('is_admin');

// Set user role
await supabase.rpc('set_user_role', {
  p_user_id: userId,
  p_role: 'admin'
});
```

---

## Realtime Subscriptions

```typescript
// Subscribe to progress changes
const channel = supabase
  .channel('progress-changes')
  .on(
    'postgres_changes',
    {
      event: 'UPDATE',
      schema: 'public',
      table: 'module_progress',
      filter: `user_id=eq.${userId}`
    },
    (payload) => {
      console.log('Progress updated:', payload.new);
    }
  )
  .subscribe();

// Cleanup
await channel.unsubscribe();
```

---

## Error Handling

### Standard Error Format

```typescript
interface SupabaseError {
  message: string;
  code: string;
  details: string | null;
  hint: string | null;
}
```

### Common Error Codes

| Code | Meaning |
|------|---------|
| PGRST116 | No rows returned |
| 23505 | Unique constraint violation |
| 23503 | Foreign key violation |
| 42501 | Insufficient privileges (RLS) |
| 42883 | Function not found |

### Error Handling Pattern

```typescript
const { data, error } = await supabase
  .from('courses')
  .select('*');

if (error) {
  console.error('Error:', error.message);
  // Handle specific error codes
  if (error.code === 'PGRST116') {
    // No results found
  }
  return;
}

// Use data
```

---

## Rate Limits

### Supabase Limits

| Resource | Limit |
|----------|-------|
| Requests/sec | Varies by plan |
| Edge Function timeout | 30 seconds |
| Payload size | 6MB |

### Best Practices

- Cache frequently accessed data
- Use pagination for lists
- Batch operations when possible
- Implement retry logic

---

## Next Steps

- Review [Security](security.md) practices
- Understand [Architecture](architecture.md)
- See [Integrations](integrations.md)
