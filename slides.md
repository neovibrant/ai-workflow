# How to Use AI for **Vibe Coding**

### Context, workflow, and keeping the agent useful

Note:
Use `workflow.md` as the shareable keynote/source notes.

---

# Context Is Key

The whole job is to build the right context for the task.

--

## The Context Balance

The AI needs:

- enough context to make good decisions
- not so much context that it gets distracted

--

## Why Too Much Context Hurts

- Context windows are limited
- Larger context can lower quality
- Irrelevant detail pushes the agent in unexpected directions

--

## The Shy Engineer Analogy

Imagine a very good engineer who just joined your business.

They learn quickly, but they do not know what matters yet.

They may avoid asking questions and make assumptions instead.

---

# Basic Context

Brief, always-on context for every task.

Put this in `AGENTS.md`.

---

# Wider Context

Keep detailed knowledge separate and pull it in only when needed.

Product. Tech. Design. Process.

--

## Need-To-Know Context

Do not paste everything into every prompt.

Reference the specific doc, ticket, or artifact the task needs.

```text
/Product/product-vision.md
/Tech/tech-stack.md
/Design/brand-identity.md
```

--

## Wider Context Evolves

As decisions are made, the context should grow.

If you repeat yourself to the agent, document it.

---

# Code Context

The agent does not load all code at once.

It searches the codebase with tools.

--

## Code Signposting

Help the agent find the right code faster.

- what each repo is for
- where major systems live
- project-specific patterns
- where deeper technical docs are kept

---

# Coding Flow

The flow is:

Spec -> solution -> implementation -> review -> workflow update

--

## The `/iterate` Skill

Make the agent ask questions and raise concerns.

```md
Ask yourself: "Do I have any questions or concerns?"

If yes:
- present them to the user
- collect clarifications
- ask yourself again

Only then proceed.
```

--

## Start With The Spec

Begin from the product perspective.

Create a PRD, ticket, epic, or markdown spec before coding.

--

## Solution Design

Ask the agent to design the implementation before writing code.

The output should be detailed enough for another agent to execute.

--

## Testing Is Part Of The Solution

Do not bolt testing on at the end.

Include:

- expected outcomes
- quality checks
- security concerns
- manual checks when automation is not enough

--

## Implementation

Give the agent the spec and solution docs.

Then let it execute with the right context.

--

## Review And Test

Ask the agent to review its own work and run tests.

If it cannot verify something, it should ask you for evidence.

---

# Improve The Workflow

After the work is done, improve the system.

- update reusable context
- extract useful skills
- clean up temporary docs
- keep the workflow repeatable

---

# Questions?
