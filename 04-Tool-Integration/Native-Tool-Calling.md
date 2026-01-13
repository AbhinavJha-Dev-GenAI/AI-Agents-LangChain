# Native Tool Calling (OpenAI & Anthropic) 🤖

Before 2023, agents worked by "parsing JSON out of raw text blocks." This was flaky and prone to errors. Today, top-tier models (OpenAI, Claude, Gemini) support **Native Tool Calling**.

---

## 🏗️ How it Differs from Traditional Parsing

| Feature | Legacy Parsing | Native Tool Calling |
| :--- | :--- | :--- |
| **Logic** | "Please output JSON" | Model has a hidden "Action" layer |
| **Reliability** | Flaky (hallucinates syntax) | Very High (Validated by provider) |
| **Multi-tool** | Difficult | Can call multiple tools at once |
| **Arguments** | Often wrong type | Respects schema types (int, bool) |

---

## 🛠️ Implementation in LangChain

To use native tool calling, you must **bind** your tools to the LLM.

```python
from langchain_openai import ChatOpenAI

llm = ChatOpenAI(model="gpt-4o")
tools = [get_weather, calculate_tax]

# The 'magic' step:
llm_with_tools = llm.bind_tools(tools)

# When you invoke, the response will have a 'tool_calls' field
ai_msg = llm_with_tools.invoke("What is the weather in NYC and tax for $100?")
print(ai_msg.tool_calls)
```

---

## 🧩 The `tool_calls` Object

Instead of a string of text, you get a structured list:
```json
[
  {
    "name": "get_weather",
    "args": {"location": "NYC"},
    "id": "call_123"
  }
]
```
**Crucial**: Your code must handle the `id`. When you return the "Observation" to the LLM, you must include this ID so the model knows which tool result belongs to which call.

---

## 🚀 Advanced: Forced Tool Calling

Sometimes you don't want the LLM to decide; you want it to **always** use a specific tool.

```python
# Force the model to use the 'search' tool
llm_forced = llm.bind_tools(tools, tool_choice="search")
```

---

## ✅ Best Practices

1.  **Prefer Native**: If your model supports it, always use `bind_tools` instead of writing custom prompt instructions for JSON.
2.  **Handle Multiple Calls**: Modern models can call the same tool 5 times with different inputs in one turn. Ensure your executor can handle lists of tool calls.
3.  **Token Efficiency**: Tool definitions count towards your input tokens. Only bind the tools that are relevant to the current task.

---

**Next Steps**: Learn how to orchestrate multiple agents, each with their own set of tools, in [`05-Multi-Agent-Systems`](../05-Multi-Agent-Systems/README.md).
