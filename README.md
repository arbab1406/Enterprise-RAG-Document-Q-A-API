# Enterprise-RAG-Document-Q-A-API
🚀 Production-ready Enterprise RAG (Retrieval-Augmented Generation) Document Q&amp;A API built with ASP.NET Core. Features Clean Architecture, CQRS (MediatR), Semantic Kernel, and Hybrid Vector Search via PostgreSQL (pgvector).


# Enterprise RAG Document Q&A API

An enterprise-grade, production-ready **Retrieval-Augmented Generation (RAG)** Document Q&A API built on the **.NET 9/8** ecosystem. This system enables organization-wide secure document ingestion (PDF, Markdown) and provides context-aware, verifiable answers grounded strictly in uploaded company documentation with exact citation tracking.

This project serves as a showcase of modern backend architecture, cloud-native AI orchestration, and advanced database indexing strategies required for enterprise generative AI applications.

## 🏗️ Architecture & Technical Stack

The system is engineered from the ground up using **Clean Architecture** principles and the **CQRS (Command Query Responsibility Segregation)** pattern to ensure strict separation of concerns, high testability, and decoupled maintainability.

*   **API Layer:** ASP.NET Core Web API, featuring Minimal APIs, structured logging (Serilog), and OpenAPI/Swagger documentation.
*   **Application Layer:** Core business logic orchestrated via **MediatR** for CQRS, utilizing FluentValidation for request pipe verification.
*   **AI Orchestration:** **Semantic Kernel** (and `Microsoft.Extensions.AI`) managing text chunking strategies, token counting, semantic memory, and Azure OpenAI / local Ollama LLM integration.
*   **Data & Vector Storage:** **Entity Framework Core (EF Core)** paired with **PostgreSQL (pgvector)** to seamlessly store relational metadata and high-dimensional vector embeddings.

## 🌟 Key Engineering Feature: Hybrid Search Engine

To significantly surpass standard vector retrieval limitations, this API implements a high-accuracy **Hybrid Search** pipeline. 

Instead of relying solely on semantic distance, the system executes two concurrent operations upon receiving a user query:
1.  **Vector Search:** Utilizes `pgvector` (Cosine Similarity) to capture semantic meaning and deep contextual intent.
2.  **Full-Text Search:** Utilizes PostgreSQL's native `tsvector` and `tsquery` to match exact keywords, proper nouns, and technical product codes.

**The Reciprocal Rank Fusion (RRF)** algorithm is then applied to merge, re-rank, and normalize these distinct result sets. This ensures the Large Language Model (LLM) receives the most precise, context-dense, and noise-free documentation snippets possible, minimizing hallucinations and optimizing token usage.

## ⚡ Key Technical Highlights Included
*   **Smart Document Chunking:** Overlapping sliding-window chunking to maintain context across paragraph boundaries.
*   **Deterministic Citations:** Every response maps the exact database text chunk ID and source document URI back to the user interface.
*   **Resiliency & Transient Faults:** Implemented Polly policies for OpenAI API rate-limiting retry back-offs and circuit breakers.
*   **Dockerized Infrastructure:** Full `docker-compose` setup for local development including PostgreSQL with `pgvector` pre-configured.
