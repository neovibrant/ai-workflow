# Building Technology Products with AI

Context is key.
- we need to make sure the AI has the full context
- we need to make sure the AI hasn't got context it doesn't need

The second is important because:
- irrelevant context fills the context (which is limited) and running with a larger context gives us lower quality
- irrelevant context confuses the AI and prompts it to go in unexpected directions

The entire effort is to build just the right context for running a task.

One way to imagine this is that you have a really good software engineer who has just joined your business and has no clue what's going on. They are very good and can learn very quickly. At the same time, they are very shy and avoid taking any action that might cause you any discomfort. For example, they prefer to make assumptions instead of bothering you with questions.

## Basic context

Give basic context about what you are doing. What your project is about and where you are with it, but be very brief about this. Keep in mind this basic context will go in every prompt, so you want to keep it high level.

This will generally go in `AGENTS.md`—the file the agent will load into context as the very first thing.

## Deeper and wider context

Presumably, your project will have all sorts of resources: ideas, product requirements, technical decisions and some other types of things like philosophies that you think will make you more effective. They all need to be documented in detail, but in a way that can be invoked and entered into context on a need-to-know basis.

Separate them in different folders like:

```
/
--> Product
 |-> product-vision.md
 |-> feature-xyz.md
--> Tech
 |-> tech-stack.md
 |-> automated-testing-strategy.md
--> Design
 |-> brand-identity.md
 |-> logo.png
```

When you're working on a particular task, you can invoke some of these files in the prompt like:

> @brand-identity.md mentioned we need to update the accent colour to #900aff, let's see where in the FE this would need an update.

Make sure this context is kept in separate files (or artifacts, like wiki pages, or tickets, or whatever) so that you can reference them when you need to without adding unnecessary things into the context.

### The wider context is a growing thing

As product and tech evolve and decisions are made, features are added and so on, this `Wider Context` also grows. Make sure to keep it updated as you go along.

## Code context

The agent won't load all your code into the context, instead it will use tools to search it. So this means you can simply make it all available to it.

It's advisable to have the agent run in such a way that it can access several repositories (usually you'll have more than 1) and add a few things about them in the `Basic Context`. This is called `Code Signposting`.

### Code Signposting

Add some information about the code so that the agent can find things. Briefly explain what the tech stack is (and explain where it can find detailed info about it in the `Wider Context` so that it can fetch it, but only if it's needed). Explain some of the patterns of the code, especially those that are specific to your project. Explain the role of several repositories and so on.

This is also something that you'll need to tweak as you go along, as projects are different and they have their own specific things.

## Coding flow

> The critical piece is to encourage the agent to **ask questions** and **raise concerns**.

### Iterate skill

Create an `/iterate` skill. You can do it yourself, this is best because then you can tweak it based on your preference and personal style of work.

Example:

```md
---
name: iterate
description: Use when the user says iterate or wants iterative clarification before work; derive the topic from text or context, then question until clear.
---

# Iterate

Derive the work from the user's text or current context.

If unclear, ask: "What are we working on?"

Once known, ask yourself: "Do I have any questions or concerns?"

If yes:
- present them to the user
- collect clarifications
- ask yourself again

Repeat until the answer is "No."

Only then proceed.
```

You will use this skill almost everywhere.

### Start with the spec (or PRD)

Start from the Product perspective and give context about the feature that needs building. Ask the agent to create a PRD or a md file in the Product folder or a Jira ticket (or whatever you're using) and explain what needs to be built. Explain to it what needs to be built and iterate on creating a detailed spec until all details are worked out.

Use `/iterate` to explore the edge cases and implications of what you are speccing.

The spec will probably cover several coding tasks (i.e. tickets). If you use Jira or similar, this will probably be an epic.

When the iteration is complete, the agent will have created a document (md file, epic description, wiki page etc) that details the spec. It must be written in detail and cover all the edge cases and decisions made, but there is no need to explain **how** the decisions were made (that's TMI).

### Solutionising

This is the stage where the spec is given and the model is asked to design a solution to it. It will go into detail about the code that it needs to write, but it will not really write anything.

In many coding tools, this is called the Plan mode or the Plan agent.

Example prompt:

> Let's document a solution for implementing `@your-spec-doc.md`. Use the `/iterate` skill to clarify the detail and at the end you must produce a detailed technical document for a software engineer (or AI agent) to pick up and know exactly how to implement the spec correctly. Save the document in the `@your-tech-detail-doc.md`.

The key is to use `/iterate` again to clarify everything and guide the agent towards the desired solution.

If you are not very experienced at coding, focus on testing outcomes and following engineering standards and good practices as well as ensuring quality and security. Just prompt it in this direction any time you have doubts or are unsure. This usually gives a good outcome.

At the end, the agent should create a document detailing the solution. This needs to be in such detail that an agent can pick it up and implement it without having any questions.

Sometimes it's a good idea to prompt the agent to validate that the document is in such a state of detail that another agent can pick it up and work on it without having any questions.

#### Testing

Remember that testing quality is part of the solution. Remind the agent about it too. Actually, this is so important that it should likely be part of your `AGENTS.md`.

### Implementing 

Give the agent the 2 documents created above, it should be enough to implement the entire feature, unattended.

In some cases, where the feature is more complex, you can do this in attended mode, following through directly from the conversation above and keeping the context. This will allow you to add things to the context, request changes, challenge the direction the agent is taking, remind them of different things they may have overlooked.

### Review and test

You should ask the agent to review the code and test it.

If it can't test certain things, it should guide you to test it and ask for results (i.e. screenshots).

You should review the code (if you are able to) and make any suggestions.

Avoid manually writing code when the goal is to improve your AI workflow. Get into the habit of guiding the agent instead.

### Process update

After everything is done, reflect on patterns that would be repeatable and could be automated.

- Was there anything that I told the agent that could be documented in the basic/wider context so that it can find it itself next time?
- are there any skills that I can extract from this in order to improve my workflow?

If yes, don't forget the agent can help you with it. It can create skills, update docs etc

### Cleanup

Cleanup docs that won't be needed anymore. Usually the solutions can go or you can ask the agent to summarise and keep the shortened version of it.

## AGENTS.md

Sometimes called `CLAUDE.md` is the most important file in your project! Tweak it and also tweak your interaction with the agent.

Here are some ideas:

```
Be brief and to the point. When generating documents, make all the possible effort to keep them **short**.

When asked a question, don't rush to conclusions, prefer to search the web for things you're not sure of. Validate your own knowledge whenever possible and practical.

Think before you answer, but make sure you don't think for too long or go in circles before coming back with an answer, use a tool or ask a question.

Before making changes, engage in discussion upfront. Do not rush into changing files, code, or documents.

Think and brainstorm before touching files. Make a plan, clarify open questions, provide feedback on the request, challenge assumptions when needed, and ask as many questions as needed upfront.
```

There are some more involved techniques out there to prevent slop, use them as slop will kill your time!

## Project structure

Don't run the agent in 1 repo if you have more repos. Have a master AI agent repo with instructions and skills and add the code repos into that folder locally.
