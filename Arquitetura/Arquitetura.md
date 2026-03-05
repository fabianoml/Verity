# Verity — Architecture Overview

## 1. System Overview

The Verity platform is designed to automate credit approval for small and medium enterprises (SMEs) using a hybrid architecture combining classical machine learning and generative AI.

The system processes approximately:

- **10,000 credit applications per day**
- Structured financial data
- Unstructured documents such as emails, contracts, and market news

The goal is to provide **automated credit decisions with explainable justifications** while minimizing financial and operational risk.

---

# 2. Architectural Principles

The architecture was designed based on the following principles:

- Hybrid AI Architecture
- Cost efficiency (FinOps)
- Explainability and auditability
- Security by design
- Scalable cloud-native infrastructure

The platform is built using services from **Google Cloud Platform**.

Key services include:

- BigQuery
- Vertex AI
- Cloud DLP
- Document AI
- Cloud Run
- Vertex AI Vector Search

---

# 3. High-Level Architecture

The solution is divided into four main layers:

## Data Layer

Responsible for storing structured financial data.

Primary components:

- BigQuery
- Feature Store

Stored data includes:

- transaction history
- financial statements
- customer registration data

---

## Document Processing Layer

Handles ingestion and processing of unstructured data.

Main components:

- Document AI for OCR processing
- Data Loss Prevention (DLP) for PII detection
- Embedding generation via Vertex AI

Processed data is stored in a vector database for semantic search.

---

## Risk Decision Engine

The risk scoring engine is based on classical machine learning models.

Primary model:

- **XGBoost**

The model calculates a credit risk score based on structured financial features retrieved from the Feature Store.

Advantages:

- Deterministic results
- High performance for tabular financial data
- Lower computational cost

---

## Context and Justification Engine

Generative AI models are used to interpret contextual information and produce explainable decisions.

The system uses a **Retrieval-Augmented Generation (RAG)** architecture.

Workflow:

1. Retrieve structured features from the Feature Store
2. Retrieve relevant documents from the vector database
3. Construct a grounded prompt
4. Generate explanation using Gemini

This ensures that generated explanations are **fact-based and auditable**.

---

# 4. Agent-to-Agent Orchestration

The platform uses an agent-based architecture with two main agents:

### Risk Agent

Responsible for numerical risk scoring.

Functions:

- feature retrieval
- credit scoring
- decision threshold evaluation

### Context Agent

Responsible for textual interpretation.

Functions:

- semantic document retrieval
- contextual analysis
- explanation generation

Both agents collaborate to produce the final decision.

---

# 5. Security and Privacy

The system processes sensitive financial and personal information.

Security measures include:

- PII detection using Cloud DLP
- tokenization and redaction of sensitive data
- strict IAM access control
- VPC Service Controls to isolate services

These mechanisms ensure compliance with **LGPD and financial regulations**.

---

# 6. FinOps Strategy

To control operational costs, the system uses a tiered AI inference strategy.

Request distribution:

- 70% handled by XGBoost
- 20% handled by Gemini Flash
- 10% handled by Gemini Pro

This architecture significantly reduces the cost of generative AI usage while maintaining high decision accuracy.

---

# 7. Governance and Observability

To ensure traceability and auditability:

- all decisions are logged
- prompts and model outputs are recorded
- feature values used in decisions are stored

Logs are centralized in **BigQuery** for auditing and monitoring.

---

# 8. Scalability

The platform is designed to scale horizontally using managed services:

- serverless inference services
- scalable vector search
- distributed data processing

This architecture supports future growth in credit applications without major structural changes.

---

# 9. Conclusion

The Verity architecture balances performance, explainability, cost efficiency, and security.

By combining classical machine learning with generative AI, the system achieves:

- scalable credit decision automation
- grounded AI explanations
- strong data governance
- efficient operational cost management