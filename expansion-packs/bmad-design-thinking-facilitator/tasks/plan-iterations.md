# Task: Plan Iterations

**Design Thinking Phase**: Test → Iterate
**Duration**: 1-2 hours
**Agent**: Test Analyst
**Difficulty**: Medium

## Purpose

Transform test insights into a clear iteration plan that prioritizes changes and defines next steps.

## Prerequisites

- [ ] Test results analyzed
- [ ] Issues prioritized
- [ ] Findings report completed
- [ ] Stakeholders briefed

## Iteration Decision Framework

### Decision 1: Iterate or Build?

**Iterate (test again)** if:
- ❌ Critical issues found (task blockers)
- ❌ Success rate <70%
- ❌ Significant redesign needed
- ❌ User feedback mostly negative

**Move to build** if:
- ✅ Users complete tasks successfully (>80%)
- ✅ Positive overall sentiment
- ✅ Issues are minor/polish-level
- ✅ Clear value validated

### Decision 2: Scope of Iteration

**Quick iteration** (1-3 days):
- Fix critical blockers only
- Test with 3-5 more users
- Validate specific changes

**Major iteration** (1-2 weeks):
- Significant redesign
- New features/approach
- Full test round (8+ users)

**Hybrid approach**:
- Fix quick wins immediately
- Plan major changes for next version
- Test incrementally

## Iteration Planning Process

### Phase 0: Document Learnings (15-20 min)

**Before planning the next iteration, formally document the key takeaways from the previous cycle.**

- Use the `iteration-learnings-template.yaml` to create a summary document.
- Capture the most critical validated/invalidated hypotheses.
- List the key successes, failures, and surprises.
- This document provides the evidence and rationale for the iteration plan.

### Phase 1: Categorize Changes (20-30 min)

**Must Fix (P0)** - Before next test:
- Task blockers
- Critical usability issues
- High-frequency problems

**Should Fix (P1)** - In next iteration:
- Significant improvements
- Medium-priority issues
- Feature enhancements

**Could Fix (P2)** - Future releases:
- Polish and refinement
- Nice-to-haves
- Low-impact issues

**Won't Fix (P3)** - Parking lot:
- Out of scope
- Edge cases
- Infeasible currently

### Phase 2: Define Iteration Scope (30 min)

**For each P0 issue, specify**:

**Issue**: [Description]
**Fix**: [Specific change to make]
**Owner**: [Who will do it]
**Timeline**: [When it'll be done]
**Success**: [How we'll know it worked]

**Example**:
```
ISSUE: Users can't find password reset

FIX: Add "Forgot password?" link directly on login screen (below password field)

OWNER: Design team

TIMELINE: 2 days

SUCCESS: 100% of users find password reset without help in next test
```

### Phase 3: Create Iteration Roadmap (20-30 min)

**Timeline approach**:

```
ITERATION 1 (This Week):
- Fix password reset visibility
- Add progress indicator to signup
- Clarify "Help" vs "Contact" labels
→ Test with 5 users next week

ITERATION 2 (Next 2 Weeks):
- Redesign onboarding flow
- Add contextual help system
- Improve error messaging
→ Test with 8 users

ITERATION 3 (Future):
- Advanced features
- Polish and refinement
- Performance optimization
```

### Phase 4: Define Success Metrics (10-15 min)

**For next test, expect**:

**Baseline** (current state):
- Task completion: 62%
- Avg time: 8 min
- Ease rating: 4.2/10

**Target** (after iteration):
- Task completion: >85%
- Avg time: <4 min
- Ease rating: >7/10

**Minimum acceptable**:
- Task completion: >75%
- Avg time: <6 min
- Ease rating: >6/10

### Phase 5: Plan Next Test (10 min)

**Define**:
- What to test: [Specific changes]
- When: [Date]
- With whom: [Same or new participants?]
- Sample size: [5-8 users]
- Focus areas: [What to watch closely]

**Example**:
```
NEXT TEST PLAN:

Focus: Validate fixes to signup flow

Changes to Test:
1. New password reset link
2. Progress indicator
3. Updated help text

Participants: 5 new users (same criteria)

Schedule: Week of [Date]

Key Questions:
- Can users complete signup without errors?
- Is time-to-completion reduced?
- Do users feel more confident?
```

## Iteration Plan Document

```
┌─────────────────────────────────────┐
│      ITERATION PLAN v[X]            │
├─────────────────────────────────────┤
│ Based on: [Test round with 8 users]│
│ Date: [Date]                        │
├─────────────────────────────────────┤
│ KEY ISSUES FOUND:                   │
│ • [Issue 1] - 7/8 users             │
│ • [Issue 2] - 6/8 users             │
│ • [Issue 3] - 5/8 users             │
├─────────────────────────────────────┤
│ ITERATION SCOPE:                    │
│                                     │
│ Must Fix (Complete by [Date]):     │
│ ☐ [Change 1] - Owner: [Name]       │
│ ☐ [Change 2] - Owner: [Name]       │
│                                     │
│ Should Fix (Next iteration):        │
│ ☐ [Change 3]                        │
│ ☐ [Change 4]                        │
├─────────────────────────────────────┤
│ NEXT TEST:                          │
│ Date: [Date]                        │
│ Participants: 5 users               │
│ Focus: Validate signup fixes        │
│                                     │
│ Success Criteria:                   │
│ - Completion rate >85%              │
│ - Time <4 min                       │
│ - Ease rating >7/10                 │
└─────────────────────────────────────┘
```

## Expected Outputs

1. **Iteration Plan**: Prioritized changes with owners
2. **Timeline**: When changes will be made
3. **Success Metrics**: Targets for next test
4. **Next Test Plan**: When and how to validate
5. **Stakeholder Update**: Summary for leadership

## Common Challenges & Solutions

### Challenge: "Too many issues to fix"

**Solutions**:
- Start with P0 blockers only
- Phased approach (multiple iterations)
- Focus on highest-impact changes
- Accept some issues for later

### Challenge: "Team wants to build, not iterate"

**Solutions**:
- Show cost of fixing issues post-launch
- Demonstrate user pain with video clips
- Calculate abandonment/support impact
- Compromise: Fix critical, move forward

### Challenge: "Disagreement on priorities"

**Solutions**:
- Use objective criteria (frequency x severity)
- Return to user data
- Decision-maker breaks tie
- Test assumptions if uncertain

## Success Indicators

✅ **Clear plan**: Know exactly what to change
✅ **Assigned**: Owners for each change
✅ **Timeline**: Realistic schedule
✅ **Measurable**: Success criteria defined
✅ **Validated**: Plan to test changes

## Related Resources

- **Previous Task**: `analyze-test-results.md`
- **Next Phase**: Return to `build-rapid-prototype.md` for iteration, or move to development
- **Parent Task**: `run-user-testing.md`

## Tips

**Iterate quickly**:
- Fix critical issues first
- Test incrementally (don't wait for perfect)
- Small changes can have big impact
- Learn fast through iteration

**Communicate clearly**:
- Share results with stakeholders
- Celebrate wins (what worked!)
- Be honest about failures
- Show user impact of changes
EOFTESTITERATE
echo "All Test tasks created successfully!"
