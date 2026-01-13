# 02. LangChain Mastery 🔗

LangChain is the industry-standard framework for building LLM applications. This folder covers the move from "legacy" chains to the modern **LangChain Expression Language (LCEL)**.

---

## 🚀 LangChain Expression Language (LCEL)

LCEL is a declarative way to compose chains. It provides:
- **First-class streaming**: Get tokens as soon as the model generates them.
- **Async support**: Built-in `ainvoke` and `astream`.
- **Parallel execution**: Run multiple branches of a chain at once.

### Simple LCEL Syntax:
```python
chain = prompt | model | parser
```

---

## 🧩 Core Components

### 1. [LangChain Expression Language (LCEL)](./LCEL-Mastery.md)
Declarative way to compose chains. It provides first-class streaming, async support, and parallel execution.

### 2. [Memory Management](./Memory-Management.md)
How do we make agents remember?
- **ConversationBufferMemory**: Standard list of messages.
- **Entity Memory**: Remembering specific facts about users.
- **Vector Store Backends**: Using Redis or Postgres for long-term history.

### 3. [Prompt Engineering for Agents](./Prompt-Engineering-Agents.md)
Tailoring prompts for high-performance reasoning and robust tool usage.

### 4. Output Parsers
Force the LLM to return structured data (JSON, CSV, Pydantic) instead of raw text.
- `JsonOutputParser`
- `PydanticOutputParser`

---

## 📂 Data Extraction & Transformation

LangChain excels at transforming unstructured text into structured data (ETL for LLMs).
- **Document Loaders**: PDF, URL, CSV, YouTube transcripts.
- **Text Splitters**: RecursiveCharacterTextSplitter for optimal chunking.
- **Vector Stores**: ChromaDB, Pinecone, FAISS for retrieval.

---

## ⚖️ Chains vs. Agents

| Feature | Chains (LCEL) | Agents |
| :--- | :--- | :--- |
| **Control** | High (Hardcoded sequence) | Low (LLM decides steps) |
| **Complexity** | Low to Medium | High |
| **Reliability** | Very High | Variable (stochastic) |
| **Logic** | Directed Acyclic Graph (DAG) | Cyclic / Self-Correcting |

---

## 🛠️ Best Practices

1.  **Use LCEL**: Avoid `SequentialChain` (legacy). LCEL is more performant and easier to debug.
2.  **Versioning**: Keep your prompts versioned and separate from your application code.
3.  **Tracing**: Always use **LangSmith** to visualize how data flows through your chain.

---

**Next Steps**: Now that you know how to build linear paths, learn how to build complex, cyclic agents in [`03-LangGraph`](../03-LangGraph/).
