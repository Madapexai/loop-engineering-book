> *A loop is not a black box — it's a system carefully composed of multiple modules. Understand each building block, and you can build your own tower.*

---

---

# Chapter 4: Automations — The Heartbeat That Makes Loops Actually Spin

If a loop is a living organism, then Automation is its heartbeat.

Without a heartbeat, no matter how powerful the body's organs are, they're meaningless — because they never get awakened. Similarly, without Automation, no matter how powerful an AI agent is, it's just a passive tool waiting to be called — it won't start on its own, won't discover problems on its own, won't begin working on its own.

### 4.1 What is Automation?

Automation (automated triggers) is the startup mechanism of a loop — it determines "when, why, and what kind of loop to launch."

Sounds simple? Isn't it just cron jobs plus event listeners?

In traditional automation, yes. But in Loop Engineering, the meaning of Automation is much richer. Because the execution主体 of a loop is an AI agent, not a fixed script — which means the trigger itself can also be intelligent.

### 4.2 Three Trigger Modes

#### Mode One: Time-Driven

The simplest and most reliable trigger method. "Run every hour," "execute at 3 AM every day," "generate a report every Monday morning."

The advantage of time-driven triggers is simplicity, predictability, and ease of debugging. You know when it will run, and problems are easy to reproduce.

The disadvantage of time-driven triggers is inflexibility. If a task is突发的 (like a production bug), time-driven triggers are too slow. And if there are no tasks but it's still running, that's wasted resources.

**Best for**: Regular inspections, scheduled reports, batch processing tasks

#### Mode Two: Event-Driven

When a specific event occurs, automatically launch a loop. For example:

- New issue created on GitHub → launch classification loop
- PR submitted → launch code review loop
- Monitoring system sends alert → launch troubleshooting loop
- Feishu document commented on → launch reply loop

Event-driven is currently the most mainstream trigger pattern. It responds in time, has high resource utilization, and perfectly fits the "task-driven" work model.

The core challenge of event-driven triggers is **event storms** — if a large number of events flood in within a short time, will the system be overwhelmed? You need queueing mechanisms, rate limiting, and priority mechanisms.

**Best for**: Real-time response tasks, event-driven workflows

#### Mode Three: Condition-Driven

This is the most intelligent and most complex trigger mode. The system continuously monitors some state, and when the state meets specific conditions, automatically launches a loop.

For example:

- "When test coverage in the codebase drops below 80%, automatically start a test-completion loop"
- "When production error rate exceeds threshold, automatically start a rollback loop"
- "When an issue goes unhandled for more than 7 days, automatically escalate notification"

The difference between condition-driven and event-driven: event-driven is "something happened," while condition-driven is "some state persists." Event-driven is pulse-based, condition-driven is continuous monitoring-based.

The challenge of condition-driven triggers is **the cost of state evaluation** — you can't evaluate all conditions every second, that would be too costly. You need to find a balance between "response speed" and "monitoring cost."

**Best for**: Quality monitoring, SLA assurance, proactive operations

### 4.3 Trigger is Design: Good Triggers are Half the Battle

Many people, when designing loops, put all their energy into "how the agent works" and neglect trigger design. But in reality, triggers determine the **rhythm and boundaries** of the entire loop.

A poorly designed trigger can lead to:

- **Too frequent triggering**: System resources exhausted, token costs skyrocket
- **Too sparse triggering**: Problems don't get handled in time, defeating the purpose of automation
- **Inaccurate trigger conditions**: Launches when it shouldn't, doesn't launch when it should
- **Lack of deduplication**: The same event triggers N loops, wasting resources and causing conflicts

A good trigger design should answer these questions:

1. **What is the trigger condition?** (Event? Time? Condition?)
2. **What is the maximum trigger frequency?** (Preventing storms)
3. **How to deduplicate?** (Same task won't be processed repeatedly)
4. **How to prioritize?** (Multiple tasks come in at once, which to handle first?)
5. **How to retry on failure?** (What if the trigger itself fails?)

### 4.4 Case Study: Ralph Loop's Trigger Mechanism

Amplitude's Ralph Loop is a classic case. Its trigger mechanism is very concise:

- **Trigger condition**: GitHub issue tagged with "ralph"
- **Deduplication**: Each issue triggers only once, unless re-tagged
- **Priority**: Sorted by issue creation time, first-come-first-served
- **Concurrency control**: Maximum N tasks running simultaneously

This design seems simple, but it's highly effective. It puts the decision of "should Ralph handle this" in human hands — engineers trigger by tagging. This preserves the flexibility of human judgment while achieving execution automation.

It's a clever design philosophy: **Let humans make judgments, let systems do the execution.**

---

---
