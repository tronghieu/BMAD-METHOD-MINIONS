# create-team-prd-from-handoff

**Task Type:** Team PRD Generation
**Agent:** mission-pm
**Purpose:** Create team-specific PRD from mission handoff document

## Overview

This task transforms a team handoff document (created by mission-po) into a team-specific PRD that lives in the team's own documentation folder. This allows each team to have their own PRD focused on their specific responsibilities while maintaining alignment with the mission.

## Prerequisites

- Team handoff document exists (typically in `docs/teams/{team-id}/handoff-{mission}.md`)
- Team folder structure exists in `docs/teams/{team-id}/`
- Mission PRD has been created and aligned

## Task Flow

### Step 1: Identify Team and Handoff
```yaml
elicit: true
prompt: |
  Which team PRD would you like to create from handoff?

  1. Specify team ID (e.g., mobile, backend, web)
  2. Mission name or ID

  Or provide path to handoff document:
```

### Step 2: Load Handoff Document
```yaml
action: load_handoff
process: |
  1. Load handoff from docs/teams/{team-id}/handoff-{mission}.md
  2. Extract team-specific requirements
  3. Identify dependencies on other teams
  4. Note integration points
```

### Step 3: Transform to Team PRD
```yaml
action: create_prd
template: |
  # {Team Name} PRD: {Mission Name}

  **Document Version:** 1.0.0
  **Team:** {team_id}
  **Mission Reference:** {mission_id}
  **Created:** {date}

  ## Executive Summary
  {extracted_from_handoff_summary}

  ## Team Objectives

  ### Primary Goals
  {team_specific_goals}

  ### Success Metrics
  {team_kpis}

  ## Requirements

  ### Functional Requirements
  {functional_requirements_for_team}

  ### Non-Functional Requirements
  {nfr_for_team}

  ## Technical Approach

  ### Architecture Components
  {team_components}

  ### Technology Stack
  {team_tech_stack}

  ## Dependencies

  ### Upstream Dependencies
  | Team | Component | Required By | Status |
  |------|-----------|-------------|---------|
  {upstream_dependencies}

  ### Downstream Dependencies
  | Team | Component | Needed By | Status |
  |------|-----------|-----------|---------|
  {downstream_dependencies}

  ## Integration Points

  ### APIs to Consume
  {apis_to_consume}

  ### APIs to Provide
  {apis_to_provide}

  ## Delivery Plan

  ### Milestones
  {team_milestones}

  ### Risks & Mitigations
  {team_risks}

  ## Acceptance Criteria
  {acceptance_criteria}

  ## RACI Reference
  See: docs/missions/{mission_id}/raci-matrix.md

  ## Related Documents
  - Mission PRD: docs/missions/{mission_id}/mission-prd.md
  - Handoff Document: docs/teams/{team_id}/handoff-{mission}.md
  - Architecture: docs/architecture/{mission_id}-architecture.md
```

### Step 4: Save Team PRD
```yaml
action: save_document
location: docs/teams/{team_id}/prd-{mission}.md
process: |
  1. Create directory if not exists: docs/teams/{team_id}/
  2. Save PRD with proper naming: prd-{mission}.md
  3. Update team's index if exists
```

### Step 5: Validate & Confirm
```yaml
elicit: true
prompt: |
  Team PRD created at: docs/teams/{{team_id}}/prd-{{mission}}.md

  Review checklist:
  [ ] All team requirements captured
  [ ] Dependencies clearly identified
  [ ] Integration points defined
  [ ] Milestones aligned with mission timeline

  Would you like to:
  1. Create another team PRD
  2. Review the created PRD
  3. Continue to next step
```

## Output Format

Creates a focused team PRD containing:
- Team-specific requirements only
- Clear dependencies on other teams
- Integration contracts
- Team's delivery milestones
- Direct link back to mission PRD

## Usage Examples

### Example 1: Mobile Team PRD
```bash
@mission-pm create-team-prd
> Team: mobile
> Mission: payment-processing

Creates: docs/teams/mobile/prd-payment-processing.md
```

### Example 2: Backend Team PRD
```bash
@mission-pm create-team-prd
> Team: backend
> Mission: payment-processing

Creates: docs/teams/backend/prd-payment-processing.md
```

## Best Practices

1. **Keep it focused** - Only include what's relevant to the team
2. **Maintain links** - Always reference the mission PRD
3. **Clear boundaries** - Explicitly state what's NOT in scope
4. **Update together** - When mission changes, update team PRDs
5. **Version control** - Track changes to team PRDs

## Integration with Workflow

This task fits into the mission workflow:
1. Mission PRD created (mission-pm)
2. Teams align on mission (mission-orchestrator)
3. Mission decomposed to handoffs (mission-po)
4. **Team PRDs created from handoffs** (mission-pm) ← This task
5. Teams execute with their PRDs (team-level work)

## Common Issues

**Issue:** Handoff document not found
**Solution:** Ensure mission-po has run shard-mission-to-teams first

**Issue:** Team folder doesn't exist
**Solution:** Create docs/teams/{team-id}/ structure

**Issue:** Conflicting requirements
**Solution:** Refer back to mission PRD for resolution