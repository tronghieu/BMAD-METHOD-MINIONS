# Task: Design Test Scenarios

**Design Thinking Phase**: Prototype → Test (Bridge)
**Duration**: 30-45 minutes
**Agent**: Prototype Builder / Test Analyst
**Difficulty**: Low-Medium

## Purpose

Create realistic user tasks and scenarios for testing prototypes that reveal genuine user behavior and feedback.

## Prerequisites

- [ ] Prototype ready (paper or digital)
- [ ] Testing objectives defined
- [ ] Target users identified

## Scenario Design Principles

**Good scenarios are**:
- Realistic (matches actual use cases)
- Goal-oriented (user has clear objective)
- Open-ended (not step-by-step instructions)
- Contextual (provides situation/motivation)

## Scenario Structure

```
[Context/Situation] + [Goal to achieve] + [Not how to do it]
```

**Good Example**:
"You need to share a file with a colleague. Show me how you'd do that."

**Bad Example** (too prescriptive):
"Click the share button, then enter an email, then click send."

## Step-by-Step Process

### Phase 1: Identify What to Test (10 min)

**From your prototype, list**:
- Core user flows to validate
- Risky assumptions to test
- Key interactions to observe
- Potential confusion points

**Example**:
```
To Test:
- Can users complete signup?
- Do they understand the value proposition?
- Can they find key features?
- Where do they get confused?
```

### Phase 2: Write Scenarios (15-20 min)

**Create 3-5 scenarios covering**:

**Scenario 1: First-Time Experience**
"You've just heard about [product] from a friend. Explore and get started..."

**Scenario 2: Core Task**
"You need to [primary goal]. Show me how you'd approach this..."

**Scenario 3: Problem Resolution**
"Something went wrong with [X]. Try to resolve the issue..."

**Scenario 4: Discovery** (optional)
"Browse around and tell me what catches your attention..."

**Scenario 5: Comparison** (optional)
"How would you use this compared to [current solution]?"

### Phase 3: Add Context Details (10-15 min)

**For each scenario, specify**:

**User Context**:
- Who they are (role/background)
- What they know/don't know
- Their current situation

**Success Criteria**:
- What completing the task looks like
- Time expectations (if relevant)
- Acceptable alternatives

**Example**:
```
SCENARIO: First Purchase

Context:
- You're a busy professional
- You've browsed the site before but never bought
- You have 10 minutes to make a purchase
- You're looking for [specific item]

Goal:
Find and purchase the item

Success:
- Reaches checkout with item in cart
- OR clearly expresses intent to complete later
```

## Scenario Templates

### Template 1: Task Completion
"You want to [achieve goal]. Show me how you would do that."

### Template 2: Exploration
"Take a few minutes to explore. Tell me what you're seeing and thinking."

### Template 3: Comparison
"You currently use [existing solution] for this. Try using this instead."

### Template 4: Recovery
"You tried to [action] but [error occurred]. What would you do?"

## Expected Outputs

1. **Test Scenarios**: 3-5 written user tasks
2. **Context Details**: Background for each scenario
3. **Success Criteria**: What completion looks like
4. **Scenario Order**: Sequence for testing

## Common Mistakes to Avoid

❌ **Too prescriptive**: "Click here, then do this..."
✅ **Better**: "Complete the signup process"

❌ **Too vague**: "Use the app"
✅ **Better**: "Find and save a recipe for dinner"

❌ **Leading**: "Use the easy search feature to..."
✅ **Better**: "Find information about..."

## Success Indicators

✅ **Realistic**: Scenarios match actual use cases
✅ **Clear**: Users understand what to do
✅ **Open**: No step-by-step instructions
✅ **Testable**: Can observe completion/failure
✅ **Representative**: Cover key prototype features

## Related Resources

- **Next Task**: `run-user-testing.md`
- **Template**: `templates/test-scenario-template.md`
- **Parent Task**: `build-rapid-prototype.md`
