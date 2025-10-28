# BMAD Method Minions - Custom Expansion Packs

This repository contains custom expansion packs, or "Minions," designed to extend the capabilities of the [BMAD-METHOD](https://github.com/bmad-code-org/BMAD-METHOD), a universal AI agent framework.

## Table of Contents

- [About BMAD and Expansion Packs](#about-bmad-and-expansion-packs)
- [Our Custom Expansion Packs](#our-custom-expansion-packs)
- [Real-World Use Cases](#real-world-use-cases)
  - [Release Management](#release-management)
  - [Autonomous Teams Mission Orchestra](#autonomous-teams-mission-orchestra)
  - [Design Thinking Facilitator](#design-thinking-facilitator)
- [Installation](#installation)
  - [Step 1: Clone BMAD-METHOD](#step-1-clone-bmad-method)
  - [Step 2: Add Custom Expansion Packs](#step-2-add-custom-expansion-packs)
  - [Step 3: Install BMAD with Expansion Packs](#step-3-install-bmad-with-expansion-packs)

## About BMAD and Expansion Packs

The BMAD-METHOD™ is a powerful framework that uses collaborative AI agents for complex tasks. While its core is focused on software development, its true potential is unlocked through **Expansion Packs**.

Expansion packs allow BMAD to be adapted to virtually any domain by providing specialized agents, workflows, and knowledge bases. They keep the core framework lean while enabling deep expertise. You can learn more in the official [BMAD Expansion Packs Guide](docs/expansion-packs.md).

Our "Minions" are custom-built expansion packs designed to tackle specific, complex domains.

## Our Custom Expansion Packs

This repository contains three primary expansion packs:

-   **Autonomous Teams Mission Orchestra**
    *   **Description**: Extends BMAD Core to support cross-team coordination in federated repository architectures (e.g., microservices, monorepos). It provides specialized agents and workflows to manage "missions" that span multiple autonomous teams while maintaining their independence.
    *   **When to Use**: Use this pack when a feature or work item requires collaboration between several distinct teams (e.g., mobile, backend, AI, data science). It's ideal for planning large-scale features, managing microservices developed by different teams, and routing work in a complex, multi-repository environment.
    *   **[Read more about the Mission Orchestra Pack...](expansion-packs/bmad-autonomous-teams-mission-orchestra/README.md)**

-   **Design Thinking Facilitator**
    *   **Description**: A comprehensive toolkit that guides teams through the five phases of innovative, human-centered problem-solving: Empathize, Define, Ideate, Prototype, and Test. It combines BMAD's agentic planning with established design thinking principles.
    *   **When to Use**: Use this pack to tackle complex problems that require deep user understanding and creative solutions. It's suitable for new product development, service design, internal process improvement, or running focused innovation sprints.
    *   **[Read more about the Design Thinking Facilitator Pack...](expansion-packs/bmad-design-thinking-facilitator/README.md)**

-   **Release Management**
    *   **Description**: A comprehensive AI-powered framework for managing software releases following Agile methodologies. Five specialized agents guide teams through release planning, quality validation, deployment strategies, monitoring, and retrospectives—transforming releases from stressful chaos to predictable excellence.
    *   **When to Use**: Use this pack for managing regular software releases (sprints, monthly, quarterly), emergency hotfixes, or major version releases with breaking changes. It's ideal for Agile/DevOps teams seeking to standardize release processes, reduce deployment risk, and improve release predictability.
    *   **[Read more about the Release Management Pack...](expansion-packs/bmad-release-management/README.md)**

## Real-World Use Cases

Here are some examples of how you can use these "Minion" packs to solve complex, real-world problems.

### Release Management

This pack transforms software releases from anxious events into routine, predictable processes.

*   **Use Case: Standard Sprint Release**
    *   **Scenario**: Your Agile team completes a 2-week sprint with new features and bug fixes ready for production deployment.
    *   **How it helps**: The `Release Manager` (Trần Hưng Đạo) guides you through comprehensive release planning with versioning, changelog generation, and scope analysis. The `Quality Gatekeeper` (Lý Thường Kiệt) validates all quality gates (tests, security, performance), while the `Deployment Coordinator` (Võ Nguyên Giáp) plans deployment strategy (Blue-Green, Canary, or Rolling) with detailed rollback procedures. Post-deployment monitoring ensures issues are caught early, and retrospectives drive continuous improvement.

*   **Use Case: Emergency Hotfix**
    *   **Scenario**: A critical security vulnerability is discovered in production requiring immediate fix and deployment (2-8 hour window).
    *   **How it helps**: The `hotfix-release` workflow streamlines the process—validating only the fix, expedited quality gates, immediate deployment with monitoring, and post-mortem analysis. The `Rollback Checklist` ensures you can revert instantly if issues arise.

*   **Use Case: Major Version with Breaking Changes**
    *   **Scenario**: Your team is releasing v2.0.0 with API breaking changes requiring customer migration over 4-8 weeks.
    *   **How it helps**: The `major-release` workflow orchestrates the complex process—beta releases, staged deployment, comprehensive migration guides drafted by the `Communication Specialist` (Phan Bội Châu), extended monitoring periods, and phased customer communications. The `Scope Analyzer` (Nguyễn Trãi) ensures only fully-ready features are included, deferring anything incomplete.

### Autonomous Teams Mission Orchestra

This pack is designed for situations where multiple, independent teams need to collaborate on a single, large-scale objective.

*   **Use Case: Cross-Functional Feature Development**
    *   **Scenario**: You need to add a new payment processing feature that involves changes to the mobile app (iOS/Android team), the backend API (Backend team), and a fraud detection model (AI team).
    *   **How it helps**: The `Mission Orchestrator` agent facilitates a planning process to create a unified "Mission PRD." The `Triage Master` routes incoming tasks, and the `Integration Specialist` defines the API contracts between teams. Each team receives a specific handoff document, allowing them to work autonomously while staying aligned with the shared goal.

*   **Use Case: Managing a Microservices Architecture**
    *   **Scenario**: Your product is composed of dozens of microservices, each owned by a different team. A bug is reported that affects multiple services.
    *   **How it helps**: The `Triage Master` analyzes the bug report and identifies all affected teams and services. It then initiates a coordinated bug-fix mission, ensuring dependencies are managed and the fix is rolled out in the correct sequence across teams.

### Design Thinking Facilitator

This pack is your AI-powered guide for human-centered problem-solving, perfect for when you have a complex challenge but no clear solution.

*   **Use Case: New Product Development**
    *   **Scenario**: You have a broad idea for a new product but need to validate the problem and develop a solution that users will love.
    *   **How it helps**: The `DT Master` agent guides you through the full Design Thinking lifecycle. The `Empathy Researcher` helps you conduct user interviews to uncover deep insights. The `Ideation Coach` facilitates brainstorming sessions to generate creative solutions, and the `Prototype Builder` and `Test Analyst` help you create and validate a tangible prototype with real users.

*   **Use Case: Improving an Existing Service**
    *   **Scenario**: Customer satisfaction for your online support service is declining, and you need to understand why and redesign the experience.
    *   **How it helps**: Use the "Service Design" workflow. The agents will help you map the current customer journey, identify pain points through empathy research, ideate on new service touchpoints (e.g., a new chatbot, a better help center), and prototype the new service experience (e.g., through role-playing or mockups) before implementation.

*   **Use Case: Optimizing an Internal Business Process**
    *   **Scenario**: Your team's internal onboarding process for new hires is slow and inefficient, leading to frustration and delays.
    *   **How it helps**: Apply the "Process Improvement" workflow. The `Empathy Researcher` will treat your employees as users, interviewing them to find bottlenecks and pain points. The `Ideation Coach` will help the team brainstorm a streamlined future-state process, which you can then pilot with the `Prototype Builder` before a full rollout.

*   **Use Case: Tackling a Complex Strategic Question**
    *   **Scenario**: Your leadership team needs to decide on the company's strategic direction for the next three years, but the path forward is unclear.
    *   **How it helps**: Launch the "Strategy Workshop" workflow. The `DT Master` and `Problem Definer` help frame the strategic challenge. The agents then guide the team through market analysis, scenario brainstorming, and strategic option development, culminating in an actionable roadmap.

*   **Use Case: Validating a New Business Idea (for Business Owners)**
    *   **Scenario**: As a business owner or entrepreneur, you have a promising idea for a new product or service but need to validate its potential with real customers before committing significant time and capital.
    *   **How it helps**: The "Innovation Sprint" workflow is a 5-day process designed for this. The `DT Master` will guide you from mapping out the problem on Day 1 to testing a realistic prototype with target customers on Day 5. This allows you to get critical feedback on your core value proposition and business model in just one week, dramatically reducing the risk of building something nobody wants.

## Installation

This section guides you through the installation of our custom BMAD expansion packs.

### Step 1: Clone BMAD-METHOD

First, clone the core BMAD-METHOD repository from GitHub and navigate into the directory.

```bash
git clone https://github.com/bmad-code-org/BMAD-METHOD.git
cd BMAD-METHOD
```

### Step 2: Add Custom Expansion Packs

Next, you need to add our custom expansion packs to the `expansion-packs` directory. The easiest way is to clone this repository (`BMAD-METHOD-MINIONS`) and then copy the pack directories over.

Assuming you clone `BMAD-METHOD-MINIONS` next to `BMAD-METHOD`:

```bash
# From within the BMAD-METHOD directory:

# Copy the Autonomous Teams Mission Orchestra pack
cp -R ../BMAD-METHOD-MINIONS/expansion-packs/bmad-autonomous-teams-mission-orchestra ./expansion-packs/

# Copy the Design Thinking Facilitator pack
cp -R ../BMAD-METHOD-MINIONS/expansion-packs/bmad-design-thinking-facilitator ./expansion-packs/

# Copy the Release Management pack
cp -R ../BMAD-METHOD-MINIONS/expansion-packs/bmad-release-management ./expansion-packs/
```

After copying, your `expansion-packs` directory should contain:
- `bmad-autonomous-teams-mission-orchestra/`
- `bmad-design-thinking-facilitator/`
- `bmad-release-management/`

### Step 3: Install BMAD with Expansion Packs

Now, run the BMAD installation script from within the `BMAD-METHOD` directory. This will install dependencies and then launch the interactive installer.

```bash
npm install
npm run install:bmad
```

During the interactive installation process, make the following selections:

1.  When prompted for installation type, choose **"Install BMAD Core + Expansion Packs"**.
    *   **Note:** This is required for the Autonomous Teams Mission Orchestra pack, which depends on core BMAD components.

2.  From the list of available expansion packs, use the spacebar to select:
    - `[x] Autonomous Teams Mission Orchestra`
    - `[x] Design Thinking Facilitator`
    - `[x] Release Management`

3.  Follow the remaining prompts to specify your target project directory.

The installer will set up BMAD Core along with the selected custom expansion packs in your project.