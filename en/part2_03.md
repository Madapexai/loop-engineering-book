"Wait, let me first tell you about our project structure…"

"Our coding standards are like this…"

"The design philosophy of this module is…"

If you work with AI agents regularly, these words must sound familiar. Every time you start a new task, you spend a lot of time explaining project background, coding standards, design patterns to AI…

Then next time, with a new task, a new session, a new agent, you have to say it all over again from scratch.

That's the problem Skills solve.

### 6.1 What is a Skill?

A Skill is a mechanism for **codifying** project knowledge, workflows, and behavior patterns. It's not a one-time instruction written in a prompt — it's persistent knowledge that agents can load and use repeatedly.

Think of a Skill as an agent's "skill book." When an agent gets a skill book, it learns a new skill — it knows what to do in specific scenarios, what standards to follow, what tools to use.

### 6.2 The Difference Between Skills and Regular Prompts

Many people ask: Aren't Skills just longer prompts? What's the essential difference?

The difference lies in **three dimensions**:

| Dimension | Regular Prompt | Skill |
|-|-|-|
| Lifecycle | One-time, gone when session ends | Persistent, can be used repeatedly |
| Management | Scattered everywhere, hard to maintain | Centralized management, version control |
| Composition | Can only be linearly concatenated | Can be loaded on demand, flexibly combined |
| Trigger | Manual input | Auto-loaded or called on demand |

For example: "You are a React expert" — that's a prompt.  
"Our project uses React 18 + TypeScript, state management with Zustand, styling with Tailwind CSS, component naming with PascalCase, file structure organized by feature module, testing with Vitest…" — that's a Skill.

Skills don't just tell the agent "who you are" — they tell the agent "how you should work in this project."

### 6.3 Four Types of Skills

Not all Skills are the same. Based on content and purpose, Skills can be divided into four categories:

#### Type One: Knowledge Skills

Tell the agent "what it is" — project background, tech stack, coding standards, design principles, business logic.

For example:

- Overall architecture and module division of the project
- Code style and naming conventions
- Commonly used design patterns and best practices
- Core concepts and terminology of the business domain

Knowledge Skills are the most foundational — they make the agent "know the ropes," so it doesn't ask basic questions or make common-sense mistakes.

#### Type Two: Process Skills

Tell the agent "how to do it" — standard processes and steps for completing certain types of tasks.

For example:

- "Standard bug-fixing process: reproduce first → locate root cause → write fix → add tests → verify"
- "Code review checklist: security, performance, readability, test coverage"
- "PR submission standards: title format, description template, linked issues"

Process Skills are efficiency multipliers — they mean agents don't have to think through the process from scratch every time, they just follow best practices.

#### Type Three: Tool Skills

Tell the agent "what to use" — what tools are available, how to use them, when to use them.

For example:

- "If you need to query the database, use the `db_query` tool, parameter format is…"
- "If you need to search code, use the `code_search` tool, supports regular expressions"
- "If you need to deploy, call `deploy_service`, but only in the test environment"

Tool Skills expand capability — they let the agent know what weapons it has and when to use which one.

#### Type Four: Role Skills

Tell the agent "who it is" — the agent's identity, responsibilities, boundaries.

For example:

- "You are a senior frontend engineer, focused on user experience and performance optimization"
- "You are a security auditor, your responsibility is to find security vulnerabilities in code"
- "You are a technical documentation editor, your goal is to make documentation clear and accessible"

Role Skills are the rudder of direction — they set the agent's stance and priorities, influencing the trade-offs it makes in decisions.

### 6.4 Skill Design Principles

Designing Skills isn't just throwing all information in. Good Skill design follows several principles:

#### Principle One: Focus, Don't Greed

One Skill does one thing. Don't stuff "React standards," "testing standards," and "deployment流程" all into one Skill. Split them into multiple small Skills and load them on demand.

#### Principle Two: Structured, Not Prose

Skills are for machines to read, not humans. Use clear headings, lists, code blocks — let the agent quickly locate and understand information.

#### Principle Three: Example-Driven

Examples are more persuasive than rules. Don't just say "we use PascalCase for component naming" — give a complete component example. Agents learn far more from examples than from rules.

#### Principle Four: Verifiable

Good Skills should be verifiable. How do you know if the agent correctly understood and executed the Skill? Give it checklists and self-test methods.

### 6.5 The Evolution of Skills: From Static to Dynamic

Currently most Skills are still static — written by humans and then unchanged. But the ultimate form of Skills is **dynamic, self-evolving**.

Imagine:

- After each task, the agent automatically summarizes "what was learned this time" and updates it into the Skill
- The system analyzes all failed tasks, automatically discovers "agents tend to make mistakes in XX scenarios," then automatically supplements the corresponding Skill
- Multiple agents share a Skill library — the mistakes one agent made, others won't repeat

That's the future of Skills — they're not human-written documentation, but collective memory that the system continuously accumulates and evolves through practice.

> **Core Idea**: Skills are the "corporate culture" of a loop system. Just as a company's culture determines how employees behave, a loop system's Skill体系 determines the quality and style of its agents' work.

---

---
