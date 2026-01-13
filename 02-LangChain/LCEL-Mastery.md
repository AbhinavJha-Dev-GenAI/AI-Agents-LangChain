# LCEL Mastery: LangChain Expression Language 🔗

**LCEL** (LangChain Expression Language) is the declarative way to compose chains in LangChain. It provides a consistent interface and several built-in features that make your LLM applications more robust and performant.

---

## 🏗️ The Pipe Operator (`|`)

LCEL uses the Unix-style pipe operator to chain components together.
- **Syntax**: `chain = prompt | model | parser`
- **Output of one** becomes the **input of the next**.

### Example:
```python
from langchain_core.prompts import ChatPromptTemplate
from langchain_openai import ChatOpenAI
from langchain_core.output_parsers import StrOutputParser

prompt = ChatPromptTemplate.from_template("Tell me a joke about {topic}")
model = ChatOpenAI()
parser = StrOutputParser()

chain = prompt | model | parser

# Execution
response = chain.invoke({"topic": "bears"})
```

---

## 🚀 Key Advantages

### 1. First-class Streaming
Everything built with LCEL supports streaming from the start. You get tokens as soon as the model generates them, improving the user experience.
```python
for chunk in chain.stream({"topic": "bears"}):
    print(chunk, end="|", flush=True)
```

### 2. Async Support
Every chain built with LCEL can be called asynchronously using `.ainvoke()`, `.astream()`, or `.abatch()`. This is critical for scaling high-traffic APIs.

### 3. Parallelism
Use `RunnableParallel` to execute multiple branches of logic concurrently. Useful for comparing outputs from different models or fetching multiple pieces of information at once.

---

## 🧩 Advanced Composition

### `RunnablePassthrough`
Allows you to pass input through a step unchanged, or add new keys to the state.
```python
from langchain_core.runnables import RunnablePassthrough

# Passing 'context' and 'question' to the prompt
setup_and_retrieval = {
    "context": retriever | format_docs,
    "question": RunnablePassthrough()
}
chain = setup_and_retrieval | prompt | model
```

### `RunnableLambda`
Wrap custom Python functions so they can be piped just like LangChain components.
```python
from langchain_core.runnables import RunnableLambda

def reverse_text(text):
    return text[::-1]

chain = prompt | model | parser | RunnableLambda(reverse_text)
```

---

## 📊 Summary of Common Methods

| Method | Behavior | Use Case |
| :--- | :--- | :--- |
| **invoke** | Single input -> Single output | Simple requests |
| **stream** | Single input -> Token chunks | Chat UIs |
| **batch** | List of inputs -> List of outputs | Bulk processing |
| **ainvoke** | Async version of invoke | Highly scalable APIs |

---

**Next Steps**: Learn how to manage long-term context in [Memory Management](./Memory-Management.md).
