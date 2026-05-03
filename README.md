# ArXiv-CS-Expert-Chatbot
Elevanceskills internship project
***

# ArXiv Computer Science Expert Chatbot

## Problem Statement
The exponential growth of computer science literature makes it challenging for researchers and engineers to extract timely insights, summarize research trends, and quickly grasp complex concepts. The goal of this project is to develop a domain-specific expert chatbot capable of answering complex queries, explaining advanced concepts, and summarizing research papers. The system leverages the Cornell University arXiv dataset, utilizing advanced Natural Language Processing (NLP) and Retrieval-Augmented Generation (RAG) techniques powered by open-source Large Language Models (LLMs) and a Streamlit interface.

## Requirements

### Dataset
* **Source:** [Cornell University arXiv Dataset on Kaggle](https://www.kaggle.com/datasets/Cornell-University/arxiv)
* **Subset:** Computer Science (`cs.*`) categories.
* **Storage Requirement:** Minimum 4.5 GB for the extracted metadata JSON, plus 1.5 GB for the vector index.

### Technical Stack
* **Framework:** Streamlit, LangChain, Sentence-Transformers, FAISS
* **LLM & Embeddings:** Mistral-7B-Instruct (via Hugging Face Inference API) and `all-MiniLM-L6-v2`
* **Environment:** Google Colab / Local environment with Python 3.10+

## Methodology

### 1. Data Ingestion & Preprocessing
To handle the large dataset within memory constraints, we employ a streaming pipeline that reads the JSON file line-by-line, filtering specifically for `cs.*` categories to reduce the footprint to relevant documents.

### 2. Information Extraction & Embedding
The relevant text (title and abstract) is embedded using the `sentence-transformers/all-MiniLM-L6-v2` model and indexed into a FAISS vector store.

### 3. RAG Architecture & Context Retrieval
When a query is submitted:
* **Retrieval:** The retriever uses similarity search to fetch the top-k most relevant papers.
* **Expert Explanation:** The context is passed to the LLM along with an expert prompt.
* **Conversational Memory:** Uses `ConversationBufferMemory` to retain context for follow-up questions.

## Deployment

### Prerequisites
1. Ensure your Hugging Face API Token is available.
2. Download the `arxiv-metadata-oai-snapshot.json` to your working directory using the Kaggle API.

### Installation
```bash
pip install -q langchain langchain-community langchain-huggingface sentence-transformers faiss-cpu streamlit
