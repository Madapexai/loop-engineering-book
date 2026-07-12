### Six Failure Modes and Three Deep Risks

"In theory, theory and practice are the same. In practice, they're not."

— Yogi Berra

When designing loops, you think only of successful scenarios — agents executing tasks perfectly, systems running automatically, efficiency dramatically improving.

But the reality is: your first loop will probably fail. Not a small failure — a big one — running amok, burning money, producing garbage, crashing the system.

This is normal. Everyone who's done Loop Engineering has stepped in pitfalls. What matters isn't avoiding all failures (impossible), but knowing what pitfalls exist and how to climb out when you fall in.

This chapter summarizes six failure modes and three deep risks.

### 12.1 Failure Mode One: No Exit Condition (Perpetual Motion Machine)

**Symptoms**: The loop starts and just keeps running and running, like it'll never finish. Tokens burn through fast, but you never see results.

**Cause**: No clearly defined exit conditions. The agent loops infinitely in a state of "I think it can still be better" — changing and changing, optimizing and optimizing, never satisfied.

**Why this happens**: When humans do tasks, we know "good enough is enough." But AI doesn't have this intuition. You don't give it a clear stop signal, it'll keep going forever.

**Solutions**:

1. **Clear success criteria**: Define "done" clearly. For example, "tests pass + lint passes = done," not "code is well-written."
2. **Max steps / max token limit**: Set hard caps. When the cap is reached, force stop regardless of completion.
3. **Diminishing returns detection**: If N consecutive iterations show no substantive improvement, stop.

> **Lesson**: "Better" is the enemy of "good." In loops, this is especially true.

### 12.2 Failure Mode Two: Repeated Failure Without Strategy Change (Hitting a Wall)

**Symptoms**: The agent encounters an error, makes a correction, tries again — same error. Corrects again, tries again — still wrong. Making the same mistake over and over, like a fly hitting a window.

**Cause**: The agent has no mechanism for learning from failure. After each failure, it just adjusts slightly and tries again the same way. If the root cause isn't found, no amount of retries helps.

**Why this happens**: When humans encounter repeated failure, they change their approach — "am I going in the wrong direction?" But AI easily gets stuck in the same thinking framework. Its "corrections" are often micro-adjustments, not fundamental rethinking.

**Solutions**:

1. **Failure count threshold**: After N consecutive failures, force a strategy change.
2. **Root cause analysis step**: After consecutive failures, stop to do root cause analysis instead of immediately retrying.
3. **Switch model / switch agent**: Let another agent (preferably a different model) diagnose the problem.
4. **Escalate to human**: If all strategies have been tried and still failing, don't push through — get a human.

### 12.3 Failure Mode Three: Context Overflow (Amnesia)

**Symptoms**: The agent starts off doing fine, but mid-task it forgets what the original goal was. Or conclusions confirmed earlier get overturned and redone later.

**Cause**: Limited context window. If the task is too long, has too many steps, earlier information gets "pushed out." The agent is like a goldfish — only remembers recent things.

**Why this happens**: This is a fundamental limitation of large models. No matter how big the context window, it's finite. And the total information of complex tasks can easily exceed the window size.

**Solutions**:

1. **Periodic summarization**: Every N steps, make a summary of current state, put the summary into context.
2. **Working memory**: Maintain a structured "working memory" — current goal, completed steps, key decisions, todo items.
3. **Modular decomposition**: Break large tasks into small tasks, each completed in an independent context.
4. **External storage**: Store detailed historical information externally (database, files), retrieve when needed.

### 12.4 Failure Mode Four: Too Vague Goals (Lost)

**Symptoms**: What the agent produces is completely different from what you wanted. Or it does a lot, but it's all trivial things — not a single key problem is solved.

**Cause**: Task definition is too vague. "Optimize this page a bit," "improve user experience," "refactor some code" — these might be enough for humans, but far from enough for AI.

**Why this happens**: Humans have "common sense" and "context" — we can automatically fill in the meaning of vague instructions. But AI doesn't have your background knowledge, your aesthetics, your business understanding. Things you find "obvious" aren't obvious to it at all.

**Solutions**:

1. **SMART principle**: Task definitions should be Specific, Measurable, Achievable, Relevant, Time-bound.
2. **Acceptance criteria**: Clearly write out "what counts as done." Ideally with auto-verifiable acceptance conditions.
3. **Example-driven**: Giving good and bad examples is far more effective than describing in words.
4. **Scope limitation**: Clearly stating "what NOT to do" is sometimes more important than stating "what to do."

### 12.5 Failure Mode Five: Lack of Tool Access (Ideas Without Means)

**Symptoms**: The agent's approach sounds reasonable, but it just can't execute. Because the tools it needs aren't available, the data it needs can't be accessed, the systems it needs can't be connected to.

**Cause**: You gave the agent a task, but didn't give it the tools and permissions needed to complete it. Like asking a carpenter to work but not giving a saw — no matter how skilled, it's useless.

**Why this happens**: When designing loops, people often focus on "what the agent does" and neglect "what the agent uses to do it." When it actually runs, you discover this and that are missing.

**Solutions**:

1. **Pre-task tool inventory**: When designing a task, first think through what tools are needed. Confirm the agent can use all of them.
2. **MCP integration**: Connect common tools with the MCP protocol. More tools = more things agents can do.
3. **Tool discovery mechanism**: Let agents know what tools they have available. Often it's not that tools don't exist, but agents don't know about them.
4. **Progressive authorization**: Start with minimum privileges, add more as needed. Balance security and efficiency.

### 12.6 Failure Mode Six: Unsafe Autonomy (Runaway)

**Symptoms**: The agent does things you never expected it would do — deletes important files, modifies production config, sends messages it shouldn't, spends enormous amounts of money.

**Cause**: Gave the agent too much authority, too few limits. In the course of executing the task, it takes "out-of-bounds" actions to achieve the goal.

**Why this happens**: AI is goal-oriented. You give it a goal, it finds ways to achieve it. But it doesn't have human "common sense boundaries" — it doesn't know what things are "absolutely not to be done" unless you explicitly tell it.

**Solutions**:

1. **Principle of least privilege**: Only give the minimum privileges necessary to complete the task. Never give admin privileges.
2. **High-risk operation confirmation**: Deletion, production environment changes, spending money — these must have human confirmation.
3. **Sandbox environment**: Let agents work in a sandbox where messing up doesn't affect real systems.
4. **Budget control**: Set token budget caps, auto-stop when exceeded.
5. **Audit logs**: All operations are recorded, traceable when problems occur.

### 12.7 The Three Deep Risks

The six failure modes above are all "technical problems" — tweak and fix and they're solved. But there are three deeper risks that go to the fundamentals of organizations and people.

#### Deep Risk One: Cognitive Surrender

**What it means**: Because AI does things fast and abundantly, humans stop thinking for themselves. AI will do it anyway, I'll just look at the results.

Over time, human judgment degenerates. You no longer think "why do it this way," "is there a better approach," "what are the risks." You go from being a designer to being a nodding machine.

**Why it's dangerous**: When AI makes mistakes (and it will), you might not notice — because you've lost the ability to judge independently.

**Countermeasures**:

- Regular "no-AI practice" — force yourself to complete a task without AI
- Maintain a "default skeptical" attitude toward AI output
- Understand every line of AI-written code; don't merge code you don't understand
- Keep learning and thinking habits — AI is a tool, not a crutch

#### Deep Risk Two: Comprehension Debt

**What it means**: Technical debt is "cutting corners now, paying later." Comprehension debt is "you don't understand code written by AI, and when problems arise later you spend even more time trying to understand it."

AI writes code much faster than humans can understand it. After a month, the codebase has tens of thousands more lines of AI-written code, but nobody can clearly explain what every line does.

**Why it's dangerous**: When complex system problems arise, nobody can understand how the whole system works. You go from "owning a system" to "depending on a black box you don't understand."

**Countermeasures**:

- Establish code ownership — every piece of code has an owner
- Code written by AI must be truly understood by the owner before merging
- Regular architecture reviews and code walkthroughs
- Higher requirements for documentation and comments — AI-written code needs good docs even more

#### Deep Risk Three: Token Cost Runaway

**What it means**: After loops start running, token costs snowball bigger and bigger. At first you think "it's not much money," but by the end of the month when you see the bill — shock.

Peter Steinberger (Director of Google Cloud AI) has a monthly bill of \$1.3 million. Theo (well-known developer) spent \$20,000 in 48 hours. These aren't rumors — they're real events.

**Why it's dangerous**: The characteristic of loops is "automatic operation" — they don't need humans to start, they just run and spend money on their own. Without controls, costs grow exponentially.

**Countermeasures**:

- Set budget alerts — trigger at 50%, 80%, 100% of budget
- Allocate budgets by task/project/team, each accounts for itself
- Cost monitoring dashboard — real-time view of how much is spent, where
- Cost optimization mechanisms — auto-detect high-cost tasks, optimize context, reduce retries
- Regular cost reviews — which loops have good ROI, which aren't worth running

> **Ultimate Reminder**: The biggest risk in Loop Engineering is never technical. Technical problems can all be solved. The biggest risk is — you also outsource the right to think.

---

---
