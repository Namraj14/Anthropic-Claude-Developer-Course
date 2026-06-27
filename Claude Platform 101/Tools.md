# Tools in Claude

## What are Tools?

Tools allow Claude to interact with external systems and perform actions beyond generating text.

A tool is simply a **function defined by the developer**. Claude cannot execute the function itself—it can only decide **when** to use it.

The developer is responsible for executing the tool and returning the result to Claude.

> **Claude decides. Your application executes.**

---

# Why Do We Need Tools?

Without tools, Claude can only answer using its knowledge.

With tools, Claude can:

- Query databases
- Call REST APIs
- Read Salesforce records
- Send emails
- Create Jira tickets
- Search the web
- Execute business logic

Tools extend Claude's capabilities beyond conversation.

---

# How Tools Work

The communication follows this flow:

```text
User
   │
   ▼
Claude
   │
Decides Tool is Needed
   │
   ▼
Requests Tool
   │
   ▼
Your Application Executes Tool
   │
   ▼
Returns Tool Result
   │
   ▼
Claude Continues Reasoning
   │
   ▼
Final Response
```

---

# Defining a Tool

Every tool is described using a **JSON Schema**.

A tool consists of three parts:

- **name** – Unique identifier for the tool.
- **description** – Explains what the tool does and when Claude should use it.
- **input_schema** – Defines the expected input parameters.

Example:

```json
{
  "name": "get_weather",
  "description": "Retrieve the current weather for a given city.",
  "input_schema": {
    "type": "object",
    "properties": {
      "city": {
        "type": "string"
      }
    }
  }
}
```

All tools are sent to Claude in the request using a **tools array**.

```text
Request
│
├── model
├── messages
└── tools[]
```

---

# Importance of Tool Descriptions

The tool description tells Claude **when the tool should be used**.

Poor description:

```text
Gets weather.
```

Good description:

```text
Returns the current weather conditions for a specified city.
Use this tool whenever the user asks about today's weather or current temperature.
```

> **The quality of the description directly affects Claude's decision-making.**

Vague descriptions are one of the most common reasons agents choose the wrong tool.

---

# stop_reason = "tool_use"

When Claude decides it needs a tool, it does **not** return a final answer.

Instead, the response contains:

```text
stop_reason = "tool_use"
```

This means:

1. Pause the conversation.
2. Execute the requested tool.
3. Return the tool result to Claude.
4. Continue the conversation.

Only after receiving the tool result can Claude generate the final response.

---

# Multiple Tools

Applications often expose several tools.

Example:

- get_weather
- create_case
- send_email
- search_products

When Claude requests a tool, your application checks the tool name and executes the correct function.

```text
Claude
    │
    ▼
Requested Tool
    │
    ▼
Switch / If-Else
    │
 ┌──┴────────────┐
 │               │
Weather      Send Email
 │               │
 ▼               ▼
Execute      Execute
```

Adding a new tool usually involves:

1. Adding the tool definition to the `tools[]` array.
2. Adding logic to execute that tool.

---

# SDK Tool Runner

Anthropic SDKs (TypeScript, Python, Ruby) include a **Tool Runner**.

Instead of manually:

- Checking `stop_reason`
- Executing tools
- Sending tool results back
- Repeating the loop

The SDK can manage the process automatically.

```text
Without Tool Runner

Claude
   │
tool_use
   │
Your Code
   │
Execute Tool
   │
Return Result
   │
Claude
```

```text
With Tool Runner

Claude
   │
SDK Tool Runner
   │
Automatically Executes Tool
   │
Returns Result
   │
Claude
```

This reduces boilerplate code and simplifies development.

---

# Delegating the Loop

There are three levels of responsibility.

### Level 1 – Manual

You manage everything.

- Agent loop
- Tool execution
- Tool results
- Retries

Maximum control.

---

### Level 2 – SDK Tool Runner

The SDK manages the tool execution loop.

You only provide the tool functions.

Less code, same flexibility.

---

### Level 3 – Managed Agents

Anthropic manages the entire agent.

They handle:

- Agent loop
- Tool execution
- Infrastructure
- Scaling
- Retries

You simply configure the agent and provide the tools.

---

# Responsibility Breakdown

| Responsibility | Developer | SDK Tool Runner | Managed Agent |
|----------------|-----------|-----------------|---------------|
| Define Tools | ✅ | ✅ | ✅ |
| Execute Tools | ✅ | Automatically | Automatically |
| Manage Agent Loop | ✅ | Automatically | Automatically |
| Handle Retries | ✅ | Partially | ✅ |
| Manage Infrastructure | ✅ | ❌ | ✅ |

---

# Quick Summary

| Concept | Description |
|----------|-------------|
| Tool | A developer-defined function Claude can request |
| JSON Schema | Describes the tool's name, purpose, and inputs |
| `tools[]` | Array containing all available tools |
| Tool Description | Helps Claude decide when to use a tool |
| `stop_reason = "tool_use"` | Indicates Claude wants a tool executed |
| Tool Runner | SDK feature that automates the tool execution loop |
| Managed Agent | Anthropic manages the entire agent loop and infrastructure |

---

# Key Takeaways

- Tools allow Claude to interact with external systems.
- Claude decides **when** to call a tool; your application executes it.
- Every tool is defined using a JSON schema containing a name, description, and input schema.
- Tool descriptions should be specific to improve Claude's decision-making.
- When `stop_reason` is `tool_use`, execute the tool and return the result to Claude.
- Multiple tools are managed by dispatching based on the requested tool name.
- SDK Tool Runners can automate the execution loop.
- Managed Agents delegate the entire agent loop and infrastructure to Anthropic.
