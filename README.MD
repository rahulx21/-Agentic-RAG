# Agentic RAG Copilot

An end-to-end **Forward Deployed Engineer (FDE) project** that turns a notebook-style Agentic RAG workflow into a deployable internal product using **LangGraph, FastAPI, Pinecone, Groq, Tavily, HTML, CSS, and JavaScript**.


### Goal
Build a secure IT Support Copilot that:

1. Searches trusted private knowledge first.
2. Checks whether retrieved evidence is good enough.
3. Uses web search only when private knowledge is insufficient.
4. Rewrites weak queries and retries.
5. Generates grounded answers.
6. Shows the decision path for transparency and debugging.
7. Lets authorized staff add new company documents.

##  Agentic RAG Workflow

This follows the same core implementation pattern as the reference notebook.

```text
Question
   ↓
[1] Route Question
   ├── Greeting / simple chat ─────────────→ Direct Answer
   │
   └── IT support question
                ↓
[2] Retrieve from Private Pinecone KB
                ↓
[3] Grade Private Evidence
       ┌────────┴────────┐
       │                 │
     GOOD               WEAK
       │                 │
       ▼                 ▼
Generate from KB    [4] Tavily Web Search
                         ↓
                  [5] Grade Web Evidence
                    ┌────┴─────┐
                    │          │
                  GOOD        WEAK
                    │          │
                    ▼          ▼
              Generate Web  [6] Rewrite Query
                               ↓
                         Retry Private KB
                               ↓
                        Max retry reached?
                               ↓
                    Insufficient Evidence