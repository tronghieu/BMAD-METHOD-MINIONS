# create-raci-matrix

**Task Type:** Mission Planning Support
**Agent:** mission-pm
**Purpose:** Create a RACI matrix for cross-team missions to clarify responsibilities

## Overview

This task helps create a comprehensive RACI (Responsible, Accountable, Consulted, Informed) matrix for missions that span multiple teams. It ensures clear ownership and accountability across team boundaries.

## Prerequisites

- Mission PRD exists with identified epics/features
- Teams have been identified for the mission
- Orchestra config loaded with team definitions

## Task Flow

### Step 1: Load Mission Context
```yaml
elicit: true
prompt: |
  Please provide the mission PRD or reference:
  - Mission name/ID
  - Path to mission PRD (if exists)
  - Or paste key mission details
```

### Step 2: Identify Work Streams
```yaml
action: analyze
inputs:
  - mission_prd
  - team_capabilities
process: |
  1. Extract major epics/features from mission
  2. Group into logical work streams
  3. Identify technical components involved
output: work_streams_list
```

### Step 3: Map Teams to Work Streams
```yaml
elicit: true
prompt: |
  For each work stream, identify participating teams:

  Work Streams Identified:
  {{work_streams_list}}

  Available Teams:
  {{teams_from_config}}

  Please confirm or adjust team assignments:
```

### Step 4: Define RACI Roles
```yaml
action: create_matrix
template: |
  # RACI Matrix for {{mission_name}}

  ## Role Definitions
  - **R** (Responsible): Does the work
  - **A** (Accountable): Ultimately answerable, approves
  - **C** (Consulted): Provides input, two-way communication
  - **I** (Informed): Kept up-to-date, one-way communication

  ## Work Stream Assignments

  | Work Stream | Component | {{team_columns}} |
  |-------------|-----------|{{team_headers}}|
  {{#each work_streams}}
  | {{name}} | {{component}} | {{team_assignments}} |
  {{/each}}

  ## Key Decisions & Approvals

  | Decision Point | {{team_columns}} |
  |----------------|{{team_headers}}|
  | Architecture Approval | {{arch_assignments}} |
  | API Contract Sign-off | {{api_assignments}} |
  | Integration Testing | {{test_assignments}} |
  | Production Release | {{release_assignments}} |

  ## Communication Protocols

  ### Regular Sync Points
  - Weekly mission sync: All Rs and As
  - Integration checkpoint: Every 2 weeks
  - Stakeholder updates: Monthly (all Is)

  ### Escalation Path
  1. Team Lead (R) → Product Owner (A)
  2. Product Owner → Mission PM
  3. Mission PM → Steering Committee
```

### Step 5: Validate Completeness
```yaml
validation_checks:
  - Every work stream has exactly one A
  - Every work stream has at least one R
  - No team is R for conflicting parallel work
  - Critical paths have identified backups
  - All teams in mission are represented
```

### Step 6: Get Team Confirmation
```yaml
elicit: true
prompt: |
  RACI Matrix created. Please review:

  {{raci_matrix}}

  Required confirmations:
  [ ] All Rs have capacity
  [ ] All As accept accountability
  [ ] Consulted parties acknowledged
  [ ] Informed parties added to distribution

  Confirm to proceed or specify changes:
```

## Output Format

The task produces:
1. `docs/missions/{mission-id}/raci-matrix.md` - Full RACI documentation
2. `docs/missions/{mission-id}/raci-summary.yaml` - Machine-readable format
3. Updates to mission PRD with RACI reference

## Integration Points

- Links to `facilitate-alignment.md` for team buy-in
- Referenced by `track-team-commitments.md` for monitoring
- Used by `assess-mission-risk.md` for risk assignment

## Best Practices

1. **Keep It Simple** - Don't over-assign roles
2. **Single Accountability** - Only one A per work stream
3. **Limit Consultations** - Too many Cs slow progress
4. **Clear Boundaries** - Minimize overlapping Rs
5. **Document Assumptions** - Note capacity constraints

## Common Patterns

### Microservices Pattern
- Backend team: R for API
- Mobile team: C for API design, R for app
- DevOps: A for deployment, C for architecture

### Data Pipeline Pattern
- Data team: R for ETL, A for data quality
- Backend: C for schema, I for changes
- Analytics: R for dashboards, C for requirements

## Troubleshooting

**Issue:** Too many As for one work stream
**Solution:** Identify true decision maker, others become C

**Issue:** Team refuses R assignment
**Solution:** Check capacity, consider splitting work or adjusting timeline

**Issue:** No clear A for technical decisions
**Solution:** Escalate to architect or technical steering committee