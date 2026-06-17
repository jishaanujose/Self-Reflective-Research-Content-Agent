# 📝 Agentic AI Research & Article Drafting Pipeline

An autonomous, multi-agent research assistant built with **LangGraph**, **Groq (Llama 3.3)**, and **Streamlit**. This project leverages modern **Agentic AI** patterns to automate web-scraping, evaluate data density, draft structured articles, and gracefully pause for human intervention.

---

## 🚀 Key Features

*   🤖 **Autonomous Multi-Agent Network**: Separate specialization blocks for query generation, search, data valuation, and writing.
*   📊 **Relevance Guardrails**: An AI evaluator analyzes raw search payloads to reject outliers and check for informational gaps.
*   🚦 **Human-In-The-Loop Interrupts**: State transitions freeze entirely before final rendering, giving users complete veto and review power.
*   🔄 **Dynamic State Time-Travel**: Uses LangGraph's advanced `Command` primitive to wipe pending queues and force-route execution backwards based on human critiques.
*   🪵 **Monitored Appending Logs**: Real-time log tracking across agent nodes using state-safe reducers.

---

## 🛠️ Tech Stack

*   **Orchestration Engine**: [LangGraph](https://github.com) (StateGraph & State Checkpointers)
*   **LLM Model Integration**: [LangChain Groq](https://github.com) (`llama-3.3-70b-versatile`)
*   **Live Web Tooling**: DuckDuckGo Search API
*   **User Interface**: Streamlit Dashboard

---

## 📐 System Flow Architecture

```text
       [START]
          │
  [query_generator] ──> Initializes State (regen_count=0)
          │
    [web_searcher]  <───┐ (Loops back up to 2 times)
          │             │
     [evaluator]        │
          │             │
   (analyse_evaluator)  │
     ├──> [No] ──> [count_check] ──> [Yes: query_regen]
     │                                └──> [No: stopper] ──> [END]
     └──> [Yes] 
          │
   [content_creator]
          │
  🚦 (INTERRUPT) ──> Human Reviews Draft on UI
          │
     [User Verdict]
     ├──> Approved  ──> [completion] ──> [END]
     └──> Rejected ──> Command(goto="query_regen") ──> Loop to top
```

---

## 💾 Installation & Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com
   cd YOUR_REPO_NAME
   ```

2. **Install required packages:**
   ```bash
   pip install langgraph langchain-groq langchain-community streamlit
   ```

3. **Set up environment variables:**
   ```bash
   export GROQ_API_KEY="your_groq_api_key_here"
   ```

4. **Launch the Streamlit App:**
   ```bash
   streamlit run app.py
   ```

---
