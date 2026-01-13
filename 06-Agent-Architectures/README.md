# 06. Agent Architectures: Design Patterns 🏗️

Building an agent is easy. Building a **production-ready** agent that doesn't hallucinate or run into infinite loops is hard. This folder explores design patterns for robust agentic systems.

---

## 🎨 Common Design Patterns

### 1. [Production Design Patterns](./Production-Patterns.md)
Mastering Routers, Supervisors, and Evaluator-Optimizer (Reflexion) architectures for industrial reliability.

### 2. [Human-in-the-Loop (HITL)](./Human-in-the-Loop.md)
Designing safe agents with interrupt, review, and feedback loops. Essential for financial and data-sensitive applications.

### 3. Observability & Evaluation
Using LangSmith to trace performance, evaluate accuracy, and monitor production costs.

---

## 👨‍💻 Human-in-the-Loop (HITL)

Purely autonomous agents are risky for enterprise apps. LangGraph makes HITL a first-class citizen.
- **Interrupts**: Pause the graph execution before a sensitive tool call (e.g., `send_payment` or `delete_bucket`).
- **Review & Edit**: A human can see the proposed arguments, edit them, and click "Approve" to continue.
- **Feedback**: A human can provide natural language feedback to the agent to redirect its reasoning.

---

## 📈 Observability & Evaluation

### LangSmith: The Developer's Best Friend
You cannot develop agents in the dark. LangSmith allows you to:
- **Trace**: See every step of the reasoning loop (Thought -> Action -> Result).
- **Evaluate**: Run datasets through your agent and grade them (Correctness, Helpfulness, Latent Reasoning).
- **Monitor**: Track cost, latency, and token usage in production.

---

## 🛡️ Guardrails & Safety

- **Rate Limiting**: Preventing infinite loops from draining your API credits.
- **PII Redaction**: Ensuring agents don't leak or search for sensitive user data.
- **Semantic Guardrails**: Using tools like **NeMo Guardrails** to ensure the agent stay on-topic.

---

**Next Steps**: Now that you have the blueprints, check out real-world implementations in [`07-Projects`](../07-Projects/).
