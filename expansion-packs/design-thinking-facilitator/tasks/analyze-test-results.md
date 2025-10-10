# Task: Analyze Test Results

**Design Thinking Phase**: Test
**Duration**: 2-3 days
**Agent**: Test Analyst
**Difficulty**: Medium-High

## Purpose

Synthesize user testing data into actionable insights, prioritized issues, and clear recommendations for iteration.

## Prerequisites

- [ ] All test sessions completed (5-8+ users)
- [ ] Session notes compiled
- [ ] Recordings available
- [ ] Metrics collected

## Analysis Process

### Phase 1: Organize Data (30-60 min)

**Compile all**:
- Session notes
- Recordings
- Task completion data
- Satisfaction ratings
- Quotes

**Create repository**:
```
/test-results
  /sessions
    - participant-01-notes.md
    - participant-02-notes.md
  /recordings
  /metrics-summary.xlsx
  /synthesis
```

### Phase 2: Identify Patterns (2-4 hours)

#### Look for Issues Across Multiple Users

**Pattern threshold**: 3+ users = pattern (not outlier)

**Create issue list**:
```
ISSUE: Can't find password reset
Frequency: 7/8 users
Severity: HIGH (blocks task)
Evidence:
- "Where's the reset button?" [P1, P3, P5]
- All users looked in wrong place
- Avg 3 min spent searching
```

#### Pattern Types

**Usability Issues**:
- Navigation confusion
- Unclear labels
- Missing functionality
- Error states

**Behavioral Patterns**:
- Common workflows
- Workarounds created
- Assumptions made

**Emotional Patterns**:
- Frustration points
- Delight moments
- Confidence vs. uncertainty

### Phase 3: Severity Rating (1-2 hours)

**Rate each issue**:

**Critical (P0)**:
- Blocks task completion
- Affects most/all users
- No workaround
- Example: "Can't complete checkout"

**High (P1)**:
- Significant confusion/frustration
- Affects many users (50%+)
- Workaround exists but hard
- Example: "Takes 3 min to find feature"

**Medium (P2)**:
- Noticeable but not blocking
- Affects some users (20-50%)
- Easy workaround
- Example: "Button label unclear"

**Low (P3)**:
- Minor annoyance
- Few users affected (<20%)
- Cosmetic/polish
- Example: "Icon could be better"

### Phase 4: Quantify Results (1-2 hours)

**Calculate metrics**:

**Task Success Rate**:
- # successful completions / # attempts
- Example: 6/8 = 75% success rate

**Time on Task**:
- Average completion time
- Compare to expected time

**Error Rate**:
- # errors / # total actions
- Types of errors

**Satisfaction**:
- Average ease rating
- Net Promoter Score (would recommend?)

**Example Summary**:
```
TASK: Complete signup

Success Rate: 5/8 (62.5%)
  - 3 users failed at password step
  
Avg Time: 8 min (expected 3 min)
  - Range: 5-12 min
  
Errors: 23 total
  - Form validation: 12
  - Navigation: 8
  - Other: 3

Ease Rating: 4.2/10
  - "Confusing and frustrating"
```

### Phase 5: Synthesize Insights (2-3 hours)

**Transform observations into insights**:

**Observation**: "All 8 users clicked 'Help' looking for customer support"
**Insight**: "Users expect 'Help' to mean human support, not FAQ. They want to talk to someone when confused."

**Observation**: "Users skipped the tutorial 7/8 times"
**Insight**: "Users want immediate value, not upfront learning. Tutorial is seen as obstacle, not help."

**Create insight statements**:
- What we observed
- Why it matters
- What it means for design

### Phase 6: Create Findings Report (2-3 hours)

#### Executive Summary (1 page)

```
USER TESTING RESULTS: [Prototype Name]

Participants: 8 users, [demographics]
Method: Moderated remote testing
Date: [Date range]

KEY FINDINGS:

1. [Top insight - positive or negative]
2. [Second key finding]
3. [Third key finding]
4. [Fourth finding]
5. [Fifth finding]

RECOMMENDATIONS:

Priority 1 (Must Fix):
- [Issue] - affects X/8 users
- [Issue] - blocks completion

Priority 2 (Should Fix):
- [Issue]
- [Issue]

SUCCESS METRICS:
- Task completion: X%
- Ease rating: X/10
- Would use: X%
```

#### Detailed Findings (5-10 pages)

**For each major issue**:
- Issue description
- Frequency & severity
- Evidence (quotes, clips, metrics)
- User impact
- Recommended fix

**Example**:
```
FINDING #1: Password Requirements Unclear

Severity: HIGH
Frequency: 7/8 users

Description:
Users failed to create valid passwords because requirements weren't visible until after submission error.

Evidence:
- "I don't know what the password needs" [P2, P5, P7]
- Avg 3.2 attempts to create valid password
- All users expressed frustration
- [Video clip timestamps]

Impact:
- Increases signup time by 2-3 min
- Creates negative first impression
- 2 users considered abandoning

Recommendation:
- Show password requirements before input
- Real-time validation as they type
- Clear visual feedback on what's met/not met
```

### Phase 7: Prioritize Changes (1-2 hours)

**Use Impact/Effort Matrix**:

```
High Impact, Low Effort = QUICK WINS
- Fix password requirements visibility
- Change "Help" label to "Contact Us"
- Add progress indicator

High Impact, High Effort = MAJOR UPDATES
- Redesign onboarding flow
- Add contextual help system

Low Impact, Low/High Effort = DEPRIORITIZE
- Icon style improvements
- Color adjustments
```

## Expected Outputs

1. **Issues List**: Categorized and prioritized problems
2. **Metrics Summary**: Quantitative results
3. **Insights**: Key learnings and patterns
4. **Test Report**: Executive + detailed findings
5. **Recommendations**: Prioritized action items
6. **Highlight Reel**: Video clips of key moments (optional)

## Common Challenges & Solutions

### Challenge: "Conflicting feedback between users"

**Solutions**:
- Look for user segments (different needs)
- Count: How many said X vs Y?
- Observe behavior over words
- Design for primary persona

### Challenge: "Too many issues to address"

**Solutions**:
- Focus on patterns (3+ users)
- Prioritize by severity x frequency
- Start with blockers
- Quick wins first

### Challenge: "Stakeholders dismissing results"

**Solutions**:
- Show video clips (hard to dismiss)
- Quantify: "6/8 couldn't complete"
- Connect to business impact
- Bring stakeholders to observe

## Success Indicators

✅ **Patterns identified**: Clear themes across users
✅ **Quantified**: Metrics calculated
✅ **Prioritized**: Know what to fix first
✅ **Evidence-based**: Data supports recommendations
✅ **Actionable**: Clear next steps
✅ **Documented**: Report ready to share

## Related Resources

- **Previous Task**: `conduct-usability-test.md`
- **Next Task**: `plan-iterations.md`
- **Parent Task**: `run-user-testing.md`
