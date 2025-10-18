# 🩺 AI Health Assistant RAG

## 📌 Overview
The **AI Health Assistant RAG** is a Retrieval-Augmented Generation (RAG) system designed to assist patients by answering medical queries based on PDF documents containing health-related information. 

It uses:
- **FAISS** for vector search
- **Mistral 7B v0.1** (Hugging Face) for AI responses
- **AutoGen** for multi-agent collaboration
- **Flask API** for backend communication
- **Streamlit** for a user-friendly UI

## 📁 Project Structure
```
📂 health_assistant_rag
│── 📂 data               # Folder containing medical PDFs
│── 📂 backend            # Backend logic for processing
│   │── data_loader.py    # Extracts text from PDFs
│   │── embed_store.py    # Embeds and stores data in FAISS
│   │── api.py            # Flask API for querying AI
│── 📂 frontend           # Frontend for user interaction
│   │── app.py           # Streamlit UI
│── requirements.txt      # Python dependencies
│── run.sh               # Shell script to run everything
```

---
## 🚀 Setup Instructions
### 1️⃣ Install Dependencies
Run the following command to install all required Python libraries:
```bash
pip install -r requirements.txt
```

### 2️⃣ Prepare Data
Place all **medical PDFs** in the `data/` folder.

### 3️⃣ Process Data & Store Embeddings
```bash
python backend/embed_store.py
```
This extracts text, splits it into chunks, generates embeddings, and stores them in FAISS.

### 4️⃣ Start the Backend (Flask API)
```bash
python backend/api.py
```
This starts an API that retrieves relevant data and queries the AI model.

### 5️⃣ Run the Frontend (Streamlit UI)
```bash
streamlit run frontend/app.py
```
This opens an interactive web UI for users to ask health-related questions.

---
## 🛠️ Components Explanation
### 📌 **1. Data Loading (`backend/data_loader.py`)**
- Extracts text from PDF documents using `PyMuPDF`.
- Reads all PDFs in `data/` and returns the extracted text.

### 📌 **2. Embedding & FAISS Storage (`backend/embed_store.py`)**
- Uses `Hugging Face` sentence-transformers (`all-MiniLM-L6-v2`).
- Splits text into chunks and stores embeddings in **FAISS vector store**.
- Saves metadata (`faiss_metadata.pkl`) for retrieval.

### 📌 **3. API Backend (`backend/api.py`)**
- Loads FAISS embeddings and retrieves relevant chunks.
- Uses **AutoGen multi-agents**:
  - `DoctorAgent`: General medical advice.
  - `SpecialistAgent`: Disease-specific recommendations.
  - `SymptomCheckerAgent`: Symptom analysis.
  - `AdvisorAgent`: Health and lifestyle suggestions.
- Runs a **Flask API** that receives queries and returns AI-generated responses.

### 📌 **4. Frontend (`frontend/app.py`)**
- **Streamlit UI** for user queries.
- Sends requests to the Flask API and displays AI-generated responses.

---
## 🏃‍♂️ Running the Project (One Command)
To start the full system, use:
```bash
bash run.sh
```
This will:
1. Generate FAISS embeddings.
2. Start the Flask API in a new terminal.
3. Launch the Streamlit UI.

---
## 🔥 Example Query
1. Open the **Streamlit UI**.
2. Enter a query like:
   ```
   What are the symptoms of diabetes?
   ```
3. The AI will retrieve relevant medical information and generate a response.

---
## 🛠️ Future Enhancements
✅ Add more specialized medical agents.  
✅ Improve the UI with **Gradio** or a custom web app.  
✅ Deploy on **AWS/GCP** for scalability.  

---
## 📜 License
This project is open-source under the **MIT License**.

---
## 📞 Contact
For any issues, feel free to reach out!

📧 **Email**: your.email@example.com  
🌐 **GitHub**: [your-github](https://github.com/your-profile)  



from logging_config import logger

logger.info("Starting embedding process...")

try:
    # Your embedding and storage logic here
    logger.info("Embeddings successfully stored in FAISS.")
except Exception as e:
    logger.error(f"Error in embedding process: {e}")
