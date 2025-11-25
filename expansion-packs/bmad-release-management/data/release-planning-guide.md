# Release Planning Guide

This guide provides a detailed, phase-by-phase methodology for creating a comprehensive release plan. It is intended to be used by the Release Manager agent during the execution of the `create-release-plan` task.

## Purpose

The goal of release planning is to create a single source of truth that aligns all stakeholders and guides the release from planning through deployment, monitoring, and retrospective. A thorough plan minimizes surprises and reduces deployment anxiety.

## Phase 1: Release Overview

This initial phase establishes the "who, what, why, and when" of the release.

#### 1.1 Determine Version Number
Consult with the user to determine the nature of the changes. Based on the changes, apply the appropriate versioning strategy as defined in `data/versioning-strategies.md`.
- **Breaking changes?** → MAJOR version bump (e.g., v1.5.2 → v2.0.0)
- **New backward-compatible features?** → MINOR version bump (e.g., v1.5.2 → v1.6.0)
- **Only bug fixes?** → PATCH version bump (e.g., v1.5.2 → v1.5.3)

#### 1.2 Define Release Type
Classify the release to set expectations for the process:
- **Major Release:** For breaking changes. Involves extensive planning and communication.
- **Minor Release:** For new features. The standard, most common workflow.
- **Patch Release:** For bug fixes. Can have a slightly streamlined process.
- **Hotfix:** For critical production emergencies. Uses a separate, expedited workflow.

#### 1.3 Establish Release Goals
Work with the product owner to define clear, measurable success criteria. What business or user goal does this release accomplish?
- *Example:* "Ship new payment integration to expand into the EU market."
- *Example:* "Reduce p95 response time for the main dashboard by 20%."

#### 1.4 Identify Stakeholders
List the key individuals and their roles for this release (Release Manager, Product Owner, Eng Lead, QA Lead, etc.).

#### 1.5 Set Target Date
Establish the target deployment window, considering any external commitments or deadlines. Avoid deploying on Fridays.

## Phase 2: Scope Analysis
The goal of this phase is to define exactly what is and is not included in the release. The `Scope Analyzer` agent should be invoked for a detailed analysis, using the `scope-analysis-checklist.md`.

- **Review Completed Work:** Check git history, closed issues/PRs, and project boards.
- **Categorize Changes:** Group items into Features, Bug Fixes, Breaking Changes, etc.
- **Assess Readiness:** Verify each item is complete, tested, and documented.
- **Document Scope:** Update the release plan document with lists of included and deferred items.

## Phase 3: Generate Changelog
Create a technical, commit-by-commit changelog. This is for developers and internal stakeholders.
- **Parse Git History:** Use `git log` and conventions (e.g., Conventional Commits) to generate a raw list.
- **Categorize Changes:** Group commits under standard headings (`Added`, `Fixed`, `Breaking Changes`, etc.) as defined in `data/changelog-conventions.md`.
- **Review and Edit:** Clean up the raw log, combine related commits, and rewrite messages for clarity.

## Phase 4: Write Release Notes
Transform the technical changelog into user-friendly release notes. This is a crucial communication task, often handled by the `Communication Specialist`.
- **Highlight Key Features:** Focus on the top 3-5 changes and explain their benefits to the user.
- **Document Breaking Changes:** Provide a clear, simple explanation of any breaking changes, the impact, and step-by-step migration instructions.
- **Write Upgrade Instructions:** Give users exact commands or steps to upgrade.
- **Document Known Issues:** Be transparent about any known bugs or limitations.

## Phase 5: Quality Assessment
This phase is owned by the `Quality Gatekeeper`. The goal is to get a formal "Go/No-Go" decision based on objective data.
- **Run Pre-Release Checklist:** Systematically go through `checklists/pre-release-checklist.md`.
- **Review Test, Security, and Performance Gates:** Document the status of all critical quality gates.
- **Make Go/No-Go Recommendation:** Based on the results, the Quality Gatekeeper recommends proceeding, stopping, or proceeding with documented risks.
- **Generate Document:** Create the `quality-assessment-plan.md` document.

## Phase 6: Deployment Planning
This phase is owned by the `Deployment Coordinator`. The output is a detailed, step-by-step runbook.
- **Select Deployment Pattern:** Choose the best strategy (Blue-Green, Canary, etc.) from `data/deployment-patterns.md` based on the release's risk profile.
- **Plan Database Migrations:** Detail the migration scripts, order, and rollback plan.
- **Define Rollback Procedures:** Document the exact triggers and steps for a rollback.
- **Create Deployment Steps:** Outline the entire deployment, phase by phase, with verification steps.
- **Generate Document:** Create the `deployment-plan.md` document.

## Phase 7: Communications Planning
This phase is owned by the `Communication Specialist`.
- **Plan Internal and External Communications:** Draft announcements for teams, stakeholders, and users.
- **Prepare Support Team:** Create a briefing document with FAQs and escalation paths.
- **Timeline:** Schedule all communications (e.g., "T-24h", "T-0", "T+1h").

## Phase 8: Monitoring Planning
Define how the release's success and health will be monitored post-deployment.
- **Define Key Metrics:** List the specific error, performance, and business metrics to watch.
- **Set Alert Thresholds:** Define what constitutes a "warning" vs. a "critical" alert for each metric.
- **Plan Monitoring Duration:** Specify the period of intensive monitoring (e.g., first 4 hours) and extended monitoring (e.g., 24-48 hours).

## Phase 9: Review and Finalize
- **Review the Plan:** Share the `release-plan.md` and all other generated documents with the full team for a final review.
- **Get Sign-Off:** Obtain formal approval from all key stakeholders.
- **Schedule Follow-up Sessions:** Book time for the deployment execution and the post-release retrospective.
