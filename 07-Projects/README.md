# 07. Hands-on Agent Projects 🚀

The best way to learn agents is to build them. This folder provides architectural roadmaps for projects ranging from simple search tools to complex multi-agent teams.

---

## 🟢 Beginner: Single-Agent Utilities

### 1. [CSV / SQL Data Analyst](./Data-Analyst-Agent.md)
Talk to your database. Master schema injection, self-correcting SQL, and automated visualization.

### 2. [Multi-Agent Coding Team](./Coding-Assistant-Team.md)
Team of 3 agents (Developer, Reviewer, Tester) working together to solve GitHub issues autonomously.

### 3. Autonomous Support Agent
Standard ReAct agent with RAG access and Human-in-the-loop escalation.

---

## 🟡 Intermediate: Stateful & Data Agents

### 3. CSV / SQL Data Analyst
**Goal**: An agent that can talk to a database, generate SQL/Python code, execute it, and create charts.
- **Tech**: LangChain `create_sql_agent` or custom LangGraph CSV logic.
- **Key Learning**: Handling structured data, error correction (retrying failed SQL), and visualization.

### 4. Autonomous Social Media Manager
**Goal**: An agent that researches trending news in a specific niche and drafts scheduled LinkedIn/Twitter posts.
- **Tech**: LangGraph (for scheduling state), Google Search API.
- **Key Learning**: Long-term state management and tone-of-voice alignment.

---

## 🔴 Advanced: Multi-Agent & Production

### 5. Multi-Agent Coding Team (The "Software House")
**Goal**: A team of 3 agents working together to solve a GitHub issue.
- **Agent A (PM)**: Breaks down the issue.
- **Agent B (Coder)**: Writes the code.
- **Agent C (Reviewer)**: Tests the code and sends it back to B if it fails.
- **Tech**: CrewAI or AutoGen.
- **Key Learning**: Orchestration, delegation, and avoiding "agent loops."

### 6. Enterprise Support Agent with HITL
**Goal**: A customer support agent that can access internal RAG docs, check order status via API, but *must* ask a human for approval before issuing a refund.
- **Tech**: LangGraph (Persistence & Human-in-the-loop).
- **Key Learning**: Building safe, persistent, and verifiable agent systems.

---

## 🛠️ Project Template
When starting a project, use this structure:
1.  **Define the State**: What does the agent need to keep track of?
2.  **Select the Tools**: What external APIs are required?
3.  **Choose the Architecture**: Router? Supervisor? Simple ReAct?
4.  **Set Guardrails**: What should the agent *never* do?

---

**Next Steps**: Want to see the science behind these agents? Check out [`08-Research-Papers`](../08-Research-Papers/).
