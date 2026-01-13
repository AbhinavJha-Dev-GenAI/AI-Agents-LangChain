# Prompt Engineering for Agents 📝

Agents require a different style of prompt engineering than standard chatbots. Success or failure depends on how well you define the agent's **Role**, **Tools**, and **Reasoning Format**.

---

## 🏗️ The 4 Pillars of an Agent Prompt

### 1. Persona & Role
Define "who" the agent is. A "Helpful Assistant" is too vague.
- **Bad**: "You are an AI assistant."
- **Good**: "You are a Senior DevOps Engineer. You specialize in AWS infrastructure and resolving CI/CD pipeline failures."

### 2. Tool Definitions
If an agent has tools, it must know exactly when and how to use them.
- **Name**: Short and descriptive (e.g., `calculate_roi`).
- **Description**: Explain what it does and what the inputs mean.
- **OpenAI/Anthropic**: Use their specific "Tool/Function Calling" schemas for 99% accuracy.

### 3. Reasoning Instructions (The Constraint)
Tell the model *how* to think.
- "Interleave thoughts and actions."
- "If you don't know the answer, use the search tool. Do not guess."
- "Always verify your output before returning it."

### 4. Zero-Shot vs. Few-Shot
- **Zero-Shot**: Provide instructions only.
- **Few-Shot**: Provide 2-3 examples of a "Perfect Tool Call" or a "Perfect Reasoning Loop." This is often the difference between success and failure for complex tasks.

---

## 🧩 Dynamic Templates (LangChain)

In LangChain, we use `ChatPromptTemplate` to build dynamic inputs.

```python
from langchain_core.prompts import ChatPromptTemplate, MessagesPlaceholder

prompt = ChatPromptTemplate.from_messages([
    ("system", "You are a research agent. Use the tools provided to answer questions."),
    # Placeholder for chat history
    MessagesPlaceholder(variable_name="history"),
    ("human", "{input}"),
    # Placeholder for agent's internal scratching/tool results
    MessagesPlaceholder(variable_name="agent_scratchpad"),
])
```

---

## 🛡️ Guardrails in Prompts

Preventing jailbreaks and hallucinations starts in the prompt:
- **Negative Constraints**: "Do not answer questions about medical advice."
- **Format Enforcement**: "You must only respond in JSON format matching this schema..."
- **Step-Limit**: "Complete this within 5 steps or escalate to a human."

---

## 📈 Iterative Refinement

Agent prompts are rarely perfect on the first try.
1.  **Trace**: Use LangSmith to see common failure points.
2.  **Adjust**: If the agent uses the wrong tool, clarify the description.
3.  **Test**: Run a benchmark dataset after every prompt change.

---

**Next Steps**: Transition from linear chains to complex, stateful graphs in [`03-LangGraph`](../03-LangGraph/README.md).
