# Multimodal-RAG-Knowledge-Assistant
A powerful **Multimodal Retrieval-Augmented Generation (RAG)** system that can ingest PDF documents, extract **text, tables, and images**, generate AI-enhanced summaries, store semantic embeddings in a vector database, and answer natural language questions using the retrieved multimodal context.

---

##  Features

-  PDF document ingestion
-  Intelligent text chunking using document structure
-  Table extraction and preservation
-  Image extraction from PDFs
-  AI-powered multimodal summarization using Gemini
-  Semantic search with vector embeddings
-  ChromaDB vector storage
-  Retrieval-Augmented Generation (RAG)
-  Natural language question answering
-  End-to-end automated ingestion pipeline

---

##  Architecture

```text
PDF Document
      │
      ▼
Document Partitioning
(Unstructured)
      │
      ▼
Content Extraction
├── Text
├── Tables
└── Images
      │
      ▼
Chunking by Title
      │
      ▼
AI Multimodal Summarization
(Gemini 2.5 Flash)
      │
      ▼
Embedding Generation
(BAAI/bge-small-en-v1.5)
      │
      ▼
Chroma Vector Database
      │
      ▼
Retriever
      │
      ▼
Question Answering
(Gemini 2.5 Flash)
```

---

##  Tech Stack

### AI & LLMs

- Google Gemini 2.5 Flash
- LangChain

### Embeddings

- BAAI/bge-small-en-v1.5

### Vector Database

- ChromaDB

### Document Processing

- Unstructured
- PDF Partitioning
- Table Extraction
- Image Extraction

### Python Libraries

- LangChain
- LangChain Chroma
- LangChain Google GenAI
- LangChain HuggingFace
- Unstructured
- Python Dotenv

---

##  Project Workflow

### 1. PDF Ingestion

The system ingests PDF documents and partitions them into structured elements.

```python
elements = partition_pdf(
    filename=file_path,
    strategy="hi_res",
    infer_table_structure=True,
    extract_image_block_types=["Image"],
    extract_image_block_to_payload=True
)
```

Extracted elements include:

- Text blocks
- Titles
- Tables
- Images

---

### 2. Content Chunking

Documents are chunked intelligently based on document structure and section titles.

Benefits:

- Preserves semantic meaning
- Improves retrieval accuracy
- Reduces context fragmentation

---

### 3. Multimodal Content Processing

Each chunk is analyzed to identify:

| Content Type | Supported |
|-------------|------------|
| Text | yes |
| Tables | yes |
| Images | yes |

The system preserves original multimodal content inside metadata for later retrieval.

---

### 4. AI-Powered Summarization

Each chunk is summarized using Gemini while retaining:

- Important textual information
- Table insights
- Visual information

This reduces token usage while maintaining retrieval quality.

---

### 5. Embedding Generation

Semantic embeddings are created using:

```python
BAAI/bge-small-en-v1.5
```

Features:

- Lightweight
- High retrieval performance
- Normalized embeddings
- Optimized for RAG systems

---

### 6. Vector Storage

Embeddings are stored in ChromaDB.

```python
vector_store = Chroma.from_documents(
    documents=documents,
    embedding=embedding_model
)
```

Benefits:

- Fast retrieval
- Persistent storage
- Scalable architecture

---

### 7. Retrieval

Relevant chunks are retrieved based on semantic similarity.

```python
retriever = db.as_retriever(search_kwargs={"k": 3})
chunks = retriever.invoke(query)
```

---

### 8. Answer Generation

Retrieved multimodal content is provided to Gemini for final response generation.

The model uses:

- Retrieved text
- Extracted tables
- Image context

to generate comprehensive answers.

---

##  Installation

### Clone Repository

```bash
git clone https://github.com/yourusername/multimodal-rag-knowledge-assistant.git

cd multimodal-rag-knowledge-assistant
```

### Install Dependencies

```bash
pip install -U "unstructured[all-docs]"
pip install -U langchain
pip install -U langchain-community
pip install -U langchain-chroma
pip install -U langchain-google-genai
pip install -U langchain-huggingface
pip install -U python-dotenv
```

---

##  Environment Variables

Create a `.env` file:

```env
GOOGLE_API_KEY=your_google_api_key
```

---

## 📖 Usage

### Run Complete Pipeline

```python
db = run_complete_ingestion_pipeline(
    "your_document.pdf"
)
```

---

### Query Documents

```python
query = "What is the complexity per layer of Convolutional networks?"

retriever = db.as_retriever(search_kwargs={"k": 3})

chunks = retriever.invoke(query)

answer = generate_final_answer(
    chunks,
    query
)
```

---

## 📊 Example Queries

- What is the main contribution of the paper?
- Summarize the methodology section.
- Explain the results shown in the tables.
- What conclusions are drawn from the experiments?
- Compare the approaches discussed in the document.
- What does the architecture diagram represent?

---

##  Output Artifacts

### Vector Database

```text
chroma_db/
```

Stores:

- Embeddings
- Metadata
- Retrieval index

### Retrieved Chunks

```json
{
  "text": "...",
  "tables": [...],
  "images": [...]
}
```

---

##  Use Cases

### Research Papers

- Scientific literature search
- Academic assistants
- Paper summarization

### Enterprise Knowledge Bases

- Internal documentation search
- Policy retrieval
- Knowledge management

### Legal Documents

- Contract analysis
- Case law retrieval
- Compliance search

### Technical Documentation

- API documentation
- Product manuals
- Engineering specifications

---

##  Key Advantages

### Traditional RAG

- Text only
- Loses visual context
- Weak table understanding

### This Multimodal RAG

- Text + Tables + Images
- Better context retention
- Improved answer quality
- More accurate retrieval

---

##  Future Improvements

- [ ] OCR support for scanned PDFs
- [ ] Multi-document collections
- [ ] Hybrid search (BM25 + Vector Search)
- [ ] Re-ranking models
- [ ] Image caption generation
- [ ] Streamlit Web UI
- [ ] Knowledge graph integration
- [ ] Agentic RAG workflows

---

##  Contributing

Contributions are welcome.

1. Fork the repository
2. Create a feature branch

```bash
git checkout -b feature/new-feature
```

3. Commit changes

```bash
git commit -m "Add new feature"
```

4. Push branch

```bash
git push origin feature/new-feature
```

5. Open a Pull Request

---

##  License

This project is licensed under the MIT License.

---

##  Acknowledgements

- LangChain
- ChromaDB
- Google Gemini
- HuggingFace
- Unstructured

---
