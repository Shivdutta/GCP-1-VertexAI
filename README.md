# GCP MultiModal RAG using Vertex AI, AstraDB (Cassandra) & LangChain - Masked Data

This project implements a **Multimodal Retrieval-Augmented Generation (RAG)** pipeline using:
- **Google Cloud Vertex AI** for LLM and Vision model inference
- **AstraDB (based on Apache Cassandra)** as the vector database
- **LangChain** for workflow orchestration
- **Data masking and sanitization** techniques for handling sensitive input (text and image)

---

## 📁 Project Structure

- `GCP_MultiModal_RAG_using_Vertex_AI_AstraDB(Cassandra)_and_Langchain_Maskdata.ipynb`: Main notebook demonstrating the full pipeline
- `.env`: (You will create this) Secure environment variable definitions
- `requirements.txt`: Python dependency list
- `utils/`: (Optional) Place to store custom Python modules or helper scripts

---

## 🔧 Detailed Installation Steps

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/multimodal-rag-gcp-astra-langchain.git
cd multimodal-rag-gcp-astra-langchain
```

---

### 2. Set Up a Virtual Environment

#### Using `venv` (Recommended for simplicity)

```bash
python3 -m venv venv
source venv/bin/activate    # On Windows: venv\Scripts\activate
```

#### Or using `conda`

```bash
conda create -n multimodal-rag python=3.10
conda activate multimodal-rag
```

---

### 3. Install Required Python Packages

#### Option A: Using `requirements.txt` (if provided)

```bash
pip install -r requirements.txt
```

#### Option B: Manual installation

```bash
pip install \
    langchain \
    google-cloud-aiplatform \
    cassio \
    cassandra-driver \
    openai \
    python-dotenv \
    pandas \
    pillow \
    torchvision
```

---

### 4. Set Up Google Cloud Authentication

#### Step 1: Install the gcloud CLI

Follow instructions from [Google Cloud SDK Installation](https://cloud.google.com/sdk/docs/install)

#### Step 2: Authenticate your CLI

```bash
gcloud auth application-default login
```

This will allow Vertex AI access from the local environment.

#### Step 3: Set environment variable

Create a service account in Google Cloud IAM with **Vertex AI User** and **Storage Object Viewer** roles. Then download the service account key file (JSON) and place it in your project directory.

In your terminal or `.env` file, set:

```env
GOOGLE_APPLICATION_CREDENTIALS=path/to/your-service-account.json
```

---

### 5. Set Up AstraDB (Cassandra) Connection

#### Step 1: Create an AstraDB Database
- Sign up or log in at [https://www.datastax.com/astra](https://www.datastax.com/astra)
- Create a new vector-enabled database
- Generate an **Application Token** with **Database Administrator** permissions

#### Step 2: Add the following to your `.env` file:

```env
ASTRA_DB_ID=your_db_id
ASTRA_DB_REGION=your_db_region
ASTRA_DB_APPLICATION_TOKEN=your_app_token
```

Example:

```env
ASTRA_DB_ID=8ac65929-xxxx-xxxx-xxxx-d917fcb6f46e
ASTRA_DB_REGION=us-east1
ASTRA_DB_APPLICATION_TOKEN=AstraCS:xxxxxxxx
```

---

### 6. Set Vertex AI Environment Variables

In the same `.env` file, add:

```env
VERTEX_PROJECT_ID=your_gcp_project_id
VERTEX_LOCATION=your_preferred_region  # e.g. us-central1
```

---

### 7. Load Environment Variables

In your notebook or script, load variables with:

```python
from dotenv import load_dotenv
load_dotenv()
```

---

### 8. Run the Jupyter Notebook

Ensure your virtual environment is activated, then launch Jupyter:

```bash
jupyter notebook
```

Open the file:
```
GCP_MultiModal_RAG_using_Vertex_AI_AstraDB(Cassandra)_and_Langchain_Maskdata.ipynb
```

---

## ✅ Notes

- Ensure the AstraDB vector search index is properly initialized before running RAG queries.
- Make sure the models you're using (e.g., text-bison, vision models) are **enabled** in Vertex AI.
- The pipeline supports multimodal input: you may input text and optionally an image.
- The notebook includes logic to **mask sensitive fields** like names, emails, or PII before invoking the model.

---

## 🧪 Optional Enhancements

- Add Streamlit or Gradio interface for live testing
- Deploy as a FastAPI service on GCP Cloud Run
- Enable data logging for compliance audits
