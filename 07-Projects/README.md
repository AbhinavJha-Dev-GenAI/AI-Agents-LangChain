# 07. AI-Agent Projects 🛠️🚀

Hands-on projects to build a cutting-edge AI Agent portfolio.

## Project 1: Autonomous Data Analyst (SQL/CSV) 📊
*   **Goal**: Create an agent that can read a database schema, translate natural language questions into SQL, run the queries, and generate a final report with charts.
*   **Tech Stack**: LangChain (SQLAgent), Pandas, Matplotlib, OpenAI.
*   **Key Learning**: Tool calling for structured data and self-correcting SQL generation.

## Project 2: Collaborative Research Team (CrewAI) 🤝
*   **Goal**: Build a team of 3 agents (Researcher, Editor, Social Media Manager) that creates a viral tech newsletter from daily news.
*   **Tech Stack**: CrewAI, Tavily (Search API).
*   **Key Learning**: Multi-agent collaboration, role definition, and sequential workflows.

## Project 3: Self-Correcting Python Coder (LangGraph) 🐍
*   **Goal**: An agent that writes a Python script, runs it in a sandbox, and if it fails, reads the error message to fix the code and re-runs it.
*   **Tech Stack**: LangGraph, E2B (Code Interpreter SDK).
*   **Key Learning**: Cyclic graphs, state management, and error-driven reasoning.

## Project 4: Enterprise Customer Helper with HITL 📞
*   **Goal**: A support agent that answers questions using RAG, but pauses and waits for a human to approve any refund requests.
*   **Tech Stack**: LangGraph, Persistence (Postgres), FastAPI.
*   **Key Learning**: "Human-in-the-Loop" architecture and state persistence.

---

## 🚀 Getting Started
1.  **Framework Choice**: For simple logic, use **LangChain**. for complex, looping logic, use **LangGraph**.
2.  **Safety First**: Always use a tool like **LangSmith** to monitor your agent's reasoning traces—they can often hallucinate tool arguments.
3.  **Costs**: Start with **GPT-4o-mini**; it is $20\times$ cheaper than GPT-4o and surprisingly good at tool calling.
