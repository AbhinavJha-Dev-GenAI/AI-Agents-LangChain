# 05. Multi-Agent Systems 🤝🤖

Why use one agent when you can have a team? Multi-Agent Systems (MAS) involve multiple specialized agents working together to solve problems that are too complex for a single "Generalist" model.

## 1. Interaction Patterns 🏗️

### Sequential Collaboration
Agent A does its task -> passes the result to Agent B -> passes to Agent C.
- *Example*: Researcher Assistant -> Content Writer -> Fact Checker.

### Hierarchical (Manager) Pattern
A "Manager Agent" breaks down the user request and delegates sub-tasks to specialized workers. The workers report back to the manager.
- *Example*: An Engineering Manager agent delegating tasks to a Coder, a Tester, and a DevOps agent.

### Joint Collaboration (Peer-to-Peer)
Agents communicate in a shared "chat" or "whiteboard" to reach a consensus.
- *Example*: A group of agents debating a stock investment strategy.

---

## 2. Key Frameworks 🛠️

*   **CrewAI**: A framework for "Role-Based" agents. It focuses on processes and handoffs. You define Agents, Tasks, and a "Crew."
*   **Microsoft AutoGen**: Focuses on "Conversational" agents. It allows agents to talk to each other to solve tasks with minimal human input.
*   **LangGraph (Multi-Agent)**: The most granular approach. You have full control over the state machine and can define exactly how agents transition to one another.

---

## 3. Why go Multi-Agent? ⚖️

1.  **Specialization**: A prompt for a "Python Expert" performs better than a prompt for a "General Expert who can also code."
2.  **Modular Debugging**: If the research is bad, you know it's the Research Agent's fault, not the Writer's.
3.  **Parallelism**: Different agents can work on different sub-tasks at the same time.

---

## 🛠️ Essential Snippet (CrewAI Concept)

```python
from crewai import Agent, Task, Crew

# 1. Define Agents (Roles)
researcher = Agent(role="Researcher", goal="Find top news about AI", ...)
writer = Agent(role="Writer", goal="Write a blog post", ...)

# 2. Define Tasks
task1 = Task(description="Research AI news", agent=researcher)
task2 = Task(description="Write blog post", agent=writer)

# 3. Form the Crew
my_crew = Crew(agents=[researcher, writer], tasks=[task1, task2])
result = my_crew.kickoff()
```

---

## 🚨 Summary
Multi-agent systems represent the "Professionalization" of AI. By moving from one complex prompt to a team of specialized workers, you achieve higher reliability and better performance on enterprise-scale tasks.
