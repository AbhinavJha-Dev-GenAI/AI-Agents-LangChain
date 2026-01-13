# Research Paper Summaries: The Agentic Foundation 📚

Understanding these papers provides the "Why" behind the "How" of agent frameworks.

---

## 🔄 ReAct (2023)
- **Problem**: Models like GPT-3 could think (CoT) or use tools, but not both efficiently.
- **The Breakthrough**: Interleaving reasoning and acting.
- **Quote**: *"By synergizing reasoning and acting, ReAct allows models to perform dynamic reasoning to create, maintain, and adjust high-level plans for acting."*

## 🧠 Reflexion (2023)
- **Problem**: Once an agent makes a mistake, it often gets stuck in a loop of errors.
- **The Breakthrough**: Verbal reinforcement learning. The agent maintains a "reflective memory" of its previous failures and explicitly looks for those patterns in new attempts.
- **Key takeaway**: Reflection is the key to autonomous self-correction.

## 🛠️ Toolformer (2023)
- **Problem**: How do we teach a model to use APIs without massive human labeling?
- **The Breakthrough**: Self-supervised learning. The model "samples" API calls and keeps the ones that help it predict the next token more accurately.
- **Result**: Models that "natively" understand when to call a calculator or a calendar.

## 🗺️ Plan-and-Solve (2023)
- **Problem**: Zero-Shot CoT is still prone to calculation errors.
- **The Breakthrough**: Enhancing the "Think step-by-step" prompt with a requirement to "devise a plan first."
- **Key Takeaway**: Planning is a distinct mental primitive from execution.

---

**Next Steps**: Practice explaining these concepts in a professional setting with [Interview Prep](../09-Interview-Prep/README.md).
