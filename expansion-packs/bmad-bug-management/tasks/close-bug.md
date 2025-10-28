# Task: Close Bug

Agent: Bug Coordinator
Difficulty: Easy
Duration: 10–20 minutes

## Purpose
Close the bug with complete documentation, linkage to releases/backports, and changelog.

## Prerequisites
- Verification passed (or accepted with documented risk)

## Steps
1) Populate Closure
   - Use `templates/bug-closure-tmpl.yaml` in bug doc
   - Include verification summary, gate link, release/hotfix link, backports, changelog entry
2) Update Status to `Closed`
3) Update metrics if tracked
4) For P0/P1 production bugs, link to release workflow (hotfix)

## Checklist
- Run `checklists/closure-checklist.md`

## Outputs
- Updated bug doc with closure details
- Status set to Closed

