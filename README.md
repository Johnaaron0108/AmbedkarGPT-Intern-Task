🧠 Local RAG Pipeline using LangChain, ChromaDB, HuggingFace Embeddings & Ollama (Mistral 7B)

This project implements a fully local, offline Retrieval-Augmented Generation (RAG) system using:

Python 3.8+

LangChain for RAG orchestration

ChromaDB for local vector storage

HuggingFace Embeddings (sentence-transformers/all-MiniLM-L6-v2)

Ollama with Mistral 7B as the LLM

Zero API keys, Zero cloud services, Zero cost

The system loads speech.txt, splits it into chunks, embeds them, stores them in a vector DB, retrieves relevant context for any user question, and generates accurate answers using a local LLM.

🚀 Features
🔒 100% Local & Offline

Everything — embeddings, vector search, and LLM inference — runs locally.
Perfect for privacy-focused or air-gapped environments.

⚡ Fast, Lightweight Embeddings

Uses the highly efficient all-MiniLM-L6-v2 model for sentence embeddings.

🧠 High-Quality Local LLM

Leverages Mistral 7B running in Ollama for fast, high-quality answers.

🗂 Persistent Vector Storage

ChromaDB stores embeddings on disk so you don’t need to reprocess the document every run.

🔧 Modular Architecture

Each step (load → chunk → embed → store → retrieve → generate) is clearly separated and reusable.

📁 RAG Pipeline Overview

The system performs the following six core steps:

1. Load Input Document

Reads the provided speech.txt file.

2. Split Text into Chunks

Uses RecursiveCharacterTextSplitter with:

Chunk size: 800

Overlap: 120

3. Generate Embeddings (Local, Offline)

Using HuggingFace:

sentence-transformers/all-MiniLM-L6-v2

4. Store Embeddings in ChromaDB (Local)

Creates a persistent vector store in chroma_db/.

5. Retrieve Relevant Chunks

Based on semantic similarity (top-k = 4 by default).

6. Generate Answer via Ollama (Mistral 7B)

Injects retrieved context + question into the LLM to produce a final answer.

📘 Google Colab Support

This repository includes a Google Colab notebook that:
✔ Installs Ollama inside Colab
✔ Downloads Mistral 7B
✔ Runs the entire pipeline end-to-end
✔ Allows uploading speech.txt
✔ Provides an interactive Q&A interface

This makes the system runnable on machines that cannot install Ollama locally.

🛠 Tech Stack
Component	Tool / Framework
Programming Lang	Python 3.8+
RAG Orchestration	LangChain
Vector Database	ChromaDB
Embeddings	all-MiniLM-L6-v2 (HuggingFace)
Local LLM	Ollama (Mistral 7B)
Notebook Environment	Google Colab
📦 Installation (Local Machine)
1️⃣ Install Ollama

Download and install Ollama from:

https://ollama.com

Then pull the Mistral model:

ollama pull mistral

2️⃣ Install Python Dependencies
pip install langchain chromadb sentence-transformers transformers torch

3️⃣ Place your document

Add your speech.txt file in the project folder.

4️⃣ Run the RAG script
python rag_local.py

▶ Usage Example

Once the system loads, simply enter:

Enter your question: What is the main theme of the speech?


The system will:

Retrieve the most relevant chunks

Feed them + your question into the LLM

Display the final answer

📂 Repository Structure
├── rag_local.py            # Main RAG pipeline script
├── RAG_Ollama_Colab.ipynb  # Colab notebook version
├── speech.txt              # Input text file
├── chroma_db/              # Persisted Chroma vector store
└── README.md               # Project documentation

🔍 How It Works (Architectural Diagram)
speech.txt
     ↓
[Text Splitter]
     ↓
[Embeddings: MiniLM-L6-v2]
     ↓
[ChromaDB Vector Store] ←→ [Retriever]
     ↓                         ↑
[Context + Question] → [LLM: Mistral 7B (Ollama)]
     ↓
Final Answer

📝 Notes

No API keys or cloud accounts are required.

Everything runs fully offline (after Ollama + embeddings model download).

ChromaDB is persistent — embeddings are saved and reused.

Works in Google Colab, Linux, Mac, and WSL.

📄 License

This project is open-source and free to use under the MIT License.

🤝 Contributing

Pull requests and feature suggestions are welcome!
Some potential enhancements:

Add FAISS backend option

Add LangGraph workflow

Add Gradio UI

Add multi-file ingestion
