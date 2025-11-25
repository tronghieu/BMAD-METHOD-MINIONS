# Retrospective Guide

This guide provides the methodology for preparing and facilitating a productive post-release retrospective. It is intended for use by the `Release Manager` when executing the `conduct-retrospective` task.

## Purpose
A retrospective is a formal meeting for the release team to reflect on the completed release process. The goal is not to assign blame but to learn from experience, celebrate successes, and create concrete, actionable improvements for the next release. It is the engine of continuous improvement.

## Core Principles
- **Blamelessness:** We focus on improving processes, not on blaming individuals. Assume everyone did their best with the information and resources they had at the time (The Prime Directive).
- **Action-Oriented:** The primary output must be a short list of specific, actionable, and assigned improvement items.
- **Data-Driven:** The discussion should be grounded in objective data (metrics, timelines, incident reports), not just feelings or anecdotes.
- **Forward-Looking:** While we discuss the past, the goal is to improve the future.

## Retrospective Phases

### Phase 1: Preparation (Before the Meeting)
A great retrospective starts with great preparation. The facilitator must gather all relevant data to provide context for the discussion.
- **Gather Metrics:** Collect all quantitative data from the release:
  - **Timeline Data:** Planned vs. actual duration for each phase.
  - **Quality Metrics:** Final test coverage, security vulnerabilities, performance benchmarks.
  - **Incident Data:** Number of incidents, rollbacks, or hotfixes required.
  - **User Impact:** Support ticket volume, user sentiment, business metric changes.
- **Review Documents:** Read through the `release-plan.md` and its `execution-log` to recall what was planned versus what actually happened.
- **Collect Async Feedback:** Send out a simple, anonymous pre-retrospective survey to allow team members to collect their thoughts beforehand.

### Phase 2: Facilitation (During the Meeting)
The facilitator's job is to guide the conversation, ensure everyone is heard, and keep the meeting focused and productive. A typical structure includes:
1.  **Set the Stage (5 min):** Welcome the team, state the purpose, and review the Prime Directive to establish psychological safety.
2.  **Review Release Summary (5 min):** Present the objective data gathered during preparation to ground the conversation in facts.
3.  **What Went Well? (20 min):** Start on a positive note. Go around the room and have everyone share one success or something they appreciated. This reinforces good practices.
4.  **What Could Be Improved? (25 min):** Discuss challenges, friction points, and things that went wrong. Use techniques like the "5 Whys" to dig for root causes rather than just identifying symptoms.
5.  **Action Items (20 min):** This is the most important part. Collaboratively brainstorm and then vote on the top 3-5 most impactful action items. For each item, ensure it is **SMART** (Specific, Measurable, Achievable, Relevant, Time-bound) and has a clear owner.
6.  **Celebrate Wins (5 min):** End the meeting by recognizing the team's hard work and celebrating the successful release.

### Phase 3: Follow-Up (After the Meeting)
The work isn't done when the meeting ends.
- **Document and Share:** Finalize the retrospective notes and action items using the `retrospective-plan.yaml` template. Share the summary with all stakeholders.
- **Track Action Items:** Add the action items to the team's regular work backlog (e.g., as tickets in Jira).
- **Review at Next Retro:** Begin the next retrospective by reviewing the action items from the previous one. This creates a culture of accountability and ensures the cycle of improvement continues.
