# Bitcoin Graph-RAG

A toolkit for crawling, indexing, and semantically searching Bitcoin-related tasks using a Graph-augmented Retrieval-Augmented Generation (Graph-RAG) pipeline.

---

## 🚀 Project Highlights

- **Bitcoin Code Mining**: Crawl different bitcoin related sites for data
- **Graph-RAG**: Build a knowledge graph from data entities and relationships. Enable graph-constrained retrieval and reasoning for LLMs.
- **Semantic Search**: Store document embeddings in Milvus for fast, scalable semantic search.
- **End-to-End Pipeline**: From web crawling to entity extraction, graph construction, embedding, and RAG querying—all in one place.

---

## 1. Bitcoin Data Crawling & Analysis

### How It Works

1. **Anonymous Crawling**
    - Crawl different sublinks inside the single link for indepth scraping

2. **RAG**
    - Build a knowledge graph on entities using gpt 4o mini

### Example Use Cases

- “how do you incentivize miners?"
- “What is the fee threshold for inclusion?.”

---

## 2. Graph-RAG Pipeline 

### What is Graph-RAG?

Graph-RAG (Graph-augmented Retrieval-Augmented Generation) combines vector search (semantic similarity) with explicit knowledge graphs. This enables:

- More accurate, context-rich retrieval for LLMs
- Graph-based constraints (e.g., “find functions that interact with both A and B”)
- Better explainability and traceability

### Pipeline Overview

1. **Crawling & Extraction**
    - Use `DataExtraction.ipynb` to fetch data.
    - Store each file in txt files.

2. **Chunking & Embedding**
    - Generate semantic embeddings and store in Milvus.

3. **Entity & Relationship Extraction**
    - Extract entities 
    - Identify relationships 

4. **Graph Construction**
    - Build a knowledge graph: nodes = data entities, edges = relationships.

5. **Graph-RAG Querying**
    - Use the graph to filter relevant code contexts.
    - Retrieve supporting chunks via vector search.
    - Feed both graph context and retrieved code to the LLM for generation.

---

## 3. How to Run


### Run the Bitcoin Code Crawler

```bash

jupyter run DataExtraction.ipynb
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

### Launch the Graph-RAG Notebook (After Data extraction)

```bash
jupyter run Graph_Rag.ipynb
```

---

## 4. Dependencies

- `aiohttp`, `bs4`, `pypdf` for crawling/parsing
- `langchain`, `openai`, `networkx` for LLMs and graphs
- `pymilvus` for vector storage

---

## 5. Links to be scraped (Potential Ones)

   **General RAG resources:**
   
    - https://bitcoinops.org/
    - https://gnusha.org/
    - https://bitcointalk.org/
    - https://gnusha.org/url/
    - https://btctranscripts.com/categories
    - https://arxiv.org/search/?query=bitcoin&searchtype=all&source=header
    - https://iacr.org/search/?q=bitcoin
    - https://delvingbitcoin.org/
    - https://scalingbitcoin.org/transcripts
