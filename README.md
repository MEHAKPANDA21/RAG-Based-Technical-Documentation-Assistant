🚀 RAG Technical Documentation Assistant
An intelligent Retrieval-Augmented Generation (RAG) system built with LangChain, LangGraph, ChromaDB, and FastAPI. This application is designed to ingest technical documentation (e.g., Pydantic docs), analyze user queries, retrieve relevant context, grade document relevance, and generate accurate responses using Google's Gemini LLM.

🛠️ Architecture & Workflow (LangGraph)
The system uses a stateful graph workflow with conditional routing:

Query Analysis (query_analysis): Refines and expands the user's technical query for better vector search results.

Retrieval (retrieve): Fetches relevant document chunks from the Chroma vector store.

Document Grading (grade_documents): Evaluates whether the retrieved documents are relevant to the query. If irrelevant, it flags for a web search or fallback (transform_query).

Answer Generation (generate): Synthesizes the final response based on the verified context.

📂 Project Structure
Plaintext
├── RAG.ipynb          # Google Colab Notebook containing the full pipeline & FastAPI server
├── README.md          # Project Documentation
└── requirements.txt   # Dependencies
⚙️ Installation & Setup
Clone the repository / Open in Google Colab:
You can run the provided notebook directly in Google Colab.

Install Dependencies:

Bash
pip install langchain langchain-core langchain-community langgraph chromadb fastapi uvicorn pydantic sentence-transformers langchain-google-genai
Set API Keys:
Set your Google Gemini API key as an environment variable:

Python
import os
os.environ["GOOGLE_API_KEY"] = "your_gemini_api_key_here"
🔌 API Endpoints
Once the FastAPI server is running (e.g., on [http://127.0.0.1:8001](http://127.0.0.1:8001)), you can interact with the following endpoints:

1. List Indexed Documents
URL: /documents

Method: GET

Description: Returns a preview of the documentation chunks indexed in the vector store from the Pydantic Documentation.

2. Query the Assistant
URL: /query

Method: POST

Payload Example:

JSON
{
  "question": "What is LangGraph?"
}
Response Example:

JSON
{
  "question": "What is LangGraph?",
  "generation": "LangGraph is a library for building stateful, multi-actor applications with LLMs...",
  "documents_count": 2
}
🧪 Testing the API
You can test the endpoints using Python's requests library:

Python
import requests

# Test /documents
response = requests.get("http://127.0.0.1:8001/documents")
print(response.json())

# Test /query
payload = {"question": "Explain Pydantic models"}
res = requests.post("http://127.0.0.1:8001/query", json=payload)
print(res.json())
