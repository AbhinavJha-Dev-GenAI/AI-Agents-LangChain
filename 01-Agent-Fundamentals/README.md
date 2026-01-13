# 01. Agent Fundamentals 🧠

Welcome to the foundation of **Agentic AI**. Before diving into frameworks like LangChain or LangGraph, it is crucial to understand the "Brain" of an agent: **Reasoning Patterns**.

---

## 🏗️ What is an AI Agent?

An agent is more than just an LLM in a loop. While a **Chain** follows a hardcoded path (A -> B -> C), an **Agent** uses the LLM as a **reasoning engine** to determine:
1.  **Which action** to take next.
2.  **When** to stop and return a final answer.

### The Agent Equation:
`Agent = LLM + Planning + Memory + Tool Use`

---

## 🧩 Reasoning Patterns

### 1. [Chain-of-Thought (CoT)](./Chain-of-Thought.md)
Encouraging the model to generate intermediate steps of reasoning.  
**Prompt Style**: *"Let's think step by step."*

### 2. [ReAct (Reason + Act)](./ReAct-Pattern.md)
The industry standard for agentic loops. It combines reasoning traces and task-specific actions.
- **Thought**: The model thinks about the current state.
- **Action**: The model picks a tool to use.
- **Observation**: The model reads the output of the tool.
- *Repeat until finish.*

### 3. [Plan-and-Execute](./Plan-and-Execute.md)
Useful for complex tasks where a single loop might get lost.
- **Plan**: Create a multi-step roadmap first.
- **Execute**: A worker agent performs each step of the plan.
- **Re-plan**: Update the roadmap based on results.

---

## 🤖 Types of Agents

| Type | Description | Best For |
| :--- | :--- | :--- |
| **Zero-Shot** | Uses only the description of tools to decide the first move. | Simple, one-off tasks. |
| **Conversational** | Maintains chat history to provide context-aware answers. | Customer support, personal assistants. |
| **ReAct Agent** | Explicitly uses the Thought/Action/Observation loop. | Tool-heavy workflows (Search, DB query). |
| **Self-Reflection** | Evaluates its own response and corrects if wrong. | Coding, high-accuracy data extraction. |

---

## 🛠️ The Prompt: The Agent's Operating System

An agent's behavior is dictated by its **System Prompt**. A typical agent prompt template includes:
- **Role**: "You are a research assistant..."
- **Tool List**: Descriptions of what each tool does.
- **Format Instructions**: "You must only respond in JSON..."
- **Constraints**: "Never search for private data..."

---

## 🚀 Key Takeaways for Engineers

1.  **Stop Hardcoding**: Move from "If-Else" logic to "LLM-Reasoning" logic.
2.  **Latent reasoning is key**: Giving the model "space to think" (CoT) significantly reduces hallucinations.
3.  **Agents are non-deterministic**: Debugging requires tracing (LangSmith) rather than just logs.

---

**Next Steps**: Head over to [`02-LangChain`](../02-LangChain/) to see how to implement these patterns using the LCEL framework.
