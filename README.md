# RAG-based QA Chatbot for Web Content

## 📖 Description

This project is a Retrieval-Augmented Generation (RAG) system built with LangChain and Hugging Face. It ingests content from a specified webpage, embeds the information into a vector database (ChromaDB), and allows a user to ask questions about that content. The system uses a `google/flan-t5-base` model to generate answers based on the retrieved context.

This was developed as part of a university master's project to demonstrate a practical end-to-end RAG pipeline.

---

## 🏛️ Architecture and Workflow

This project follows a standard Retrieval-Augmented Generation (RAG) architecture, divided into two main phases: an offline **Indexing Phase** and a real-time **Retrieval & Generation Phase**.

![Project Architecture Diagram](https://github.com/KhushalKhare/A-Conversational-QA-System-for-Online-Course-Material/blob/main/RAG%20ARCHITECTURE%20DIAGRAM.png)

### Phase 1: Indexing (Offline)
This is a one-time, preparatory process to build the system's knowledge base.
1.  **Load Content**: The system ingests the raw text from the source webpage.
2.  **Chunk Text**: The text is split into smaller, manageable chunks to ensure effective embedding.
3.  **Embed Chunks**: Each text chunk is converted into a numerical vector (embedding) using the `all-MiniLM-L6-v2` model. This vector captures the semantic meaning of the text.
4.  **Store Vectors**: The embeddings and their corresponding text chunks are stored in a ChromaDB vector store, which indexes them for fast and efficient searching.

### Phase 2: Retrieval & Generation (Real-time)
This phase is executed every time a user asks a question.
1.  **Embed Query**: The user's question is converted into a vector using the same embedding model.
2.  **Similarity Search**: The system searches the ChromaDB store to find the text chunks with vectors most similar to the user's query vector. These chunks are the most relevant pieces of context.
3.  **Augment Prompt**: The retrieved context is combined with the original query to create a detailed prompt for the Language Model.
4.  **Generate Answer**: This augmented prompt is sent to the `google/flan-t5-base` LLM, which generates a final answer grounded in the provided context.

---

## ✨ Features

* **Web Content Ingestion**: Dynamically loads and parses text content from a live URL.
* **Text Chunking**: Splits the document into smaller, manageable chunks for effective embedding.
* **Vector Embeddings**: Uses the `sentence-transformers/all-MiniLM-L6-v2` model to create vector representations of the text.
* **Vector Storage**: Stores and indexes the embeddings in a persistent local ChromaDB database.
* **Question-Answering**: Utilizes a `RetrievalQA` chain to find relevant documents and generate answers with the `google/flan-t5-base` LLM.

---

## 💻 Technology Stack

* **Core Framework**: LangChain
* **LLM**: `google/flan-t5-base` (via Hugging Face Transformers)
* **Embedding Model**: `sentence-transformers/all-MiniLM-L6-v2`
* **Vector Database**: ChromaDB
* **Language**: Python 3.12

---

## 🚀 Setup and Installation

Follow these steps to set up the project locally.

### 1. Clone the Repository

```bash
git clone [https://github.com/your-username/your-repo-name.git](https://github.com/your-username/your-repo-name.git)
cd your-repo-name
```

### 2. Create a Virtual Environment

It's highly recommended to use a virtual environment to manage project dependencies.

```bash
# For Unix/macOS
python3 -m venv venv
source venv/bin/activate

# For Windows
python -m venv venv
venv\Scripts\activate
```

### 3. Install Dependencies

Install all the required packages from the `requirements.txt` file.

```bash
pip install -r requirements.txt
```

### 4. Set Up Environment Variables

You need a Hugging Face API key to download and use the models. Create a file named `.env` in the root of your project directory and add your key:

```
HUGGING_FACE_API_KEY="hf_YourHuggingFaceApiKeyHere"
```

---

## ▶️ How to Run

The primary logic is contained within the `rag_qa_system.py` script.

1.  Ensure your virtual environment is activated and dependencies are installed.
2.  Run the script from your terminal:
    ```bash
    python rag_qa_system.py
    ```
3.  The script will:
    * Load data from the URL.
    * Create and persist the ChromaDB vector store in a local folder (`./chroma_db_web`).
    * Initialize the QA chain.
    * Run example queries and print the results to the console.

---

## 📝 Example Usage

You can modify the queries within the `rag_qa_system.py` file to ask your own questions about the source content.

**Example Query:**

```python
query = "What projects are covered in the course?"
result = qa_chain.invoke({"query": query})
print(result["result"])
```

**Expected Output:**

The model will provide a summary of the projects mentioned on the webpage, such as building a neural network with TensorFlow, an end-to-end chatbot with Streamlit, and an app for image generation.
