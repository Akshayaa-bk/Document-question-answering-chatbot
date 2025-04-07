# 🧠 RAG Chatbot - Document-Aware Conversational AI

This project implements a Retrieval-Augmented Generation (RAG) based chatbot that allows users to upload their own documents and interact with an intelligent assistant capable of understanding and answering queries grounded on the uploaded content.

---

## 🚀 Deliverables

### ✅ How to Run the Chatbot

1. **Download the Notebook**
   - Download the [`rag_chatbot_ailaysa_(3).ipynb`](./rag_chatbot_ailaysa_(3).ipynb) notebook from this repository.

2. **Set Up Environment**
   - Create a `.env` file and populate it with the required access tokens:
     ```
     OPENAI_API_KEY=your_openai_key
     PINECONE_API_KEY=your_pinecone_key
     PINECONE_ENV=your_pinecone_env
     ```

3. **Load Secrets into Google Colab**
   - Add the above environment variables as **secrets** in your Google Colab runtime using:
     - `Files` > `Upload .env` manually, or
     - `secrets` settings on Colab (recommended for security)

4. **Run the Notebook**
   - Execute all cells in the notebook in order.
   - You will be prompted to upload documents (PDF, TXT, etc.)
   - An OpenGrok-style search interface will be generated to explore content.
   - Start chatting with your intelligent assistant, which now has contextual awareness of the uploaded documents!

---

## 🛠️ Technical Overview

### ⚙️ Tech Stack

- **Python**
- **LangChain** for building the chatbot pipeline
- **OpenAI GPT-3.5/GPT-4** for language generation
- **Pinecone** as the vector store for efficient document retrieval
- **FAISS** (fallback option for local vector search)
- **Streamlit / Colab UI** for interaction
- **dotenv** for secure credential handling

---

### 🧩 Response Structuring Approach

- **Document Embedding**: Uploaded files are parsed, chunked, and embedded using OpenAI Embeddings.
- **Vector Storage**: Chunks are stored in Pinecone with metadata to allow quick and relevant retrieval.
- **Query Handling**:
  - User queries are transformed into embeddings.
  - Relevant document chunks are retrieved based on vector similarity.
  - Retrieved context is appended to the prompt and sent to GPT for final answer generation.
- **Answer Composition**: Responses are structured to include:
  - A direct answer
  - Optionally, source or context references (if traceable)

---

## 🧠 Challenges & Solutions

### 1. **Token Limitations**
   - **Problem**: Context length exceeded OpenAI token limits.
   - **Solution**: Implemented dynamic chunk sizing and filtered irrelevant chunks to keep prompts concise.

### 2. **Document Diversity**
   - **Problem**: Files of various formats (PDF, DOCX, TXT) caused inconsistent parsing.
   - **Solution**: Unified all input into plain text using `langchain.document_loaders` and fallback manual extractors.

### 3. **Query Irrelevance**
   - **Problem**: Sometimes chatbot answered questions unrelated to the documents.
   - **Solution**: Enforced a retrieval confidence threshold and instructed the model to say "I don't know" if context is insufficient.

---

## 📎 Links

- 📂 Notebook: [`rag_chatbot_ailaysa_(3).ipynb`](./rag_chatbot_ailaysa_(3).ipynb)
- 🔎 OpenGrok-style interface: *(Generated at runtime)*

---

## 📬 Contact

For questions or collaboration inquiries, feel free to open an [issue](https://github.com/your-username/your-repo/issues) or reach out.

---

🌟 If you find this useful, please give it a star and consider contributing!
