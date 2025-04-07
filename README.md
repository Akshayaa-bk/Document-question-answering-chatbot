# 🤖 RAG Chatbot – AILaysa

A Retrieval-Augmented Generation (RAG) based chatbot that allows users to upload documents and interact with them via natural language questions. Powered by modern LLMs, LangChain, PINECONE, and Streamlit.

---

## 📌 Table of Contents
- [💡 Project Overview]
- [🚀 Getting Started]
- [🛠️ Tech Stack]
- [📦 Project Structure]
- [🧩 Response Structuring Approach]
- [⚠️ Challenges & Solutions]
- [📸 Demo & Screenshots]
  

---

## 💡 Project Overview

This chatbot enhances user interaction with document data using LLMs and vector-based retrieval. It takes in user-uploaded documents, extracts meaningful chunks, embeds them into a vector space, and answers user queries based on relevant information.

---

## 🚀 Getting Started

### 🔧 Prerequisites

Ensure the following are installed:
```bash
pip install -r /project/requirements.txt
```

### 📂 Running the App

Follow these steps:

1. **Launch the Jupyter Notebook**
   - Open and run all the cells in`rag_chatbot_ailaysa.ipynb`.

2.**Set secret keys**
  - set the env variables which are available in the .env file as keys in google colab

3. **Get the App Link**
   - Once executed, you'll receive a "...ngrok-free.app"  link from the last cell as an output.

4. **Open the Link**
   - Click the link to open the Streamlit app in your browser. (click "visit site" in the ngrok.app link prompted before the streamlit)

5. **Upload Documents**
   - Use the sidebar in the streamlit app to upload PDF, TXT, or DOCX files.

6.**Start Chatting!**
   - Enter any question related to your uploaded documents and get contextual answers.

---

## 🛠️ Tech Stack

| Layer                | Technology                    | Purpose                                                                 |
|---------------------|-------------------------------|-------------------------------------------------------------------------|
| 💬 Language Model    | Mistral-7B-Instruct-v0.2       | Generates human-like responses                                          |
| 🤗 Model Provider    | Hugging Face Hub               | Hosts and serves the LLM via nt`                     |
| 🔍 Vector Store       | Pinecone                        | Stores and retrieves semantic embeddings                                |
| 🧠 Retrieval Method   | Hybrid Search (Semantic + Keyword) | Enhances retrieval accuracy by combining dense and sparse search        |
| 🧱 Framework          | LangChain                       | Document parsing, chunking, embedding, retrieval, and orchestration     |
| 🌐 Interface          | Streamlit                       | UI for document upload and interaction                                  |
| 🌉 Hosting (Dev)      | Gradio / ngrok                  | Share the app externally during development                             |

---

## 📦 Project Structure inside the ipynb

```

├──project
├──project
   ├──.gitignore
   ├──.env
   ├──utils
      ├──document_processor.py
      ├──embedding_manager.py
      ├──__init__.py
      ├──retrieval_engine.py
      ├──llm_interface.py
   ├──requirements.txt
   ├──app.py
   ├──main.py                      
```

---

## 🧩Workflow

The chatbot follows a pipeline-based architecture:

1. **Document Loading**
   - Files are uploaded via the Streamlit sidebar.

2. **Chunking**
   - Documents are split into manageable text segments for embedding using RecursiveCharacterTextSplitter.
   - Tables are identified and processed separately
   -  Each chunk is tagged with source, page, and relationship data
   -  Related chunks are organized hierarchically for context

3. **Embedding**
   - Each chunk is converted into a vector using all-mpnet-base-v2 Embeddings.
   - Preserves document structure in vector store

4. **Storage in Pinecone**
   - Vectors are indexed in Pinecone for fast similarity-based retrieval.

5. **Query Handling**
   - User inputs a question.
   - Top-k relevant document chunks are retrieved from Pinecone
   - A prompt is created combining these chunks + user query.

6.**Retrieval Engine**
   - The RetrievalEngine class provides a simplified interface for document retrieval using    different methods:

      - Dense vector retrieval (using a vector database)
      -Sparse retrieval (using BM25 algorithm)
      -Ensemble retrieval (combining both methods)

7. **LLM Response**
   - Chains the retriever with an LLM **Mistral-7B-Instruct-v0.2** for context-aware response generation
   -  Structured Prompt Design
   - Includes a custom prompt template enforcing:
     - Use of **Markdown tables** for structured data.
     - Use of **bullet points** for lists and clear formatting.
     - Natural language fallback when the answer isn’t available.
   - Ensures consistent, readable, and informative responses.

---


## ⚠️ Challenges & Solutions

| Challenge | Solution |
|-----------|----------|
| File upload state inconsistency | Managed uploads using Streamlit session state and unique keys |
| Token limit issues in LLMs | Used chunking, trimming, and prompt templates to stay within token limits |
| Slow retrieval for large docs | Implemented FAISS for fast similarity search |
| Redundant responses due to poor prompts | Refined prompt template for contextual grounding and clarity |

---

## 📸 Demo & Screenshots

![image](https://github.com/user-attachments/assets/752fc6c6-b3a7-419c-ad1c-b35c6fed5bd7)


---


Built by Akshayaa B K 
