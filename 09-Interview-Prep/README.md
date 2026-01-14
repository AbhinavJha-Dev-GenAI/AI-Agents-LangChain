# 09. AI Agent Interview Preparation 🧠🏛️

Technical, architectural, and ethical questions for AI Engineer roles focused on Agents.

## 1. Concepts & Patterns 📖

*   **Q: What is the difference between an LLM "Chain" and an "Agent"?**
    - *A:* A Chain is a pre-defined sequence of steps. An Agent uses an LLM to dynamically decide which steps to take and which tools to call based on the user's input.
*   **Q: How does the ReAct pattern work?**
    - *A:* It follows a cycle: **Thought** (the model explains its logic), **Action** (the model selects a tool), and **Observation** (the model reads the tool output). It repeats this until it can answer the user.
*   **Q: What are "Tool Hallucinations"?**
    - *A:* When an LLM tries to call a tool that doesn't exist or provides invalid arguments that don't match the function's schema.

---

## 2. Design & Scalability 🏗️

*   **Q: How do you prevent an agent from getting stuck in an infinite loop?**
    - *A:* 1. Set a `max_iterations` limit. 2. Use a "Self-Reflection" node to detect repetitive behavior. 3. Set a hard timeout on the execution.
*   **Q: When is a Multi-Agent system better than a single complex agent?**
    - *A:* When the task requires specialized domain knowledge (e.g., Coding vs. Legal), or when you want modular debugging and parallel execution.
*   **Q: Explain the role of "State" in LangGraph.**
    - *A:* State is the persistent memory shared across all nodes in the graph. It allows the agent to remember what happened in Step 1 when it is making a decision in Step 5.

---

## 3. Engineering Scenarios 🧪

*   **Scenario: Your coding agent keeps writing buggy code. How do you fix it?**
    - *A:* Implement a **Reflexion** pattern. Add a "Reviewer" agent or a "Test" node that runs the code and feeds the error messages back to the primary agent for correction.
*   **Scenario: You need an agent to search internal PDFs and the web. How do you design it?**
    - *A:* Use **Agentic RAG**. Create two tools: `internal_search` (Vector DB) and `web_search` (Tavily). Let the LLM decide which tool is appropriate for the query.

---

## 🎯 Agent Engineering Cheat Sheet
1. **Best for Statefulness**: LangGraph.
2. **Best for Collaboration**: CrewAI / AutoGen.
3. **Best for Monitoring**: LangSmith.
4. **Best Pattern**: ReAct + Reflexion.
