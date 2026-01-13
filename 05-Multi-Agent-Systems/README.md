# 05. Multi-Agent Systems (MAS) 🤝

One agent is powerful, but a **team of agents** is unstoppable. Multi-agent systems involve specialized agents working together to solve problems that are too complex for a single LLM.

---

## 🏗️ Interaction Patterns

### 1. Manager Pattern (Hierarchical)
One "Boss" agent receives the task, breaks it down, and assigns sub-tasks to specialized "Worker" agents.
- **Best For**: Enterprise workflows where quality control is critical.
- **Framework**: **CrewAI** (Manager role).

### 2. Collaborative Pattern (Joint Chat)
Agents talk to each other in a common chat room. One agent might suggest code, another might review it, and a third might test it.
- **Best For**: Creative problem solving and open-ended research.
- **Framework**: **AutoGen**.

### 3. Sequential Pattern (Relay)
Agent A passes its output to Agent B, who passes it to Agent C.
- **Best For**: Fixed pipelines (e.g., Blog Post Generation: Researcher -> Writer -> Editor).

---

## 🚀 Frameworks to Know

### 1. [CrewAI Deep Dive](./CrewAI-Deep-Dive.md)
Mastering the Role-Goal-Backstory framework. Focus on structured business workflows and hierarchical team management.

### 2. [AutoGen Patterns](./AutoGen-Patterns.md)
Conversational agents that can write and execute code. Best for dynamic, peer-to-peer problem solving and human-proxy interactions.

### 3. LangGraph for Multi-Agent
Using stateful graphs to define custom, high-precision handoffs between agents.

---

## 🧩 Key MAS Concepts

- **Delegation**: Can an agent ask another agent for help?
- **Shared State**: Do all agents see the same memory, or do they only see what is passed to them?
- **Termination**: How does the team know when the project is finished? (e.g., specific keyword or max iterations).

---

## ⚖️ Single Agent vs. Multi-Agent

| Feature | Single Agent | Multi-Agent |
| :--- | :--- | :--- |
| **Context Window** | Fills up quickly | Distributed across agents |
| **Specialization** | Generalist (Jack of all trades) | Experts (Specialized tools) |
| **Latency** | Lower | Higher (Sequential turns) |
| **Complexity** | Easy to debug | Challenging (Emergent behavior) |

---

**Next Steps**: Now that you understand the team dynamics, learn how to design these systems for production in [`06-Agent-Architectures`](../06-Agent-Architectures/).
