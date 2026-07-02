---
name: vibe-coding-prd
description: Turn requirements, rough PRDs, competitor analysis, or Lark/Feishu document inputs into a concise Markdown PRD that can be sent directly to Claude Code, Codex, or another coding agent. Use when the user says "帮我写一个用来vibe coding的PRD" or asks to produce a coding-ready Vibe coding PRD from unclear ideas, clear product needs, raw PRDs, competitive research, or implementation-oriented planning material.
---

# Vibe Coding PRD

Create a concise, coding-agent-ready PRD from user requirements, raw PRDs, competitor analysis, or linked source documents. The output should help Claude Code/Codex build the product with minimal extra interpretation.

## Core Rules

- Do not invent the user's intent. If the target user, scenario, pain point, product form, priority, or core workflow is unclear, ask before drafting.
- Prefer `request_user_input` for confirmation when it is available. Use short multiple-choice questions. If no UI confirmation tool is available, ask structured choices in chat and wait.
- Keep the PRD lean. Remove business-value narration, market background, rhetorical framing, stakeholder reporting language, and vague adjectives.
- Write for a coding agent: concrete screens, states, data, workflows, tools, prompts, acceptance criteria, and out-of-scope items matter more than persuasion.
- Do not finish with a PRD until the user has confirmed feature scope, MVP priority, technology direction, and core prototype structure.

## Input Triage

Classify the user's input before designing:

1. **Clear requirement**: has a recognizable user, scenario, pain point, and desired outcome. Proceed to clarify product form and scope.
2. **Raw PRD**: looks like an engineer-facing PRD, spec, or planning document. Extract only what a coding agent needs: users, workflows, features, data, permissions, integrations, constraints, edge cases, and acceptance criteria.
3. **Competitor analysis**: describes other products, feature comparisons, screenshots, reviews, or market observations. Convert observations into user needs and candidate features, then ask the user which direction to adopt.
4. **Unclear input**: missing the real user need or product goal. Stop and guide the user with multiple-choice questions.

If the input contains a Feishu/Lark document URL or token, use the `lark-doc` skill to fetch the document before triage. If the document contains embedded sheets, bases, or other resources, follow `lark-doc` routing instructions only when those resources are necessary to understand the product requirements.

## Clarification Workflow

Ask the minimum number of questions needed to avoid guessing. Prefer grouped choices that materially change the PRD.

For unclear input, ask for:

- Target user: who will use it.
- Scenario: when and where they use it.
- Pain point: what problem is painful today.
- Product form: web app, mobile app, browser extension, bot, automation, internal tool, API, plugin, or other.
- Desired outcome: what should be true after the product works.

For clear input or raw PRDs, confirm:

- MVP scope versus later scope.
- Feature priority order.
- Must-use or must-avoid technology constraints.
- Whether the product is AI-heavy or traditional software.
- Core screens or flows to include in the first version.

## Design Workflow

Once the need is clear, work through these steps in order.

### 1. Define The Requirement

State:

- Who the product is for.
- What scenario it serves.
- What pain point it solves.
- What product form will be built.
- What outcome counts as success.

### 2. Build The Feature List

Create a table with:

- Level 1 module.
- Level 2 feature.
- Feature description.
- Recommended priority: MVP, V1, or Later.
- Reason for priority.

Ask the user to confirm what to do, what not to do, what to defer, and whether the priority order is correct. MVP priority should favor the shortest path to a usable product that proves the core workflow.

### 3. Recommend The Tech Stack

Recommend a stack based on product size, complexity, implementation timeline, and user skill level. Explain in plain language.

Include:

- Frontend or client choice.
- Backend or automation runtime choice.
- Data storage choice.
- AI/model/tooling choice when relevant.
- Deployment choice.
- Why this stack is recommended.
- Simpler alternative, only if the tradeoff is meaningful.

Do not overwhelm non-technical users with exhaustive options. Make a clear recommendation and ask for confirmation.

### 4. Draft The Wireframe Prototype

Design framework-level wireframes for the core screens or flows. Use compact ASCII layout, Mermaid, or structured screen descriptions.

Include:

- Main navigation or entry points.
- Primary screen layout.
- Core user actions.
- Empty, loading, success, and error states when relevant.

Ask the user to confirm the prototype before writing detailed modules.

### 5. Detail Functional Modules

For AI products, include:

- Agent workflow: trigger, planning, tool use, memory/context, output, fallback.
- Prompt design: system role, user input variables, output format, guardrails.
- Tool system: tool name, purpose, inputs, outputs, failure handling.
- Human confirmation points.

For traditional products, include:

- User flows.
- Data model or key entities.
- API/interface expectations.
- Permissions and roles.
- State handling and edge cases.
- Integration points.

### 6. Write Acceptance Criteria

Every feature must have concrete, testable acceptance criteria. Use observable behavior.

Good:

- "Clicking `Create project` opens a modal with name, description, and visibility fields."
- "When required fields are empty, clicking `Save` shows field-level error messages and does not create a record."
- "After successful generation, the PRD appears in the preview area and the export button becomes enabled."

Bad:

- "Experience is smooth."
- "The page is user-friendly."
- "The AI understands the user well."

## Output Format

Output one complete Markdown PRD. Use this structure unless the user requests a different one:

```markdown
# [Product Name] Vibe Coding PRD

## 1. Requirement Definition
- Target user:
- Scenario:
- Pain point:
- Product form:
- Success outcome:

## 2. MVP Scope And Priority
| Priority | Module | Feature | Description | Build Now? | Notes |
|---|---|---|---|---|---|

## 3. Recommended Tech Stack
| Layer | Recommendation | Why |
|---|---|---|

## 4. Prototype Wireframe
[Core screen structure and main flow]

## 5. Detailed Functional Design
### 5.1 [Module Name]
- User flow:
- Data/state:
- Edge cases:
- For AI products: agent workflow, prompts, tools, fallback:

## 6. Acceptance Criteria
### [Feature Name]
- [Concrete, testable criterion]

## 7. Out Of Scope
- [Explicitly deferred or excluded work]

## 8. Open Questions
- [Only questions that remain unresolved after confirmation]
```

Keep the final PRD concise, implementation-oriented, and free of unconfirmed assumptions.
