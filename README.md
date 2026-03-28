# Corrective-RAG-Based-ML-Tutor
This project implements a Corrective Retrieval Augmented Generation (RAG) pipeline using LangChain + LangGraph + FAISS + Groq LLM to build an intelligent ML Tutor system.
It retrieves information from multiple PDFs, evaluates relevance, optionally performs web search, and generates accurate answers.

## Features
- Multi-document PDF ingestion  
- Semantic search using FAISS  
- LLM-powered document evaluation (relevance scoring)  
- Sentence-level context refinement  
- Web search fallback (Tavily API)    
- Dynamic routing using LangGraph  
- Answer generation using Groq (LLaMA 3)

## Architecture

<img width="216" height="747" alt="Screenshot (1648)" src="https://github.com/user-attachments/assets/62199c17-0f10-46df-b6d5-695d801c2e0d" /><br>

## Tech Stack
- LangChain
- LangGraph
- FAISS
- HuggingFace Embeddings (BAAI/bge-small-en-v1.5)
- Groq LLM (llama-3.3-70b-versatile)
- Tavily API (Web Search)
- Python

## Project Structure
```bash
├── documents/  
├── Final.ipynb
├── README.md 
└── requirements.txt
```

## Setup Instructions

### 1. Clone the repository

```bash
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
```
### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Set your API keys before running

```bash
import os
os.environ["GROQ_API_KEY"] = "your_groq_key"
os.environ["TAVILY_API_KEY"] = "your_tavily_key"
```

## How It Works
1. Document Processing
PDFs are loaded and split into chunks
Text is cleaned and embedded
2. Retrieval
FAISS retrieves top-k relevant chunks
3. Evaluation
Each document is scored by LLM
```bash
Threshold-based filtering:
> 0.7 → Relevant
< 0.3 → Irrelevant
```
4. Routing Logic
If relevant -> refine context
Else -> rewrite query -> web search
5. Context Refinement
Break into sentences
Keep only useful information
6. Answer Generation
LLM generates answer using refined context only
