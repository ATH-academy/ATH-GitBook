# Certification Review

Manage certification approvals and issue credentials.

---

## Overview

When students complete certification requirements, their applications are reviewed and approved by admins before credentials are issued.

---

## Accessing Certification Review

1. Log in with admin account
2. Go to Admin Dashboard
3. Click "Certification Review" tab

---

## Review Process

### Certification Workflow

```
Student Completes Requirements
         ↓
Appears in Review Queue
         ↓
Admin Reviews Application
         ↓
    ┌────┴────┐
    ↓         ↓
 Approve   Reject
    ↓         ↓
Certificate  Feedback
  Issued      Sent
```

### Review Queue

The queue shows candidates who:
- Completed all required courses
- Passed all required quizzes
- Met minimum score thresholds
- Have not yet been reviewed

---

## Certification Requirements

### ATH-CCP (Certified Crypto Professional)

| Requirement | Details |
|-------------|---------|
| Courses | Complete core curriculum |
| Quizzes | Pass all required assessments |
| Min Score | 80% average |
| Prerequisites | None |

### ATH-CDS (Certified DeFi Specialist)

| Requirement | Details |
|-------------|---------|
| Courses | Complete DeFi curriculum |
| Quizzes | Pass all DeFi assessments |
| Min Score | 80% average |
| Prerequisites | ATH-CCP recommended |

### ATH-CMA (Certified Market Analyst)

| Requirement | Details |
|-------------|---------|
| Courses | Complete advanced trading |
| Quizzes | Pass all TA assessments |
| Min Score | 85% average |
| Prerequisites | ATH-CCP required |

---

## Review Interface

### Candidate List View

| Column | Description |
|--------|-------------|
| Name | Student name |
| Email | Contact email |
| Certification | Which credential |
| Submitted | Date ready for review |
| Score | Overall average |
| Status | Pending/Approved/Rejected |

### Candidate Detail View

Clicking a candidate shows:
- Full course completion
- All quiz scores
- Time to completion
- Previous certifications
- Notes/comments

---

## Approving Certifications

### Standard Approval

1. Find candidate in queue
2. Click to review details
3. Verify requirements met
4. Click "Approve"
5. Add notes (optional)
6. Confirm approval

### What Happens on Approval

1. Status updated to "Approved"
2. Certificate generated (PDF)
3. User notified via email
4. Certificate available for download
5. Dashboard updated

---

## Rejecting Applications

### When to Reject

- Requirements not actually met
- Suspicious activity detected
- Policy violations
- Technical errors in progress

### Rejection Process

1. Find candidate
2. Click "Reject"
3. Enter rejection reason (required)
4. Add detailed notes
5. Confirm rejection

### Rejection Reasons

| Reason | Action |
|--------|--------|
| Incomplete requirements | User must complete remaining |
| Score below threshold | User can retry quizzes |
| Suspicious activity | Review with security |
| Technical error | Investigate and resolve |

### Post-Rejection

- User notified with reason
- Can address issues
- Resubmit when ready
- Will appear in queue again

---

## Bulk Operations

### Bulk Approval

For multiple approvals:
1. Select candidates (checkbox)
2. Click "Bulk Approve"
3. Add shared notes (optional)
4. Confirm action

### When to Use Bulk

- Multiple clear approvals
- Same certification
- Similar timeframe

### Caution

- Review each briefly before bulk
- Don't bulk approve blindly
- Better to approve individually if unsure

---

## Certification Certificates

### PDF Certificate Contents

- Student name
- Certification name and code
- Date of completion
- Unique certificate ID
- All Time High Academy seal
- Verification instructions

### Certificate Storage

- Stored in platform database
- Accessible via user dashboard
- Downloadable anytime
- Unique ID for verification

---

## Verification System

### Verifying a Certificate

1. Receive certificate ID
2. Go to verification page
3. Enter certificate ID
4. See validation result

### Verification Shows

- Valid/Invalid status
- Student name
- Certification type
- Issue date
- Issuing organization

---

## Review Guidelines

### What to Check

| Check | Why |
|-------|-----|
| Completion dates | Reasonable timeline |
| Quiz scores | Consistent performance |
| Attempt patterns | No suspicious activity |
| Previous certs | Proper progression |

### Red Flags

- Unusually fast completion
- Perfect scores on all quizzes
- Same answers on retries
- Multiple failures then sudden pass

### When Uncertain

1. Review in detail
2. Check user history
3. Consult with team
4. Request additional info if needed

---

## Tracking & History

### Review History

For each candidate:
- Previous submissions
- Review dates
- Reviewer names
- Decisions and notes

### Audit Trail

All actions logged:
- Who reviewed
- When reviewed
- Decision made
- Notes added

---

## Best Practices

### Regular Review

- Check queue daily
- Don't let candidates wait
- Aim for 48-hour turnaround

### Consistency

- Apply same standards
- Document decisions
- Communicate with team

### Quality

- Take time to review properly
- Don't rubber-stamp
- Maintain credential value

---

## Troubleshooting

### Candidate Not Appearing

1. Verify all requirements met
2. Check progress data
3. Verify quiz passes
4. Check for sync issues

### Certificate Not Generating

1. Check PDF generation service
2. Verify template exists
3. Check for errors
4. Generate manually if needed

### Wrong Info on Certificate

1. Do not issue
2. Correct user data
3. Regenerate certificate
4. Issue corrected version

---

## Future Enhancements

### Planned Features

- Automatic approval for clear cases
- LinkedIn credential integration
- NFT certificate issuance
- Expiration and renewal system

---

## Next Steps

- Review [Analytics](analytics.md) for certification metrics
- Understand [User Management](user-management.md)
- Configure [Quiz Management](quiz-management.md)
