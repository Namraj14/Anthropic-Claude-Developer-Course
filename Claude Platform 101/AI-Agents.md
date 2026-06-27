# Understanding AI Agents

## What is an AI Agent?

An AI Agent is **Claude running in a continuous loop**.

Instead of answering just one question, Claude repeatedly:

1. Observes the current situation.
2. Decides what to do next.
3. Uses tools if needed.
4. Receives the tool's result.
5. Thinks again.
6. Repeats until the task is complete.

This is known as the **Agent Loop**.

---

# The Agent Loop

```text
        User Request
              │
              ▼
        Claude Observes
              │
              ▼
      Decides Next Action
              │
              ▼
     Needs a Tool?
       │          │
      No         Yes
       │          │
       ▼          ▼
  Final Answer  Run Tool
                   │
                   ▼
          Tool Returns Result
                   │
                   ▼
         Claude Thinks Again
                   │
                   ▼
        Continue or Finish?
```

The loop continues until Claude determines the task is complete.

---

# How the Loop Works

Every iteration follows the same pattern:

```text
Send Messages
      │
      ▼
Claude Reasons
      │
      ▼
Tool Requested?
      │
      ▼
Run Tool
      │
      ▼
Return Tool Result
      │
      ▼
Claude Continues Thinking
      │
      ▼
Repeat
```

The loop stops when Claude returns:

```text
stop_reason = end_turn
```

This means Claude has finished the task and no further tool calls are required.

---

# Who Owns What?

One of the most important concepts is understanding the responsibilities.

| You (Developer) | Claude |
|-----------------|--------|
| Create the loop | Thinks and reasons |
| Build the tools | Decides which tool to use |
| Execute tool calls | Interprets tool results |
| Return tool results | Determines the next action |
| Stop when instructed | Produces the final response |

### Simple Rule

> **You own the execution. Claude owns the intelligence.**

---

# Example

Suppose the user asks:

```text
What's the weather in Mumbai today?
```

The workflow becomes:

```text
User
      │
      ▼
Claude
      │
      ▼
"I need weather information."
      │
      ▼
Request Weather Tool
      │
      ▼
Your Application Calls Weather API
      │
      ▼
Returns:
30°C, Sunny
      │
      ▼
Claude Reads Result
      │
      ▼
Generates Final Answer
```

Claude never calls the Weather API directly.

Your application does.

---

# Why is it Called an Agent?

Unlike a normal chatbot:

```text
Question
      │
      ▼
Answer
```

An agent can:

- Think
- Plan
- Use tools
- Gather information
- Continue reasoning
- Complete multi-step tasks

It behaves more like an assistant than a simple chatbot.

---

# Scalability

The same agent loop works for every application.

Small Demo:

```text
Claude
      │
      ▼
Weather Tool
```

Production Application:

```text
Claude
      │
      ├── Salesforce
      ├── Slack
      ├── Jira
      ├── GitHub
      ├── Database
      ├── Email Service
      └── Internal APIs
```

The loop never changes.

Only the available tools change.

---

# Managed Agents

Sometimes you don't want to manage:

- The loop
- Tool execution
- Infrastructure
- Scaling
- Retries

Anthropic provides **Managed Agents**.

With Managed Agents:

```text
Your Application
        │
        ▼
Managed Agent
        │
        ▼
Claude
        │
        ▼
Tools
```

Anthropic manages the entire agent loop for you.

You simply configure the agent and provide the necessary tools.

---

# Developer-Owned vs Managed Agents

| Developer-Owned Agent | Managed Agent |
|------------------------|---------------|
| You write the loop | Anthropic manages the loop |
| You execute tools | Anthropic manages execution |
| You handle retries | Anthropic handles retries |
| More control | Easier to build |
| More responsibility | Less operational work |

---

# Quick Summary

| Concept | Description |
|----------|-------------|
| Agent | Claude running in a continuous reasoning loop |
| Observe | Claude reads the current conversation and tool outputs |
| Decide | Claude determines the next action |
| Act | Claude requests a tool or responds to the user |
| Repeat | Continue until the task is complete |
| `stop_reason = end_turn` | Signals that the agent has finished |

---

# Key Takeaways

- An AI Agent is **Claude running in a loop**.
- The loop follows: **Observe → Decide → Act → Repeat**.
- Your application sends messages, executes tool calls, and returns the results.
- Claude is responsible for reasoning and deciding what to do next.
- The loop ends when `stop_reason` is `end_turn`.
- The same loop powers everything from simple demos to enterprise AI systems.
- Managed Agents allow Anthropic to manage the agent loop and infrastructure on your behalf.
