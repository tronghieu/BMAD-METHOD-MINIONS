# Task: Document Prototype

**Design Thinking Phase**: Prototype
**Duration**: 15-30 minutes
**Agent**: Prototype Builder
**Difficulty**: Low

## Purpose

Create clear documentation of prototype specifications, limitations, and usage instructions for testing and handoff.

## Prerequisites

- [ ] Prototype completed
- [ ] Testing scenarios defined

## Documentation Components

### 1. Prototype Overview (5 min)

**Document**:
- **Purpose**: What this prototype tests
- **Fidelity Level**: Low/Medium/High
- **Key Features**: What's included
- **Limitations**: What doesn't work

**Example**:
```
PROTOTYPE: Onboarding Assistant v1
Purpose: Test AI-guided setup experience
Fidelity: Medium (clickable wireframes)
Features: Welcome flow, step-by-step guidance, progress tracking
Limitations: No actual AI, fake data, limited to happy path
```

### 2. What Works / What Doesn't (5 min)

**List clearly**:

**Functional**:
- User can click through signup flow
- Progress bar updates
- Success confirmation appears

**Non-Functional** (simulated):
- AI responses are pre-scripted
- Form validation doesn't work
- Back button only works on certain screens
- Data isn't saved

### 3. How to Use for Testing (10 min)

**Instructions for facilitators**:
- How to start the prototype
- What to explain to users
- How to "operate" it (for paper prototypes)
- What to do when users hit non-functional areas

**Example**:
```
TESTING INSTRUCTIONS:

Starting:
1. Open [prototype link/show first screen]
2. Say: "This is a prototype, not everything works"
3. Present first scenario

Operating:
- For paper: Swap screens when user "taps"
- For digital: Let them click through
- If they hit non-functional area: Note it, gently redirect

Common Issues:
- Search doesn't work: "Let's assume you found X"
- Form validation off: Accept any input
- Back button missing: Tell them to use browser back
```

### 4. Test Scenarios Reference (5 min)

**Attach or link to**:
- Written test scenarios
- Expected user paths
- Success criteria

### 5. Photo/Screenshot Documentation (5 min)

**Capture**:
- All key screens
- Important interactions
- Full user flow (sequence)
- Any special elements

## Documentation Template

```
┌──────────────────────────────────────┐
│    PROTOTYPE SPECIFICATION           │
├──────────────────────────────────────┤
│ Name: [Prototype Name v#]            │
│ Date: [Date Created]                 │
│ Fidelity: [Low/Medium/High]          │
│ Purpose: [What we're testing]        │
├──────────────────────────────────────┤
│ FEATURES INCLUDED:                   │
│ • [Feature 1]                        │
│ • [Feature 2]                        │
│ • [Feature 3]                        │
├──────────────────────────────────────┤
│ WHAT WORKS:                          │
│ ✓ [Interaction 1]                    │
│ ✓ [Interaction 2]                    │
│                                      │
│ WHAT DOESN'T WORK (simulated):       │
│ ✗ [Limitation 1]                     │
│ ✗ [Limitation 2]                     │
├──────────────────────────────────────┤
│ TESTING NOTES:                       │
│ [How to use, known issues]           │
└──────────────────────────────────────┘
```

## Expected Outputs

1. **Prototype Spec Doc**: One-page overview
2. **Usage Instructions**: How to test with it
3. **Screenshots/Photos**: Visual documentation
4. **Known Issues List**: What to expect

## Success Indicators

✅ **Clear**: Anyone can understand what works
✅ **Complete**: All limitations documented
✅ **Usable**: Testers know how to use it
✅ **Visual**: Screenshots/photos included

## Related Resources

- **Next Task**: `run-user-testing.md`
- **Parent Task**: `build-rapid-prototype.md`
