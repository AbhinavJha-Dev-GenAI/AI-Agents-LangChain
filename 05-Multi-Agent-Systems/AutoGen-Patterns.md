# AutoGen Patterns: Conversational Agent Teams 🤖💬

**AutoGen** (by Microsoft) is a framework that allows multiple agents to talk to each other to solve a task. Its core strength lies in its **conversational** nature and its ability to seamlessly incorporate humans into the loop.

---

## 🧩 The Core Agent: `ConversableAgent`

In AutoGen, every agent is "conversable." They can send messages, receive messages, and generate replies based on their internal logic or tools.

### Key Capabilities:
- **LLM-Based Reply**: Using a model to generate text.
- **Code Execution**: The agent can write *and run* Python code in a safe environment (Docker).
- **Human Feedback**: The agent can stop and ask a human for input.

---

## 🏗️ Common Interaction Patterns

### 1. Two-Agent Chat
Example: A **Coder** and a **Reviewer**. The Reviewer keeps finding bugs until the Coder produces a working script.

### 2. Group Chat (The "Room")
A **GroupChatManager** orchestrates a discussion between 5+ experts. It decides whose turn it is to speak based on the current context.
- **Use Case**: Strategic planning or architectural design.

### 3. Joint Human-AI Teams
A human acts as a "Proxy Agent." The AI proposes a solution, the human types "Add a login screen," and the AI updates the code.

---

## 🚀 Unique Feature: Code Execution

AutoGen agents are famous for being able to solve problems by **writing code**.
1.  **LLM**: Writes a Python script to calculate Fibonacci.
2.  **Executor**: Runs the script in a local environment.
3.  **LLM**: Sees the output (or the traceback error) and fixes the code dynamically.

---

## ⚖️ AutoGen vs. CrewAI

| Feature | AutoGen | CrewAI |
| :--- | :--- | :--- |
| **Logic** | Dynamic Conversation | Task/Role Based |
| **Code Execution** | First-class native feature | Requires specific tools |
| **Orchestration** | Peer-to-peer / Manager | Sequential / Hierarchical |
| **Best For** | Coding, Data Science | Business Workflow, Research |

---

## ✅ Best Practices

1.  **Dockerize Execution**: Never run agent-generated code directly on your host machine. Always use a Docker container.
2.  **Max Auto-Reply**: Set `max_consecutive_auto_reply` to prevent two agents from talking to each other forever.
3.  **System Messsage Precision**: Clearly define the termination keyword (e.g., "TERMINATE") so the agents know when to stop the loop.

---

**Next Steps**: Learn how to design these multi-agent systems for production-scale reliability in [`06-Agent-Architectures`](../06-Agent-Architectures/README.md).
