# ReAct Pattern: Synergizing Reasoning and Acting 🔄

The **ReAct** (Reason + Act) pattern is the foundational framework for modern autonomous agents. It solves a critical problem in LLM application design: the trade-off between **hallucination** and **blind execution**.

---

## 🏛️ The Core Problem

1.  **Reasoning-only (CoT)**: Models can think step-by-step but lack access to real-time data. They hallucinate facts to complete their internal logic.
2.  **Acting-only**: Models can call tools but lack a "mental model" of what they are doing. If a tool fails, they don't know how to pivot.

**ReAct** bridges this gap by interleaving reasoning traces and task-specific actions.

---

## 🧩 The Anatomy of a ReAct Loop

A typical ReAct interaction follows this cycle:

### 1. Thought 🧠
The model generates a "thought" based on the current context.  
*Example: "To answer the user's question about the stock price, I first need to find the ticker symbol for Apple Inc."*

### 2. Action 🛠️
The model decides to use a tool.  
*Example: `Search(Apple Inc ticker)`*

### 3. Observation 👁️
The model receives the output of the tool.  
*Example: "AAPL"*

### 4. Repeat 🔄
The model uses the observation to generate the next thought.  
*Example: "Now that I have the ticker (AAPL), I will use the Yahoo Finance tool to find today's closing price."*

---

## 🛠️ Implementation Example (Simplified)

```python
# A conceptual ReAct prompt template
prompt = """
Answer the following questions as best you can. You have access to the following tools:
{tool_descriptions}

Use the following format:
Question: the input question you must answer
Thought: you should always think about what to do
Action: the action to take, should be one of [{tool_names}]
Action Input: the input to the action
Observation: the result of the action
... (this Thought/Action/Action Input/Observation can repeat N times)
Thought: I now know the final answer
Final Answer: the final answer to the original input question

Begin!
Question: {input}
Thought: 
"""
```

---

## ✅ Best Practices for ReAct Agents

1.  **Stop Condition**: Always set a `max_iterations` limit to prevent infinite loops (and massive API bills).
2.  **Rich Tool Descriptions**: The LLM's "mental model" of a tool comes entirely from its description. Be precise.
3.  **Human Feedback**: Allow the "Observation" step to occasionally come from a human instead of a tool.

---

## 🔬 Challenges

- **Stochastic Loops**: Because the "Thought" is non-deterministic, the agent might take a different path every time.
- **Latency**: Each loop requires a full LLM call, which can be slow for multi-step tasks.

---

**Next Steps**: Learn how to improve the quality of thoughts using [Chain-of-Thought](./Chain-of-Thought.md).
