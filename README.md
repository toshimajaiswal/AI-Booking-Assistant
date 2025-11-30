# 🤖 AI-Powered Meeting Room Booking Assistant  
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

## 🚀 Features

### 🔹 1. Chat-based AI Assistant (Streamlit UI)
- Natural conversation with the AI assistant  
- Handles general queries and booking-related tasks  
- Maintains conversation memory  
- Clean, friendly chat interface  

### 🔹 2. FastAPI Backend
- Handles chat, uploads, bookings, vector store ops  
- Validates payloads (Pydantic)  
- Provides REST endpoints for all major actions  

### 🔹 3. RAG Pipeline (Retrieval-Augmented Generation)
- **PDF Upload → Text extraction (PyPDF2) → Chunking → Embeddings → FAISS**  
- Embedding model: **SentenceTransformers — `all-MiniLM-L6-v2`**  
- Vector DB: **FAISS (IndexFlatIP)** for similarity search  
- Query embeddings + top-k chunk retrieval  

### 🔹 4. LLM Generation (Groq)
Uses **Groq API** with model:  
`openai/gpt-oss-20b`  
Fast, low-latency, and optimized for production.

### 🔹 5. Slot-Filling Multi-Turn Booking Flow
Collects these booking fields:
- Name  
- Email  
- Phone  
- Room type  
- Date  
- Time  
- Duration  

Validates → Summarizes → Confirms → Saves → Emails user  

### 🔹 6. SQLite Database + SQLAlchemy ORM
Tables:
- `customers`  
- `bookings`  
- `chunks` (for RAG metadata)

### 🔹 7. Email Notification (SMTP)
- Sends booking confirmation emails  
- Gracefully handles failures  
- Uses Gmail / App Password  

### 🔹 8. Admin Dashboard (Streamlit)
- View all bookings  
- Filter/search by name/email/date  
- View occupancy  
- Reset / rebuild vector database  
- Inspect chunk & embedding stats  

---

## 🏛️ Architecture Overview

