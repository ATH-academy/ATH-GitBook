# Analytics & Reporting

Monitor platform performance and user engagement.

---

## Overview

Analytics help you understand how users interact with the platform, identify areas for improvement, and measure educational effectiveness.

---

## Dashboard Analytics

### Key Metrics

| Metric | Description |
|--------|-------------|
| Active Users | Users active in last 30 days |
| Total Enrollments | All course enrollments |
| Completion Rate | % of enrollments completed |
| Avg Quiz Score | Platform-wide average |
| Total Watch Time | Aggregate video viewing |

---

## User Analytics

### Engagement Metrics

| Metric | Description |
|--------|-------------|
| DAU | Daily Active Users |
| WAU | Weekly Active Users |
| MAU | Monthly Active Users |
| Session Duration | Average time per visit |
| Return Rate | Users returning within 7 days |

### User Segments

| Segment | Criteria |
|---------|----------|
| New | Registered < 7 days |
| Active | Activity in last 7 days |
| At Risk | No activity 14-30 days |
| Churned | No activity 30+ days |

---

## Course Analytics

### Per-Course Metrics

| Metric | Description |
|--------|-------------|
| Enrollments | Total enrolled users |
| Active Learners | Currently in progress |
| Completions | Finished the course |
| Completion Rate | Completions / Enrollments |
| Avg Time to Complete | Days from start to finish |
| Rating | User satisfaction |

### Module-Level Data

| Metric | Description |
|--------|-------------|
| Views | Times module accessed |
| Completions | Times marked complete |
| Completion Rate | % who finish module |
| Avg Time Spent | Time in module |
| Drop-off Rate | % who abandon here |

---

## Quiz Analytics

### Overall Quiz Performance

| Metric | Description |
|--------|-------------|
| Total Attempts | All quiz submissions |
| Pass Rate | % of attempts that pass |
| Avg Score | Mean score across attempts |
| Retry Rate | % who retry after failure |
| First-Attempt Pass | % passing on first try |

### Per-Question Analysis

| Metric | Description |
|--------|-------------|
| Correct Rate | % answering correctly |
| Difficulty Index | Based on correct rate |
| Discrimination Index | Quality indicator |
| Common Wrong Answers | Most chosen incorrect options |

### Identifying Problem Questions

| Correct Rate | Interpretation | Action |
|--------------|----------------|--------|
| 90%+ | Too easy | Consider harder questions |
| 70-90% | Appropriate | Good difficulty |
| 50-70% | Challenging | Review content alignment |
| <50% | Too hard | Review question/content |

---

## Progress Analytics

### Learning Progress Viewer

Access: Admin > Learning Progress

**Displays:**
- Student list with metrics
- Per-student course progress
- Quiz scores
- Time spent
- Last activity

### Aggregated Progress

| Metric | Calculation |
|--------|-------------|
| Avg Modules/User | Total modules completed / Users |
| Avg Courses/User | Courses enrolled / Users |
| Platform Completion | Completed enrollments / Total |

---

## Revenue Analytics

### Subscription Metrics

| Metric | Description |
|--------|-------------|
| Active Subscriptions | Current paid subscribers |
| MRR | Monthly Recurring Revenue |
| ARR | Annual Recurring Revenue |
| Churn Rate | % canceling per month |
| LTV | Lifetime Value per user |

### Tier Distribution

| Tier | Count | % |
|------|-------|---|
| Free | - | - |
| Community | - | - |
| VIP | - | - |
| Concierge | - | - |

> Note: Actual data from Whop/Stripe dashboards

---

## Certification Analytics

### Certification Metrics

| Metric | Description |
|--------|-------------|
| Candidates | Users working toward cert |
| Issued | Certifications granted |
| Issue Rate | Issued / Candidates |
| Avg Time to Cert | Days from start to certification |

### Per-Certification Data

| Certification | Candidates | Issued | Rate |
|---------------|------------|--------|------|
| ATH-CCP | - | - | - |
| ATH-CDS | - | - | - |
| ATH-CMA | - | - | - |

---

## Using Analytics

### Improving Course Content

1. **Low completion rate module?**
   - Content may be too long
   - Material may be confusing
   - Consider breaking up

2. **High drop-off point?**
   - Review content quality
   - Check for technical issues
   - Consider engagement hooks

3. **Low quiz scores?**
   - Content may not prepare well
   - Questions may be unclear
   - Consider review material

### Improving Engagement

1. **Low return rate?**
   - Add email reminders
   - Improve content hooks
   - Consider gamification

2. **Short session times?**
   - Content may not engage
   - Navigation may be confusing
   - Mobile experience check

---

## Reports

### Standard Reports

| Report | Contents | Frequency |
|--------|----------|-----------|
| Weekly Summary | KPIs, enrollments, completions | Weekly |
| Course Performance | Per-course metrics | Monthly |
| User Engagement | DAU/MAU, retention | Weekly |
| Quiz Analysis | Scores, pass rates | Monthly |

### Custom Reports

For specific needs:
1. Define metrics needed
2. Set date range
3. Filter by segment
4. Export data
5. Analyze externally if needed

---

## Data Sources

### Platform Data
- User activity (Supabase)
- Course progress (Supabase)
- Quiz attempts (Supabase)

### External Data
- Payments (Stripe/Whop)
- Video analytics (MUX)
- Email engagement (Resend)

---

## Analytics Best Practices

### Regular Review

| Frequency | Review |
|-----------|--------|
| Daily | Active users, new signups |
| Weekly | Engagement trends, completions |
| Monthly | Course performance, revenue |
| Quarterly | Strategic metrics, trends |

### Taking Action

1. **Identify patterns** in data
2. **Hypothesize** cause
3. **Implement** change
4. **Measure** impact
5. **Iterate** based on results

### Avoiding Pitfalls

- Don't react to daily noise
- Look for trends, not spikes
- Consider context
- Validate with qualitative feedback

---

## Future Analytics

### Coming Soon

- Real-time dashboard
- Cohort analysis
- Predictive churn
- A/B testing framework
- Custom segments

### Integration Plans

- Advanced video analytics
- Support ticket correlation
- Marketing attribution

---

## Next Steps

- Configure [Certification Review](certification-review.md)
- Review [Content Management](content-management.md)
- Set up [Quiz Management](quiz-management.md)
