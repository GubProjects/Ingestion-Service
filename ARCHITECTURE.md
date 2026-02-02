# Architecture

**Governed RAG Ingestion & Retrieval Control Plane**

This document describes the high-level system architecture of the Ingestion Service. It explains control boundaries, data flow, and governance layers without exposing internal implementation details.

> The system is designed around one principle: **Knowledge must be treated as a regulated production asset, not an ad-hoc data pipeline.**

## 1. System Overview

The platform is structured into three logical planes:

```
┌─────────────────────────────┐
│        Operator UI          │
│ (Ingestion, releases, audit)│
└──────────────┬──────────────┘
               │
┌──────────────▼──────────────┐
│  Control & Governance       │
│  (Release Orchestrator)     │
└──────────────┬──────────────┘
               │
┌──────────────▼──────────────┐
│   Artifact & Evidence       │
│ (Storage, vector indexes)   │
└─────────────────────────────┘
```

**All content and queries pass through the control plane before reaching any storage or retrieval engine.**

## 2. Major Subsystems

### 2.1 Operator UI

- Manages domains, releases, gates, quarantines
- Views audit trails and evidence packs
- Configures policies and backends

**No ingestion logic runs in the UI.**

### 2.2 Control & Governance Plane

The control plane is the source of truth.

**Responsibilities:**

- Orchestrate release lifecycle
- Enforce policy gates
- Mediate ingestion stages
- Enforce RBAC & domain isolation
- Produce audit & observability events

**Key logical components:**

| Component | Responsibility |
|-----------|-----------------|
| Release Orchestrator | Manages lifecycle & promotion |
| Policy Engine | Enforces gates and rules |
| Domain Registry | Domain isolation & config |
| Pipeline Router | Selects stage implementations |
| Audit & Evidence Manager | Traceability & reporting |
| Retrieval Gateway | Policy-enforced search |

**This layer executes no embeddings or chunking itself.**

### 2.3 Artifact & Evidence Plane

Stores all immutable outputs and lineage:

| Store | Purpose |
|-------|---------|
| Artifact Store | Raw, normalized, chunked content |
| Vector Index | Search & similarity |
| Evidence Store | Audit trails, lineage |
| Telemetry Store | Metrics & run history |

**All writes are append-only.**

## 3. Ingestion Flow

```
Source → Capture
        ↓
      Distill
        ↓
  Canonicalize
        ↓
      Chunk
        ↓
      Embed
        ↓
      Index
        ↓
  Validate (Gates)
        ↓
  Promote / Rollback
```

Each stage produces an immutable artifact linked to a release and domain.

## 4. Release Lifecycle

```
Draft → Validating → Quarantined → Approved → Active → Retired
```

Releases can be:

- Promoted
- Locked
- Rolled back
- Merged

**Every transition is audited.**

## 5. Governance Gates

| Gate | Purpose |
|------|---------|
| Quarantine Gate | Isolate risky content |
| Health Gate | Validate pipeline quality |
| Golden Queries | Validate retrieval |
| PII Gate | Block sensitive data |

**No release reaches production without passing all required gates.**

## 6. Domain Isolation

Each domain is a governed namespace with:

- Separate vector indexes
- Policies
- RBAC scopes
- Connectors
- Releases

This prevents cross-domain data leakage.

## 7. Retrieval Flow

```
User → Retrieval Gateway
        ↓
   Policy Validation
        ↓
   Vector Search
        ↓
   Artifact Mapping
        ↓
   Audit & Evidence
```

**Every query is traceable to its source artifacts.**

## 8. Security Model

| Boundary | Enforcement |
|----------|-------------|
| UI → Control | OIDC, RBAC |
| Control → Pipeline | Policy & domain validation |
| Pipeline → Storage | Artifact immutability |
| Query → Retrieval | Domain + release enforcement |

## 9. Extensibility Model

All stages are pluggable:

- Connectors
- Distillers
- Chunkers
- Embeddings
- Vector stores
- Gates

Registered via configuration, not code changes.

## 10. Design Goals

- Governance by default
- Deterministic state transitions
- Audit-first design
- Domain isolation
- Vendor neutrality

This architecture treats knowledge as a regulated system, not a pipeline.

---

**For operational details**, see the README  
**For pipeline configuration**, refer to the configuration guide  
**For questions**, open an issue or discussion
