# Quiz Management

Configure and manage quizzes and assessments.

---

## Overview

The Quiz Manager allows admins to create, configure, and monitor quizzes throughout the platform.

---

## Accessing Quiz Manager

1. Log in with admin account
2. Navigate to Admin Dashboard
3. Click "Quiz Manager" tab

---

## Global Quiz Settings

### Configuring Defaults

Set platform-wide defaults for all quizzes:

| Setting | Description | Default |
|---------|-------------|---------|
| Default Passing Score | Minimum % to pass | 70% |
| Default Max Attempts | Retries allowed (0=unlimited) | 0 |
| Attempt Cooldown | Wait time between retries | None |

### Changing Global Settings

1. Go to Admin > Quiz Manager
2. Click "Global Settings"
3. Adjust values
4. Save changes
5. Applies to new quizzes

> **Note:** Existing quizzes keep their specific settings.

---

## Creating a Quiz

### Step 1: Select Module

1. In Quiz Manager, find the course
2. Select the module for the quiz
3. Click "Create Quiz" or "Edit Quiz"

### Step 2: Configure Quiz Settings

| Setting | Description |
|---------|-------------|
| Title | Quiz name |
| Description | Instructions for students |
| Passing Score | Minimum % to pass |
| Max Attempts | Number of retries (0=unlimited) |
| Time Limit | Seconds to complete (0=none) |
| Shuffle Questions | Randomize order |
| Shuffle Answers | Randomize answer options |
| Allow Retry | Enable retry attempts |
| Success Message | Message on passing |

### Step 3: Add Questions

1. Click "Add Question"
2. Enter question text (prompt)
3. Add explanation (optional)
4. Set position order
5. Save question

### Step 4: Add Answer Options

For each question:
1. Click "Add Option"
2. Enter option text
3. Mark if correct (one per question)
4. Set position order
5. Repeat for all options

### Step 5: Save and Publish

1. Review all questions and answers
2. Click "Save Quiz"
3. Test the quiz as a student
4. Publish when ready

---

## Question Types

### Multiple Choice (Standard)

- 4 answer options
- 1 correct answer
- Most common type

**Example:**
```
Q: What is Bitcoin's maximum supply?
A: 21 million (correct)
B: 100 million
C: 1 billion
D: Unlimited
```

### True/False (2 Options)

- 2 answer options
- True or False
- Quick knowledge checks

---

## Quiz Configurations

### Short Quiz (3 Questions)
- **Questions:** 3
- **Pass requirement:** 2/3 (67%)
- **Use case:** Quick lesson check

### Standard Quiz (10 Questions)
- **Questions:** 10
- **Pass requirement:** 8/10 (80%)
- **Use case:** Module assessment

### Certification Exam (25+ Questions)
- **Questions:** 25+
- **Pass requirement:** 80-85%
- **Use case:** Final certification

---

## Multi-Language Support

### Adding Translations

Each quiz element supports translations:
1. Edit question
2. Find translation fields
3. Enter Spanish translation
4. Save changes

### Translation Fields

| Field | Translation Available |
|-------|----------------------|
| Question prompt | Yes |
| Question explanation | Yes |
| Option text | Yes |
| Success message | Yes |

---

## Quiz Editor Interface

### Editor Panel Components

```
┌─────────────────────────────────────┐
│ Quiz Settings                        │
│ ├── Title, Description              │
│ ├── Passing Score, Time Limit       │
│ └── Shuffle, Retry Options          │
├─────────────────────────────────────┤
│ Questions                            │
│ ├── Question 1 [Edit] [Delete]      │
│ │   ├── Option A                    │
│ │   ├── Option B ✓ (correct)        │
│ │   ├── Option C                    │
│ │   └── Option D                    │
│ ├── Question 2 [Edit] [Delete]      │
│ └── [Add Question]                  │
├─────────────────────────────────────┤
│ [Save Quiz] [Preview] [Publish]     │
└─────────────────────────────────────┘
```

### Editing Questions

1. Find question in list
2. Click "Edit"
3. Modify prompt or explanation
4. Update options as needed
5. Save changes

### Reordering Questions

1. Drag questions to reorder
2. Or change position number
3. Save new order

### Deleting Questions

1. Click "Delete" on question
2. Confirm deletion
3. Options deleted automatically

---

## Quiz Best Practices

### Question Writing

1. **Be clear**: Avoid ambiguous wording
2. **One concept**: Test one idea per question
3. **Plausible distractors**: Wrong answers should seem reasonable
4. **Avoid "all of the above"**: Often gives away answer
5. **Consistent length**: Options similar in length

### Quiz Structure

1. **Difficulty progression**: Start easier, get harder
2. **Coverage**: Touch all key concepts
3. **Balance**: Mix question types
4. **Review**: Test yourself before publishing

### Common Mistakes to Avoid

- Using trick questions
- Making correct answer obviously longer
- Using absolute words (always, never)
- Testing trivial details
- Unclear instructions

---

## Monitoring Quiz Performance

### Quiz Progress Viewer

Access via Admin > Quiz Progress:
- See all student attempts
- View scores and pass rates
- Identify struggling questions
- Track completion rates

### Available Metrics

| Metric | Description |
|--------|-------------|
| Attempts | Total quiz attempts |
| Pass Rate | % of passing attempts |
| Avg Score | Average score achieved |
| Completion Time | Average time to complete |
| Question Difficulty | Pass rate per question |

### Using Data

- **Low pass rate question?** May need clarification
- **High skip rate?** Content may not prepare well
- **Fast completions?** May be too easy
- **Many retries?** Check content alignment

---

## Quiz Scoring

### How Scores Calculate

```
Score = (Correct Answers / Total Questions) × 100%
```

### Score Tracking

For each student:
- **Best Score**: Highest achieved
- **Last Score**: Most recent attempt
- **Attempt Count**: Total tries

### Pass/Fail Logic

```
If Score >= Passing Score:
    Status = Passed
    Module = Completed
    Next Module = Unlocked
Else:
    Status = Failed
    Module = Incomplete
    Next Module = Locked
```

---

## Troubleshooting

### Quiz Won't Save

1. Check all required fields filled
2. Verify at least one correct answer per question
3. Check for validation errors
4. Try refreshing and re-entering

### Students Can't Access Quiz

1. Verify module is published
2. Check previous module completed
3. Verify quiz is saved properly
4. Check access level settings

### Scores Not Recording

1. Check quiz submitted properly
2. Verify database connection
3. Review error logs
4. Test with another user

---

## RPC Functions Reference

### Admin Quiz Functions

| Function | Purpose |
|----------|---------|
| `admin_get_quiz_global_settings` | Get default settings |
| `admin_update_quiz_global_settings` | Update defaults |
| `admin_get_quiz_detail` | Get quiz with questions |
| `admin_upsert_quiz_question` | Create/update question |
| `admin_upsert_quiz_option` | Create/update option |
| `admin_delete_quiz_option` | Remove option |
| `admin_get_quiz_progress` | Get student attempts |

---

## Next Steps

- Set up [User Management](user-management.md)
- Review [Analytics & Reporting](analytics.md)
- Configure [Certification Review](certification-review.md)
