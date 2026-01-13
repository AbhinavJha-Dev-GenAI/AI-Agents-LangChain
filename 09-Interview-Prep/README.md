# 09. Agentic AI Interview Prep 🎤

Preparing for an ML/AI Engineer role in the era of agents requires a shift in mindset from simple RAG to complex cognitive architectures. Here are the most common technical questions and their detailed answers.

---

## 🏛️ [Categorized Interview Q&A](./Categorized-QA.md)
Deep-dive questions on Architecture, Production Engineering, and AI Safety.
**Answer**: 
- **Zero-shot Agents**: Use only the tool descriptions to decide the first action. They don't typically iterate or "think" out loud. They are "one-and-done."
- **ReAct Agents**: Use a "Thought-Action-Observation" loop. They reason about the result of one action before deciding on the next. They are far more robust for multi-step tasks.

### Q2: When is Multi-Agent better than Single-Agent?
**Answer**: 
- **Context Management**: A single agent's context window fills up with tool outputs. Multiple agents can share only relevant summaries.
- **Specialization**: You can use different models (e.g., GPT-4o for the Manager, GPT-4o-mini for Workers) to optimize cost and performance.
- **Complexity**: Tasks with conflicting requirements (e.g., "Write creative code" vs. "Perform strict security audit") are handled better by separate personas.

---

## 🛠️ Tool Calling & Debugging

### Q3: How do you handle "Tool Hallucinations"?
**Answer**:
1.  **Pydantic Validation**: Use strict schemas so the LLM physically cannot pass invalid JSON.
2.  **Few-shotting**: Provide examples in the system prompt of correct tool usage.
3.  **Error Feedback**: If a tool fails, pass the error message back to the LLM (as an Observation) so it can self-correct.
4.  **Narrow Descriptions**: Make tool descriptions extremely specific about what they *don't* do.

### Q4: How do you prevent an agent from getting stuck in an infinite loop?
**Answer**:
1.  **Max Iterations**: Set a hard limit (e.g., 10 steps) in your graph or agent executor.
2.  **State Inspection**: In LangGraph, monitor if the state isn't changing across multiple nodes.
3.  **Recursion Limit**: Built-in feature in LangGraph and LangChain to kill the process if it exceeds a certain depth.

---

## 📦 State & Persistence

### Q5: Explain the role of "State" in LangGraph.
**Answer**: State is a shared, versioned schema (dict or Pydantic) that nodes use to communicate. Unlike simple chat history, State can hold structured data like "extracted_entities," "search_results," or "is_verified_bool." This allows for complex logic based on previous steps.

### Q6: What is "Time Travel" in the context of agents?
**Answer**: It’s the ability to rewind the agent's state to a previous checkpoint. This is critical for:
- **Debugging**: Seeing exactly where an LLM's reasoning went off-track.
- **Human Editing**: A human can "go back in time," edit a bad LLM decision, and let the agent continue from the corrected state.

---

## 🚀 Scenario-Based Questions

### Q7: "Your agent is spending too much money on tokens. How do you optimize it?"
**Answer**:
1.  **Routing**: Use a small model to decide if the query needs a complex agent or just a simple RAG chain.
2.  **Summarization**: Don't pass full tool outputs back to the prompt; pass only relevant snippets.
3.  **System Prompt Compression**: Remove redundant instructions.
4.  **Caching**: Cache common tool results (e.g., Redis for web searches).

---

**Next Steps**: Review the [Root README](../README.md) to ensure you've mastered the full syllabus. Good luck! 🚀
