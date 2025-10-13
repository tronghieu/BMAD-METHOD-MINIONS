# Orchestrate Mission Task

## Purpose

Coordinate the end-to-end mission workflow from initial planning through team handoffs, ensuring all autonomous teams are aligned and committed to shared goals while maintaining their independence.

## Task Instructions

### 1. Mission Initialization

When starting a new mission, first understand the context:

**Questions to Ask:**
- What triggered this mission? (Strategic initiative, market opportunity, customer need)
- Which teams will likely be involved?
- What's the expected timeline and urgency?
- Are there any hard constraints or dependencies?
- Has initial discovery work been done? (Brainstorming, research, project brief)

**Set Mission Parameters:**
- Mission code name (short, memorable identifier)
- Mission duration estimate (in sprints/months)
- Success metrics definition
- Team participation requirements

### 2. Pre-Planning Phase

**If No Project Brief Exists:**
- Recommend using the analyst agent for brainstorming
- Suggest market research if competitive factors exist
- Guide creation of project brief to feed into mission PRD

**If Project Brief Exists:**
- Review brief for completeness
- Identify gaps that need addressing
- Extract key elements for mission PRD
- Flag any assumptions that need validation

### 3. Mission PRD Creation

**Orchestration Steps:**

1. **Facilitate Mission PRD Development**
   - Use mission-prd-tmpl.yaml template
   - Focus on cross-team shared goals (not implementation)
   - Define high-level epics that span teams
   - Keep technical details minimal at this stage

2. **Team Involvement Mapping**
   - For each epic, identify required teams
   - Document why each team is needed
   - Note critical vs nice-to-have involvement

3. **Integration Points Identification**
   - Map data flows between teams
   - Identify API requirements
   - Note shared resources or systems
   - Flag potential bottlenecks

4. **Dependency Analysis**
   - Create preliminary dependency map
   - Identify critical path items
   - Note any external dependencies
   - Assess risk levels

### 4. Pre-Alignment Preparation

**Team Readiness Check:**
```markdown
For each team, verify:
- [ ] Team lead identified and available
- [ ] Current capacity understood
- [ ] Any competing priorities identified
- [ ] Technical capabilities confirmed
- [ ] Resource constraints known
```

**Documentation Preparation:**
- Mission PRD draft complete
- Supporting documentation assembled
- Technical architecture outlined
- Risk assessment completed
- Initial timeline proposed

**Stakeholder Communication:**
- Send mission PRD to team leads (minimum 48 hours before meeting)
- Include agenda and expectations
- Request initial feedback
- Schedule alignment meeting

### 5. Alignment Meeting Facilitation

**Before the Meeting:**
- Create meeting document from alignment-meeting-tmpl.yaml
- Prepare presentation materials
- Set up collaboration tools
- Send reminders with dial-in/location

**During the Meeting:**

1. **Mission Overview (10 min)**
   - Present the why behind the mission
   - Share success metrics
   - Emphasize shared ownership

2. **Epic Review (20 min)**
   - Walk through each cross-team epic
   - Gather team feedback
   - Note concerns and questions
   - Adjust scope if needed

3. **Dependency Discussion (20 min)**
   - Review dependency map
   - Identify new dependencies
   - Discuss mitigation strategies
   - Assign dependency owners

4. **Commitment Ceremony (20 min)**
   - Each team states their commitment level:
     - Full commit
     - Conditional commit (with conditions)
     - Cannot commit (with reasons)
     - Needs investigation (spike required)
   - Document all commitments formally

5. **Integration Planning (15 min)**
   - Define integration milestones
   - Agree on contract formats
   - Set mock delivery dates
   - Plan integration tests

6. **Next Steps (5 min)**
   - Confirm action items
   - Set follow-up meetings
   - Define success criteria for kick-off

**After the Meeting:**
- Update meeting notes immediately
- Send to all attendees within 24 hours
- Track action item completion
- Schedule follow-ups as needed

### 6. Team Decomposition & Handoffs

**For Each Team:**

1. **Create Team Handoff Document**
   - Use team-handoff-tmpl.yaml
   - Extract team-specific information from mission PRD
   - Include all dependencies and timelines
   - Provide clear success criteria

2. **Facilitate Handoff Session**
   - Meet with each team individually
   - Walk through their handoff document
   - Answer questions and clarify expectations
   - Confirm understanding and buy-in

3. **Enable Team Planning**
   - Support creation of team PRDs
   - Help break down epics into stories
   - Assist with estimation if requested
   - Ensure consistency with mission goals

### 7. Mission Execution Coordination

**Ongoing Orchestration Activities:**

**Weekly:**
- Check team progress against milestones
- Identify any new blockers
- Facilitate cross-team communication
- Update mission dashboard

**Sprint Boundaries:**
- Coordinate integration testing
- Manage submodule updates
- Resolve conflicts or disputes
- Adjust timelines if needed

**At Milestones:**
- Verify deliverables complete
- Coordinate integrated testing
- Update stakeholders
- Plan next phase

### 8. Risk & Issue Management

**Continuous Monitoring:**
- Track risks identified in planning
- Watch for new risks emerging
- Monitor team health and capacity
- Check dependency delivery

**Issue Resolution Process:**
1. **Identify** - Detect issues early through regular check-ins
2. **Assess** - Determine impact on mission and teams
3. **Escalate** - Bring to appropriate level for resolution
4. **Mitigate** - Implement workarounds or solutions
5. **Communicate** - Ensure all affected teams informed
6. **Document** - Record for future reference

### 9. Success Metrics Tracking

**Define Measurement Plan:**
- How will each metric be measured?
- Who is responsible for measurement?
- When will measurements occur?
- Where will data be stored?

**Regular Reporting:**
- Weekly status to team leads
- Bi-weekly to stakeholders
- Monthly mission health check
- Quarterly strategic review

## Orchestration Principles

### Autonomy with Alignment
- Teams own their implementation decisions
- Mission provides the "what" and "why"
- Teams determine the "how"

### Transparent Communication
- Over-communicate to prevent surprises
- Share both good news and bad news
- Make information accessible to all

### Collaborative Problem-Solving
- Bring teams together to solve cross-cutting issues
- Facilitate, don't dictate solutions
- Build consensus through discussion

### Continuous Adaptation
- Be ready to adjust plans based on learning
- Keep the mission goal stable, flex on approach
- Learn from each mission for the next

## Tools and Artifacts

### Required Tools
- Communication platform (Slack, Teams, etc.)
- Documentation repository
- Project tracking system
- Video conferencing
- Shared calendars

### Key Artifacts Produced
- Mission PRD
- Alignment meeting notes
- Team handoff documents
- Commitment matrix
- Dependency maps
- Integration contracts
- Status reports
- Success metrics dashboard

## Success Criteria

The orchestration is successful when:
- All teams understand and commit to mission goals
- Dependencies are identified and managed
- Integration points are clearly defined
- Teams can work autonomously within constraints
- Progress is visible and measurable
- Mission goals are achieved

## Common Pitfalls to Avoid

- **Over-controlling teams** - Remember they're autonomous
- **Under-communicating** - Err on the side of more updates
- **Ignoring early warnings** - Small issues become big problems
- **Forcing commitments** - Voluntary commitment is stronger
- **Skipping planning** - Invest time upfront to save time later
- **Assuming understanding** - Verify through questions
- **Missing dependencies** - They always exist, find them early