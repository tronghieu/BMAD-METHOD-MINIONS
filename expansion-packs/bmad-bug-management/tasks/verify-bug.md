# Task: Verify Bug

Agent: QA Verifier (pairs with core QA)
Difficulty: Medium
Duration: 20–60 minutes

## Purpose
Verify the fix, run targeted regression, and summarize NFR checks.

## Prerequisites
- Bug status set to `Verification`
- Dev has included Links to commits/PR

## Steps
1) Execute Verification Plan
   - Use bug doc → Verification; populate using `templates/verification-plan-tmpl.yaml`
2) Targeted Regression
   - Validate nearby paths/functionality affected by the fix
3) NFR spot checks
   - Security/perf/reliability/maintainability
4) Gate (optional)
   - If formal gate desired, use core QA: `@qa *review {bug}` then `@qa *gate {bug}`
   - Link the gate file under Links (e.g., `docs/qa/gates/bug-<id>.yml`)
5) Result
   - If pass → proceed to closure; if fail → set Status `Reopened` (loop to InProgress)

## Checklist
- Run `checklists/verification-checklist.md`

## Outputs
- Verification summary and result in bug doc; linked QA gate if used

