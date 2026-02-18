# 🤖 🤖 Enterprise Q&A Bot: Retrieval-Augmented Generation (RAG)

### *Generative AI Study with IBM Watsonx & LangChain*

![RAG Architecture Diagram](images/rag_architecture.png)
*Figure 1: End-to-End RAG Pipeline featuring Semantic Search and LLM Context Augmentation.*

---

## 📋 Project Objective
Capstone project for the IBM GenAI Engineering with Python, LangChain & Watsonx course. This QA system leverages LangChain to automate information retrieval from extensive PDF libraries. It combines document loaders, embedding models, a vector database, and a Generative AI model to provide precise answers to user queries via a user-friendly Gradio front-end.

---

## 🏗️ System Architecture
The `qa-bot-langchain-rag` system is built on a modular **Retrieval-Augmented Generation (RAG)** architecture. Unlike traditional LLMs that rely solely on pre-trained knowledge, this system dynamically fetches relevant context from uploaded documents to provide grounded, factually accurate responses.

### 🔄 The Data Pipeline
The architecture follows a linear, four-stage lifecycle for every query:

1. Document Ingestion & Preprocessing
- **Loading:** The system uses `PyPDFLoader` to parse unstructured PDF data into a machine-readable format.
- **Semantic Chunking:** To maintain context window efficiency, the text is processed via a `RecursiveCharacterTextSplitter`. This ensures that chunks are small enough for the LLM but large enough to retain semantic meaning.
2. Vectorization & Embedding
- **Semantic Mapping:** Each text chunk is converted into a high-dimensional vector using **Watsonx Text Embeddings**.
- **Persistent Storage:** These vectors are indexed in a **ChromaDB** vector store, allowing for sub-second similarity searches based on the mathematical distance between a user's query and the document's content.
3. Contextual Retrieval
- **Query Embedding:** When a user asks a question, the query itself is vectorized.
- **Similarity Search:** The system retrieves the top-$k$ most relevant chunks from ChromaDB that match the intent of the query.
4. Augmented Generation
- **Prompt Construction:** The retrieved context is "stuffed" into a prompt template alongside the user's question.
- **Inference:** The **Granite-3-8B-Instruct** model analyzes the provided context to synthesize a final answer. If the answer is not present in the context, the model is instructed to remain silent rather than hallucinate, ensuring enterprise-grade reliability.

### 🎨 User Interface Layer
The entire backend is wrapped in a **Gradio** web interface, providing a seamless "Drag-and-Drop" experience for document uploading and a real-time chat window for interaction.

![Gradio Interface Preview](assets/gradio_ui.png)
*Figure 2: User interface showing PDF upload and context-grounded chat interaction.*

---

## ⚙️ Execution Guide

### 1. Clone the repository
git clone https://github.com/yourusername/qa-bot-langchain-rag.git

### 2. Environment Setup
It is recommended to use an environment with Python 3.12:
##### Using Conda (Recommended):
```bash
conda env create -f environment.yml
conda activate qabot-research
```
##### Using Pip:
```bash
pip install -r requirements.txt
```

### 3. Set up IBM Watsonx Credentials
Create a .env file in the root directory to store your API keys securely:
```Code snippet
WATSONX_API_KEY=your_key_here
PROJECT_ID=your_project_id_here
```

### 4. Run the Application
Navigate to the `app/` directory and launch the script via an IDE.
```bash
python qabot.py
```

---

## 💻 Tech Stack

This project leverages an enterprise-grade AI stack designed for high-fidelity information retrieval and scalable deployment.

- **Orchestration & Framework:** LangChain (Chains, Retrievers, and Document Loaders)
- **Generative AI Models:** IBM Watsonx.ai
    - **LLM:** Granite-3-8B-Instruct (Context-aware reasoning)
    - **Embeddings:**Watsonx Text Embeddings (Semantic vectorization)
- **Vector Database:** ChromaDB (Persistent vector storage and similarity search)
- **Data Processing:** PyPDF (Document parsing) and Recursive Character Splitting (Semantic chunking)
- **Interface:** Gradio (Production-ready web UI for document interaction)
- **Language:** Python 3.12 (Environment managed via Conda/Pip)

---

### 🚀 Technical Requirements

Note on Environment: This implementation is designed for **Enterprise AI Environments**. It requires an active IBM Watsonx.ai instance and API credentials. This choice reflects a focus on scalable, secure, and governed AI solutions rather than consumer-grade local inference.