"You review your own code? Then it's like not reviewing at all, right?"

This is common sense in software development: the person who writes code and the person who reviews it should be different people. Because when you're writing code, you get lost in the details and it's hard to see your own blind spots. An outsider's perspective is clearer — someone else looking at it can often spot problems at a glance.

The same principle applies to AI agents.

An agent that both writes code and checks it itself is like a student grading their own exam — it carries the same mental blind spots, and mistakes it made before are likely to be made again.

That's why we need Sub-agents.

### 8.1 What is a Sub-agent?

A Sub-agent is an independent agent created by the main agent (or the system) within a main loop, responsible for completing specific subtasks.

Sounds like team collaboration? Exactly — Sub-agents essentially move human team collaboration patterns into AI systems. What one person can't finish, divide among several people. Code one person can't review accurately, have someone else review it again.

### 8.2 Maker-Checker Pattern: The Classic Sub-agent Architecture

The most common and most effective sub-agent pattern is the **Maker-Checker pattern**.

- **Maker**: Responsible for writing code, implementing, producing results
- **Checker**: Responsible for reviewing code, verifying results, finding problems

What the Maker produces, the Checker finds faults in. What faults the Checker finds, the Maker fixes. Both sides iterate repeatedly until the Checker is satisfied.

Why does this pattern work? Because **different agents have different perspectives**:

- The Maker focuses on "how to implement" — its thinking is constructive, creative
- The Checker focuses on "what problems exist" — its thinking is critical, skeptical

These two modes of thinking are difficult for a single agent to possess simultaneously. Asking the same agent to be both player and referee, it can hardly switch modes.

> **Core Insight**: Having an agent check its own code gives linear efficiency improvement. Having two different agents check each other's work gives exponential quality improvement.

### 8.3 Sub-agent Division Modes

Maker-Checker is just the most basic pattern. Depending on task complexity, sub-agents can have richer division-of-labor approaches.

#### Mode One: By Responsibility

Different sub-agents are responsible for different responsibilities. For example:

- **Architect agent**: Responsible for overall方案 design and technology selection
- **Developer agent**: Responsible for concrete code implementation
- **Tester agent**: Responsible for writing tests and doing verification
- **Security agent**: Responsible for security auditing
- **Documentation agent**: Responsible for writing docs and comments

This is like a complete development team, each person (agent) has their own role.

#### Mode Two: By Module

Split a large task into multiple modules, each sub-agent负责 one module. For example, refactoring a large system:

- Agent A负责 the frontend module
- Agent B负责 the API layer
- Agent C负责 the database layer
- Agent D负责 integration and joint debugging

This division method works well for scenarios with clear task boundaries and low coupling between modules.

#### Mode Three: By Perspective (Red Team / Blue Team)

Not divided by work content, but by stance. For example, evaluating a technical proposal:

- **Blue team agent**: Responsible for arguing the feasibility and advantages of the proposal
- **Red team agent**: Responsible for finding faults, identifying risks, raising objections
- **Judge agent**: Synthesizes both sides' opinions, makes the final judgment

This pattern is best for decision-making tasks — when you need to comprehensively consider pros and cons, having agents of different stances debate each other is far more thorough than one agent thinking it through alone.

### 8.4 The Coordination Challenge of Sub-agents

Sub-agents sound great, but in practice you run into many problems. The hardest part isn't creating sub-agents — it's **coordinating them**.

Several typical coordination challenges:

#### Challenge One: Context Transfer

How does the main agent completely pass task background, relevant information, and constraints to the sub-agent? Pass too little and the sub-agent can't do a good job; pass too much and it wastes tokens.

**Solution**: Design standardized task description templates containing four elements: goal, background, constraints, deliverables.

#### Challenge Two: Result Integration

Results produced by multiple sub-agents — how to integrate them together? If two sub-agents' results conflict, who do you listen to?

**Solution**: Clearly define each sub-agent's responsibility boundaries to avoid overlap. Set up an "integration agent" specifically responsible for merging and coordinating results.

#### Challenge Three: Cost Control

Work that one agent could finish, split among five agents — token costs multiply several times. Is it worth it?

**Solution**: Decide based on task importance and complexity. Simple tasks don't need splitting; high-risk tasks才 need multi-agent cross-verification.

#### Challenge Four: Communication Overhead

Communication between agents also costs money. Going back and forth discussing for half the day, it might have been faster for one agent to just do it directly.

**Solution**: Minimize direct interaction between agents, let the main agent do information relay and coordination. Design clear interfaces and delivery standards.

### 8.5 Case Study: AddWeb AI's 7-Agent Self-Correction Loop

AddWeb AI is an edtech company that built a self-correction loop system of 7 specialized agents for developing their education platform.

The 7 agents are:

1. **Product Manager Agent**: Defines requirements and acceptance criteria
2. **Architect Agent**: Designs technical approach
3. **Frontend Agent**: Implements frontend code
4. **Backend Agent**: Implements backend code
5. **Tester Agent**: Writes tests and verifies functionality
6. **Security Agent**: Performs security audits
7. **Review Agent**: Synthesizes all feedback, decides whether to pass

A requirement, from entering the system to final delivery, goes through the relay of these 7 agents. Each agent only does what it's best at, then passes it to the next. If a problem is found at any stage, it's sent back to the previous stage for correction.

What was the result? Their education platform development cycle went from the traditional 16-20 weeks down to a stage every 4 weeks.

This case teaches us: **specialized division of labor + closed-loop collaboration = qualitative leap.**

---

---
