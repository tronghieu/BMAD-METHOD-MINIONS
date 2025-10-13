# Facilitate Alignment Meeting Task

## Purpose

Guide the facilitation of cross-team alignment meetings where autonomous teams review mission PRDs, identify dependencies, and make formal commitments to shared goals. This critical ceremony transforms a mission plan into coordinated team action.

## Task Instructions

### 1. Pre-Meeting Preparation (2-3 Days Before)

#### A. Confirm Attendance

**Required Attendees Checklist:**
```markdown
Critical Attendees (meeting cannot proceed without):
- [ ] Product Manager/Mission Owner
- [ ] Technical Architect
- [ ] All affected Team Leads
- [ ] Integration Specialist (if applicable)

Optional but Valuable:
- [ ] QA Lead (for test strategy alignment)
- [ ] DevOps Lead (for deployment coordination)
- [ ] UX Lead (for design system consistency)
- [ ] Executive Sponsor (for kick-off only)
```

**Send Calendar Invites Including:**
- Meeting title: "Mission Alignment: [Mission Name]"
- Duration: 90 minutes (book 2 hours to allow overflow)
- Location/Video link
- Agenda attachment
- Pre-read documents

#### B. Distribute Pre-Read Materials

**48 Hours Before Meeting:**
```
Email Subject: Mission Alignment Pre-Read - [Mission Name]

Team Leads,

Please review these materials before our alignment meeting:

Required:
1. Mission PRD (attached) - Focus on sections relevant to your team
2. Proposed timeline and milestones
3. Initial dependency map

Optional:
1. Technical architecture overview
2. Market/competitive context
3. Risk assessment

Please come prepared to:
- Commit (or not) to your team's portion
- Identify dependencies and blockers
- Suggest timeline adjustments if needed

Questions? Reach out before the meeting so we can prepare answers.
```

#### C. Prepare Facilitation Materials

**Meeting Supplies:**
- Alignment meeting template document
- Mission PRD displayed/printed
- Dependency tracking board (physical or virtual)
- Commitment tracking matrix
- Timer for agenda management
- Parking lot for off-topic items

**Virtual Meeting Setup:**
- Collaborative document for real-time notes
- Miro/Mural board for dependency mapping
- Screen sharing tested
- Backup facilitator designated
- Recording enabled (if appropriate)

### 2. Meeting Facilitation Guide

#### Opening (5 minutes)

**Facilitator Script:**
```
"Welcome everyone. Today we're aligning on the [Mission Name] mission.

Ground Rules:
1. We're here to achieve shared understanding and voluntary commitment
2. Speak up about concerns - now is the time
3. 'No' is an acceptable answer if explained
4. We'll document all decisions and commitments
5. Parking lot for items needing separate discussion

Our outcome: Clear commitments from each team or a path to get there."
```

**Quick Check-in:**
- Each team lead: 30 seconds on current capacity
- Any major concerns to flag upfront?
- Confirm everyone reviewed pre-read materials

#### Mission Overview (10 minutes)

**Product Manager/Mission Owner Presents:**

1. **The Why** (3 minutes)
   - Business driver for this mission
   - Customer/user impact
   - Strategic importance
   - Cost of not doing this

2. **The What** (5 minutes)
   - Mission success metrics
   - High-level scope
   - What's explicitly out of scope
   - Timeline imperatives

3. **The How** (2 minutes)
   - Proposed approach
   - Why this approach vs alternatives
   - Key assumptions we're making

**Facilitation Technique:**
- No interruptions during overview
- Capture clarifying questions for next section
- Watch body language for concerns

#### Epic Review & Discussion (20 minutes)

**For Each Major Epic:**

1. **Present Epic** (2 minutes per epic)
   - User story and value
   - Proposed team assignments
   - Key acceptance criteria

2. **Team Feedback Round** (3 minutes per epic)
   - Each affected team's initial reaction
   - Feasibility assessment
   - Resource concerns
   - Technical constraints

**Facilitation Techniques:**
- Use round-robin for feedback (no one dominates)
- Capture concerns on visible board
- Flag items needing deeper discussion
- Keep momentum - don't solve everything now

**Concern Categorization:**
- 🟢 Green: Understood and feasible
- 🟡 Yellow: Feasible with conditions
- 🔴 Red: Blocking concerns exist

#### Dependency Identification (20 minutes)

**Interactive Dependency Mapping:**

1. **Self-Identification** (5 minutes)
   - Each team lists what they need from others
   - Write on cards/virtual stickies
   - Include timing requirements

2. **Dependency Matching** (10 minutes)
   - Match needs with providers
   - Identify gaps (needs without providers)
   - Find conflicts (timing mismatches)
   - Surface hidden dependencies

3. **Critical Path Analysis** (5 minutes)
   - Which dependencies could block the mission?
   - What's the longest chain of dependencies?
   - Where are single points of failure?

**Visual Dependency Map:**
```
Mobile Team ──needs API──> Backend Team (by Sprint 2)
     ↓                           ↓
needs specs                 needs model
     ↓                           ↓
UX Team                      AI Team (by Sprint 1)
```

**Facilitation Techniques:**
- Make dependencies visible to all
- Color code by risk level
- Get verbal confirmation from providers
- Document fallback plans for critical items

#### Commitment Ceremony (20 minutes)

**Structured Commitment Process:**

1. **Set Context** (2 minutes)
   ```
   "We're now going to get formal commitments. Remember:
   - Commitment means your team will deliver as specified
   - Conditional commitment must state clear conditions
   - No commitment is better than false commitment
   - We'll document everything formally"
   ```

2. **Team-by-Team Commitment** (15 minutes)

   For each team, capture:

   **Team Lead Statement Format:**
   ```
   "[Team Name] [commits/conditionally commits/cannot commit] to:
   - [Specific deliverables]
   - By [Timeline]
   - With these conditions: [if applicable]
   - These risks exist: [if applicable]"
   ```

   **Commitment Levels:**
   - ✅ **Full Commit**: "We will deliver X by Y"
   - ⚠️ **Conditional**: "We can deliver X by Y if Z happens"
   - ❌ **Cannot Commit**: "We cannot deliver because..."
   - 🔬 **Needs Investigation**: "We need to research before committing"

3. **Address Non-Commitments** (3 minutes)
   - What would enable commitment?
   - Can scope be adjusted?
   - Can timeline be shifted?
   - Can resources be added?

**Documentation in Real-Time:**
```markdown
| Team | Component | Commitment | Conditions | Timeline | Notes |
|------|-----------|------------|------------|----------|-------|
| Mobile | UI Update | ✅ Full | None | Sprint 3 | |
| Backend | API v2 | ⚠️ Conditional | Need DBA resource | Sprint 2 | Hiring in progress |
| AI | ML Model | ✅ Full | None | Sprint 4 | |
```

#### Integration Planning (15 minutes)

**Integration Coordination:**

1. **Integration Points Review** (5 minutes)
   - Where do teams need to integrate?
   - What are the interface contracts?
   - When does integration testing happen?

2. **Mock/Stub Strategy** (5 minutes)
   - Who provides mocks and when?
   - What level of fidelity needed?
   - How to handle mock limitations?

3. **Integration Schedule** (5 minutes)
   - First integration test
   - Incremental integration milestones
   - Full system integration
   - Production deployment coordination

**Integration Timeline:**
```
Sprint 1: API contracts finalized
Sprint 2: Mocks available, parallel development
Sprint 3: First integration test
Sprint 4: Full system test
Sprint 5: Production deployment
```

#### Next Steps & Action Items (5 minutes)

**Clear Action Assignment:**

| Action | Owner | Due Date | Critical Path? |
|--------|-------|----------|----------------|
| Finalize API contracts | Backend Lead | 3 days | Yes |
| Create integration test plan | QA Lead | 1 week | Yes |
| Resolve DBA resource | Manager | 2 days | Yes |
| Schedule team kick-offs | Team Leads | This week | No |

**Next Meetings:**
- Team kick-offs: When?
- First integration checkpoint: When?
- Regular sync cadence: Weekly? Bi-weekly?

**Close with Clarity:**
```
"Let's confirm what we've agreed:
1. [Summarize key commitments]
2. [State major dependencies]
3. [Confirm next steps]

Meeting notes will be sent within 24 hours.
Please confirm your commitments via email within 48 hours.
Thank you for your collaboration!"
```

### 3. Post-Meeting Activities

#### Immediate (Within 2 Hours)

1. **Quick Debrief with Key Stakeholders**
   - What went well?
   - What concerns remain?
   - Any immediate escalations needed?

2. **Send Thank You & Summary**
   ```
   Subject: Thank You - Mission Alignment [Mission Name]

   Team,

   Thank you for productive alignment session.

   Key Outcomes:
   - X teams fully committed
   - Y conditions to resolve
   - Z next steps identified

   Full notes coming within 24 hours.
   ```

#### Within 24 Hours

1. **Distribute Complete Meeting Notes**
   - Use alignment-meeting-tmpl.yaml
   - Include all commitments
   - List all action items with owners
   - Attach updated dependency map

2. **Follow Up on Non-Commitments**
   - Schedule 1:1s with teams that couldn't commit
   - Work on resolution plans
   - Escalate if needed

3. **Update Mission Documents**
   - Revise PRD if scope changed
   - Update timeline based on commitments
   - Document any pivots or decisions

#### Within 48 Hours

1. **Get Written Confirmations**
   ```
   Subject: Please Confirm - Your Team's Mission Commitment

   [Team Lead],

   Per our alignment meeting, please confirm:

   Your team commits to:
   [List specific commitments]

   Timeline: [Dates]
   Conditions: [If any]

   Reply to confirm or correct.
   ```

2. **Resolve Open Items**
   - Chase down action items
   - Schedule follow-up meetings
   - Clear blockers identified

3. **Kick Off Team Planning**
   - Teams begin creating team PRDs
   - Start breaking down epics
   - Begin sprint planning

### 4. Facilitation Techniques

#### Managing Dynamics

**The Dominator:**
- Use explicit turn-taking
- "Let's hear from teams we haven't heard from"
- Private message: "Great points - let's get others' input"

**The Silent Team:**
- Direct questions: "[Name], what's your team's view?"
- Break into smaller groups
- Follow up 1:1 after meeting

**The Pessimist:**
- Acknowledge concerns: "Valid point, let's document that risk"
- Focus on solutions: "What would address that concern?"
- Time-box negativity

**The Over-Committer:**
- Reality check: "Let's verify capacity"
- "What would you de-prioritize for this?"
- Document assumptions explicitly

#### Keeping Energy Up

- Take a 5-minute break at 45 minutes
- Stand up for dependency mapping
- Use humor appropriately
- Celebrate agreements vocally
- Keep visible progress tracker

#### Managing Conflict

**When Teams Disagree:**
1. Clarify the disagreement precisely
2. Find common ground first
3. Explore win-win options
4. Escalate if needed (but rarely)
5. Document disagreement and path forward

**When Resources Are Contested:**
1. Return to mission priorities
2. Look for creative solutions
3. Consider phasing or alternating
4. Escalate to leadership if critical

### 5. Success Metrics

**Immediate Success Indicators:**
- 80%+ teams gave firm commitments
- All critical dependencies identified
- No unresolved blocking issues
- Clear next steps for all teams
- Positive energy leaving meeting

**Follow-Up Success Indicators:**
- Written confirmations received within 48 hours
- Team PRDs created within 1 week
- No surprise blockers in first sprint
- Integration points clearly defined
- Teams report clarity on their scope

### 6. Common Pitfalls

**Avoid These Mistakes:**

❌ **Forcing Commitment**
- Pressuring teams to commit when not ready
- Better to identify issues now than fail later

❌ **Solving Everything**
- Trying to resolve all issues in meeting
- Focus on alignment, solve details later

❌ **Poor Time Management**
- Letting one topic dominate
- Stick to agenda, use parking lot

❌ **Vague Commitments**
- "We'll do our best"
- Get specific deliverables and dates

❌ **Missing Documentation**
- Relying on memory
- Document everything in real-time

❌ **Skipping Follow-Up**
- Assuming everyone's aligned
- Always get written confirmation

### 7. Contingency Planning

**If Key People Missing:**
- Reschedule if critical mass not present
- Or focus on what you can align on
- Schedule follow-up for missing pieces

**If Major Blocking Issue Surfaces:**
- Document the blocker clearly
- Assign owner to resolve
- Schedule follow-up alignment
- Proceed with what you can

**If Meeting Runs Over:**
- Ask for 15 more minutes consent
- Or schedule immediate follow-up
- Prioritize commitments if time limited

**If No Consensus Reached:**
- Document different positions
- Escalate to executive sponsor
- Schedule decision meeting
- Pause mission if necessary

## Templates and Tools

**Meeting Artifacts:**
- alignment-meeting-tmpl.yaml - Documentation template
- commitment-matrix.xlsx - Track commitments
- dependency-map.miro - Visual dependencies
- action-tracker.md - Follow-up items

**Communication Templates:**
- pre-read-email.md
- confirmation-request.md
- meeting-summary.md
- escalation-template.md