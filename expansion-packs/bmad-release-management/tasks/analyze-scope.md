# Task: Analyze Release Scope

**Release Management Phase**: Planning
**Duration**: 30-60 minutes
**Agent**: Scope Analyzer
**Difficulty**: Medium

## Purpose

To systematically review all completed work and produce a clear, evidence-based recommendation for the release scope.

## Prerequisites

- Access to the project's git repository and issue tracker.
- The version/tag of the last release has been identified.
- The `scope-analysis-checklist.md` is available.

## High-Level Process

As the Scope Analyzer, your goal is to produce a definitive list of items to be included in, and deferred from, the release. Use the `checklists/scope-analysis-checklist.md` to guide your work and refer to `data/scope-analysis-guide.md` for detailed methodology.

### 1. Gather Work Items
- [ ] Systematically review git history, the issue tracker, and pull requests to build a comprehensive list of all potential work items. Follow the "Gather Work Items" phase in the guide.

### 2. Categorize and Assess
- [ ] For each item, assign a category (Feature, Fix, etc.) and assess its readiness against the "Definition of Done". Follow the "Categorize Changes" and "Assess Readiness" phases in the guide.

### 3. Analyze Dependencies
- [ ] Map all dependencies between work items to ensure a viable release. Follow the "Identify Dependencies" phase in the guide.

### 4. Formulate Recommendation
- [ ] Apply the inclusion criteria from the guide to create a final recommendation.
- [ ] Assess the overall balance of the scope (not too big, not too small).
- [ ] Prepare a clear list of items to **INCLUDE**, items to **DEFER** (with reasons), and any items that require further **DISCUSSION**.

### 5. Document and Review
- [ ] Document your findings and recommendations clearly.
- [ ] Present the recommended scope to the Release Manager, Product Owner, and Engineering Lead for final sign-off.

## Expected Outputs

- A **Scope Analysis Report** containing:
  - A definitive list of items (features, fixes) recommended for inclusion.
  - A list of items recommended for deferral, with clear reasons.
  - A list of any identified dependencies or risks associated with the proposed scope.

## Related Resources
- **Execution Checklist**: `checklists/scope-analysis-checklist.md`
- **Methodology Guide**: `data/scope-analysis-guide.md`
- **Supporting Data**: `data/changelog-conventions.md`
