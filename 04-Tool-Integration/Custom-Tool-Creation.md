# Custom Tool Creation 🛠️

In LangChain, a **Tool** is a utility that an LLM can use to interact with the external world. Creating high-quality custom tools is the single most important factor in building a reliable agent.

---

## 🎨 The `@tool` Decorator

The easiest way to create a tool is to wrap a standard Python function with the `@tool` decorator.

```python
from langchain_core.tools import tool

@tool
def get_weather(location: str) -> str:
    """Get the current weather for a given city."""
    # Logic to call a weather API
    return f"The weather in {location} is sunny."
```

### Why use `@tool`?
1.  **Auto-Schema**: LangChain automatically extracts the function name and types to create the JSON schema the LLM needs.
2.  **Docstring Parsing**: The text inside `""" """` is passed to the LLM to explain *when* to use the tool.

---

## 🗝️ Docstring Optimization (The "Prompting" for Tools)

The LLM doesn't see your code; it only sees the **name** and **description** of your tool.

- **Bad Description**: `"""Search for info."""` (Vague, LLM might use it for math or local files).
- **Good Description**: `"""Use this tool to search the internet for real-time news and public data. Input should be a specific search query."""`

### Tips:
- **Be Explicit**: Mention what the input should look like (e.g., "ISO code" vs "Country name").
- **Mention Constraints**: "Only use this for documents released after 2021."

---

## 📦 Complex Inputs with Pydantic

If your tool needs multiple arguments or nested structures, use a Pydantic model to define the `args_schema`.

```python
from pydantic import BaseModel, Field

class SearchInput(BaseModel):
    query: str = Field(description="The search query")
    max_results: int = Field(description="Maximum results to return", default=5)

@tool(args_schema=SearchInput)
def search_api(query, max_results):
    """Search for items with a limit on results."""
    # Logic
    return results
```

---

## 🛡️ Best Practices for Robust Tools

1.  **Error Messages as Observations**: Instead of letting your code crash, catch exceptions and return the error string. The LLM can then try to fix its input.
    - *Example: "Error: The city 'Londnon' was not found. Did you mean London?"*
2.  **Return Data, Not Formatting**: Tools should return raw facts (JSON/String). Let the LLM handle the "niceness" of the response.
3.  **Privacy**: Never give an agent a tool that can delete data unless you have a **Human-in-the-Loop** step.

---

**Next Steps**: Learn how modern models handle tool calling natively in [Native Tool Calling](./Native-Tool-Calling.md).
