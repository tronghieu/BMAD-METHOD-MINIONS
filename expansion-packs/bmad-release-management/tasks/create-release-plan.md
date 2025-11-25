# Task: Create Release Plan

**Release Management Phase**: Planning
**Duration**: 60-120 minutes
**Agent**: Release Manager
**Difficulty**: Medium

## Purpose

To orchestrate the creation of a comprehensive set of release planning documents, serving as the single source of truth for the release. This task focuses on coordinating agents and processes to generate the required artifacts.

## Prerequisites

- [ ] Release goals are broadly understood.
- [ ] Work for the release is mostly complete.
- [ ] Key stakeholders (Product Owner, Eng Lead) are available for consultation.

## High-Level Process

This task follows a phase-based approach to ensure all aspects of the release are planned thoroughly. For detailed instructions on each step, refer to the **`data/release-planning-guide.md`**.

### 1. Establish Release Overview
- [ ] Determine the **Version Number** and **Release Type** (Major, Minor, Patch).
- [ ] Define and document the primary **Release Goals**.
- [ ] Identify and list all **Stakeholders**.
- [ ] Set a **Target Release Date** and deployment window.
- [ ] **Action**: Populate the `Release Overview` section of the `release-plan.yaml` template.

### 2. Define Scope
- [ ] **Action**: Invoke the **Scope Analyzer** agent (`*agent scope-analyzer`) to perform a detailed analysis.
- [ ] The Scope Analyzer will use `checklists/scope-analysis-checklist.md` to identify all completed work.
- [ ] Review the inclusion/deferral recommendations from the Scope Analyzer.
- [ ] **Action**: Populate the `Scope` section of the `release-plan.yaml` template.

### 3. Generate Changelog & Release Notes
- [ ] **Action**: Generate a technical **Changelog** from git history.
- [ ] **Action**: Invoke the **Communication Specialist** (`*agent communication-specialist`) to transform the changelog into user-friendly **Release Notes**.
- [ ] **Action**: Populate the `Changelog` and `Release Notes` sections of the `release-plan.yaml` template.

### 4. Coordinate Quality & Deployment Planning
- [ ] **Action**: Invoke the **Quality Gatekeeper** (`*agent quality-gatekeeper`) to perform the quality assessment and generate the `quality-assessment-plan.md` document.
- [ ] **Action**: Invoke the **Deployment Coordinator** (`*agent deployment-coordinator`) to create the `deployment-plan.md` (the runbook).
- [ ] Review the outputs from both agents to ensure alignment with the release goals.

### 5. Plan Communications & Monitoring
- [ ] **Action**: Work with the **Communication Specialist** to finalize the `Communications Plan`.
- [ ] **Action**: Define the `Monitoring Plan`, including key metrics and alert thresholds.
- [ ] **Action**: Populate the `Communications Plan` and `Monitoring Plan` sections of the `release-plan.yaml` template.

### 6. Finalize and Distribute
- [ ] Review all generated documents (`release-plan.md`, `quality-assessment-plan.md`, `deployment-plan.md`) for completeness and consistency.
- [ ] Obtain final sign-off from all stakeholders.
- [ ] Share the completed plans with the entire team.
- [ ] Schedule the deployment execution and the post-release retrospective.

## Expected Outputs
- A complete and approved `release-plan.md`.
- A complete and approved `quality-assessment-plan.md`.
- A complete and approved `deployment-plan.md`.

## Related Resources
- **Primary Guide**: `data/release-planning-guide.md`
- **Supporting Data**: `data/versioning-strategies.md`, `data/changelog-conventions.md`, `data/deployment-patterns.md`
- **Checklists**: `checklists/pre-release-checklist.md`, `checklists/scope-analysis-checklist.md`
