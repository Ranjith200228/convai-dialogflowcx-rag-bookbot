# 🧠 ConvAI — Production-Grade RAG Chatbot on Google Cloud (Dialogflow CX)

> A cloud-native, retrieval-augmented conversational AI system built on **Google Cloud Platform** using **Dialogflow CX**, **Vertex AI Search (Data Store)**, and **Cloud Storage** to deliver grounded, citation-backed responses via **web chat and voice calling**.

---

## 🚀 Project Overview

ConvAI is an enterprise-style conversational AI platform designed to demonstrate **production-grade architecture**, **LLM grounding**, and **multi-channel deployment**.

The system allows users to ask complex questions about a book corpus while ensuring responses remain:

✅ Factually grounded  
✅ Citation-backed  
✅ Low hallucination  
✅ Scalable  
✅ Cloud secure  

This project reflects how modern organizations deploy **Retrieval-Augmented Generation (RAG)** systems in real-world environments.

---

## 🚀 Features

- **Dialogflow CX Integration**: Utilizes Dialogflow CX for advanced conversational capabilities.
- **Retrieval-Augmented Generation**: Fetches relevant information from the book stored in GCS.
- **Citation Support**: Provides sources for the information presented.
- **Multi-Modal Interaction**: Accessible via web chat and phone calls.
- **Web Interface**: Embedded Dialogflow Messenger for seamless web interactions.

---

## 🏗️ High-Level Architecture

```mermaid
flowchart LR

%% ---------------- USERS ----------------
subgraph Users
U1[User — Web Chat]
U2[User — Phone Call]
end

%% ---------------- CHANNELS ----------------
subgraph Channels
WEB[Dialogflow Messenger]
PHONE[Phone Gateway]
end

U1 --> WEB
U2 --> PHONE

%% ---------------- CX ----------------
subgraph Orchestration["Conversation Orchestration — Dialogflow CX"]
CX[Dialogflow CX Agent  
• Intents  
• Flows  
• Generative Fallback  
• Safety Policies]
end

WEB --> CX
PHONE --> CX

%% ---------------- RAG ----------------
subgraph Retrieval["Retrieval Layer — Vertex AI Search / Data Store"]
RETRIEVER[Semantic Retriever]
RANK[Top-K Ranking Engine]
end

CX --> RETRIEVER
RETRIEVER --> RANK

%% ---------------- KNOWLEDGE ----------------
subgraph Knowledge["Knowledge Base"]
GCS[(Google Cloud Storage  
Book PDF Corpus)]
PIPE[Ingestion Pipeline  
Parse → Chunk → Index]
end

GCS --> PIPE --> RETRIEVER

%% ---------------- RESPONSE ----------------
subgraph Response["Grounded Response Generation"]
GEN[Answer Synthesis]
CITE[Citation Cards]
