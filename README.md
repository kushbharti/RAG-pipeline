# RAG Document Search and Summarization System

A Python-based Retrieval-Augmented Generation (RAG) project that loads documents from multiple file formats, converts them into embeddings, stores them in a FAISS vector database, and retrieves relevant context to generate query-based summaries using a Groq LLM.

## Project Context

This project represents my foundational implementation of a Retrieval-Augmented Generation (RAG) system. It serves as a structured, hands-on effort to understand how modern document ingestion, embedding, vector search, and LLM-based summarization work together in a real pipeline.



## Architecture Diagrams

### RAG Overview

<img width="1228" height="478" alt="Rag--1" src="https://github.com/user-attachments/assets/b5abc013-683a-4997-abfa-2c395957c5bf" />

### Complete RAG Pipeline

<img width="1430" height="873" alt="Rag--3" src="https://github.com/user-attachments/assets/0757f35a-e1de-435a-a220-6486fe0b46c5" />

<img width="1536" height="639" alt="Rag--2" src="https://github.com/user-attachments/assets/5bbeeece-2e14-489e-be1c-dfeb0d85828b" />



## Features

- Load documents from multiple formats:
  - PDF
  - TXT
  - CSV
  - Excel (`.xlsx`)
  - Word (`.docx`)
  - JSON
- Split raw documents into semantic chunks using `RecursiveCharacterTextSplitter`
- Generate embeddings with `sentence-transformers`
- Store and search embeddings using FAISS
- Retrieve top-k relevant chunks for a user query
- Summarize retrieved context using Groq LLM integration
- Persist vector index and metadata locally

## Project Structure

```bash

├── data/
├── faiss_store/
│   ├── faiss.index
│   └── metadata.pkl
├── src/
│   ├── data_loader.py
│   ├── embedding.py
│   ├── vectorstore.py
│   └── search.py
├── .env
├── requirements.txt
├── app.py
└── README.md
```

## Tech Stack

- **Python**
- **LangChain Community Loaders**
- **Sentence Transformers**
- **FAISS**
- **Groq LLM API**
- **python-decouple**
- **NumPy**

## Installation

```bash
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
pip install -r requirements.txt
```

## Environment Setup

Create a `.env` file in the project root:

```env
GROQ_API_KEY=your_groq_api_key_here
```

## Strengths

- Supports multiple document formats
- Clear modular separation of loading, embedding, storage, and retrieval
- Simple and practical FAISS-based implementation
- Easy to extend with APIs or UI layers
- Good foundation for advanced RAG experimentation

## Current Limitations

- Uses basic FAISS `IndexFlatL2` without advanced filtering or metadata search
- Stores only chunk text in metadata
- No re-ranking stage
- No API or frontend interface yet
- Limited prompt engineering and evaluation workflow

## Future Improvements

- Add metadata-aware retrieval
- Introduce reranking for better relevance
- Expose the pipeline through FastAPI or Streamlit
- Add conversational memory
- Support hybrid search
- Improve prompt templates and response evaluation

## Learning Outcome

This project helped establish a practical understanding of the end-to-end RAG workflow, from raw document ingestion to semantic retrieval and LLM-powered answer generation. It also creates a strong base for building more advanced retrieval systems in future iterations.

## License

This project is for educational and learning purposes.
