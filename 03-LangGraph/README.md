# 03. LangGraph: Stateful Agents 🕸️

While LangChain is great for Directed Acyclic Graphs (DAGs), real-world agents are often **cyclic**. **LangGraph** is a library for building stateful, multi-agent applications with LLMs.

---

## 🏗️ Why LangGraph?

Standard chains have no "cycles" — you can't easily go back from Step 3 to Step 1. LangGraph allows:
1.  **Cyclic Graphs**: Loop back for self-correction or multi-turn reasoning.
2.  **Fine-grained State Management**: Control exactly what data passes between steps.
3.  **Human-in-the-Loop**: Pause the graph, wait for human approval, and resume.

---

## 🧩 Core Concepts

### 1. [Nodes & Edges](./Graphs-Nodes-Edges.md)
The foundational building blocks of a graph. Nodes perform work, and edges define the flow of control.

### 2. [State & Persistence](./State-Persistence.md)
How to manage shared memory and ensure agents survive crashes and support long-running tasks.

### 3. [Time Travel & Debugging](./Time-Travel-Debugging.md)
The ability to rewind, inspect, and fork an agent's state to fix errors and analyze performance.

---

## 🛠️ Advanced Features

### Persistence (Checkpointers)
LangGraph can save the state of a thread to a database (SQLite, Postgres, etc.).
- **Benefit**: If your server crashes, the agent can resume right where it left off.
- **Threads**: Support multiple concurrent conversations effortlessly.

### Time Travel ⏳
Because state is versioned (checkpointed), you can:
1.  **View** previous states of the graph.
2.  **Rewind** to a specific step.
3.  **Fork** a state to test a different path or correct an LLM error manually.

---

## 🚀 Building a Self-Correction Agent (Self-RAG)

A classic LangGraph pattern:
1.  **Retrieve**: Fetch docs.
2.  **Grade**: Are these docs relevant?
3.  **Generate**: If yes, generate answer.
4.  **Reflect**: Does the answer actually address the user query?
5.  **Loop**: If no, go back to Search or Refine.

---

## 📊 LangGraph vs. LangChain LCEL

| Feature | LCEL | LangGraph |
| :--- | :--- | :--- |
| **Logic** | Linear / Branching | Cyclic |
| **State** | Implicit / Hard to manage | Explicit & Persistent |
| **Memory** | Basic Chat History | Full State Persistence |
| **Complex Teams** | Very Difficult | Native Support |

---

**Next Steps**: Learn how to bridge your graph to the real world in [`04-Tool-Integration`](../04-Tool-Integration/).
