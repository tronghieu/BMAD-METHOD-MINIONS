# Task: Gate Update (QA)

Agent: QA Verifier / core QA
Difficulty: Easy
Duration: 10–15 minutes

## Purpose
Update or create a QA gate decision for a bug fix when a formal decision is required.

## Steps
1) Run core QA agent commands if not already done:
   - `@qa *review {bug}` for comprehensive assessment
   - `@qa *gate {bug}` to write/update the gate file
2) Link the gate file in the bug doc → Links (e.g., `docs/qa/gates/bug-<id>.yml`)
3) Summarize gate result in bug doc → QA Results

## Outputs
- Gate file written/updated
- Bug doc linked and summarized

