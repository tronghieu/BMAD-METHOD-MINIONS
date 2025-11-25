# Task: Conduct Release Retrospective

**Release Management Phase**: Learning & Improvement
**Duration**: 60-90 minutes (for the meeting)
**Agent**: Release Manager
**Difficulty**: Medium

## Purpose

To facilitate a structured, blameless retrospective meeting that produces actionable insights for improving future release processes.

## Prerequisites

- The release has been stable in production for at least 48 hours.
- All post-deployment monitoring data has been collected.
- Key team members involved in the release are available to meet.

## High-Level Process

As the Release Manager and facilitator, your goal is to guide the team through a productive reflection on the recent release. Refer to `data/retrospective-guide.md` for the detailed methodology on how to conduct an effective retrospective.

### 1. Prepare for the Retrospective
- [ ] Gather all objective data about the release: deployment timelines, quality metrics, incident reports, and user feedback.
- [ ] Send out a pre-retrospective survey to the team to gather initial thoughts asynchronously.
- [ ] Prepare the meeting agenda, typically including: successes, areas for improvement, and action items.

### 2. Facilitate the Meeting
- [ ] **Set the Stage:** Begin by stating the purpose and reviewing the "Prime Directive" to ensure a blameless, psychologically safe environment.
- [ ] **Review Data:** Present a summary of the release data to ground the discussion in facts.
- [ ] **Guide Discussion:** Facilitate a balanced conversation covering "What went well?" and "What could be improved?".
- [ ] **Drive to Action:** Guide the team to brainstorm and then commit to a small number of specific, measurable, and owned action items.

### 3. Document and Follow Up
- [ ] **Action**: Use the `retrospective-plan.yaml` template to generate the official `retrospective.md` document, capturing the key discussion points and, most importantly, the action items.
- [ ] Share the summary document with all stakeholders.
- [ ] Ensure the action items are added to the team's work backlog and are reviewed at the beginning of the next retrospective.

## Expected Outputs

- A final **`retrospective.md`** document containing:
  - A summary of what was discussed.
  - Key learnings and insights.
  - A prioritized list of specific, assigned action items with due dates.

## Related Resources
- **Methodology Guide**: `data/retrospective-guide.md`
- **Output Template**: `templates/retrospective-plan.yaml`
- **Knowledge Base**: `data/release-management-kb.md`

