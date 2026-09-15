# The Docket

> A full-stack Legal RAG Assistant for querying uploaded legal documents using semantic search, keyword retrieval, neural reranking, and LLM-powered generation.

[![React](https://img.shields.io/badge/Frontend-React-61DAFB?logo=react&logoColor=black)](https://react.dev/)
[![FastAPI](https://img.shields.io/badge/Backend-FastAPI-009688?logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![Python](https://img.shields.io/badge/Python-3.14-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![MongoDB](https://img.shields.io/badge/Database-MongoDB-47A248?logo=mongodb&logoColor=white)](https://www.mongodb.com/)
[![Supabase](https://img.shields.io/badge/Storage-Supabase-3ECF8E?logo=supabase&logoColor=white)](https://supabase.com/)
[![Vercel](https://img.shields.io/badge/Frontend%20Hosting-Vercel-000000?logo=vercel&logoColor=white)](https://vercel.com/)

🌐 Live Demo: https://legal-rag-assistant-ten.vercel.app/

---

## Overview

Full-stack Legal RAG (Retrieval-Augmented Generation) application designed to let users interact with their own legal documents.

Users can upload a PDF, create conversations around it, and ask questions about its contents. Instead of sending the entire document to an LLM, The Docket retrieves the most relevant sections from the uploaded document and provides them as context for answer generation.

The application combines:

- Semantic retrieval
- Keyword retrieval
- Neural reranking
- LLM generation
- Persistent document storage
- Persistent RAG indexes
- User authentication
- Conversation management

The goal is to provide answers that remain grounded in the uploaded legal document rather than relying solely on the model's general knowledge.

---

## Features

### Authentication

- User registration
- User login
- JWT-based authentication
- Password hashing with bcrypt
- Protected API endpoints
- User-specific conversations and documents

### Conversations

- Create conversations
- Rename conversations
- Select conversations
- Delete conversations
- Persistent chat history
- Copy generated answers

### Document Management

- Upload PDF legal documents
- One document per conversation
- Replace uploaded documents
- Remove documents
- Private document storage
- Automatic document cleanup

### RAG Pipeline

- PDF text extraction
- Document chunking
- Semantic embeddings
- FAISS vector search
- BM25 keyword search
- Hybrid retrieval
- Neural reranking
- Context-aware answer generation
- Article and section detection

### Persistence

RAG artifacts are persisted in Supabase Storage so that the application does not depend on the backend's local filesystem.

Stored artifacts include:

- FAISS index
- Document metadata
- Tokenized documents
- BM25 index

This allows previously processed documents to be restored after backend restarts.

---

# Architecture

```text
                         ┌──────────────────────┐
                         │        Vercel        │
                         │                      │
                         │    React + Vite      │
                         │     Frontend         │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │    FastAPI Cloud     │
                         │                      │
                         │ Authentication       │
                         │ Conversations        │
                         │ Document handling     │
                         │ RAG retrieval         │
                         │ Reranking             │
                         │ LLM generation        │
                         └───────┬───────┬──────┘
                                 │       │
                    ┌────────────┘       └────────────┐
                    ▼                                 ▼
          ┌──────────────────┐              ┌──────────────────┐
          │   MongoDB Atlas  │              │     Supabase     │
          │                  │              │                  │
          │ Users            │              │ Uploaded PDFs    │
          │ Conversations    │              │ FAISS indexes    │
          │ Messages         │              │ Metadata         │
          │ Documents        │              │ BM25 indexes     │
          └──────────────────┘              └──────────────────┘
