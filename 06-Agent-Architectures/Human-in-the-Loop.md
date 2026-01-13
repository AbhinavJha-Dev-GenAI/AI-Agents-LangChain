# Human-in-the-Loop (HITL) for Agents 👨‍💻🤖

Complete autonomy is dangerous for high-stakes actions. **Human-in-the-Loop** is a design pattern where the agent pauses and waits for human intervention before proceeding.

---

## 🧩 The Three Pillars of HITL

### 1. Interrupt (The "Pause" button)
The agent is prohibited from calling certain "Sensitive" tools (e.g., `execute_trade`, `send_email`) without a specific authorization flag.
- **LangGraph**: Use the `interrupt_before` or `interrupt_after` configuration during compilation.

### 2. Review & Edit (The "Override")
The human doesn't just "Approve" or "Deny." They can see the arguments the agent *intended* to use and **edit** them.
- *Example: Agent wants to refund $500. Human edits it to $50.*

### 3. Feedback (The "Teacher")
The human provides natural language feedback to the agent's internal state. This "steers" the agent's reasoning without restarting the process.

---

## 🏗️ Common HITL Workflows

- **Approval Workflow**: Agent suggests -> Human clicks "Approve" -> Agent executes.
- **Correction Workflow**: Agent makes a mistake -> Human rewinds state -> Human gives a hint -> Agent tries again.
- **Escalation Workflow**: Agent gets stuck -> Agent explicitly calls a `request_human_help` tool.

---

## 🛠️ Implementation Strategy (LangGraph)

LangGraph's persistence layer makes HITL easy. Because the state is saved, the "waiting for human" step can last minutes, hours, or even days.

```python
# Compile the graph with an interrupt
app = graph.compile(
    checkpointer=memory,
    interrupt_before=["delete_node"]
)

# When the human approves, just invoke with None to resume
app.invoke(None, config)
```

---

## ✅ Best Practices for Safety

1.  **Define Sensitivity**: Only use HITL for actions that are irreversible or expensive. Don't interrupt for simple searches.
2.  **Rich UI**: The human needs to see the "Thought" process, not just the "Action," to make an informed decision.
3.  **Audit Logs**: Always record who approved what action and when. This is critical for enterprise compliance (SOC2/GDPR).

---

**Next Steps**: See how these patterns are applied in real world scenarios in [`07-Projects`](../07-Projects/README.md).
