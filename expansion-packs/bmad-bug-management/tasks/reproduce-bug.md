# Task: Reproduce Bug

Agent: Repro Specialist
Difficulty: Medium
Duration: 20–60 minutes

## Purpose
Establish a minimal, reliable reproduction with environment details and evidence.

## Prerequisites
- Bug doc exists and triage completed or in progress

## Steps
1) Create/Update Reproduction Notes
   - Use `templates/repro-record-tmpl.yaml` in the bug doc
2) Minimal Repro
   - Reduce steps/scope to the smallest case that still reproduces consistently
3) Capture Environment
   - Fill table fields (OS/Device/AppVersion/Build/Locale)
4) Attach Evidence
   - Save to `docs/bugs/assets/{{bug_id}}/` and link
5) Investigate Introducing Change (optional)
   - Perform bisect; record suspected root cause if identified
6) Hand off to Dev when reproducible and scoped

## Checklist
- Run `checklists/reproduction-checklist.md`

## Outputs
- Reproduction Notes updated with minimal repro, environment, evidence
- Suspected root cause (optional)

