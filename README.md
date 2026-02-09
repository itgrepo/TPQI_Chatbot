# ⚖️ E-Workforce Ecosystem (EWE) Intelligent Career & Labor Advisor

An AI-powered chatbot designed to provide accurate guidance on **Thai Labor Laws** and **Professional Qualifications (TPQI)**. This project leverages **RAG (Retrieval-Augmented Generation)** technology to ensure reliable, citation-backed answers.

## 🚀 Key Features
- **Semantic Search:** Utilizes Vector Search via Google Firestore to understand query context.
- **RAG Architecture:** Retrieves relevant legal/professional documents before generating answers to minimize hallucinations.
- **Hybrid Deployment:** Frontend hosted on **Hostinger** (via Git), Backend powered by **Firebase Cloud Functions** (Python).

## 🛠 Tech Stack
- **Frontend:** Python (Streamlit)
- **Backend:** Python, Firebase Cloud Functions
- **AI/LLM:** OpenAI GPT-4o, LangChain
- **Database:** Firestore (Vector Store)

## 🏗 Architecture
[Frontend @Hostinger] <--> [API Gateway] <--> [Firebase Cloud Functions] <--> [Firestore Vector DB] <--> [OpenAI]
