# Task: Run User Testing

**Design Thinking Phase**: Test
**Duration**: 3-10 days (includes recruitment, sessions, analysis)
**Agent**: Test Analyst
**Difficulty**: Medium-High

## Purpose

Validate prototypes with real users to learn what works, what doesn't, and how to improve. Testing provides evidence to iterate designs and build confidence before full development.

## Prerequisites

- [ ] **Prototype ready** (functional enough to test)
- [ ] **Testing objectives clear** (what we need to learn)
- [ ] **Test scenarios written** (tasks for users to complete)
- [ ] **Participants recruited** (5-8 users minimum)
- [ ] **Testing space/tools** ready (room or remote setup)
- [ ] **Observation template** prepared
- [ ] **Recording permissions** obtained

## Key Principles

**Test to learn, not validate**:
- ✅ Observe what users struggle with
- ✅ Discover unexpected behaviors
- ✅ Identify improvements needed
- ❌ Prove your design is great
- ❌ Get compliments
- ❌ Confirm what you already believe

**Show, don't tell**:
- Let prototype speak for itself
- Minimal explanation before test
- Observe actual behavior
- Ask about actions after completing

## Step-by-Step Process

### Phase 1: Test Preparation (1-2 days)

#### 1.1 Define Learning Objectives

What do we need to learn?
- Can users complete core task?
- Do they understand the value proposition?
- Where do they get confused?
- What delights or frustrates them?
- Would they use this?

**Output**: 3-5 test objectives

#### 1.2 Create Test Scenarios

Write realistic tasks (not step-by-step instructions):

**Good**: "You need to share a file with a colleague. Show me how you'd do that."
**Bad**: "Click the share button, then enter an email, then click send."

**Scenario structure**:
- Context/motivation
- Goal to achieve
- No hints about how

**Example scenarios**:
1. "You've just downloaded the app. Get started and complete your first task."
2. "You need to [goal]. Show me how you'd approach this."
3. "Something went wrong. Try to resolve the issue."

Create 3-5 scenarios testing different aspects

#### 1.3 Prepare Discussion Guide

**Opening** (5 min):
- Build rapport
- Explain think-aloud protocol
- Set expectations (testing product, not person)

**Task scenarios** (30-40 min):
- Present scenarios one at a time
- Observe and take notes
- Probe when stuck
- Don't help immediately

**Debrief questions** (10-15 min):
- Overall impressions
- Likes/dislikes
- Comparison to current solutions
- Likelihood to use/recommend

#### 1.4 Set Up Testing Environment

**In-Person**:
- Private, quiet room
- Prototype on appropriate device
- Observer seating (out of direct view)
- Recording equipment
- Note-taking materials

**Remote**:
- Screen sharing + recording tool (Zoom, Teams)
- Prototype link sent in advance
- Test video/audio beforehand
- Note-taking template ready

### Phase 2: Conduct Tests (3-5 days)

#### 2.1 Test Session Structure (50-60 min)

**Welcome & Context** (5 min):
- Thank participant
- Explain purpose
- Get consent for recording
- Emphasize: "We're testing the product, not you"

**Think-Aloud Training** (3 min):
- "Please say what you're thinking out loud"
- Demo with simple task (e.g., "Find weather for London")
- Practice narrating thoughts

**Task Scenarios** (30-40 min):
- Present scenario context
- Start timing (note start time)
- Observe without interrupting
- Take notes on:
  - Where they click/tap
  - Hesitations and pauses
  - Facial expressions
  - Verbal reactions ("Huh?", "Oh!", "Where is...")
  - Errors and recovery
  - Time to complete

**When to probe**:
- After they complete or give up
- "What were you expecting to happen?"
- "What were you looking for just now?"
- "Why did you click there?"

**When they're stuck** (after 30-60 seconds):
- "What are you thinking?"
- "What would you expect to see?"
- If truly blocked: Give minimal hint to continue

**Debrief** (10-15 min):
- "Overall, what did you think?"
- "What worked well?"
- "What was frustrating?"
- "How does this compare to [current solution]?"
- "Would you use this? Why/why not?"
- "What would make this better?"

**Closing** (2 min):
- Thank them
- Explain next steps
- Provide compensation

#### 2.2 Observation & Note-Taking

**Real-time notes template**:
```
Participant: P3 (Maria, 28, frequent user)
Scenario 1: First-time setup
[00:02] Started clicking explore tabs
[00:05] [CONFUSION] "Where do I actually start?"
[00:08] Found start button after scanning
[00:12] [SUCCESS] Completed signup
Time: 12 min (expected 5 min)

Scenario 2: Complete core task
[00:15] [ERROR] Clicked wrong button, expected X got Y
[00:18] [FRUSTRATION] "This doesn't make sense"
[00:22] [HELP NEEDED] Gave hint about menu location
[00:25] [SUCCESS] Completed after hint
Time: 10 min (expected 3 min)

Key observations:
- Didn't see start CTA initially (placement issue?)
- Expected X feature in Y location
- Confused by terminology "Z"

Quotes:
- "I like the idea, but it's not obvious how to begin"
- "Once I got it, it was easy"

Severity ratings:
- Can't find start: CRITICAL
- Wrong button label: MEDIUM
- Terminology confusion: LOW
```

#### 2.3 Capture Evidence

**Record**:
- Screen + audio (minimum)
- Face if possible (emotions valuable)
- Note timestamps of key moments

**Photos**:
- Participant using prototype (with permission)
- Gestures or pointing
- Environment context

**Metrics** (if relevant):
- Task completion rate
- Time to complete
- Error count
- Clicks/taps to success
- Help requests

### Phase 3: Analysis & Synthesis (2-3 days)

#### 3.1 Review Sessions

After each test:
- Clean up notes (same day!)
- Highlight critical issues
- Note patterns across participants
- Clip video of key moments (10-15 second snippets)

After all tests:
- Compile all notes
- Create issues database

#### 3.2 Identify Patterns

Look for issues mentioned by 3+ users (patterns):

**Severity framework**:
- **CRITICAL**: Blocks task completion
- **HIGH**: Causes significant confusion/frustration
- **MEDIUM**: Noticeable but workaround exists
- **LOW**: Minor annoyance

**Pattern analysis**:
```
Issue: "Can't find start button"
Frequency: 6/8 users
Severity: CRITICAL
Impact: Delayed setup by avg 3 min
Evidence: [Video clips, quotes]
Hypothesis: Placement below fold, low contrast
```

#### 3.3 Synthesize Insights

Transform observations into insights:

**Observation**: "7/8 users clicked wrong button expecting feature X"
**Insight**: "Users have mental model where X lives in Y location (from competitors/past experience)"

**Observation**: "All users said they'd use this weekly"
**Insight**: "Core value proposition resonates; solves real need"

**Create findings summary**:
1. What worked well (keep/enhance)
2. What didn't work (fix/remove)
3. What was missing (add/consider)
4. Unexpected discoveries (explore further)

#### 3.4 Prioritize Changes

Use impact vs effort matrix:

**Quick Wins** (High impact, Low effort):
- Fix terminology
- Adjust button placement
- Change default setting

**Major Updates** (High impact, High effort):
- Redesign workflow
- Add missing feature
- Change core interaction

**Low Priority** (Low impact, any effort):
- Polish details
- Nice-to-have features

### Phase 4: Reporting & Next Steps (1 day)

#### 4.1 Create Test Report

**Executive Summary** (1 page):
- Participants overview
- Key findings (top 5)
- Recommendations
- Next steps

**Detailed Findings** (5-10 pages):
- Each major issue with:
  - Description
  - Evidence (quotes, clips, metrics)
  - Severity and frequency
  - Recommended fix

**What Worked Well**:
- Positive feedback
- Successful interactions
- Validated assumptions

**Appendix**:
- Full participant notes
- Metrics summary
- Video clips links

#### 4.2 Prioritized Iteration Plan

**Must Fix** (before next test):
- Critical blockers
- High-frequency issues
- Quick wins

**Should Fix** (in next version):
- Medium severity issues
- Feature requests from majority

**Consider** (future iterations):
- Nice-to-haves
- Low-impact improvements

#### 4.3 Decide: Iterate or Build?

**Iterate (test again)** if:
- Critical issues found
- Significant redesign needed
- Success rate <70%
- User feedback mostly negative

**Move to build** if:
- Users successfully complete tasks (>80%)
- Positive overall sentiment
- Clear value proposition validated
- Issues are minor/polish-level

## Expected Outputs

1. **Test Sessions**: 5-8 completed user tests
2. **Session Notes**: Detailed observations for each
3. **Video Clips**: Key moments captured (30-60 seconds each)
4. **Findings Summary**: Patterns and insights
5. **Prioritized Issues**: What to fix, in what order
6. **Test Report**: Documented findings and recommendations
7. **Iteration Plan**: Next steps clearly defined

## Common Challenges & Solutions

### Challenge: "Users are too polite/positive"

**Solutions**:
- Observe behavior, not just words
- Ask about specific moments: "Why did you pause there?"
- Compare to alternatives: "How does this differ from [current tool]?"
- Watch for hesitations and errors (tells real story)

### Challenge: "We're getting conflicting feedback"

**Solutions**:
- Look for segments (maybe different user types need different things)
- Count: How many said X vs Y?
- Consider severity: What blocks tasks?
- Design for primary persona, accommodate others

### Challenge: "Too many issues to fix"

**Solutions**:
- Focus on task blockers first
- Fix patterns (3+ users), not one-offs
- Quick wins before major redesigns
- Test iteratively, don't fix everything at once

### Challenge: "Stakeholders dismissing feedback"

**Solutions**:
- Show video clips (hard to dismiss real users)
- Quantify: "6/8 couldn't complete task"
- Connect to business impact: "This causes abandonment"
- Bring stakeholders to observe tests live

## Success Indicators

✅ **Clear patterns**: Multiple users have same issues
✅ **Evidence captured**: Video clips and quotes
✅ **Actionable insights**: Know what to change
✅ **Validated value**: Users see benefit
✅ **Team alignment**: Agree on priorities
✅ **Iteration plan**: Next steps defined

## Related Resources

- **Test Protocol Template**: `templates/test-protocol-template.md`
- **Observation Template**: `templates/observation-notes-template.md`
- **Analysis Checklist**: `checklists/analysis-completeness-checklist.md`

## Next Steps

**If critical issues found**:
→ **build-rapid-prototype.md** - Iterate and test again

**If validation successful**:
→ Move to development/implementation phase
