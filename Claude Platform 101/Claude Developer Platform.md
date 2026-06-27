# Claude Developer Platform

## What is the Claude Developer Platform?

The Claude Developer Platform is Anthropic's platform for building AI applications using Claude programmatically.

Instead of interacting with Claude through a chat interface, developers send structured API requests from their applications and receive structured responses. The platform gives full control over the AI model, prompts, tools, token usage, and application behavior.

---

# Components of the Claude Developer Platform

The platform consists of four main components:

## 1. REST API
The primary interface for communicating with Claude from any programming language using HTTP requests.

**Purpose:** Send prompts and receive responses programmatically.

---

## 2. SDKs
Official Software Development Kits that simplify working with the REST API.

**Purpose:** Reduce boilerplate code and make development easier in languages like Python, JavaScript, Java, and Go.

---

## 3. Command Line Interface (CLI)
A command-line tool for interacting with Claude directly from the terminal.

**Purpose:** Useful for testing, scripting, and automation.

---

## 4. Console
A web-based dashboard for managing Claude applications.

The console allows developers to:

- Manage API Keys
- Monitor API usage
- Track billing
- Test prompts
- Deploy managed agents
- View logs and application activity

---

# Claude Developer Platform Architecture

The platform can be understood as three layers.

```
                Controls
                   ▲
                   │
            Infrastructure
                   ▲
                   │
              Primitives
                   ▲
                   │
               Claude Model
```

---

# 1. Primitives

Primitives are the **core capabilities provided by Claude** that developers use to build AI applications.

Think of them as the building blocks of every Claude application.

Examples include:

- Messages API
- Tool Use
- Files
- Web Search
- Code Execution
- MCP Servers
- Skills

### Purpose

These capabilities are already built by Anthropic. Developers simply use and combine them to create intelligent applications.

---

# 2. Infrastructure

Infrastructure provides the services required to run AI applications reliably and at scale.

As applications grow from a few users to thousands, infrastructure ensures stability, performance, and scalability.

Examples include:

- Managed Agents
- Retries
- Queues
- Observability

### Purpose

Infrastructure handles the operational side of AI systems, ensuring they remain reliable and scalable in production.

---

# 3. Controls

Controls are the management and monitoring tools used once an AI application is deployed.

Examples include:

- Dashboards
- Evals
- Usage Monitoring

### Purpose

Controls help developers:

- Monitor application health
- Track token usage and costs
- Measure AI performance
- Evaluate prompt quality
- Improve production systems

---

# Quick Summary

| Layer | Purpose | Examples |
|--------|---------|----------|
| **Primitives** | Core AI capabilities provided by Claude | Messages API, Tool Use, Files, Web Search, Code Execution, MCP, Skills |
| **Infrastructure** | Services that make AI applications reliable and scalable | Managed Agents, Retries, Queues, Observability |
| **Controls** | Tools for monitoring, evaluating, and managing applications | Dashboards, Evals, Usage Monitoring |

---

# Simple Analogy

Imagine building a house:

- **Primitives** → Building materials (bricks, cement, steel)
- **Infrastructure** → Construction equipment and machinery
- **Controls** → CCTV, maintenance tools, and monitoring systems

Similarly:

- **Primitives** provide the AI capabilities.
- **Infrastructure** keeps the application running smoothly.
- **Controls** help monitor and improve the application after deployment.

---

# Key Takeaways

- The Claude Developer Platform allows developers to integrate Claude into their own applications.
- It consists of a REST API, SDKs, CLI, and a management Console.
- The platform is organized into three layers:
  - **Primitives** → AI capabilities
  - **Infrastructure** → Reliability and scalability
  - **Controls** → Monitoring and evaluation
- Together, these layers enable developers to build, deploy, and manage production-ready AI applications.
