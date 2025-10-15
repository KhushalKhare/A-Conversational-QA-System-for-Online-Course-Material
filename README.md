

## 📖 Description

This project is a Retrieval-Augmented Generation (RAG) system built with LangChain and Hugging Face. It ingests content from a specified webpage, embeds the information into a vector database (ChromaDB), and allows a user to ask questions about that content. The system uses a `google/flan-t5-base` model to generate answers based on the retrieved context.

This was developed as part of a university master's project to demonstrate a practical end-to-end RAG pipeline.

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

You need a Hugging Face API key to download and use the models.

Create a file named `.env` in the root of your project directory and add your key:

```
HUGGING_FACE_API_KEY="hf_YourHuggingFaceApiKeyHere"
```

*Your notebook code will need a slight modification to use this `.env` file instead of `google.colab.userdata`.*

**Replace this code:**
```python
# from google.colab import userdata
# import os
# os.environ['HUGGING_FACE_API_KEY'] = userdata.get('huggingface')
```
**With this:**
```python
import os
from dotenv import load_dotenv

load_dotenv() # Loads variables from .env file

# The API key is now loaded into the environment automatically
# You can optionally check it with:
# api_key = os.getenv("HUGGING_FACE_API_KEY")
# print("API Key Loaded.")
```

---

## ▶️ How to Run

The primary logic is contained within the Jupyter Notebook (`Untitled84 (1).ipynb`).

1.  Ensure your virtual environment is activated and dependencies are installed.
2.  Launch Jupyter Notebook or JupyterLab:
    ```bash
    jupyter notebook
    ```
3.  Open the notebook file and run the cells sequentially from top to bottom. The script will:
    * Load data from the URL.
    * Create and persist the ChromaDB vector store in a local folder (`./chroma_db_web`).
    * Initialize the QA chain.
    * Run example queries and print the results.

---

## 📝 Example Usage

After running the notebook, you can modify the query in the final cells to ask your own questions about the source content.

**Example Query:**

```python
query = "What projects are covered in the course?"
result = qa_chain.invoke({"query": query})
print(result["result"])

```

**Expected Output:**

The model will provide a summary of the projects mentioned on the webpage, such as building a neural network with TensorFlow, an end-to-end chatbot with Streamlit, and an app for image generation.
