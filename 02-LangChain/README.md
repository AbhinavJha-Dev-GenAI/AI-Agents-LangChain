# 02. LangChain Mastery 🔗🛠️

LangChain is the industry-standard framework for building LLM applications. It provides the "glue" to connect models, data, and tools.

## 1. LCEL: LangChain Expression Language 🏗️

LCEL is a declarative way to compose chains. It looks like Unix pipes:
`prompt | model | output_parser`

**Why use LCEL?**
- **Streaming**: Results are streamed automatically.
- **Async Support**: Native `await` for high-performance apps.
- **Tracing**: Integrates perfectly with LangSmith for debugging.

---

## 2. Components of a Chain 🧩

*   **Prompt Templates**: dynamic templates like `Translate {text} into {language}`.
*   **Models**: Wrappers for OpenAI, Anthropic, or Local LLMs (Ollama).
*   **Output Parsers**: Changing raw text into structured JSON or Python objects (Pydantic).
*   **Memory**: Storing conversation state in Redis, Postgres, or local memory.

---

## 3. The Shift to "Chains" vs. "Agents" ⚖️

*   **Chains**: A fixed sequence of steps. (e.g., "Summarize -> Translate").
*   **Agents**: Use an LLM to *decide* the sequence of steps dynamically.

---

## 🛠️ Essential Snippet (A Simple LCEL Chain)

```python
from langchain_openai import ChatOpenAI
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser

# 1. Define Components
model = ChatOpenAI(model="gpt-4o")
prompt = ChatPromptTemplate.from_template("Tell me a short joke about {topic}")
output_parser = StrOutputParser()

# 2. Compose Chain (| is the pipe operator)
chain = prompt | model | output_parser

# 3. Invoke
response = chain.invoke({"topic": "bears"})
print(response)
```

---

## 🧩 Pro-Tip: Debugging with LangSmith
Building chains is easy; debugging them is hard. Always set `LANGCHAIN_TRACING_V2=true` in your env variables to see exactly what prompts are being sent and what tokens are being returned in the LangSmith dashboard.
