# Task: Resolve Bug (Dev)

Agent: Dev (reuse core)
Difficulty: Medium
Duration: 30–120 minutes

## Purpose
Implement the fix with a failing test first, expand coverage, and keep scope tight.

## Prerequisites
- Fix Plan drafted in bug doc (`fix-plan-tmpl.yaml`)

## Steps
1) Write failing test first
   - Unit where possible; integration or e2e when required
2) Implement the fix
   - Keep changes minimal; adhere to project standards
3) Expand tests
   - Add targeted regression tests for impacted paths
4) Sanity NFR checks
   - Security/perf/reliability/maintainability impacts
5) Update Links
   - Add PR/commit references in bug doc → Links
6) Mark status to `InProgress` → then `Verification` when ready

## Checklist
- Run `checklists/fix-checklist.md`

## Outputs
- Passing tests and implemented fix
- Updated bug doc (Links, Fix Plan completion notes)

