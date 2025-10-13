# Assumption Mapping Checklist

Use this checklist to identify, categorize, and prioritize assumptions before building a prototype. The goal is to ensure your prototype is designed to test the most critical and uncertain assumptions.

## 1. Brainstorm Assumptions

- [ ] **List all assumptions:** Write down every belief you have about your users, the problem, and your proposed solution. Don't filter yet.
- [ ] **User Assumptions:** What do you assume users need, want, or do? (e.g., "Users will understand this icon.")
- [ ] **Problem Assumptions:** What do you assume about the nature of the problem? (e.g., "The main problem is speed, not discoverability.")
- [ ] **Solution Assumptions:** What do you assume about your solution's effectiveness? (e.g., "This feature will solve the user's problem.")
- [ ] **Business Assumptions:** What do you assume about the business viability? (e.g., "Users will be willing to pay for this.")

## 2. Categorize Assumptions (The 2x2 Matrix)

For each assumption, place it into one of the four quadrants.

### Quadrant 1: High Importance / High Uncertainty (Critical Risks)
*These are your most important assumptions to test. Your project's success depends on them.*
- [ ] Identify the 2-3 most critical, riskiest assumptions.
- [ ] **Action:** These MUST be the primary focus of your prototype and testing plan.

### Quadrant 2: High Importance / Low Uncertainty (Known Facts)
*These are your core beliefs that you are confident in.*
- [ ] List the assumptions you consider to be well-supported by evidence.
- [ ] **Action:** You don't need to test these extensively, but confirm they are truly low-uncertainty.

### Quadrant 3: Low Importance / High Uncertainty (Secondary Risks)
*These are interesting but not critical to the core concept.*
- [ ] Identify assumptions that are highly uncertain but would not derail the project if wrong.
- [ ] **Action:** Deprioritize testing these. Keep them in a "parking lot" to explore in later iterations if they become more important.

### Quadrant 4: Low Importance / Low Uncertainty (Trivial Facts)
*These are things you know to be true but that have little impact on the project's success.*
- [ ] List any assumptions that fall into this category.
- [ ] **Action:** Ignore these for now.

## 3. Formulate Testable Hypotheses

For each assumption in Quadrant 1 (Critical Risks), rephrase it as a testable hypothesis.

**Format:** "We believe that [assumption]. We will know we are right if we see [observable user behavior or metric]."

- [ ] **Hypothesis 1:** (e.g., "We believe users will understand the 'swoosh' icon represents sending a message. We'll know we're right if 80% of test participants can send a message without hesitation.")
- [ ] **Hypothesis 2:** (e.g., "We believe users are willing to complete a 5-step setup process. We'll know we're right if the drop-off rate during the prototype's setup flow is less than 15%.")
- [ ] **Hypothesis 3:** ...

## 4. Link Hypotheses to Prototype Features

- [ ] For each hypothesis, identify the specific feature or part of the prototype that will test it. (e.g., "Hypothesis 1 will be tested by the chat interface in the prototype.")
- [ ] Ensure your `plan-prototype-strategy.md` explicitly calls for building these features.
- [ ] If a critical hypothesis cannot be tested with the current prototype plan, flag it as a major risk.

## Final Review

- [ ] Have you identified at least 2-3 critical, high-uncertainty assumptions?
- [ ] Have you converted them into specific, testable hypotheses?
- [ ] Is your prototype plan designed to test these specific hypotheses?
