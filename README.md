# Bitcoin Graph-RAG & Code Intelligence

A toolkit for crawling, indexing, and semantically searching Bitcoin-related source code using a Graph-augmented Retrieval-Augmented Generation (Graph-RAG) pipeline.

---

## 🚀 Project Highlights

- **Bitcoin Code Mining**: Crawl GitHub for Bitcoin-related `.py` and `.js` files, enabling code search, analysis, and downstream LLM-based code understanding.
- **Graph-RAG for Code**: Build a knowledge graph from code entities and relationships. Enable graph-constrained retrieval and reasoning for LLMs.
- **Semantic Search**: Store code/document embeddings in Milvus for fast, scalable semantic search.
- **End-to-End Pipeline**: From web crawling to entity extraction, graph construction, embedding, and RAG querying—all in one place.

---

## 1. Bitcoin Code Crawling & Analysis

### How It Works

1. **Anonymous Crawling**
    - Crawl GitHub search results for “bitcoin” in `.py` and `.js` files (no API key required).
    - Download raw code files into a local directory structure.

2. **Storage & Organization**
    - Files are organized by language, repo, and file path.
    - Easily extensible to crawl other platforms (GitLab, Bitbucket).

3. **Indexing & Embedding**
    - Extract code chunks (functions, classes).
    - Generate embeddings (e.g., OpenAI, CodeBERT).
    - Store in Milvus for semantic code search.

4. **RAG for Code**
    - Build a code knowledge graph (e.g., function call graphs, dependency graphs).
    - Enable graph-constrained code search and LLM-based code Q&A.

### Example Use Cases

- “Find all Python Bitcoin wallet implementations using ECDSA.”
- “Summarize how transaction signing is handled in JavaScript Bitcoin libraries.”
- “Trace dependencies between Bitcoin smart contract modules.”

---

## 2. Graph-RAG Pipeline (for Code)

### What is Graph-RAG?

Graph-RAG (Graph-augmented Retrieval-Augmented Generation) combines vector search (semantic similarity) with explicit knowledge graphs for code. This enables:

- More accurate, context-rich retrieval for LLMs
- Graph-based constraints (e.g., “find functions that interact with both A and B”)
- Better explainability and traceability

### Pipeline Overview

1. **Crawling & Extraction**
    - Use `bitcoin_crawler.py` to fetch code from GitHub.
    - Store each file with metadata.

2. **Chunking & Embedding**
    - Split code into logical units (functions, classes).
    - Generate semantic embeddings and store in Milvus.

3. **Entity & Relationship Extraction**
    - Extract code entities (functions, classes, modules).
    - Identify relationships (e.g., function calls, imports).

4. **Graph Construction**
    - Build a knowledge graph: nodes = code entities, edges = relationships.

5. **Graph-RAG Querying**
    - Use the graph to filter relevant code contexts.
    - Retrieve supporting code chunks via vector search.
    - Feed both graph context and retrieved code to the LLM for generation.

---

## 3. How to Run

### Environment Setup

```bash
pip install -r requirements.txt
```

### Run the Bitcoin Code Crawler

```bash
python bitcoin_crawler.py --pages 5 --output ./downloads
```

### Start Milvus (Vector DB)

```bash
docker run -d --name milvus -p 19530:19530 milvusdb/milvus:v2.3.9
```

### Index Entities and Embeddings

```python
from your_index_module import (
    read_indexer_entities, MilvusVectorStore, store_entity_semantic_embeddings
)

entities = read_indexer_entities(entity_df, entity_embedding_df, COMMUNITY_LEVEL)
description_embedding_store = MilvusVectorStore(collection_name="entity_description_embeddings")
description_embedding_store.connect(uri="http://localhost:19530")
entity_description_embeddings = store_entity_semantic_embeddings(
    entities=entities, vectorstore=description_embedding_store
)
```

### Launch the Graph-RAG Notebook

```bash
jupyter lab mi/MiAILaw/src/Graph_Rag.ipynb
```

---

## 4. Customization & Extensibility

- **Change code crawling keywords or platforms**: Edit `bitcoin_crawler.py`.
- **Switch embedding models**: Swap out LLM or code embedding models as needed.
- **Extend graph logic**: Add new entity/relationship types for richer graphs.

---

## 5. Dependencies

- `aiohttp`, `bs4`, `pypdf` for crawling/parsing
- `langchain`, `openai`, `networkx` for LLMs and graphs
- `pymilvus` for vector storage

---

## 6. License

MIT License

---