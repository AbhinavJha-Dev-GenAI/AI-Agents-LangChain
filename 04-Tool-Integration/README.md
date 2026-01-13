# 04. Tool Integration: Giving Agents Hands 🛠️

An LLM is just a brain. **Tools** are the hands that allow it to interact with the world — whether it’s searching the web, querying a database, or sending an email.

---

## 🏗️ How Tool Calling Works

Contrary to popular belief, the LLM does not *run* the tool. 
1.  **System**: Sends tool definitions (JSON schema) to the LLM.
2.  **LLM**: Decides to use a tool and returns the arguments (e.g., `{"location": "London"}`).
3.  **App**: Executes the Python function/API with those arguments.
4.  **LLM**: Receives the tool output and continues reasoning.

---

### 1. [Custom Tool Creation](./Custom-Tool-Creation.md)
Crafting high-quality utilities for your agents. Focus on docstring optimization and Pydantic schemas.

### 2. [Native Tool Calling](./Native-Tool-Calling.md)
Mastering established patterns for OpenAI, Anthropic, and Gemini to ensure 99% accuracy in tool selection.

### 3. API Connections
How to securely connect agents to external SaaS APIs (Slack, GitHub, Twitter).

## 🧩 Creating Custom Tools

In LangChain, you can create tools using the `@tool` decorator.

```python
from langchain_core.tools import tool

@tool
def multiply(a: int, b: int) -> int:
    """Multiplies two integers together."""
    return a * b
```

### 🗝️ The Secret Sauce: Docstrings
The LLM selects a tool based on its **name** and **description**. If your docstring is vague, the agent will hallucinate.
- **Bad**: `def search(q): return ...`
- **Good**: `def search_tavily(query: str): """Use this tool to search the internet for real-time information. Input should be a search string."""`

---

## 🤖 Native Tool Calling (OpenAI/Anthropic)

Modern LLMs support native tool calling, which is more robust than "parsing JSON from text."
- **Binding Tools**:
  ```python
  llm_with_tools = llm.bind_tools([multiply, search_api])
  ```

---

## 🛠️ Handling Challenges

### 1. Tool Hallucinations
Sometimes agents try to use tools that don't exist or pass wrong arguments.
- **Solution**: Use Pydantic schemas for strict validation and retry loops in LangGraph.

### 2. Large Data Outputs
Tools might return massive datasets that blow the context window.
- **Solution**: Summarize tool outputs or store them in a vector DB and only return the URI/ID to the LLM.

### 3. Error Handling
If an API fails, the agent should know *why* so it can try again or pivot.
- **Solution**: Wrap tool logic in try-except blocks and return the error message as an "Observation".

---

## 📂 Popular Toolkits

- **Search**: Tavily, DuckDuckGo, Serper.
- **Compute**: Python REPL, Wolfram Alpha.
- **Files**: CSV/SQL/PDF Agents.
- **Web**: Playwright, Selenium.

---

**Next Steps**: Now that your agent can use tools, learn how to build teams of agents in [`05-Multi-Agent-Systems`](../05-Multi-Agent-Systems/).
