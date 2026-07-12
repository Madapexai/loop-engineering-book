If a loop starts up every time as if seeing the project for the first time — not knowing what was done before, not knowing which approaches were tried and failed, not knowing the project's coding style — how efficient would it be?

The answer is: not very.

It would repeatedly step in the same pitfalls, revisit already-rejected approaches, and understand the project from scratch every time. Like a person without long-term memory — every day is a new day, but every day is standing still.

That's the importance of the Memory system. If Automation is the loop's heartbeat, Worktree is its body, and Skill is its knowledge, then Memory is the loop's **spine** — without it, the whole system can't stand up.

### 9.1 What is a Memory System?

The Memory system is the module in a loop responsible for **storing, organizing, and retrieving historical information**. It ensures loops don't start from zero every time, but can stand on the shoulders of past experience.

What's the difference between Memory and Skill?

- **Skills** are relatively stable knowledge — project standards, tech stack, workflows. They change slowly and are usually written by humans.
- **Memory** is dynamically accumulated experience — what tasks were done, what pitfalls were encountered, which approaches work, which users reported what problems. It grows continuously and is usually auto-recorded by the system.

Put simply: **Skills are "textbook knowledge," Memory is "hands-on experience."**

### 9.2 Four Levels of Memory

A complete Memory system typically includes four levels of memory:

#### Level One: Episodic Memory

Memory of the current session/current task. Files the agent read during this task, attempts it made, intermediate thought processes.

Episodic memory is characterized by high volume, detail, but short lifecycle. After the task ends, most of it is no longer needed.

**Storage medium**: Usually directly in the context window

#### Level Two: Working Memory

A summary of key information for the current task — what the task goal is, what's been done, what problems were found, what the next steps are.

Working memory is the agent's "workbench" — it doesn't need to remember all details, but needs to remember key nodes and current state.

**Storage medium**: Structured state objects, task summaries

#### Level Three: Long-Term Memory

Cross-task memory — what was done before in this project, which approaches proved effective, which pitfalls to avoid, what user preferences exist.

Long-term memory is the most valuable part of a loop system — it makes the system smarter the more you use it. The first task might be bumpy; the hundredth task will be smooth.

**Storage medium**: Vector databases, knowledge graphs, structured databases

#### Level Four: Collective Memory

Cross-agent, cross-project memory — a shared experience library for all loops across the organization. Pitfalls encountered by Project A won't be repeated by Project B; best practices summarized by one agent benefit all agents.

Collective memory is the ultimate form — it makes an organization's entire AI system form "collective intelligence" rather than fighting各自 battles.

**Storage medium**: Centralized knowledge platform, shared Skill library, organization-level memory bank

### 9.3 Core Operations of Memory: What to Store, How to Store, How to Retrieve

Designing a Memory system, the core is answering three questions: What to store? How to store? How to retrieve?

#### What to Store? — Memory Filtering

Not everything is worth remembering. Remembering too much irrelevant information反而 interferes with retrieval and wastes resources.

You need to filter:

- ✅ Final results and key decisions of tasks
- ✅ Failed attempts and their causes (to avoid repeating)
- ✅ User preferences and feedback (personalized service)
- ✅ Newly learned patterns and best practices
- ❌ Detailed logs of intermediate processes (too trivial)
- ❌ Outdated information (misleading)

#### How to Store? — Memory Organization

Storage method determines retrieval efficiency. Common organization methods:

- **Vector storage**: Embed memories into vectors for semantic retrieval
- **Structured storage**: Store key information as database records for conditional querying
- **Knowledge graph**: Store relationships between entities, supporting reasoning and association discovery

The best approach is **hybrid storage** — vector storage for semantic search, structured storage for precise queries, knowledge graphs for relational reasoning.

#### How to Retrieve? — Memory Retrieval

The value of memory lies in being usable. If you store a huge pile but can't find anything, it's the same as not storing.

Retrieval strategies:

- **By relevance**: Which historical memories are most relevant to the current task?
- **By time**: Have there been similar tasks recently?
- **By importance**: Are there high-priority memories to check first?
- **By failure pattern**: What pitfalls have been encountered for this type of task before?

### 9.4 Two Major Traps of Memory

Bigger isn't always better when it comes to Memory systems. Two common traps to watch for:

#### Trap One: Memory Contamination

If wrong information is stored in memory, agents will repeatedly make the same mistakes. And wrong memory is scarier than no memory — because the agent will firmly believe in it.

**Countermeasures**:

- Validation mechanism before memories enter the store
- Memories have "confidence" scores; low-confidence memories aren't used first
- Periodically "clean memories" — mark or delete memories proven wrong

#### Trap Two: Memory Overload

With too many memories, retrieval pulls up a bunch of irrelevant stuff that反而 interferes with the agent's judgment. It's like how people who know too much tend to overthink — relevant and irrelevant all surge up, making it hard to decide.

**Countermeasures**:

- Strict relevance thresholds for memory retrieval
- Limit the number of memories returned per retrieval
- Memories have "usage frequency" and "recency" weights; prioritize returning commonly used and fresh memories

### 9.5 Case Study: How Memory Makes Systems "Smarter the More You Use Them"

Imagine a code review loop. When it first launches:

- Day 1: Review quality is mediocre, often misses project-specific standard issues
- Week 1: It starts remembering some common error patterns, review quality noticeably improves
- Month 1: It has accumulated hundreds of review cases, knows what problems this project is most prone to, what the team cares about most
- Month 3: Its review quality already surpasses most junior engineers — because it's seen more cases than any single person

That's the power of the Memory system — **it lets system capability grow linearly over time, while human capability growth has a ceiling.**

> **Ultimate Vision**: A mature loop system should be like a veteran employee who's been at the company for ten years — knows all the history, understands all the unwritten rules, has stepped in every pit, knows who to go to for any problem. The difference is, this veteran employee doesn't need to sleep and never quits.

---

---
