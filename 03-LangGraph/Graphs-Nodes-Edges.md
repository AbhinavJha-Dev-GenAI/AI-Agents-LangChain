# Anatomy of a LangGraph: Nodes and Edges 🕸️

LangGraph treats LLM application logic as a **Directed Graph**. Unlike standard LangChain, these graphs can be **cyclic**, allowing for self-correction and iterative loops.

---

## 🟢 1. Nodes: The Building Blocks

A **Node** is essentially a Python function (or a `Runnable`).
- **Input**: The current `State` of the graph.
- **Output**: A dictionary updating one or more keys in the `State`.

```python
def retrieve_docs(state: dict):
    # Logic to fetch docs
    query = state["query"]
    docs = vector_store.search(query)
    # Update the state
    return {"documents": docs}
```

---

## ➡️ 2. Edges: The Connectors

Edges define the control flow between nodes.

### Standard Edges
A direct path from Node A to Node B.
```python
graph.add_edge("retrieve", "generate")
```

### Conditional Edges
Decision logic based on the current state. Often used to check if an agent's response is a "Final Answer" or a "Tool Call."
```python
def should_continue(state: dict):
    if state["is_answered"]:
        return "end"
    return "tools"

graph.add_conditional_edges("generate", should_continue, {
    "end": END,
    "tools": "action"
})
```

---

## 📦 3. State: The Single Source of Truth

The `State` is a shared object (usually a Pydantic model or a TypedDict) that travels through the graph. Nodes don't communicate with each other directly; they only communicate by reading and writing to the `State`.

- **Reducers**: You can define *how* state keys are updated. For example, a list of messages should be *appended* to, not overwritten.

---

## 🏗️ The Compiler

Once you've defined your nodes and edges, you must "Compile" the graph into a `Runnable`. This handles the underlying orchestration and prepares it for execution (and persistence if a checkpointer is added).

```python
app = graph.compile()
```

---

## ✅ Best Practices

1.  **Atomic Nodes**: Each node should do ONE thing (e.g., "Summarize," not "Search and Summarize").
2.  **Cycle Logic**: Always ensure there is a guaranteed exit condition (`END`) to prevent infinite loops.
3.  **Visualization**: Use `app.get_graph().draw_mermaid_png()` to visualize your architecture before running it.

---

**Next Steps**: Learn how to make your graphs survive server crashes in [State & Persistence](./State-Persistence.md).
