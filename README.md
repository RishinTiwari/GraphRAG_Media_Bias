# GraphRAG Media Bias Detection

This project investigates media bias in news articles using advanced **Knowledge Graph (KG)** and **Retrieval-Augmented Generation (RAG)** pipelines. We use Neo4j to construct a graph of entities and their relationships from scraped political and non-political articles, and then apply **GraphRAG** and **RAG** techniques for answering complex questions. The goal is to identify **narrative differences** and **bias** across media outlets using structured knowledge and large language models (LLMs).

---

## 📌 Project Objectives

- Detect and compare **media bias** across news sources.
- Build a **Knowledge Graph** using Named Entity Recognition (NER) and co-occurrence relations.
- Implement both **RAG** and **GraphRAG** pipelines.
- Query and analyze articles to study linguistic framing, factual consistency, and entity-level relationships.
- Evaluate output using **RAGAS metrics** (Relevancy, Faithfulness, Precision, Recall).

---

## 🗂️ Project Structure

GraphRAG_MediaBias/
│
├── Article_Scraping.ipynb # Scrapes articles and stores metadata
├── final_normalized_articles.csv # Final cleaned dataset with NER normalization
├── KG_neo4j.ipynb # Creates knowledge graph in Neo4j from NER
├── Table_Results.pdf # Evaluation results for RAG vs GraphRAG
├── Report.pdf # Formal project report
├── README.md # Project overview and documentation
└── .gitignore # Optional - for ignoring local files


---

## 📄 Dataset

- **Total Articles:** 60  
- **Topics Covered:**  
  - Trump-Zelenskyy Meeting (Bias)  
  - Tariffs & Trade War (Bias)  
  - NCAA Basketball Championship (Non-Bias)  
  - California Wildfires (Non-Bias)

- **Fields:**  
  `Topic`, `Source`, `Media Bias Rating`, `Link`, `Bias`, `Content`, `Content_Normalized`

Articles were scraped using the `newspaper3k` library. Manual and automatic normalization was applied to unify entities (e.g., “Donald J. Trump”, “Trump”, etc.).

---

## 🏗️ Pipeline Overview

### 1. Data Collection & Scraping
- Used `newspaper3k` to extract article text.
- Stored article metadata and full content in a CSV.

### 2. Named Entity Recognition (NER)
- Applied **spaCy** for entity extraction.
- Focused on `PERSON` entities and built co-occurrence-based relationships.

### 3. Entity Normalization
- Created a custom mapping to resolve entity variants (e.g., Trump, Donald Trump).
- Replaced text in articles with normalized entities.

### 4. Knowledge Graph Construction (Neo4j)
- Created `Person` nodes and `RELATED_TO` edges in Neo4j Aura using the official driver.
- Used entity co-occurrence logic to build meaningful relationships.
- Reduced node count from ~3000 to ~112 using NER normalization.

### 5. RAG vs GraphRAG Pipeline
- **RAG Pipeline:** Used FAISS vector store + Mistral via Groq API.
- **GraphRAG Pipeline:** Used `neo4j-graphrag` with vector index + GPT-4o via Neo4j LLM Chat interface.

---

## 🔍 Sample Questions

- What actions did Donald Trump take during the Ukraine talks?
- What sources reported on both tariffs and the Russia-Ukraine war?
- How did NCAA basketball finals coverage differ by media bias?
- What are the connections between key people in wildfire coverage?

---

## 📊 Results (GPT-4o Pipeline Only)


- **GraphRAG** outperforms in relationship-aware queries.
- **RAG** is faster and better suited for factual summaries.

---

## 🛠️ Tech Stack

- **Python**, **Pandas**, **spaCy**, **tqdm**
- **Neo4j Aura DB** (cloud)
- **LangChain**, **Groq API (Mistral model)**
- **Ollama (LLaMA3.1)** – initially used for local LLM querying
- **neo4j-graphrag** for GraphRAG pipeline
- **RAGAS** for evaluation metrics

---

