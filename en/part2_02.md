Imagine: you have 10 AI agents working simultaneously, all modifying the same codebase. One agent is changing the login module, another is refactoring the payment system, a third is fixing an urgent bug. They're all writing files at the same time, running tests at the same time, submitting code at the same time...

What happens?

The answer is: **disaster.** They'll overwrite each other's changes, cause test failures because of each other's code, and turn the codebase into a mess.

That's why we need Worktrees.

### 5.1 What is a Worktree?

A Worktree is a Git feature that allows you to check out multiple branches simultaneously in the same repository, each branch in a different directory. This way you can work on multiple branches at the same time without switching.

In the context of Loop Engineering, the meaning of Worktree has been expanded — it generally refers to the mechanism of **creating an independent work environment for each task**. Not just Git branches, but also independent virtual environments, independent database instances, independent configuration files.

The core idea: **Each loop works in its own sandbox, without interfering with others.**

### 5.2 Why is Worktree Infrastructure for Loops?

In the era of human coding, parallel work wasn't a big problem — you'd have at most two or three branches open at once, and you knew what each branch was doing.

But in the era of AI agents, the degree of parallelism is completely different. You might have dozens, even hundreds of agents working simultaneously. Without isolation mechanisms, the system simply can't function.

Worktrees solve three key problems:

#### Problem One: Conflict Isolation

Different tasks execute in different Worktrees, their file modifications don't interfere with each other. Agent A modifying `user.py` won't affect the payment refactoring Agent B is working on.

#### Problem Two: State Isolation

Each Worktree has its own dependency environment, its own database, its own configuration. Agent A upgrading a dependency version won't cause Agent B's tests to suddenly fail.

#### Problem Three: Concurrent Scaling

With Worktree isolation, you can easily scale horizontally — run as many simultaneous tasks as you want, as long as you have the resources.

### 5.3 Three Levels of Worktrees

Worktrees aren't all-or-nothing — there are different isolation levels, and you can choose the appropriate level based on the task's characteristics.

#### Level One: Branch-Level Isolation

The most basic isolation. Each task creates a new branch, working in a separate directory. This is Git Worktree's native capability.

**Pros**: Lightweight, fast, almost no extra cost  
**Cons**: Only isolates code, not runtime environment  
**Best for**: Simple code changes, documentation updates, lint fixes

#### Level Two: Environment-Level Isolation

Each task has not only an independent code branch but also an independent runtime environment — independent Python virtual environments, independent node_modules, independent configurations.

**Pros**: Avoids dependency conflicts, reliable test results  
**Cons**: Environment creation takes time, higher resource consumption  
**Best for**: Tasks requiring test runs, projects with complex dependencies

#### Level Three: Sandbox-Level Isolation

The most thorough isolation. Each task runs in an independent container (Docker) or virtual machine, with independent filesystem, independent networking, independent everything.

**Pros**: Complete isolation, absolute safety  
**Cons**: Heaviest, slowest, highest cost  
**Best for**: Untrusted code, tasks involving sensitive data, production environment operations

> **Rule of Thumb**: Start with the lightest isolation level and upgrade only when problems arise. In most cases, branch-level + environment-level isolation is sufficient.

### 5.4 Worktree Lifecycle Management

Creating a Worktree is easy — the hard part is managing its lifecycle. A complete Worktree lifecycle includes:

1. **Creation**: When a task starts, create a new Worktree based on the main branch
2. **Initialization**: Install dependencies, configure environment, prepare data
3. **Execution**: Agent completes the task in the Worktree
4. **Cleanup**: After the task ends, delete the Worktree, free resources
5. **Archiving**: (Optional) Keep the Worktree for a period for debugging

The most easily overlooked part is the **cleanup step**. If Worktrees aren't cleaned up when tasks fail, your disk will quickly fill up with hundreds or thousands of abandoned Worktrees.

You need a "garbage collection" mechanism — periodically checking for timed-out, failed, or completed Worktrees and automatically cleaning them up.

### 5.5 Case Study: Ralph Loop's Worktree Practice

Ralph Loop's Worktree management is worth learning from. Its approach:

- Each issue corresponds to an independent Git branch and Worktree directory
- After task completion (whether success or failure), Worktree is automatically cleaned up
- If the task fails, the Worktree is kept for 24 hours for debugging, then auto-deleted
- A background task periodically checks and cleans up zombie Worktrees

This design ensures isolation while controlling resource costs. The key insight: **cleanup mechanisms are just as important as creation mechanisms.**

---

---
