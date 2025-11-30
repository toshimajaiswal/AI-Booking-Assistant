#  AI-Powered Meeting Room Booking Assistant  
### Built with FastAPI • Streamlit • RAG • FAISS • SentenceTransformers • Groq LLM (`openai/gpt-oss-20b`)

This project is an **AI-driven corporate meeting room booking assistant** that enables users to interact using natural language, book meeting rooms, check availability, and retrieve information from uploaded documents using a **RAG pipeline** (Retrieval-Augmented Generation).

It combines:
- A friendly **chat-based interface**
- A powerful backend using **FastAPI**
- **RAG** (PDF → Chunk → Embedding → FAISS)
- **Groq LLM** for fast, low-latency generation
- **Slot-filling booking engine**
- **SQLite database** for storing customers & bookings
- **SMTP email notifications**
- **Streamlit admin dashboard**

---

##  Features

###  1. Chat-based AI Assistant (Streamlit UI)
- Natural conversation with the AI assistant  
- Handles general queries and booking-related tasks  
- Maintains conversation memory  
- Clean, friendly chat interface  

###  2. FastAPI Backend
- Handles chat, uploads, bookings, vector store ops  
- Validates payloads (Pydantic)  
- Provides REST endpoints for all major actions  

###  3. RAG Pipeline (Retrieval-Augmented Generation)
- **PDF Upload → Text extraction (PyPDF2) → Chunking → Embeddings → FAISS**  
- Embedding model: **SentenceTransformers — `all-MiniLM-L6-v2`**  
- Vector DB: **FAISS (IndexFlatIP)** for similarity search  
- Query embeddings + top-k chunk retrieval  

###  4. LLM Generation (Groq)
Uses **Groq API** with model:  
`openai/gpt-oss-20b`  
Fast, low-latency, and optimized for production.

###  5. Slot-Filling Multi-Turn Booking Flow
Collects these booking fields:
- Name  
- Email  
- Phone  
- Room type  
- Date  
- Time  
- Duration  

Validates → Summarizes → Confirms → Saves → Emails user  

###  6. SQLite Database + SQLAlchemy ORM
Tables:
- `customers`  
- `bookings`  
- `chunks` (for RAG metadata)

###  7. Email Notification (SMTP)
- Sends booking confirmation emails  
- Gracefully handles failures  
- Uses Gmail / App Password  

###  8. Admin Dashboard (Streamlit)
- View all bookings  
- Filter/search by name/email/date  
- View occupancy  
- Reset / rebuild vector database  
- Inspect chunk & embedding stats  

---

##  Architecture Overview

User → Streamlit UI → FastAPI Backend
→ (RAG Pipeline: PDF → PyPDF2 → Chunk → Embedding → FAISS)
→ Groq LLM (openai/gpt-oss-20b)
→ Booking Engine → SQLite → SMTP Email → Streamlit Output


**Frontend:** Streamlit  
**Backend:** FastAPI + Uvicorn  
**LLM:** Groq (openai/gpt-oss-20b)  
**Embeddings:** SentenceTransformers  
**Vector DB:** FAISS  
**DB:** SQLite  
**Email:** SMTP  

---

## 🗂️ Project Structure
backend/
- app/
  - main.py
  - schemas.py
- routers/
  - chat.py
  - upload.py
  - bookings.py
services/
  - llm_client.py
  - rag_pipeline.py
  - booking_manager.py
  - email_service.py
db/
  - database.py
  - models.py
  - requirements.txt

frontend/
  - streamlit_app.py
  - ui.py

 .env (not committed)
 README.md


---

## ⚙️ Installation & Setup

### 1️. Clone the Repository
```bash
git clone https://github.com/toshimajaiswal/AI-Booking-Assistant

```

2️. Create Virtual Environment
```bash
python3 -m venv myenv
source myenv/bin/activate
```

3️. Install Backend Requirements
```bash
pip install -r backend/requirements.txt
```

4️. Add Environment Variables

Create a .env file:
```
# Groq API
GROQ_API_KEY=your_api_key_here
GROQ_MODEL="openai/gpt-oss-20b"

# Embeddings
EMBEDDING_MODEL_NAME=all-MiniLM-L6-v2

# FAISS paths
FAISS_INDEX_PATH=rag_faiss.index
FAISS_MAPPING_PATH=rag_faiss_mapping.pkl

# SQLite
SQLITE_PATH=bookings.db

# Email
SMTP_EMAIL=your_email@gmail.com
SMTP_PASS=your_app_password
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587

# Uploads
UPLOADS_DIR=backend/uploads
```
 Running the Application
Start Backend (FastAPI)
```
uvicorn app.main:app --reload --port 8000
```

Start Frontend (Streamlit)
```
streamlit run frontend/streamlit_app.py
```
Now visit:

http://localhost:8501


RAG Flow (Summary)

- User uploads PDF

- PyPDF2 → Extract text

- Chunking

- Embedding → SentenceTransformers

- Store vectors → FAISS

- Query embedding → FAISS search

- Retrieve relevant chunks

- Build prompt

- Generate answer via Groq LLM
