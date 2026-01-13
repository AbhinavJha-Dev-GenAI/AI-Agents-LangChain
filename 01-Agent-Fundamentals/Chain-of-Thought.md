# Chain-of-Thought (CoT) Reasoning 🔗

**Chain-of-Thought (CoT)** is a prompting technique that encourages large language models to generate intermediate steps of reasoning before arriving at a final answer.

---

## 🧠 Why it Works

Standard LLM completions (Input -> Output) often fail on complex tasks because the model "jumps to conclusions." By forcing the model to map out its "latent logic," we:
1.  **Increase Accuracy**: The model spends more "computation" (tokens) on the reasoning process.
2.  **Improve Explainability**: We can see exactly *where* the model's logic went wrong if it arrives at a false conclusion.

---

## 🧩 Types of CoT

### 1. Zero-Shot CoT
The simplest form. Just add a specific trigger phrase to the prompt.
- **Trigger**: *"Let's think step by step."*
- **Effect**: Signals the model to break the problem into smaller logical units.

### 2. Few-Shot CoT
Provide the model with examples of both the **Problem** and the **Step-by-Step Logic** required to solve it.
- **Example**:
  ```text
  Q: Roger has 5 tennis balls. He buys 2 more cans. Each can has 3 balls. How many balls does he have now?
  A: Roger started with 5 balls. 2 cans with 3 balls each is 6 balls. 5 + 6 = 11. The answer is 11.
  
  Q: [New Question Here]
  A: 
  ```

---

## 🛠️ Application in Agents

In an agentic context, CoT serves as the "Thinking" phase of the ReAct loop. 

- **Implicit CoT**: The LLM writes a paragraph of thoughts before calling a tool.
- **Explicit CoT**: The agent outputs a structured "Plan" or "Reasoning" object.

---

## 📊 Comparison: Standard vs. CoT

| Feature | Standard Prompting | Chain-of-thought |
| :--- | :--- | :--- |
| **Response Time** | Fast | Slower (More tokens) |
| **Logic Consistency** | Low | High |
| **Complex Math/Logic** | Poor | Excellent |
| **Hallucination** | Higher | Lower (Logic-bound) |

---

## 🚀 Optimization Tips

1.  **Self-Consistency**: Run the CoT prompt multiple times and take the majority answer.
2.  **Least-to-Most Prompting**: Ask the model to define the sub-problems first, then solve them one by one.

---

**Next Steps**: See how to scale this into long-term strategies with [Plan-and-Execute](./Plan-and-Execute.md).
