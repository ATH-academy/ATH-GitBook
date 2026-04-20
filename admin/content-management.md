# Content Management

Manage courses, modules, and learning content.

{% hint style="warning" %}
**Sync with the real admin UI:** The live app’s admin area is organized into tabs such as **Learning progress**, **Quiz manager**, **Webinars**, **Attendance**, etc. See [Dashboard Overview](dashboard-overview.md) for the up-to-date list. This page describes **content concepts**; some editorial workflows may happen in the database or tools outside the SPA.
{% endhint %}

---

## Overview

The admin dashboard allows you to create, edit, and publish educational content for All Time High Academy. Operational staff should cross-check with [Dashboard Overview](dashboard-overview.md) for day-to-day screens.

---

## Accessing Content Management

### Requirements
- Admin role in the system
- Access to admin dashboard

### Navigation
1. Log in with admin account
2. Go to Dashboard
3. Click "Admin" in navigation
4. Select content section

---

## Course Management

### Course Structure

```
Course
├── Metadata (title, description, etc.)
├── Settings (access level, pricing)
├── Modules
│   ├── Module 1
│   │   ├── Lessons
│   │   └── Quiz
│   ├── Module 2
│   └── ...
└── Resources
```

### Creating a Course

1. Navigate to Admin > Courses
2. Click "Create Course"
3. Fill in required fields:
   - **Title**: Course name
   - **Slug**: URL-friendly identifier
   - **Description**: Course overview
   - **Category**: Select category
   - **Level**: Beginner/Intermediate/Advanced
   - **Access Level**: Free/Premium/VIP/Whale
4. Add optional fields:
   - Instructor assignment
   - Featured image
   - Intro video (MUX ID or YouTube)
   - Price (if applicable)
5. Save as draft or publish

### Course Fields Reference

| Field | Required | Description |
|-------|----------|-------------|
| Title | Yes | Display name |
| Slug | Yes | URL path (auto-generated) |
| Description | Yes | Course overview |
| Category | Yes | Classification |
| Level | Yes | Difficulty level |
| Access Level | Yes | Who can access |
| Instructor | No | Assigned instructor |
| Featured | No | Highlight on homepage |
| Price | No | Cost (if separate) |
| Status | Yes | Draft/Published/Archived |

### Editing a Course

1. Find course in course list
2. Click "Edit"
3. Modify fields as needed
4. Save changes
5. Changes reflect immediately for published courses

### Publishing a Course

1. Ensure all content is complete
2. Verify module structure
3. Check quizzes are configured
4. Set status to "Published"
5. Confirm publication

---

## Module Management

### Module Types

| Type | Purpose |
|------|---------|
| Video | Video lesson content |
| Text | Written content |
| Quiz | Knowledge assessment |
| Assignment | Student submissions |
| Live | Scheduled sessions |
| Download | Downloadable resources |

### Creating a Module

1. Navigate to course modules section
2. Click "Add Module"
3. Select module type
4. Fill in required fields:
   - **Title**: Module name
   - **Description**: Module overview
   - **Type**: Video/Text/Quiz/etc.
   - **Position**: Order in course
5. Add type-specific content:
   - **Video**: MUX Asset ID or YouTube URL
   - **Text**: Written content
   - **Quiz**: Configure quiz settings
6. Set access level if different from course
7. Save and publish

### Module Hierarchy

Modules can be nested:
- Parent modules (containers)
- Child modules (actual content)

```
Parent Module: "Bitcoin Fundamentals"
├── Child: "What is Bitcoin" (video)
├── Child: "How Bitcoin Works" (video)
├── Child: "Bitcoin Quiz" (quiz)
```

### Module Ordering

1. Drag and drop in module list
2. Or set position number manually
3. Save order changes
4. Verify sequential unlocking works

---

## Video Content

### MUX Integration

For video lessons:
1. Upload video to MUX
2. Obtain Asset ID and Playback ID
3. Enter MUX Asset ID in module
4. System generates signed playback URL
5. Video streams securely to students

### YouTube Alternative

For YouTube videos:
1. Upload video to YouTube
2. Get video ID from URL
3. Enter YouTube ID in module
4. Video embeds in lesson

### Video Best Practices
- Keep videos 5-15 minutes
- Clear audio is essential
- Include visual demonstrations
- Add chapter markers in MUX
- Consider transcript for accessibility

---

## Resource Management

### Adding Resources to Modules

1. Navigate to module
2. Click "Add Resource"
3. Upload file or enter URL
4. Set resource details:
   - Title
   - Description
   - Resource type
   - Access level
5. Save resource

### Resource Types

| Type | File Extensions |
|------|----------------|
| PDF | .pdf |
| Document | .doc, .docx |
| Spreadsheet | .xls, .xlsx |
| Presentation | .ppt, .pptx |
| Image | .jpg, .png, .gif |
| Archive | .zip |

### Resource Settings

- **Download limit**: Max downloads per user
- **Access level**: Required membership
- **Visibility**: Public or restricted

---

## Content Publishing

### Draft vs Published

| Status | Visible to Students | Editable |
|--------|---------------------|----------|
| Draft | No | Yes |
| Published | Yes | Yes (careful) |
| Archived | No | Yes |

### Publishing Workflow

1. Create content as draft
2. Review and test internally
3. Verify all quizzes configured
4. Check sequential flow
5. Publish course/modules
6. Monitor student feedback

### Updating Published Content

**Best Practices:**
- Minor fixes: Edit directly
- Major changes: Consider versioning
- Quiz changes: Careful with active attempts
- Always test after changes

---

## Access Level Control

### Course Access Levels

| Level | Who Can Access |
|-------|---------------|
| Free | All users |
| Premium | Community+ subscribers |
| VIP | VIP+ members |
| Whale | Concierge clients |

### Module Override

Individual modules can have different access:
- Useful for preview content
- Lock advanced content
- Promotional freemium model

---

## Content Localization

### Bilingual Support

Content supports English and Spanish:
1. Create content in primary language
2. Add translations in translation fields
3. System shows appropriate language

### Translation Fields

- Title (title_translations)
- Description (description_translations)
- Content (content_translations)

---

## Instructor Assignment

### Adding Instructors

1. Go to Admin > Instructors
2. Create instructor profile:
   - Name and bio
   - Profile photo
   - Credentials
   - Social links
3. Assign to courses

### Instructor Profile Fields

| Field | Description |
|-------|-------------|
| Name | Display name |
| Bio | Background and expertise |
| Photo | Profile image |
| Credentials | Certifications, experience |
| Social | Twitter, LinkedIn, etc. |

---

## Content Analytics

### Available Metrics

| Metric | What It Shows |
|--------|---------------|
| Enrollments | Students enrolled |
| Completion Rate | % who finish |
| Module Views | Views per module |
| Quiz Scores | Performance data |
| Time Spent | Engagement duration |

### Using Analytics

- Identify popular content
- Find struggling points
- Improve low-performing modules
- Optimize learning paths

---

## Best Practices

### Content Creation
1. Plan curriculum before building
2. Keep lessons focused and concise
3. Include practical examples
4. Test all quizzes before publishing
5. Get peer review

### Maintenance
1. Regularly update outdated content
2. Monitor student feedback
3. Fix broken links/videos promptly
4. Archive obsolete courses
5. Keep resources current

### Quality Assurance
1. Test entire course flow
2. Verify all videos play
3. Check quiz scoring
4. Test on multiple devices
5. Review as a student would

---

## Troubleshooting

### Common Issues

**Video not playing:**
- Check MUX Asset ID
- Verify playback ID exists
- Check MUX account status

**Quiz not saving:**
- Verify all required fields
- Check question/answer count
- Save quiz settings first

**Module not unlocking:**
- Check previous module completion
- Verify quiz passed
- Review module dependencies

---

## Next Steps

- Configure [Quiz Management](quiz-management.md)
- Set up [User Management](user-management.md)
- Review [Analytics](analytics.md)
