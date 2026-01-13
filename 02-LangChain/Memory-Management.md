# Memory Management in AI Agents 🧠

Memory is what allows an agent to maintain state across multiple turns of a conversation. In LangChain, memory management has evolved from simple buffers to complex, persistent architectures.

---

## 🧩 Types of Memory

### 1. ConversationBufferMemory
The simplest form. It stores every message in the conversation.
- **Pros**: Easy to implement.
- **Cons**: Context window fills up quickly; costs increase as the conversation grows.

### 2. ConversationBufferWindowMemory
Keeps a sliding window of the last `K` interactions.
- **Pros**: Prevents context window overflow.
- **Cons**: The agent "forgets" anything older than K turns.

### 3. ConversationSummaryMemory
Instead of storing raw messages, an LLM summarizes the conversation so far.
- **Pros**: Efficient use of tokens for long conversations.
- **Cons**: Summarization can lose specific details (e.g., names or numbers).

---

## 📂 Long-Term Memory (Persistent)

For agents to remember users across sessions, you need external storage.

- **Redis**: Fast, key-value storage for chat history.
- **Postgres (Zep/LangChain)**: Using relational databases for structured message storage.
- **Vector Stores**: Storing previous conversations as embeddings to perform "Retrieval Augmented Memory."

---

## 🛠️ Implementation Strategy (LCEL)

In modern LangChain, we often manage memory manually within a chain or using `RunnableWithMessageHistory`.

```python
from langchain_core.chat_history import InMemoryChatMessageHistory
from langchain_core.runnables.history import RunnableWithMessageHistory

store = {}

def get_session_history(session_id: str):
    if session_id not in store:
        store[session_id] = InMemoryChatMessageHistory()
    return store[session_id]

# Wrap your chain
with_message_history = RunnableWithMessageHistory(
    chain,
    get_session_history
)
```

---

## ✅ Best Practices

1.  **Summarize Early**: Don't wait for the context window to hit 100% before summarizing.
2.  **Entity Memory**: Extract specific facts (e.g., "User likes Python") and store them in a JSON field instead of relying on raw history.
3.  **Tiered Memory**: 
    - **Tier 1 (RAM)**: Last 3-5 messages (Raw).
    - **Tier 2 (Summarization)**: Global summary of the conversation.
    - **Tier 3 (DB)**: Key facts and user preferences (Long-term).

---

**Next Steps**: Learn how to tailor your prompts for high-performance agent reasoning in [Prompt Engineering for Agents](./Prompt-Engineering-Agents.md).
