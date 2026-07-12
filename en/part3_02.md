"The good thing about automation is getting work done faster. The bad thing about automation is getting garbage work done faster."

— A veteran engineer

Without quality gates, a loop is just a "garbage production machine." The faster it runs, the more garbage it produces. You think you're improving efficiency, but actually you're creating technical debt.

Quality Gates are the most critical safety net in a loop system. They ensure — only output meeting quality standards passes;不合格 output is sent back for rework.

### 11.1 What Are Quality Gates?

Quality gates are checkpoints in the loop flow — an agent's output must pass these checks to enter the next stage.

You can think of them as quality inspection stations in a factory. Products come off the assembly line, and inspectors check for problems. Those without issues pass, those with problems are sent back for rework.

In loop systems, quality gates can be automated (tool checks), intelligent (AI agent reviews), or manual (human approval).

### 11.2 The Seven-Layer Quality Gate System

A complete loop system should have multiple layers of quality gates. Earlier gates are lighter and more automated; later gates are stricter and require more intelligent judgment.

#### G0: Syntax Gate

The most basic check — does the code compile? Are there syntax errors? Does lint pass?

- **What it checks**: Compilation, lint, formatting
- **Executor**: Automated tools
- **Cost**: Very low
- **Speed**: Seconds

This is the most basic gate. Code that doesn't pass G0 isn't even qualified to be reviewed.

#### G1: Test Gate

Is the functionality correct? — Do tests pass?

- **What it checks**: Unit tests, integration tests, E2E tests
- **Executor**: Automated test frameworks
- **Cost**: Low to medium
- **Speed**: Seconds to minutes

Test gates are the basic guarantee of functional correctness. But note — tests can only prove "there IS a bug," not "there is NO bug." Passing tests doesn't mean the functionality is correct; it only means "current test cases found no problems."

#### G2: Static Analysis Gate

How's the code quality? — Are there security vulnerabilities? Performance issues? Code smells?

- **What it checks**: Security scanning, code complexity, duplicate code, potential bugs
- **Executor**: Static analysis tools + AI review
- **Cost**: Low
- **Speed**: Seconds to minutes

Static analysis tools can find many pattern-based problems, but are powerless against design-level or architecture-level issues.

#### G3: AI Review Gate

Another AI agent reviews the code — doing a comprehensive check from the perspectives of design, readability, and best practices.

- **What it checks**: Code design, readability, edge cases, error handling, best practices
- **Executor**: Checker agent (different model, different role)
- **Cost**: Medium
- **Speed**: Minutes

This is the core环节 of the Maker-Checker pattern. Having "another brain" check often finds many problems that "one's own brain" can't see.

> **Best Practice**: Use different models for Maker and Checker. For example, use Claude Opus to write code and GPT-4o to review. Or vice versa. Different models have different blind spots, and cross-verification works best.

#### G4: Integration Gate

Put the changes into the complete system — does it work properly?

- **What it checks**: Integration tests, regression tests, performance benchmarks
- **Executor**: CI/CD system + automated testing
- **Cost**: Medium to high
- **Speed**: Minutes to hours

Many problems can't be found when looking at code in isolation — they only surface in the complete system. The integration gate catches these.

#### G5: Staging Gate

Deploy to staging environment, run it for real, see if there are problems?

- **What it checks**: Staging environment verification, canary release, smoke tests
- **Executor**: Automated tools + AI agents
- **Cost**: High
- **Speed**: Hours

The closer to the real environment, the more real the problems you find. But the cost is also higher.

#### G6: Human Gate

The last line of defense — humans make the final confirmation.

- **What it checks**: Business logic judgment, design decisions, risk assessment
- **Executor**: Human engineers
- **Cost**: Extremely high (human time is most expensive)
- **Speed**: Hours to days

Many people think the goal of Loop Engineering is "no humans needed at all." That's a misunderstanding. The goal of Loop Engineering is "let humans only do what truly requires humans."

What requires humans? Judgment, decision-making, trade-offs. Not repetitive labor, not mechanical checking, not staying up late monitoring processes.

### 11.3 Principles of Gate Design

Designing quality gates — more isn't always better. Too many gates, and the流程 becomes too slow, defeating the purpose of automation. Too few gates, and quality can't be guaranteed.

Several design principles:

#### Principle One: Shift-Left Principle

Problems that can be found early, don't leave for later.

The later the gate, the higher the cost. G0 (syntax check) costs almost nothing, G6 (human review) costs the most. So try to eliminate problems in earlier gates.

This is "quality shift-left" — push quality checks as early as possible.

#### Principle Two: Layering Principle

Different gates check different things — don't repeat.

For example, G0 checks syntax, so don't have G3 check syntax again. G3 should check things G0 can't — design, readability, edge cases.

Each layer of gate has its own clear responsibility — no overlap, no gaps.

#### Principle Three: Cost Matching Principle

High-value tasks use high-cost gates; low-value tasks use low-cost gates.

Putting the full G0-G6 suite on a typo fix? That's using a sledgehammer to crack a nut. Only putting G0-G2 on a core payment system change? That's playing with fire.

Based on task importance and risk level, flexibly configure the number and strictness of gates.

#### Principle Four: Traceability Principle

Each gate's check results must be recorded — when it was checked, what was checked, what the result was, why it passed/failed.

This isn't just for tracing blame when problems occur — it's for analysis and optimization — which gate finds the most problems? Which gate never finds problems (is it too lenient?).

### 11.4 Case Study: Amplitude's Ralph Loop Quality Control

Ralph Loop is Amplitude's AI development agent that delivers 102 features per week. With such high output volume, how is quality guaranteed?

Their quality control system works like this:

1. **Automated testing**: Every PR automatically runs the complete test suite. Failures are sent back directly.
2. **AI code review**: Code written by Ralph goes through初步 review by another AI agent.
3. **Human engineer review**: The final PR still needs human review. But because there are already two layers of filtering before it, there's much less for humans to review.
4. **Progressive merging**: Merge to development branch first, run for a few days with no issues before merging to main.

The key insight: **Ralph Loop's goal isn't 100% automation — it's reducing human workload to 1/10 of before.** Humans still review code, but where they used to review 10 PRs in the time it took, now they can review 100 — because most low-level problems have been filtered by earlier gates.

> **Core Idea**: The purpose of quality gates isn't "ensuring 100% no problems" — that's impossible. The purpose of quality gates is "reducing problem density to a level humans can handle."

---

---
