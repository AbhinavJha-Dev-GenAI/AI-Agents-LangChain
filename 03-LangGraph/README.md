# 03. LangGraph: Stateful Agents 🕸️💾

While standard LangChain is great for linear paths (DAGs), real-world agents often need to **loop** (e.g., "If the tool output is bad, try again"). LangGraph is the library for building cyclic, stateful multi-agent systems.

## 1. Why LangGraph? 🔄

Traditional chains are hard to control when:
- You need the agent to self-correct.
- You want multiple agents to pass data back and forth.
- You need to pause the agent for "Human-in-the-Loop" approval.

**LangGraph solves this by treating the agent as a State Machine.**

---

## 2. Core Concepts 🧬

### The State
A shared dictionary that stores the "memory" of the graph. Every node can read from and write to this state.

### Nodes (Functions)
Individual steps in your workflow (e.g., "Call LLM," "Call Tool," "Format Answer").

### Edges (Transitions)
The path between nodes.
- **Normal Edges**: Always go from Node A to Node B.
- **Conditional Edges**: Use a function to decide which node to go to next (e.g., "If result is successful, go to Finish; else, go back to Search").

---

## 3. Persistence & Time Travel ⏳

LangGraph allows you to **Checkpoint** the state after every node.
- **Human-in-the-loop**: Pause the agent, let a human review the state, modify it if needed, and let the agent continue.
- **Time Travel**: Rewind the agent to a previous step to see where it went wrong.

---

## 🛠️ Essential Snippet (Basic LangGraph Flow)

```python
from langgraph.graph import StateGraph, END
from typing import TypedDict, Annotated

# 1. Define State
class State(TypedDict):
    input: str
    output: str

# 2. Define Nodes
def call_model(state: State):
    # Logic to call LLM...
    return {"output": "Processed " + state["input"]}

# 3. Build Graph
workflow = StateGraph(State)
workflow.add_node("agent", call_model)
workflow.set_entry_point("agent")
workflow.add_edge("agent", END)

# 4. Compile and Run
app = workflow.compile()
response = app.invoke({"input": "Hello Agents"})
```

---

## 📊 Summary
LangGraph is the preferred way to build **Production Agents**. It provides the reliability of a coded state machine with the flexibility of an LLM reasoning engine.
