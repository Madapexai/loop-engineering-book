> *Knowing the names of all the building blocks doesn't mean you can build a bridge. Theory meets reality through the cycle of design, practice, failure, and iteration.*

---

---

# Chapter 10: Designing Your First Loop

### A Five-Step Methodology from Scratch

Alright, you've understood the core concepts and six modules of Loop Engineering. Now you want to design a loop yourself. Where do you start?

Many people's first reaction is: "I need to build a complete system, all six modules, nothing less."

Wrong.

The right approach to designing a loop isn't starting with architecture — it's starting with **a specific pain point**. Find the task that gives you the biggest headache, the most repetitive one, and turn it into your first loop.

Here's a battle-tested five-step methodology.

### Step One: Choose the Right Task — Not All Tasks Are Suitable for Loop-ification

The first step is also the most crucial one: **choose the right first task.** Choose well, and you get twice the result with half the effort. Choose poorly, and you might lose faith in Loop Engineering forever.

What kind of task makes a good first loop?

**Good candidate tasks have these characteristics:**

- ✅ **High repetition**: Done weekly/daily, frequent enough
- ✅ **Well-defined**: What's the input, what's the output, what's the success criteria — all clear
- ✅ **Controlled risk**: Even if done wrong, consequences aren't severe, easy to roll back
- ✅ **Verifiable**: Can automatically judge if the result is correct, no need for human to check every time
- ✅ **Single/few steps**: Don't start with complex multi-agent collaboration

**Bad candidate tasks:**

- ❌ Tasks done once a year (too low ROI)
- ❌ Vague goals like "improve user experience" (can't verify)
- ❌ Tasks that directly modify production databases (too risky)
- ❌ Tasks requiring deep business judgment (AI can't handle)

> **Rule of Thumb**: Your first loop should be the kind of task where "getting it right is no big deal, but getting it wrong won't kill anyone." Build confidence first, then upgrade gradually.

### Step Two: Define Clearly — Input, Output, Success Criteria

After choosing the task, don't rush to write code. First answer three questions clearly:

**1. What is the input?**  
Where does the loop get tasks from? GitHub Issues? Feishu messages? Time triggers? What's the input format? What fields are required?

Think of input as a function's parameters — with clearly defined parameters, the function can be written correctly.

**2. What is the output?**  
What does the loop deliver when it's done? A PR? An analysis report? A comment? An email?

Output format also needs to be clear. For example, PR title format, description template, what tags to add.

**3. What is the success criteria?**  
This is the most important and most easily overlooked question. How do you judge that what the loop did is "correct"?

Success criteria could be:

- Tests pass
- No lint errors
- Code compiles successfully
- Meets certain acceptance conditions
- (For tasks that can't be auto-verified) Approved by a human

Without clear success criteria, the loop will become — as Chapter 12 discusses — a perpetual motion machine with no exit condition.

### Step Three: Design the Flow — Draw Your Loop Diagram

After defining inputs and outputs clearly, you can design the loop's internal flow.

The simplest loop flow looks like this:

```
Trigger → Receive task → Agent executes → Verify result → Success?→ Yes → Deliver
                                      ↓No
                                    Retry?→ Yes → Agent executes (with error feedback)
                                      ↓No
                                    Escalate to human
```

When designing the flow, ask yourself:

- **How many steps?** Keep it simple — getting the first version right is good enough
- **Who makes decisions?** Is the decision-maker at each step the agent or the system?
- **What happens on failure?** How many retries? What's different each time? When to give up?
- **When do humans介入?** No humans needed at all? Or human confirmation needed at the end?

I recommend drawing it on paper or a whiteboard — a visualized flow chart helps you discover many problems you wouldn't find just thinking.

### Step Four: Minimal Implementation — Get It Running First, Then Optimize

Many people fall into the "perfectionism trap" when designing loops — wanting the most elegant architecture, the most complete features, the best experience. Result: three months of work and still not launched.

Remember this principle: **the first version just needs to work.**

Your first loop can be very crude:

- No MCP, just call CLI tools directly
- No Worktree, just work in one directory (anyway, the task is simple, low conflict probability)
- No Skills, write all instructions in the prompt
- No Memory, start from scratch every time
- No Sub-agents, just one agent doing everything

Crudeness doesn't matter. What matters is — **it actually runs, it actually saves you time.**

Once it's running, you can gradually optimize based on real pain points in usage. Whatever hurts the most, optimize that first.

It's the same principle as building products: have an MVP (Minimum Viable Product) first, then iterate.

### Step Five: Measure and Iterate — Let the Loop Get Better Over Time

Launching the loop isn't the end — it's the beginning.

You need to measure key metrics to judge the loop's effectiveness and guide next-step optimization:

- **Success rate**: How many tasks completed successfully? How many failed?
- **Accuracy**: Among successful tasks, how many were actually done correctly (no rework needed)?
- **Average time**: How long does it take to complete one task on average?
- **Human intervention rate**: How many tasks require human handling?
- **Cost**: How many tokens/money does each task cost on average?

With these metrics, you'll know what to optimize:

- Low success rate? → Optimize prompts, add verification steps
- Low accuracy? → Add Checker agents, strengthen quality gates
- High human intervention rate? → Analyze intervention reasons, target optimization
- Too costly? → Optimize context, reduce retries, use smaller models

> **Core Idea**: The loop itself is also an iterative cycle. You design the loop, then the loop's运行数据反过来 guides you to optimize the loop. That's the real "loop engineering."

### Case Study: An Engineer's First Loop

Xiao Wang is a backend engineer. The thing he finds most annoying is that every time someone files a bug issue, he has to spend time分类 — which module does this bug belong to? How severe is it? Is it a duplicate?

He decided to automate this with a loop.

**Step One, choose task**: Issue classification. High repetition (daily), well-defined (input is Issue, output is tags), low risk (just change it back if wrong), verifiable (humans can spot-check).

**Step Two, define clearly**:

- Input: GitHub Issue title and description
- Output: Tag the issue with module and priority labels
- Success criteria: Tag accuracy reaches 80%+ (human spot-check verification)

**Step Three, design flow**:

```
New issue created → Trigger loop → Agent reads issue content → Agent judges module and priority → Add tags → End
(If fails, retry once; if still fails, skip and wait for human)
```

**Step Four, minimal implementation**: Used GitHub Actions + Claude Code API, wrote a few dozen lines of script. No Worktree, no Skills, no Memory — just the simplest implementation.

**Step Five, iterate**:

- Week 1: 60% success rate, often mislabeling modules. → Added project module documentation as context.
- Week 2: 80% success rate, but priority judgment was off. → Added detailed explanation and examples of priority criteria.
- Month 1: 90% success rate, basically no need to manage. → Added Memory, storing historical classification results, getting more accurate over time.

Now, this loop saves Xiao Wang about 8 hours per month. The total time he spent building and optimizing it: less than 10 hours.

**That's the ROI of Loop Engineering: spend a little time upfront, benefit continuously later.**

---

---
