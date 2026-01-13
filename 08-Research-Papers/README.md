# 08. Agentic Research Papers 📄

To stay ahead in the AI field, you must understand the academic foundations of agentic reasoning. This folder summarizes the key papers that move LLMs from "Next-token predictors" to "Reasoning Agents."

---

## 🏛️ [Foundational Papers Summaries](./Detailed-Summaries.md)
Deep dives into the logic and impact of ReAct, Reflexion, Toolformer, and Plan-and-Solve.

### 2. Reflexion: Language Agents with Verbal Reinforcement Learning (2023)
- **Concept**: Agents that "think" about their mistakes.
- **Mechanism**: An agent fails at a task, an "Evaluator" provides feedback, and the agent tries again with the memory of the previous failure.
- **Key Takeaway**: Dynamic self-correction is better than static fine-tuning.

### 3. Toolformer: Language Models Can Teach Themselves to Use Tools (2023)
- **Concept**: Teaching models to decide when to call an API.
- **Mechanism**: Meta (FAIR) trained a model to insert API calls (e.g., `[QA("Who is...")]`) into text automatically.
- **Key Takeaway**: Agents don't just use tools; they know *why* they need them.

### 4. Plan-and-Solve: Prompting Strategy for Multi-Step Reasoning (2023)
- **Concept**: Improving on Zero-shot CoT.
- **Mechanism**: Forcing the model to first devise a plan and then execute it, rather than "thinking on the fly."
- **Key Takeaway**: Planning reduces long-horizon drift in agents.

---

## 🏗️ Emerging Trends (2024-2025)

1.  **Voyager**: An open-ended agent in Minecraft that uses a "skill library" to learn infinitely.
2.  **AutoGPT / BabyAGI**: The early experiments in autonomous loops that sparked the current craze.
3.  **Human-in-the-loop Architectures**: Moving from "Full Autonomy" to "Collaborative Intelligence."

---

## 📚 Reading List Recommendation

1.  **ReAct** (MUST READ)
2.  **Toolformer** (Understanding API integration)
3.  **Reflexion** (Understanding memory and state)

---

**Next Steps**: Prepare for your next AI role in [`09-Interview-Prep`](../09-Interview-Prep/).
