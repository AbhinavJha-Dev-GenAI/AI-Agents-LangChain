# Plan-and-Execute Architecture 🗺️

**Plan-and-Execute** is a sophisticated agent architecture designed for complex, long-horizon tasks. While ReAct agents "think on their feet" (deciding one step at a time), Plan-and-Execute agents create a comprehensive roadmap before taking their first action.

---

## 🏗️ The Two-Agent System

This architecture typically separates the "Brain" into two distinct roles:

### 1. The Planner 🧠
Receives the high-level goal and breaks it down into a list of sequential steps or sub-tasks.
- **Input**: "Build a research report on the 2024 AI industry trends."
- **Output**: 
  1. Search for key hardware developments (Nvidia, Blackwell).
  2. Search for major software breakthroughs (LLAMA 3, Gemini Ultra).
  3. Synthesize findings into a 5-page draft.
  4. Edit for professional tone.

### 2. The Executor 🛠️
A specialized (often smaller) agent that takes one step from the plan and completes it using available tools. It reports the result back to the Planner.

---

## 🧩 The Workflow Loop

1.  **Plan**: Generate the full list of steps.
2.  **Execute**: Finish the first step.
3.  **Reflect/Re-plan**: Look at the result of the execution. Is the original plan still valid? 
4.  **Loop**: If yes, move to the next step. If no, update the plan.

---

## ✅ Why use Plan-and-Execute?

- **Reduced Drifting**: ReAct agents can get distracted by tool outputs ("rabbit holes"). A plan acts as an anchor.
- **Better Resource Management**: You can use a very powerful (expensive) model for the Planning phase and a cheaper model for the mundane Execution steps.
- **Parallelism**: Some steps in a plan can be executed concurrently.

---

## ⚖️ Plan-and-Execute vs. ReAct

| Feature | ReAct | Plan-and-Execute |
| :--- | :--- | :--- |
| **Approach** | Step-by-step decision | Pre-defined roadmap |
| **Error Handling** | Pivot in real-time | Periodic re-planning |
| **Task Complexity** | Simple to Moderate | High / Long-horizon |
| **Reliability** | Variable | High (Structured) |

---

## 🛠️ Implementation Pattern (LangGraph)

In LangGraph, this is represented as a stateful loop:
- **Node A**: `Planner` -> Updates `plan` in state.
- **Node B**: `Executor` -> Updates `results` in state.
- **Edge**: Check if all steps are done. If not, go back to `Planner` (Re-plan) or `Executor` (Next step).

---

**Next Steps**: Ready to build? Explore the [LangChain Mastery](../02-LangChain/README.md) to see the tools used to implement these architectures.
