# 🚀 RAG Technical Documentation Assistant

An intelligent Retrieval-Augmented Generation (RAG) system built with **LangChain**, **LangGraph**, **ChromaDB**, and **FastAPI**. This application is designed to ingest technical documentation (e.g., Pydantic & LangGraph docs), analyze user queries, retrieve relevant context, grade document relevance, and generate accurate responses using Google's Gemini LLM.

---

## 🛠️ Architecture & Workflow (LangGraph)
The system uses a stateful graph workflow with conditional routing:

1. **Query Analysis (`query_analysis`)**: Refines and expands the user's technical query for better vector search results.
2. **Retrieval (`retrieve`)**: Fetches relevant document chunks from the Chroma vector store.
3. **Document Grading (`grade_documents`)**: Evaluates whether the retrieved documents are relevant to the query. If irrelevant, it triggers a query rewrite (`transform_query`).
4. **Answer Generation (`generate`)**: Synthesizes the final response based on the verified context.

---

## 📂 Project Structure
```text
├── RAG.ipynb          # Google Colab Notebook containing the full pipeline & FastAPI server
├── README.md          # Project Documentation
└── requirements.txt   # Dependencies
