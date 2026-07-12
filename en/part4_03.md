### A Practical System of 1 Hub + 4 Closed Loops + 7 Gates

Previous chapters introduced the concepts, modules, and general frameworks of Loop Engineering. But if you want to truly implement it in your own team or project, you need a more concrete, more actionable, battle-tested methodology.

This is the M-LOOP Framework.

M-LOOP is a practical system we refined across multiple enterprise projects. It's not a product of theoretical deduction — it's总结 from the successes and failures of real projects.

### 17.1 M-LOOP Framework Overview

The core architecture of M-LOOP can be summarized with a set of numbers: **1 Hub + 4 Closed Loops + 7 Gates**.

```
                    ┌──────────────────┐
                    │   Rex Hub Engine │
                    │  Research/Route  │
                    │  Review/Rescue   │
                    │     Record       │
                    └────────┬─────────┘
                             │
        ┌────────────────────┼────────────────────┐
        │                    │                    │
  ┌─────▼─────┐        ┌─────▼─────┐        ┌─────▼─────┐
  │ Task Loop │        │ Verify    │        │Collab Loop│
  │  任务闭环  │        │ 验证闭环   │        │ 协作闭环   │
  └───────────┘        └───────────┘        └───────────┘
                             │
                        ┌────▼─────┐
                        │Knowledge│
                        │知识闭环  │
                        └──────────┘
          ┌───────────────────────────────┐
          │  G0 G1 G2 G3 G4 G5 G6         │
          │  7-Layer Quality Gates        │
          └───────────────────────────────┘
```

**1 Hub**: Rex Hub Engine — the brain of the entire system, responsible for scheduling, decision-making, rescue, and recording  
**4 Closed Loops**: Task Loop, Verify Loop, Collaboration Loop, Knowledge Loop — the four wheels of system operation  
**7 Gates**: G0-G6 seven-layer quality gates — the safety net of system output

Let's unpack each one.

### 17.2 Rex Hub: One Brain Manages Everything

Rex is the central control system of the M-LOOP Framework. It's not an agent that executes tasks — it's an **agent that manages agents** — responsible for making the entire system run efficiently, reliably, and orderly.

Rex encompasses five core capabilities (5R):

#### Research (Analysis & Routing)

After a task comes in, Rex first analyzes it — what type of task is this? How difficult? How risky? Which agent team should it be assigned to? What processes should it go through?

This is like the first thing a project manager does after receiving requirements — evaluate, decompose, assign.

#### Route (Scheduling & Routing)

Based on task type and priority, Rex decides:

- Which model to use? (Opus? Sonnet? Local small model?)
- Which agents to call? (Frontend agent? Backend agent? Full-stack?)
- What process to follow? (Simple flow or full 7-layer gates?)
- What priority? (Immediate or queue?)

The core of scheduling is **the balance of cost-quality-speed**. High-value, high-risk tasks get the best resources and strictest processes; low-value, low-risk tasks get the lightest configuration and fastest speed.

#### Review (Oversight & Gatekeeping)

Rex doesn't do execution directly, but it's responsible for review at key nodes. For example:

- Is the agent's approach reliable? Should it be sent back to redo?
- Tests passed, but is it really fine?
- Can this task auto-deliver, or does it need escalation to human?

Review isn't checking every step — that would be too inefficient. Rex only intervenes at critical decision points.

#### Rescue (Recovery & Escalation)

Agent stuck? Failed? Run amok? Rex is responsible for rescue.

Rescue strategies include:

- Auto-retry (retry with a different strategy)
- Switch agents (try a different model, a different role agent)
- Degrade handling (reduce task difficulty, do core part first)
- Escalate to human (if really stuck, get a person)

Core principle of Rescue: **Never let a task die halfway.** Failure isn't scary — what's scary is failing and nobody knowing.

#### Record (Logging &沉淀)

Rex is responsible for recording everything that happens in the system — who did what, why they did it, what the result was, how much it cost.

These records aren't just for auditing — they're for the knowledge loop — all experience and lessons eventually沉淀 into the Skill library and memory system.

### 17.3 The Four Closed Loops: Four Wheels of System Operation

#### Loop One: Task Loop

**Goal**: Efficiently complete individual tasks

**Process**:

```
Task input → Task decomposition → Agent execution → Result output
    ↑                                                ↓
    └───────────────────Feedback─────────────────────┘
```

The Task Loop is the most fundamental loop — turning a task from input to output. Its core is **agent execution ability** and **self-correction ability**.

The Task Loop corresponds to the Agent Loop layer in LangChain's four-layer loop architecture.

#### Loop Two: Verify Loop

**Goal**: Ensure output quality

**Process**:

```
Task output → Automated checks → AI review → (Optional) Human review → Pass/Send back
    ↑                                                                 ↓
    └──────────────────────────Correction─────────────────────────────┘
```

The Verify Loop adds multiple layers of quality checks outside the Task Loop. Its core is **multi-perspective cross-verification** — different agents, different tools, different dimensions, collectively guaranteeing quality.

The Verify Loop corresponds to the Verification Loop layer in LangChain's four-layer architecture.

#### Loop Three: Collaboration Loop

**Goal**: Multiple agents/people collaborate efficiently

**Process**:

```
Task assignment → Multi-agent parallel/serial work → Result integration → Conflict resolution → Final output
```

The Collaboration Loop solves the "1+1>2" problem. Multiple agents working together isn't simply division of labor — it requires coordination, communication, integration.

Key mechanisms of the Collaboration Loop:

- **Task decomposition**: Break large tasks into small ones, each with clear boundaries
- **Interface definition**: Clear formats and standards for deliverables between agents
- **Conflict arbitration**: Mechanism to resolve conflicts when multiple agents' results clash
- **Human intervention points**: Complex collaboration decisions are made by humans

#### Loop Four: Knowledge Loop

**Goal**: The system gets smarter the more you use it

**Process**:

```
Task execution → Result recording → Experience distillation → Skill/memory update → Guide next task
    ↑                                                                                     ↓
    └─────────────────────────────────────────────────────────────────────────────────────┘
```

The Knowledge Loop is the most important and most easily overlooked loop. It changes the system from "starting from zero every time" to "standing on past experience."

Core outputs of the Knowledge Loop:

- **Reusable Skills**: Best practices distilled from successful cases
- **Failure pattern library**: Common pitfalls and avoidance methods summarized from failures
- **Project memory**: Project-specific knowledge, norms, preferences
- **Optimization suggestions**: Process and strategy optimization based on data analysis

> **Core Insight**: Many teams' loop systems run for a long time but don't show significant improvement. Why? Because they only have the first three loops, no knowledge loop. The system keeps running but isn't learning. No matter how much it runs, its level won't improve.

### 17.4 Seven-Layer Quality Gates (G0-G6)

Quality gates are the safety net of the M-LOOP Framework. We already detailed the seven gates in Chapter 11 — here's a brief review and their positioning in the M-LOOP Framework:

| Gate | Name | What It Checks | Executor |
|-|-|-|-|
| G0 | Syntax Gate | Compilation, lint, formatting | Automated tools |
| G1 | Test Gate | Unit tests, integration tests | Automated testing |
| G2 | Static Analysis Gate | Security scanning, code quality | Static analysis + AI |
| G3 | AI Review Gate | Design, readability, best practices | Checker agent |
| G4 | Integration Gate | Integration tests, regression tests | CI/CD system |
| G5 | Staging Gate | Staging environment validation | Automation + AI |
| G6 | Human Gate | Business logic, design decisions | Human engineers |

In the M-LOOP Framework, gates aren't "all tasks go through all gates." The Rex Hub **dynamically configures the number and strictness of gates** based on task type, risk, and priority.

For example:

- Fixing a typo → Only G0+G1
- Adding a small feature → G0-G3
- Changing core modules → G0-G5
- Changing payment/security-related → Full G0-G6 suite

This **dynamic gate** design ensures quality for high-risk tasks without burdening low-risk tasks with unnecessary cost and delay.

### 17.5 Supporting Mechanisms

In addition to the core "1+4+7" architecture, M-LOOP has several supporting mechanisms:

#### Feishu @ Verification Iron Rule

This is a simple but extremely effective mechanism: **Any content produced by a loop, if it involves human collaboration (sending notifications, writing documents, replying to messages), must have a "@relevant person to confirm" step.**

Why call it an "iron rule"? Because it's a non-negotiable bottom line — it ensures humans are always at the boundary, and loops never do things that affect others without people knowing.

#### 30-Minute Active Reporting

Any running loop, if it produces no progress output within 30 minutes, must actively report its current status and encountered problems to the person in charge.

This mechanism prevents "loop is stuck but nobody knows" situations — loops can be slow, but they can't go AWOL.

#### Audit Logs

All operations have complete audit logs — who (which agent), when, what was done, why, what the result was.

Audit logs aren't just for accountability — they're for analysis and optimization — by analyzing logs, you can discover system bottlenecks, agent weaknesses, process problems.

#### External Second Verification

For high-risk tasks, in addition to internal system verification, an "external force" is brought in for secondary verification — it could be another team's agent, a different company's model, or an external security audit service.

"Checking yourself" always has blind spots. External second verification is an effective means of breaking through blind spots.

#### Skill Precipitation Mechanism

After each task is completed, the system automatically analyzes: is there any new experience from this task that can be precipitated into a Skill? Any new pitfalls to add to the failure pattern library?

The knowledge loop isn't just empty slogans — it has concrete mechanisms to ensure it.

### 17.6 M-LOOP Implementation Path

The M-LOOP Framework isn't about getting there in one step — it's incremental. You can implement it gradually following this path:

**Phase 1: Build the Task Loop (1-2 months)**

- First get single-task execution flow working
- Use simplest trigger method (manual is fine)
- Use most basic quality checks (G0+G1)
- Goal: Can auto-complete some simple tasks

**Phase 2: Add the Verify Loop (2-3 months)**

- Add AI review gate (G3)
- Establish Maker-Checker pattern
- Start measuring success rate and accuracy
- Goal: Output quality is stable, not much manual rework needed

**Phase 3: Build the Collaboration Loop (3-4 months)**

- Support multi-agent division of labor and collaboration
- Establish Rex Hub's scheduling capability
- Add Rescue mechanisms
- Goal: Can handle complex tasks requiring multi-role collaboration

**Phase 4: Perfect the Knowledge Loop (ongoing)**

- Establish Skill precipitation mechanism
- Build project memory system
- Start doing process optimization and strategy iteration
- Goal: System gets smarter with use, continuously improves

> **M-LOOP Philosophy**: Don't pursue perfection, pursue progress. Each phase has clear goals — achieve them and move forward, don't achieve them and stop to optimize. Loops run continuously, and the construction of loop systems is also continuous.

---

---
