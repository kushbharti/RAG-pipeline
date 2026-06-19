# RAG Document Search and Summarization System

A Python-based Retrieval-Augmented Generation (RAG) project that loads documents from multiple file formats, converts them into embeddings, stores them in a FAISS vector database, and retrieves relevant context to generate query-based summaries using a Groq LLM.

## Project Context

This project represents my foundational implementation of a Retrieval-Augmented Generation (RAG) system. It serves as a structured, hands-on effort to understand how modern document ingestion, embedding, vector search, and LLM-based summarization work together in a real pipeline.

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

## Architecture Overview

The system follows a standard RAG pipeline:

1. **Document Loading**  
   Files are scanned from the `data/` directory and loaded into LangChain document format.

2. **Chunking**  
   Documents are split into smaller overlapping chunks for better retrieval quality.

3. **Embedding Generation**  
   Each chunk is converted into a dense vector using the `all-MiniLM-L6-v2` sentence transformer model.

4. **Vector Storage**  
   Embeddings are stored in a FAISS index along with chunk metadata.

5. **Retrieval**  
   A user query is embedded and matched against the vector store to fetch the most relevant chunks.

6. **Generation**  
   Retrieved chunks are passed to the Groq LLM to generate a concise summary based on the query.

## Project Structure

```bash
.
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

## Module Breakdown

### `data_loader.py`

Loads supported files recursively from the given data directory using LangChain community loaders.

### `embedding.py`

Handles:

- document chunking
- embedding generation
- embedding model initialization

### `vectorstore.py`

Builds, saves, loads, and queries the FAISS vector store.

### `search.py`

Connects retrieval with generation. It retrieves relevant chunks and sends them to the Groq LLM for summarization.

### `app.py`

Example entry point to:

- load documents
- build vector index
- run similarity search
- generate summaries

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

## Usage

### 1. Add documents

Place your files inside the `data/` folder.

### 2. Build the vector store and test retrieval

```bash
python app.py
```

### 3. Example query flow

The system can process a query like:

```python
query = "What is attention mechanism?"
```

Then it:

- retrieves the most relevant chunks from FAISS
- builds a context block
- sends the context to the Groq LLM
- returns a generated summary

## Architecture Diagrams

Add your three project images inside an `assets/` folder and reference them like this:

```md
## Architecture Diagrams

### RAG Overview

### Complete RAG Pipeline

### End-to-End Architecture
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
