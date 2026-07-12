An AI agent that can only read and write code files can do very limited things.

It wants to reproduce a bug? It needs to be able to run tests.  
It wants to check data in the database? It needs to connect to the database.  
It wants to see user feedback? It needs to read the support ticket system.  
It wants to deploy a version? It needs to call the deployment platform.

If an agent can only spin around in code files, it's like a craftsman locked in a room — no matter how skilled, it can't accomplish much.

That's why we need Plugins and Connectors.

### 7.1 What Are Plugins and Connectors?

**Plugins** are extension modules that add specific capabilities to agents. For example, the GitHub plugin lets agents operate GitHub, the Slack plugin lets agents send messages, the database plugin lets agents query data.

**Connectors** are a more general concept — they refer to all mechanisms by which agents connect to external systems. Plugins are one form of Connector implementation, MCP servers are another, API integrations are another.

Put simply: **Plugins & Connectors solve the problem of "how far an agent's hands can reach."**

### 7.2 MCP: The Standard Protocol for Connection

When talking about Connectors, you can't avoid MCP (Model Context Protocol).

MCP is an open protocol proposed by Anthropic that defines standard interaction methods between AI agents and external tools. Before MCP, each tool had its own integration method, and agents had to be redeveloped to connect to each new tool. After MCP, as long as a tool supports the MCP protocol, agents can use it directly.

It's like the USB interface — with the USB standard, you don't have to design a separate interface for each peripheral, just plug it in.

MCP's core concepts are simple:

- **MCP Server**: A service provided by an external tool, exposing a set of tool functions
- **MCP Client**: The client on the agent side, calling tools provided by the Server
- **Tool call protocol**: Standard request/response format

The significance of MCP is that it turns "agents connecting to the world" from a project that requires custom integration one by one, into an ecosystem that can scale systematically.

> **Importance**: If large language models are the CPU of the AI era, then MCP is the USB bus of the AI era.

### 7.3 Categories of Connectors

Agents need to connect to all kinds of systems. We can divide them into several major categories:

#### Code & Version Control

- **Git/GitHub/GitLab**: Read code, submit PRs, manage issues, code review
- **Code search tools**: Sourcegraph, local search
- **CI/CD systems**: Jenkins, GitHub Actions, GitLab CI

#### Data & Storage

- **Databases**: MySQL, PostgreSQL, MongoDB, Redis
- **Data warehouses**: BigQuery, Snowflake, ClickHouse
- **Object storage**: S3, OSS

#### Communication & Collaboration

- **Instant messaging**: Slack, Feishu, Discord, Teams
- **Project management**: Jira, Linear, Trello, Asana
- **Document systems**: Notion, Feishu Docs, Confluence, Google Docs

#### Monitoring & Operations

- **Monitoring systems**: Prometheus, Grafana, Datadog
- **Logging systems**: ELK, Loki
- **Alerting systems**: PagerDuty, Opsgenie
- **Cloud platforms**: AWS, GCP, Azure

#### Business Systems

- **CRM**: Salesforce, HubSpot
- **Customer service**: Zendesk, Intercom
- **Finance**: QuickBooks, Xero

Each category of system you connect expands the agent's capability boundary. The more connections, the more complete the things agents can do.

### 7.4 Security Boundaries of Connectors

With great power comes great risk. Connecting connectors to agents isn't about connecting as many as possible — you need to carefully consider security boundaries.

Several key security principles:

#### Principle One: Principle of Least Privilege

Agents should only have the minimum privileges necessary to complete their tasks. They need to read the database? Give read-only access. They need to send messages? Only give messaging permissions for specific channels. They need to deploy? Only give deployment permissions for the test environment.

Never give an agent admin privileges. Never.

#### Principle Two: Audit Log Principle

Every external operation an agent performs must have complete audit logs. Who (which agent), when, what operation was performed, what the result was — all must be recorded.

Audit logs aren't just for tracing problems — they let you observe and analyze agents' behavior patterns.

#### Principle Three: Human Confirmation Principle

For high-risk operations (like deleting data, modifying production environment configurations, transferring money), there must be a human confirmation step. Agents can initiate operations, but must wait for human approval before execution.

This isn't about not trusting agents — it's engineering discipline. Human engineers go through approval processes for high-risk operations too — why should agents be exceptions?

### 7.5 Case Study: Minglue Technology's Agent Connector Practice

Minglue Technology is a company with over 1,400 employees and 2,900+ deployed AI agents. Their agents handle various tasks like financial reporting, customer service, and data analysis.

Their Connector system has several characteristics:

1. **Layered authorization**: Different levels of agents have different Connector access permissions. Basic agents can only read public data, while advanced agents can access sensitive systems.
2. **Unified gateway**: All external calls from agents go through a unified gateway that handles authentication, rate limiting, and auditing.
3. **Operation分级**: Operations are divided into three levels: "read," "write," and "execute." Read operations can execute automatically, write operations require approval, and execute operations (like deployment) require double confirmation.

This system allows their 2,900+ agents to work efficiently without going out of control. The core lesson: **connector design is essentially trust boundary design.**

---

---
