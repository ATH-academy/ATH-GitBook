# User Management

Manage users, roles, and access on the platform.

---

## Overview

User management allows admins to view, manage, and support platform users.

---

## User Roles

### Current Roles

| Role | Access Level | Description |
|------|-------------|-------------|
| Student | Standard | Default role for learners |
| Instructor | Standard | Can view content (dashboard planned) |
| Admin | Full | Complete platform access |

### Role Capabilities

| Capability | Student | Instructor | Admin |
|------------|---------|------------|-------|
| View courses | Yes | Yes | Yes |
| Complete quizzes | Yes | Yes | Yes |
| Track progress | Yes | Yes | Yes |
| View admin panel | No | No | Yes |
| Manage content | No | No | Yes |
| Manage users | No | No | Yes |
| View analytics | No | No | Yes |

---

## Viewing Users

### User List

Access via Admin > Users:
- View all registered users
- See role and status
- Filter and search

### User Information

| Field | Description |
|-------|-------------|
| Email | User email address |
| Name | Display name |
| Role | Student/Instructor/Admin |
| Status | Active/Inactive |
| Created | Registration date |
| Last Active | Last login |
| Discord | Connected Discord ID |

---

## Student Progress View

### Learning Progress Viewer

Access via Admin > Learning Progress:

| Metric | Description |
|--------|-------------|
| Courses Enrolled | Number of courses started |
| Courses Completed | Number finished |
| Completion Rate | % of enrolled courses completed |
| Modules Completed | Total modules finished |
| Avg Quiz Score | Average across all quizzes |
| Total Time | Time spent on platform |
| Last Access | Most recent activity |
| Discord Connected | Yes/No |

### Viewing Individual Progress

1. Find user in list
2. Click to expand details
3. See per-course breakdown
4. Review quiz scores
5. Check certification status

---

## Managing User Roles

### Changing User Role

1. Find user in admin list
2. Click "Edit Role"
3. Select new role
4. Confirm change
5. User gains/loses access immediately

### Role Assignment Guidelines

| Assign Role | When |
|-------------|------|
| Student | Default for all users |
| Instructor | Content creators (future) |
| Admin | Team members with full access |

### Security Considerations

- Limit admin accounts
- Review admin list regularly
- Remove access when not needed
- Audit role changes

---

## User Search & Filter

### Search Options

- By email
- By name
- By Discord ID

### Filter Options

| Filter | Options |
|--------|---------|
| Role | Student, Instructor, Admin |
| Status | Active, Inactive |
| Plan | Free, Community, VIP, Concierge |
| Discord | Connected, Not Connected |

---

## Subscription Management

### Viewing Subscriptions

For each user:
- Current plan
- Billing status
- Expiration date
- Payment history

### Subscription Sources

| Source | Description |
|--------|-------------|
| Whop | Managed via Whop platform |
| Stripe | Direct credit card |
| Internal | Manual assignments |

### Manual Plan Assignment

For special cases:
1. Find user
2. Click "Manage Subscription"
3. Assign plan manually
4. Set expiration if needed
5. Save changes

> **Use for:** Comped access, special arrangements, testing

---

## User Support Actions

### Common Admin Actions

| Action | When to Use |
|--------|-------------|
| Reset Progress | User requests fresh start |
| Extend Access | Grace period needed |
| Unlock Module | Technical issue |
| Reset Password | User locked out |
| Merge Accounts | Duplicate accounts |

### Handling Support Requests

1. Verify user identity
2. Understand the issue
3. Take appropriate action
4. Document the change
5. Notify user

---

## Discord Integration

### Viewing Discord Status

For each user:
- Discord connected: Yes/No
- Discord User ID
- Connection date

### Discord Troubleshooting

If user can't connect:
1. Check if already connected
2. Verify OAuth permissions
3. Have user revoke and reconnect
4. Check Discord server status

---

## Enrollment Management

### Viewing Enrollments

For each user:
- Courses enrolled
- Enrollment date
- Progress %
- Status (Active/Completed/Dropped)

### Manual Enrollment

1. Find user
2. Click "Manage Enrollments"
3. Add course enrollment
4. Set access level
5. Save

### Removing Enrollment

1. Find enrollment
2. Click "Remove"
3. Confirm action
4. Progress preserved in database

---

## Data Export

### Available Exports

| Export | Contents |
|--------|----------|
| User List | All users with basic info |
| Progress Report | Learning metrics |
| Quiz Report | Quiz attempts and scores |
| Enrollment Report | Course enrollments |

### Export Format
- CSV format
- Downloadable from admin panel
- Filtered by date range

---

## Privacy & Compliance

### User Data Handling

- View only what's needed
- Don't share user data
- Follow data retention policies
- Respect privacy requests

### Data Deletion Requests

If user requests deletion:
1. Verify identity
2. Document request
3. Follow deletion procedure
4. Confirm completion

---

## Troubleshooting

### User Can't Log In

1. Check account exists
2. Verify email verified
3. Check if account locked
4. Reset password if needed
5. Check OAuth connections

### Access Issues

1. Verify subscription status
2. Check access level
3. Review module locks
4. Test with user credentials

### Progress Discrepancies

1. Check database records
2. Verify sync status
3. Compare with user report
4. Correct if needed

---

## Admin Best Practices

### Daily Tasks
- Review new signups
- Check support requests
- Monitor active sessions

### Weekly Tasks
- Review analytics
- Check subscription status
- Update user access as needed

### Monthly Tasks
- Audit admin accounts
- Review data exports
- Clean up test accounts

---

## Next Steps

- Review [Analytics & Reporting](analytics.md)
- Configure [Certification Review](certification-review.md)
- Understand [Content Management](content-management.md)
