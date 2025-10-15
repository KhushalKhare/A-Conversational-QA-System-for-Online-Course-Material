# A-Conversational-QA-System-for-Online-Course-Material
Add a brief, clear description. For example: "A RAG-based chatbot using LangChain and Flask to answer questions about the Educosys Generative AI course. Developed for a university master's project.

# RAG-Powered Course Advisor

This project is a command-line Retrieval-Augmented Generation (RAG) advisor that answers questions about the Educosys Generative AI course. It is built using LangChain, Hugging Face Transformers, and ChromaDB.

This was developed as a proof-of-concept for a university master's project, demonstrating the practical application of RAG pipelines for specialized question-answering systems.

---

## ## Features

* **Automated Data Ingestion**: Automatically fetches the latest course content from the official website.
* **Advanced RAG Pipeline**: Uses a sentence-transformer model (`all-MiniLM-L6-v2`) for efficient retrieval and a Large Language Model (`google/flan-t5-base`) for answer generation.
* **Interactive Command-Line Interface**: A simple and intuitive chat session that runs directly in your terminal.

---

## ## How It Works

The system follows a classic RAG pipeline to provide accurate, context-aware answers:

1.  **Data Loading & Chunking**: The script begins by scraping the content from the target webpage. This content is then split into smaller, overlapping chunks suitable for processing.
2.  **Embedding & Storage**: Each text chunk is converted into a numerical vector (an embedding) using a sentence-transformer model. These vectors are then stored in an in-memory ChromaDB vector store, creating a searchable knowledge base.
3.  **Retrieval & Generation**: When you ask a question:
    * Your query is also converted into an embedding.
    * The system performs a similarity search in the vector store to find the most relevant text chunks from the original document.
    * These relevant chunks, along with your original question, are fed into the LLM (`flan-t5-base`).
    * The LLM generates a coherent, human-readable answer based on the provided context.



---

## ## Setup and Installation

Follow these steps to set up and run the project on your local machine.

### ### Prerequisites

* Python 3.8 or higher
* Git

### ### Installation Steps

1.  **Clone the repository:**
    Open your terminal and clone the project files.
    ```bash
    git clone [https://github.com/](https://github.com/)<your-username>/rag-powered-course-advisor.git
    cd rag-powered-course-advisor
    ```

2.  **Create and activate a virtual environment:**
    It's highly recommended to use a virtual environment to manage dependencies.
    ```bash
    # For macOS/Linux
    python3 -m venv venv
    source venv/bin/activate

    # For Windows
    python -m venv venv
    .\venv\Scripts\activate
    ```

3.  **Install the required packages:**
    Use pip to install all the necessary libraries from the `requirements.txt` file.
    ```bash
    pip install -r requirements.txt
    ```
    *Note: If you have a CUDA-enabled GPU, ensure PyTorch is installed with the correct CUDA version for significantly better performance.*

---

## ## How to Run

1.  Make sure your virtual environment is activated.

2.  Run the main chat script from the project's root directory:
    ```bash
    python chat.py
    ```

3.  **Wait for initialization.** The first time you run the script, it will download the embedding and language models (several hundred MBs) and set up the RAG pipeline. This may take a few minutes depending on your internet connection.

4.  **Start chatting!** Once you see the welcome message, you can start asking questions directly in the terminal. To end the session, simply type `exit` and press Enter.
