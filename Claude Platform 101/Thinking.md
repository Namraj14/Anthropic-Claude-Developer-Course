# Extended Thinking in Claude

## What is Extended Thinking?

Extended Thinking is a feature that gives Claude additional time to **reason and analyze** before generating a response.

Instead of answering immediately, Claude spends extra time thinking through the problem, making it better at solving complex tasks.

Think of it as:

> **Normal Mode** → Answer immediately.

> **Extended Thinking** → Think first, then answer.

---

# Why Use Extended Thinking?

Some problems require more than a quick response.

Examples:

- Complex coding problems
- Architecture design
- Multi-step reasoning
- Mathematical proofs
- Business strategy
- Trade-off analysis
- Agent planning

Extended Thinking allows Claude to spend more effort on these types of problems.

---

# How It Works

Normal Response

```text
User
   │
   ▼
Claude
   │
   ▼
Answer
```

Extended Thinking

```text
User
   │
   ▼
Claude
   │
Think...
Analyze...
Reason...
Compare Options...
Plan...
   │
   ▼
Final Answer
```

---

# Enabling Extended Thinking

For Claude Opus 4.7, Extended Thinking is enabled by adding:

```json
thinking: {
    "type": "adaptive"
}
```

Unlike older versions, you do **not** specify a thinking token budget.

Claude automatically decides:

- Whether thinking is needed.
- How much thinking is required.

This is why it's called **Adaptive Thinking**.

---

# Thinking Effort Levels

You can control how much reasoning Claude performs using the `effort` parameter inside `output_config`.

Available levels:

- **low**
- **medium**
- **high** (default)
- **xhigh**
- **max**

Example:

```text
output_config
    │
    ▼
effort = medium
```

---

# What Each Level Means

### Low

- Fast responses
- Minimal reasoning
- Lower token usage

Best for:

- Simple questions
- Basic coding
- Summaries

---

### Medium

- Balanced reasoning
- Faster than High
- Good for everyday development

Best for:

- API design
- Standard programming tasks
- Documentation

---

### High (Default)

- Strong reasoning
- Better decision making
- More detailed analysis

Best for:

- Complex coding
- Architecture discussions
- Technical explanations

---

### XHigh

- Deep reasoning
- More planning
- Better handling of difficult problems

Best for:

- Multi-step workflows
- AI Agents
- System Design
- Large codebases

---

### Max

- Maximum reasoning effort
- Highest quality
- Slowest response
- Highest token usage

Best for:

- Research
- Difficult debugging
- Critical business decisions
- Advanced planning

---

# When Should You Use It?

Use Extended Thinking for:

- Complex programming
- Architecture design
- Agent planning
- Business decisions
- System design
- Root cause analysis
- Comparing multiple solutions
- Trade-off discussions

---

# When Should You Avoid It?

Do **not** use Extended Thinking for simple tasks like:

- Greeting users
- Grammar corrections
- Basic Q&A
- Simple summaries
- Simple CRUD code
- Small calculations

For these tasks it only increases:

- Response time (latency)
- Token consumption
- Cost

without improving the answer significantly.

---

# Trade-Off

```text
More Thinking
      │
      ▼
Better Quality
      ▲
      │
Higher Cost
Longer Latency
More Tokens
```

There is always a balance between quality and speed.

---

# Example

Simple Question

```text
User:
What is Apex?
```

Normal response is sufficient.

---

Complex Question

```text
Design a scalable Salesforce integration
between SAP, MuleSoft, and Salesforce
handling retries, failures, and event-driven
communication.
```

Extended Thinking is recommended because Claude needs to:

- Analyze requirements
- Compare architectures
- Consider trade-offs
- Plan the solution
- Explain the design

---

# Salesforce Analogy

Think of Extended Thinking like assigning work to different developers.

### Low

Junior Developer

Quick answer.

---

### Medium

Mid-Level Developer

Some analysis before implementation.

---

### High

Senior Developer

Considers architecture and best practices.

---

### Max

Technical Architect

Evaluates multiple solutions, compares trade-offs, and designs the best long-term approach.

---

# Quick Summary

| Concept | Description |
|----------|-------------|
| Extended Thinking | Gives Claude additional reasoning time before answering |
| Adaptive Thinking | Claude decides automatically whether and how much to think |
| thinking.type | `"adaptive"` |
| effort | Controls reasoning depth |
| Levels | low, medium, high, xhigh, max |
| Best For | Complex reasoning and planning |
| Avoid For | Simple tasks where extra reasoning isn't needed |

---

# Key Takeaways

- Extended Thinking allows Claude to reason before answering.
- Enable it using `thinking: { "type": "adaptive" }`.
- Claude automatically decides how much thinking is needed.
- The `effort` parameter controls reasoning depth.
- Higher effort generally improves answer quality but increases latency, token usage, and cost.
- Use Extended Thinking for complex problems and avoid it for simple requests.
