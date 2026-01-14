# 06. Agent Architectures 🏛️🧩

Designing a production-grade agent requires more than just a loop. It requires a "Cognitive Architecture" that manages how the agent thinks, remembers, and acts.

## 1. The Reasoning Engine 🧠

The core of the architecture is the **Reasoning Loop**.
- **ReAct**: The most common.
- **Reflexion**: Adding a "Self-Correction" step where the agent critiques its own past action before deciding the next one.
- **Tree of Thoughts**: The agent explores multiple branches of reasoning in parallel and picks the best one.

---

## 2. Planning Strategies 🗺️

*   **Task Decomposition**: Breaking a big goal (e.g., "Build a website") into small, actionable steps.
*   **Dynamic Re-planning**: If Step 2 fails (e.g., the API is down), the agent dynamically changes Step 3 and 4.

---

## 3. Memory Architectures 💾

An agent's memory is divided into two parts:
1.  **Short-term (Scratchpad)**: Current conversation history and intermediate tool outputs. This is usually stored in the LLM prompt.
2.  **Long-term (RAG)**: Billions of documents indexed in a Vector DB. The agent "retrieves" only what it needs for the current task.

---

## 4. Design Patterns for Reliability 🛡️

*   **Human-in-the-Loop (HITL)**: For critical actions (e.g., sending an email or deleting a file), the agent *must* pause and wait for a human "OK."
*   **Max Iterations**: Always set a hard limit (e.g., 10 loops) to prevent your agent from getting stuck in an "Infinite Loop" and burning your API credits.
*   **Schema Enforcement**: Use Pydantic to ensure that the agent's tool calls and final answers always follow a specific format.

---

## 🛠️ Essential Comparison

| Pattern | Best For... | Complexity |
| :--- | :--- | :--- |
| **Linear Chain** | Simple, predictable tasks. | Low |
| **Simple Agent** | Research, tool calling. | Medium |
| **Self-Reflective** | Coding, complex analysis. | High |
| **Multi-Agent** | Enterprise workflows. | Very High |

---

## 🌍 Summary
Architectures are about **Constraint**. A completely "Free" agent is dangerous and unpredictable. A well-architected agent has clear guardrails, specific tools, and a structured way to handle its own mistakes.
