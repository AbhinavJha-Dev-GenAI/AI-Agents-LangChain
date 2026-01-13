# Categorized Agentic AI Interview Q&A 🎤

Use these questions to test your knowledge or prepare for a Senior AI Engineer interview.

---

## 🏛️ Architecture & Theory
- **Q**: Why is `LangGraph` preferred over `SequentialChain` for agents?
  - **A**: `LangGraph` supports cycles (loops), which are essential for self-correction. It also provides explicit, persistent state management, whereas chains are stateless and linear.
- **Q**: Explain the difference between "Shared State" and "Local State" in a multi-agent system.
  - **A**: Shared state is a global object all agents can see. Local state is info passed between specific agents. Use shared state for long-term consistency and local state for privacy/performance.

## 🛠️ Engineering & Production
- **Q**: How do you prevent an agent from looping indefinitely in production?
  - **A**: Use `Max Iterations` constraints, recursion limits in the framework (LangGraph), and semantic monitoring to see if the agent's thought process is "drifting."
- **Q**: What is the "Redeemer" pattern?
  - **A**: A specific node in a graph designed to handle error outputs from tools. It takes a traceback, simplifies it for the LLM, and asks the LLM to fix the input.

## 🛡️ Ethics & Safety
- **Q**: How do you implement "Human-in-the-Loop" for an agent that sends emails?
  - **A**: Insert a "Wait" node before the `send_email` tool. The agent saves its state (subject, body, recipient) and creates a "Review Task" for a human. Only when the human approves does the agent proceed to the execution node.

---

**Next Steps**: Go back to the [Root README](../README.md) for a final review.
