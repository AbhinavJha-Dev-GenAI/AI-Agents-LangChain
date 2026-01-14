# 01. Agent Fundamentals 🤖🧠

An "Agent" is a system that uses an LLM as its "Reasoning Engine" to interact with the world, solve multi-step problems, and achieve goals autonomously.

## 1. What makes an Agent? 🧩

A simple chatbot responds to a prompt. An **Agent** follows a loop:
1.  **Planning**: Breaking down a complex goal into smaller steps.
2.  **Memory**: Remembering past interactions and tool outputs.
3.  **Tool Use**: Knowing when to call an external API, search the web, or run code.
4.  **Reasoning**: Evaluating the results of its actions and deciding what to do next.

---

## 2. Reasoning Patterns 🔄

### ReAct (Reason + Act)
The loop of **Thought**, **Action**, and **Observation**.
- *Thought*: "I need to find the price of Apple stock."
- *Action*: Call `get_stock_price(symbol="AAPL")`.
- *Observation*: "The price is $180."
- *Thought (Next)*: "Now I can answer the user's question..."

### Chain-of-Thought (CoT)
Encouraging the model to "think step-by-step" before providing a final answer. This drastically improves performance on logic and math tasks.

### Plan-and-Execute
First, the agent creates a full multi-step plan. Then, it executes each step one by one, refining the plan only if something fails.

---

## 3. Types of Agents 🎭

*   **Zero-shot Agents**: Receive a prompt and tool descriptions, and try to solve the task immediately.
*   **Conversational Agents**: Maintain a chat history while performing tasks.
*   **Self-Reflective Agents**: Critique their own work and regenerate if the quality is low (e.g., "Does this code have bugs? Yes. Fixing...").

---

## 🛠️ Essential Concept: The "Agentic" Shift

| Aspect | Standard LLM Call | Agentic Workflow |
| :--- | :--- | :--- |
| **Logic** | Linear (In -> Out) | Cyclic (Loop until Done) |
| **Tools** | None | API, SQL, Python, Search |
| **Error Handling** | Fails or Hallucinates | Retries / Corrects itself |

---

## 📊 Summary
Agents transition LLMs from "Consultants" who give advice to "Employees" who get things done. Understanding the **ReAct** loop is the single most important foundation for building any autonomous system.
