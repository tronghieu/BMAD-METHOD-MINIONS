# Shard Mission to Teams Task

## Purpose

Decompose a mission-level PRD into team-specific handoff documents, ensuring each autonomous team receives exactly the information they need to execute their part of the mission independently while maintaining alignment with the overall goals.

## Task Instructions

### 1. Pre-Sharding Analysis

**Inputs Required:**
- Completed and approved Mission PRD
- Alignment meeting notes with commitments
- Team structure from orchestra-config.yaml
- Any technical architecture documents

**Validation Checks:**
```markdown
Before sharding, verify:
- [ ] Mission PRD is final and approved
- [ ] All teams have committed in alignment meeting
- [ ] Dependencies are fully mapped
- [ ] Integration contracts are defined
- [ ] Timeline and milestones are agreed
```

### 2. Team Identification & Scoping

**For each team involved in the mission:**

1. **Identify Team Scope**
   - Which epics involve this team?
   - What are their primary deliverables?
   - What are their dependencies?
   - What's their role (Responsible, Accountable, Consulted, Informed)?

2. **Determine Information Needs**
   - What context do they need from the mission?
   - Which other teams will they interact with?
   - What integration points affect them?
   - What constraints apply to their work?

3. **Assess Current State**
   - What existing systems will they modify?
   - What new components will they build?
   - What technical debt might impact them?
   - What skills or resources might they need?

### 3. Sharding Process

**Step 1: Create Team Directories**
```bash
docs/
├── mission/
│   └── mission-prd.md
├── teams/
│   ├── mobile/
│   │   └── handoff-{mission-code}.md
│   ├── backend/
│   │   └── handoff-{mission-code}.md
│   ├── ai/
│   │   └── handoff-{mission-code}.md
│   └── web/
│       └── handoff-{mission-code}.md
```

**Step 2: Extract Team-Specific Information**

For each team, extract and organize:

#### A. Mission Context
From the Mission PRD, extract:
- Overall mission goal (keep high-level)
- Success metrics that this team impacts
- Timeline and major milestones
- Why this mission matters (business context)

#### B. Team-Specific Epics
From the cross-team epics, extract:
- Only epics where team is Responsible or Accountable
- Full epic description and acceptance criteria
- User stories that apply to this team
- Definition of done for their components

#### C. Dependencies

**Inbound Dependencies** (what they need):
```markdown
For each dependency:
- Source team and contact
- What exactly is needed
- Format/specification
- When it's needed
- Impact if delayed
- Fallback plan
```

**Outbound Dependencies** (what others need from them):
```markdown
For each dependency:
- Consumer team and contact
- What must be delivered
- Format/specification
- Delivery deadline
- Impact if delayed
- Priority level
```

#### D. Integration Contracts
Extract only contracts where team is involved:
- APIs they will consume (with endpoints)
- APIs they must provide (with SLAs)
- Data formats and schemas
- Authentication methods
- Error handling requirements

#### E. Technical Requirements
Filter to team-relevant requirements:
- Performance targets for their components
- Security requirements they must implement
- Compatibility constraints
- Technology stack decisions
- Architectural patterns to follow

### 4. Creating Team Handoff Documents

**Use the team-handoff-tmpl.yaml template for each team:**

1. **Personalize the Context**
   - Address the team directly ("Your team will...")
   - Emphasize their importance to mission success
   - Highlight how their work enables others

2. **Provide Clear Scope**
   - List exactly what they're building
   - Define boundaries (what's NOT their responsibility)
   - Clarify any gray areas upfront

3. **Make Dependencies Actionable**
   - Include contact information
   - Provide fallback plans
   - Set clear escalation paths

4. **Include Practical Information**
   - Repository locations
   - Environment details
   - Tool access requirements
   - Communication channels

### 5. Dependency Validation

**Cross-Team Dependency Matrix:**

Create a matrix to ensure consistency:

| Provider Team | Consumer Team | Dependency | Provider Date | Consumer Needs By | Status |
|---------------|---------------|------------|---------------|-------------------|--------|
| Backend | Mobile | User API | Sprint 2 | Sprint 3 | Aligned |
| AI | Backend | ML Model | Sprint 3 | Sprint 4 | Aligned |
| Backend | Web | Admin API | Sprint 2 | Sprint 2 | Risk |

**Validation Steps:**
1. Every outbound dependency has a matching inbound
2. Dates align between provider and consumer
3. No circular dependencies exist
4. Critical path dependencies are marked

### 6. Epic Decomposition Guidance

**For each team's epics, provide structure for further breakdown:**

```markdown
Epic: [Epic Title]
│
├── Technical Design Needed
│   ├── Architecture decisions
│   ├── Technology choices
│   ├── Integration approach
│   └── Security considerations
│
├── Suggested Story Breakdown
│   ├── Foundation stories (setup, configuration)
│   ├── Core functionality stories
│   ├── Integration stories
│   ├── Testing stories
│   └── Documentation stories
│
└── Risk Factors
    ├── Technical risks
    ├── Dependency risks
    └── Resource risks
```

### 7. Timeline Alignment

**Create Team-Specific Timeline:**

For each team, translate mission milestones to team deliverables:

```markdown
Mission Milestone: "Beta Release" (Sprint 4)

Your Team's Deliverables for Beta:
- [ ] Feature X fully implemented
- [ ] Integration with Team Y complete
- [ ] API documentation published
- [ ] Performance testing passed
- [ ] Security review completed
```

### 8. Quality Assurance

**Handoff Document Checklist:**

For each team handoff document, verify:

```markdown
Content Completeness:
- [ ] Mission context provided
- [ ] All relevant epics included
- [ ] Dependencies fully documented
- [ ] Integration contracts specified
- [ ] Timeline clearly stated
- [ ] Success criteria defined

Clarity:
- [ ] No ambiguous ownership
- [ ] Technical terms defined
- [ ] Acronyms explained
- [ ] Contact information current

Actionability:
- [ ] Clear first steps identified
- [ ] Resources accessible
- [ ] Blockers highlighted
- [ ] Escalation path defined
```

### 9. Distribution & Confirmation

**Distribution Process:**

1. **Initial Distribution**
   - Send handoff document to team lead
   - CC technical lead and PM
   - Include link to mission PRD
   - Set review deadline

2. **Review Meeting**
   - Schedule 30-minute review with each team
   - Walk through document together
   - Capture questions and concerns
   - Update document based on feedback

3. **Confirmation**
   - Get written confirmation of receipt
   - Confirm understanding of scope
   - Verify no blocking issues
   - Document any caveats or conditions

### 10. Maintain Alignment

**Post-Sharding Synchronization:**

- Keep a master tracking document linking all handoffs
- When mission PRD changes, update affected handoffs
- Track which teams have been notified of changes
- Version control all documents

**Change Management Process:**
1. Identify change in mission or dependencies
2. Assess which teams are affected
3. Update relevant handoff documents
4. Notify affected teams with diff
5. Get re-confirmation if major change

## Sharding Principles

### Clarity Over Completeness
- Give teams exactly what they need
- Avoid overwhelming with unnecessary detail
- Link to detailed docs rather than duplicating

### Autonomy Through Context
- Provide the "why" to enable good decisions
- Share constraints but not implementation details
- Trust teams to figure out the "how"

### Explicit Over Implicit
- State assumptions clearly
- Define interfaces precisely
- Document edge cases

### Iteration-Friendly
- Expect and plan for changes
- Make documents easy to update
- Version control everything

## Common Sharding Patterns

### Pattern 1: Frontend/Backend Split
- Frontend gets UI/UX requirements, API contracts
- Backend gets business logic, data models, performance requirements
- Both get integration touchpoints

### Pattern 2: Service Decomposition
- Each service team gets their bounded context
- Clear API contracts between services
- Shared data models where necessary

### Pattern 3: Platform/Application Split
- Platform team gets infrastructure, tools, shared services
- Application teams get business features, user facing components
- Clear abstraction boundaries

## Success Metrics

Effective sharding achieved when:
- Each team can start work independently
- No team is blocked waiting for clarification
- Dependencies are understood by all parties
- Integration points are clearly defined
- Teams feel confident in their scope

## Troubleshooting

### Common Issues and Solutions

**Issue: Overlapping Responsibilities**
- Solution: Create explicit boundary definitions
- Add RACI matrix for gray areas
- Designate tie-breaker for disputes

**Issue: Missing Information**
- Solution: Create FAQ document
- Schedule office hours for questions
- Maintain decision log

**Issue: Dependency Conflicts**
- Solution: Prioritize critical path
- Negotiate timeline adjustments
- Consider parallel work streams

**Issue: Scope Creep**
- Solution: Reference back to mission PRD
- Require formal change process
- Assess impact before accepting

## Tools & Templates

- team-handoff-tmpl.yaml - Main template for handoffs
- dependency-matrix.xlsx - Track cross-team dependencies
- epic-decomposition-guide.md - Help teams break down epics
- scope-boundary-template.md - Define clear boundaries