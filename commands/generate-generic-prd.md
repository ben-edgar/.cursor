---
name: Generate PRD (Generic)
description: Create a user-centered PRD with clear grouping and non-technical language.
parameters:
  - name: product_name
    type: string
    required: false
    description: Product or project name (e.g., "Acme App")
  - name: feature_name
    type: string
    required: true
    description: Short, human-readable feature name (e.g., "Smart Reminders")
  - name: target_audience
    type: string
    required: false
    description: Primary users and empathy notes
  - name: problem_statement
    type: string
    required: false
    description: What user problem are we solving and why now?
  - name: goals
    type: string
    required: false
    description: Top 3–5 outcomes this feature should achieve
  - name: non_goals
    type: string
    required: false
    description: Explicitly out-of-scope items to prevent scope creep
  - name: background_research
    type: string
    required: false
    description: Links or notes from research, market analysis, user interviews
  - name: user_personas
    type: string
    required: false
    description: Persona list or notes
  - name: user_stories
    type: string
    required: false
    description: Optional pre-written user stories (one per line)
  - name: primary_flows
    type: string
    required: false
    description: Key user flows (one per line; ordered)
  - name: constraints
    type: string
    required: false
    description: Business, legal, privacy, platform, or device constraints
  - name: success_metrics
    type: string
    required: false
    description: Leading and lagging indicators (e.g., completion rate, retention)
  - name: ai_agent_scope
    type: string
    required: false
    default: None
    description: None | Assistance | Autonomous tasks (optional)
  - name: risks
    type: string
    required: false
    description: Top risks and mitigations
  - name: stakeholders
    type: string
    required: false
    description: Product, Design, Eng, Data, Legal, Marketing
  - name: timeline
    type: string
    required: false
    description: Key milestones and proposed release window
  - name: references
    type: string
    required: false
    description: Useful links or internal docs
---

You are a senior product manager. Generate a clear, user-first PRD in Markdown. Keep language non-technical and focused on user experience. Do not reference code, classes, APIs, or file names. Group requirements logically. Prefer concise bullets, bold keywords, and scannable sections. If there is a selection present, treat it as additional notes. Merge selection with inputs.

Inputs:
- Product: {{product_name}}
- Feature: {{feature_name}}
- Audience: {{target_audience}}
- Problem: {{problem_statement}}
- Goals: {{goals}}
- Non-goals: {{non_goals}}
- Research: {{background_research}}
- Personas: {{user_personas}}
- Stories: {{user_stories}}
- Flows: {{primary_flows}}
- Constraints: {{constraints}}
- Metrics: {{success_metrics}}
- AI Scope: {{ai_agent_scope}}
- Risks: {{risks}}
- Stakeholders: {{stakeholders}}
- Timeline: {{timeline}}
- References: {{references}}

Also incorporate relevant ideas from the current selection if provided:
{{selection}}

Write the PRD using only '##' and '###' headings.

## Product Requirements Document (PRD)

### Executive Summary
- **Product**: {{product_name}}
- **Feature**: {{feature_name}}
- **One-liner**: What it is in plain language.
- **Target audience**: {{target_audience}}
- **Problem we solve**: {{problem_statement}}
- **Why now**: Brief rationale (market/user insight/opportunity).
- **AI involvement**: {{ai_agent_scope}} (if applicable).

### Background and Research
- **Context**: Summarize relevant research and insights.
- **User insights**: Pain points and motivations.
- **Market/benchmark**: Comparable patterns worth adopting or avoiding.
- **References**: {{references}}
- **Notes**: {{background_research}}

### Objectives
- **Goals**: 3–5 outcome-oriented goals. {{goals}}
- **Non-goals**: What is explicitly out of scope. {{non_goals}}
- **Success metrics**: Leading/lagging indicators and how we’ll measure. {{success_metrics}}

### Users and Use Cases
- **Personas**: {{user_personas}}
- **Core use cases**:
  - Describe the top tasks users want to accomplish.
  - Emphasize convenience, clarity, and repeat engagement.

### Feature Description
- **Narrative**: What this feature enables, from the user’s perspective.
- **Key capabilities**:
  - List main capabilities and outcomes (avoid technical details).
- **Content considerations**:
  - Tone, prompts, microcopy, personalization.

### User Stories
If provided, incorporate; otherwise propose. Format:
- As a [user], I want [goal] so that [benefit].
- Add acceptance hints (what “good” looks like), not technical steps.
{{user_stories}}

### User Flows
Provide 2–4 essential flows. Each flow should be stepwise and succinct.
{{primary_flows}}

### Non-Functional Requirements (User-Centric)
- **Performance**: Feels instant; no noticeable delays. Median interactions < 100ms; p95 < 300ms (product-level target).
- **Visual stability**: No flicker on refresh or during updates.
- **Delight**: Micro-interactions feel polished and reassuring.
- **Accessibility**: Legible typography and contrast; supports assistive tech.
- **Themes**: Works in light and dark modes (if applicable).
- **Privacy and trust**: Clear data use; simple export/delete controls.
- **Localization**: Copy and formats adaptable to multiple locales.

### AI Agent Considerations (Optional)
- **Scope**: {{ai_agent_scope}} — where the agent appears and what it can/cannot do.
- **User promises**: How the agent helps (e.g., suggest prompts, summarize) without taking control away.
- **Quality bar**: Friendly tone; avoid hallucinations; gracefully decline when unsure.
- **Safety and privacy**: Handle sensitive content respectfully; explain storage; easy opt-out.
- **Feedback loops**: Lightweight rating and “was this helpful?” with routing.
- **Failure states**: Offer simple, human-friendly alternatives when the agent can’t help.

### Acceptance Criteria
Use behavior-focused, testable statements. Avoid technical implementation.
- When [scenario], the user can [task] and sees [expected outcome].
- Empty states guide action with helpful prompts.
- Errors are recoverable, with clear explanations and no dead ends.

### Dependencies and Assumptions
- **Dependencies**: Design input, analytics, notifications, app settings (as applicable).
- **Assumptions**: List any assumptions that, if wrong, change the plan.

### Risks and Mitigations
- **Engagement risk**: Users may not return → progressive disclosure, gentle nudges.
- **Complexity risk**: Too many options → defaults, sensible presets.
- **Privacy risk**: Sensitive data → clear controls and transparent copy.
{{risks}}

### Rollout and Measurement
- **Phased rollout**: Internal, beta, GA with criteria for each stage.
- **KPIs**: Primary and guardrail metrics (define ownership and cadence).
- **Instrumentation**: Describe events at a high level (no code).

### Launch Plan
- **Stakeholders**: {{stakeholders}}
- **Timeline**: {{timeline}}
- **GTM notes**: Messaging, screenshots, FAQ updates.

### Out of Scope
- Clarify items deferred to future milestones to keep focus.

### Open Questions
- Capture decisions needed to proceed and owners.

### Version Control and Change Log
- Record notable changes to scope, requirements, or goals with dates.

### Appendix
- Wireframe notes, example prompts, tone/voice guardrails.
- Research summaries and anonymized quotes.
- Links to inspiration and competitive examples.

---

References for PRD best practices:
- [Product Requirements Documentation Best Practices: How to write actionable specs - NextSprints](https://nextsprints.com/blog/product-documentation-best-practices)
- [Product Compass - AI-Powered PRD Creation](https://www.productcompass.tech/blog/best-practices-effective-prds)
- [Product requirements document (PRD) template](https://type.ai/writing-templates/product-requirements-document-prd)
