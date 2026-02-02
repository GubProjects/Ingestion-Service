# Ingestion Service

**Governed RAG Ingestion & Retrieval Control Plane**

Knowledge is not a script. It is a production system.

This project is a modular ingestion and governance control plane for building auditable, versioned knowledge bases for RAG systems.

Unlike typical RAG pipelines that hard-wire a chunker, embedding model, and vector store into a single script, this platform treats knowledge ingestion as software delivery:

- Content moves through a release lifecycle
- Every stage is policy-driven and swappable
- Quality, safety, and compliance are enforced by gates
- All actions are observable and auditable

> **This is an enterprise control plane, not a demo pipeline.**

## 🎯 What Is This?

A governed ingestion system that transforms raw content into production-ready knowledge.

### Sources

- URLs
- File uploads
- Enterprise connectors

### Pipeline

```
Capture → Distill → Canonicalize → Chunk → Embed → Index → Validate → Promote
```

Each step:
- Produces immutable artifacts
- Is policy-driven
- Is auditable
- Can be swapped without rewriting the platform

Releases can be promoted, locked, rolled back, merged, and audited — **just like software.**

## 👥 Who This Is For

| Role | Why |
|------|-----|
| Security & Compliance | Audit trails, lineage, governance gates |
| Platform Engineers | Scalable, multi-domain RAG foundations |
| AI / ML Teams | Reliable ingestion with quality checks |
| Enterprises | Treat knowledge as regulated assets |

This is designed for regulated, enterprise environments.

## ✨ Core Capabilities

| Capability | Description |
|-----------|-------------|
| Release Lifecycle | Create → Validate → Promote → Rollback |
| Quarantine | Automatically isolate policy-breaking input |
| Health Gates | Validate ingestion & retrieval quality |
| Golden Queries | Test retrieval before promotion |
| Domain Isolation | Namespaces with policies, RBAC, connectors |
| Evidence Packs | Audit trails, lineage, decision logs |
| Pluggable Backends | Swap chunkers, embeddings, vector stores |
| Observability | Run telemetry, history, event logs |
| Enterprise Auth | OIDC + domain-scoped RBAC |

## 🧱 Core Concepts

### Domains

Governed namespaces (finance, support, security, etc.). Each domain has its own:

- Policies
- Connectors
- RBAC
- Releases
- Vector stores

### Releases

A versioned snapshot of a domain's knowledge base. Releases move through a controlled lifecycle and can be audited or rolled back.

### Artifacts

Each stage produces immutable outputs linked to releases and audit records.

### Gates

Quality & safety checkpoints that must pass before promotion:

- Quarantine Gate
- Health Gate
- Golden Queries
- PII Gate

## ⚖️ What This Is Not

- Not a chatbot
- Not a full RAG application framework
- Not an LLM service
- Not an end-user chat UI

This platform governs ingestion and retrieval. You bring:

- Your LLM
- Your prompts
- Your application UI

## 🏗️ Reference Architecture

```
User → Operator UI
        ↓
   Ingestion API
        ↓
Control & Governance Plane
        ↓
Artifact + Evidence Stores
        ↓
 Vector Index & Retrieval
```

The control plane mediates every state transition and enforces policy.

## 🔌 Modular Pipeline

```
[Connector] → Distill → Canonicalize → Chunk → Embed → Vector Store
```

Each layer is replaceable via configuration and policy.

**Supported patterns:**
- Local models
- Cloud APIs
- Enterprise search backends

## 🔐 Governance & Security

- OIDC SSO
- Domain-scoped RBAC
- Full audit trails
- Artifact lineage
- Evidence packs for compliance
- Policy-driven gates

## 📊 Observability

Every ingestion and retrieval event is traceable:

```
Query → Vectors → Chunks → Documents → Sources → Release
```

Evidence can be exported for audits and investigations.

## 🚀 Deployment

This system supports:

- Local development
- Containerized deployments
- Enterprise environments

Installation, configuration, and operational support are available through commercial licensing.

## 💡 Philosophy

> Ingestion is not a script. It is a control plane.

This platform exists to turn RAG pipelines into governed production systems — auditable, safe, and scalable.

---

**For architecture details**, see [ARCHITECTURE.md](./ARCHITECTURE.md)  
**For deployment options**, contact sales or open an issue  
**For technical questions**, open a discussion
