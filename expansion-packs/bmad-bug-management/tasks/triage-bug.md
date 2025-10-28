# Task: Triage Bug

Agent: Bug Coordinator
Difficulty: Easy
Duration: 10–20 minutes

## Purpose
Deduplicate, classify, prioritize, and assign the bug; set SLA and decision.

## Prerequisites
- Bug doc exists at `docs/bugs/{{bug_id}}.md`

## Steps
1) Deduplicate
   - Search repo/docs/issue tracker; link duplicates/related bugs under Triage Notes → Dedupe Links
2) Set Severity & Priority
   - Use `data/severity-priority-rubric.md`
   - Record rationale; set SLA
3) Routing & Ownership
   - Set component; assign owner; notify
4) Decision
   - Choose Accept / Defer / Park; set Status accordingly (Assigned if accepted)
5) Update Triage Notes via `templates/triage-notes-tmpl.yaml` if needed

## Checklist
- Run `checklists/triage-checklist.md`

## Outputs
- Updated bug doc with triage data
- Status updated (e.g., Assigned)

