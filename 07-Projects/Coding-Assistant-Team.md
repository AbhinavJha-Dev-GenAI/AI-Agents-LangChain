# Project Roadmap: Multi-Agent Coding Team 💻🤖

This project demonstrates how to orchestrate a team of specialized agents (Developer, Reviewer, Tester) to solve a complex coding task autonomously.

---

## 🏗️ Team Architecture

### 1. The Architect / PM (Supervisor)
- **Role**: Plans the implementation.
- **Workflow**: Breaks the user request into a list of specific files to create or functions to update.

### 2. The Developer (Worker)
- **Role**: Writes the code.
- **Backstory**: "A senior Python developer with a focus on PEP 8 and clean architecture."
- **Tool**: `FileWriteTool`.

### 3. The Reviewer / Tester (QA)
- **Role**: Critiques the code.
- **Mechanism**: Use a Python REPL to run the code. If it fails, capture the traceback and send it back to the Developer.
- **Logic**: Only approve the task when all tests pass.

---

## 🧩 Key MAS Patterns Used

- **Self-Correction**: The Developer and Reviewer form a loop.
- **Hierarchical Delegation**: The Architect assigns sub-tasks to the Developer.
- **Shared State**: All agents have access to a shared `workspace/` directory.

---

## 🛠️ Implementation Steps

### Level 1: One-off Script Coder
A simple loop where an LLM writes code and a Python interpreter runs it, repeating until successful.

### Level 2: Multi-File Project Manager (CrewAI)
Assign roles to agents and use `kickoff()` to run a sequential or hierarchical process.
- **Task 1**: Research requirements.
- **Task 2**: Write implementation.
- **Task 3**: Write unit tests.
- **Task 4**: Execute and Verify.

---

## 🛡️ Safety & Guardrails
- **Dockerization**: **WARNING**: Never allow an agent to execute code directly on your host. Use the `langchain-experimental` Docker REPL tool.
- **Network Isolation**: Prevent the coding agent from accessing the internet unless specifically required.

---

**Next Steps**: See the research that inspired these multi-agent workflows in [`08-Research-Papers`](../08-Research-Papers/README.md).
