# 04. Tool Integration 🛠️🔌

Tools are the "hands" of an AI agent. Without them, an LLM is just a brain in a jar. Tools allow agents to interact with the real world (Search, Code, APIs, Databases).

## 1. How Tool Calling Works 📡

Tool calling is a two-step communication between the LLM and your code:
1.  **Selection**: You provide a list of tool descriptions (JSON schemas). The LLM decides *which* tool to use and *what* arguments to pass.
2.  **Execution**: Your Python code runs the actual function and sends the result back to the LLM.

> [!IMPORTANT]
> **The LLM does NOT run the tool.** Your server runs the code. The LLM only generates the JSON to tell you what to run.

---

## 2. Types of Tools 🎭

*   **Pre-built Tools**: Search (Tavily, DuckDuckGo), YouTube search, Wikipedia.
*   **Custom Tools**: Wrapping any Python function.
*   **Structured Tools**: Tools that require complex, nested JSON inputs.

---

## 3. Best Practices for Tool Design 📝

- **Clear Descriptions**: The LLM relies solely on the tool's docstring. Be extremely clear about what the tool does and what the parameters mean.
- **Error Handling**: If a tool fails (e.g., 404 API error), catch it and return it as a "Tool Result" so the LLM can try an alternative.
- **Sandboxing**: Never let an LLM run code (Python/SQL) directly on your production server. Always use a sandboxed environment (e.g., Docker or `E2B`).

---

## 🛠️ Essential Snippet (Defining a Custom Tool)

```python
from langchain.tools import tool

@tool
def calculate_shipping_cost(weight: float, zip_code: str) -> str:
    """Useful to calculate shipping costs for orders. 
    Weight must be in kg. Returns cost in USD."""
    # Logic to call shipping API...
    cost = weight * 5.0 
    return f"The shipping cost to {zip_code} is ${cost}"

# LangChain automatically converts this into a JSON schema 
# that can be passed to an LLM like GPT-4 or Claude 3.
```

---

## 🌎 Summary
Mastering tool integration is about providing the LLM with the right "Interfaces." The better your tool descriptions, the more reliable your agent will be.
