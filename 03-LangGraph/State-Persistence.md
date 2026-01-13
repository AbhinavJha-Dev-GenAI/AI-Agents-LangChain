# State & Persistence in LangGraph 📦💾

One of LangGraph's most powerful features is **Persistence**. It allows agents to remember across different sessions, survive crashes, and support multi-user "threads" natively.

---

## 🧩 The Checkpointer Architecture

A **Checkpointer** is a component that saves the graph's `State` after every node execution. 

### Why do we need it?
1.  **Resilience**: If the server fails mid-task, the agent picks up from the last successful node.
2.  **Memories**: Different users can have their own "Thread ID," and the agent will keep their states separate.
3.  **Review**: You can inspect the state at any point in the past.

---

## 🛠️ Implementation Example (SQLite)

```python
from langgraph.checkpoint.sqlite import SqliteSaver

# 1. Initialize Saver (Using SQLite for local dev)
memory = SqliteSaver.from_conn_string(":memory:")

# 2. Compile with Checkpointer
app = graph.compile(checkpointer=memory)

# 3. Run with a Thread ID
config = {"configurable": {"thread_id": "user_123"}}
app.invoke({"input": "Hello!"}, config)
```

---

## 🔄 Reducers: Managing State Evolution

In a standard dict, `{"key": "value"}` overwrites previous values. In LangGraph, we use **Reducers** to control how the state evolves.

- **Append**: For `messages`, we want to add new messages to the existing list.
- **Merge**: For custom objects, we might want to merge fields.

```python
from typing import Annotated
from operator import add

class State(TypedDict):
    # This tells LangGraph to ADD to the list, not replace it
    messages: Annotated[list, add]
    count: int
```

---

## 📂 Persistent Storage Options

| Storage Type | Best For | Implementation |
| :--- | :--- | :--- |
| **Memory** | Local testing | `MemorySaver` |
| **SQLite** | Local dev (Persistent) | `SqliteSaver` |
| **Postgres** | Production | `PostgresSaver` |
| **Redis** | High-performance sync | Custom Implementation |

---

## ✅ Best Practices

1.  **Keep State Slim**: Don't store large documents in the state. Store their IDs/URIs and fetch them as needed.
2.  **Thread Hygiene**: Use unique Thread IDs for every distinct conversation.
3.  **Explicit Keys**: Always define exactly what keys are in your state to avoid "Untyped State" errors.

---

**Next Steps**: Learn how to use persistent states to fix errors manually in [Time Travel & Debugging](./Time-Travel-Debugging.md).
