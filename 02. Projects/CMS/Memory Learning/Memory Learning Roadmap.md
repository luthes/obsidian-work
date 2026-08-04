# Curriculum: Memory for AI and LLM Systems

**Audience:** Experienced systems/data-platform engineer with production experience in RAG, agents, tools, streaming systems, and distributed data platforms.

**Goal:** Progress from “I understand conversational memory” to being able to evaluate, design, and lead a production memory platform using hybrid stores, retrieval, temporal models, evaluation, and AWS Neptune.

**Recommended pace:** 10–12 weeks at 4–6 hours per week.

---

# How to Follow This Curriculum

Each phase contains four kinds of material:

- **Required reading:** The smallest set that establishes the important concepts.
- **Required viewing:** Talks or courses that make the architecture easier to understand.
- **Optional deep dives:** Material for greater implementation or research depth.
- **Practical work:** A concrete output that proves you understand the phase.

Use this sequence for each phase:

1. Read the phase overview in the roadmap.
2. Complete the required reading in order.
3. Watch the required video.
4. Write short notes using the provided questions.
5. Complete the practical exercise.
6. Check the completion gate.
7. Only then use the optional material.

Do not try to memorize every taxonomy. Focus on being able to explain tradeoffs and apply them to an architecture.

---

# Note-Taking Template

Use this template for every paper, article, or system:

```text
Title:
Type: paper / documentation / video / product architecture
Main problem:
Definition of memory:
Memory representation:
Write policy:
Management policy:
Retrieval policy:
Evaluation:
Strongest idea:
Biggest weakness:
Production implication:
How this relates to Neptune:
Questions:
```

For academic papers, do not get stuck on equations. Read in this order:

1. Abstract
2. Introduction
3. Architecture diagrams
4. Examples
5. Evaluation questions and benchmark setup
6. Results
7. Limitations
8. Methods and equations only where needed

---

# Phase 0 — Industry Landscape

## Goal

Understand what the industry currently means by memory, how the field is organized, and why memory is more than a storage technology.

## Required Reading

### 1. Memory for Autonomous LLM Agents: Mechanisms, Evaluation, and Emerging Frontiers

**Type:** Current survey  
**Why first:** Provides a broad write–manage–read framing and maps the major architecture families.

- Abstract and HTML: https://arxiv.org/abs/2603.07670
- Full paper: https://arxiv.org/pdf/2603.07670

Focus on:

- The write–manage–read lifecycle
- Representation substrates
- Memory control policies
- Evaluation trends
- Open research problems

### 2. Memory in the Age of AI Agents

**Type:** Survey / conceptual framing  
**Why:** Shows how fragmented terminology has become and helps prevent overcommitting to one vendor’s definitions.

- https://arxiv.org/abs/2512.13564

Focus on:

- Competing definitions of memory
- The difference between memory mechanisms and memory capabilities
- Gaps in current evaluation

### 3. LangGraph Memory Overview

**Type:** Official production documentation  
**Why:** Gives a clean practical distinction between thread-scoped state and cross-thread long-term memory.

- Concepts: https://docs.langchain.com/oss/python/concepts/memory
- Persistence: https://docs.langchain.com/oss/python/langgraph/persistence
- Long-term memory: https://docs.langchain.com/oss/python/langchain/long-term-memory

Focus on:

- Checkpointer versus store
- Thread state versus durable memory
- Namespace and scope
- JSON documents as memory records

## Required Viewing

### LLMs as Operating Systems: Agent Memory

**Provider:** DeepLearning.AI / Letta  
**Why:** Accessible introduction to context management and memory hierarchies from the MemGPT authors.

- Course announcement: https://www.youtube.com/watch?v=RQ5HzSAx27I
- Search for the full DeepLearning.AI course titled **LLMs as Operating Systems: Agent Memory**

## Optional Deep Dives

### From Storage to Experience: A Survey on the Evolution of LLM Agent Memory Mechanisms

- https://arxiv.org/abs/2605.06716

Use this to understand the progression:

```text
Storage → Reflection → Experience
```

### Lifelong Learning of Large Language Model Based Agents: A Roadmap

- https://arxiv.org/abs/2501.07278

Use this to connect memory with continual adaptation.

## Practical Work

Create:

- [ ] A one-page glossary
- [ ] A diagram separating context, state, memory, RAG, and knowledge graphs
- [ ] A one-page summary of the write–manage–read lifecycle
- [ ] A list of five areas where industry terminology is inconsistent

## Completion Gate

You can clearly explain why:

- A context window is not a memory platform
- A checkpoint is not necessarily long-term memory
- A vector database is not a complete memory system
- A knowledge graph is not a complete memory system
- Memory requires policies, not just persistence

---

# Phase 1 — Memory Taxonomy

## Goal

Understand working, episodic, semantic, procedural, prospective, user, agent, and organizational memory.

## Required Reading

### 1. Mem0 Memory Types

**Type:** Official product documentation  
**Why:** Provides an accessible mapping from cognitive categories to practical system layers.

- https://docs.mem0.ai/core-concepts/memory-types

Read critically. Treat this as one implementation’s taxonomy, not a universal standard.

### 2. LangChain Long-Term Memory Conceptual Guide

- https://docs.langchain.com/oss/python/langchain/long-term-memory

Focus on:

- Semantic memory
- Episodic memory
- Procedural memory
- In-hot-path versus background writes

### 3. Generative Agents: Interactive Simulacra of Human Behavior

**Type:** Peer-reviewed, UIST 2023  
**Why:** One of the clearest early architectures for observation, memory streams, reflection, retrieval, and planning.

- ACM publication: https://dl.acm.org/doi/10.1145/3586183.3606763
- Free paper: https://arxiv.org/abs/2304.03442
- Code: https://github.com/joonspk-research/generative_agents

Focus on:

- Memory stream
- Importance
- Recency
- Relevance
- Reflection
- Planning
- Ablation results

## Required Viewing

### Generative Agents Talk by Joon Sung Park

- https://www.youtube.com/watch?v=gPeIgjHdB6w

Alternative shorter conceptual overview:

- TED talk: https://www.ted.com/talks/joon_sung_park_a_simulation_of_human_reality_powered_by_ai

## Optional Deep Dives

### Hello Again! LLM-Powered Personalized Agent for Long-Term Dialogue

**Venue:** NAACL 2025

- https://aclanthology.org/2025.naacl-long.272/

Use this to study event summaries and persona extraction as separate modules.

## Practical Work

Take a single production-agent interaction and label:

- [ ] Working state
- [ ] Raw events
- [ ] Episode
- [ ] Semantic facts
- [ ] Potential procedure
- [ ] Future commitment
- [ ] User scope
- [ ] Organization scope
- [ ] Agent scope

## Completion Gate

You can classify a proposed memory record and explain why it is episodic, semantic, procedural, prospective, or merely runtime state.

---

# Phase 2 — Memory Lifecycle

## Goal

Understand memory as an end-to-end lifecycle: capture, extract, admit, store, consolidate, retrieve, use, evaluate, and forget.

## Required Reading

### 1. How Mem0 Works

**Type:** Official architecture documentation  
**Why:** A concrete, production-oriented extraction, deduplication, embedding, and entity-linking pipeline.

- https://docs.mem0.ai/core-concepts/how-it-works

Also review:

- Add: https://docs.mem0.ai/core-concepts/memory-operations/add
- Search: https://docs.mem0.ai/core-concepts/memory-operations/search
- Update: https://docs.mem0.ai/core-concepts/memory-operations/update

Focus on:

- Extraction
- Deduplication
- Additive writes
- Embedding
- Entity linking
- Search
- Update semantics

### 2. Mem0 OSS Migration: New Memory Algorithm

**Why:** This is unusually valuable because it explains how a real memory architecture changed.

- https://docs.mem0.ai/migration/oss-v2-to-v3

Focus on:

- Why extraction changed
- ADD-only extraction
- Hybrid search
- Entity matching
- Latency and evaluation claims

### 3. Memory for Autonomous LLM Agents — Lifecycle Sections

Revisit the lifecycle and management sections:

- https://arxiv.org/abs/2603.07670

## Required Viewing

### Stateful Agents Workshop with Charles Packer

- https://www.youtube.com/watch?v=E0k9Ppq6yXY

Focus on:

- Memory management as context management
- Agent-managed versus application-managed memory
- Persistent agents
- Operational implications

## Optional Deep Dives

### MemOS: An Operating System for Memory-Augmented Generation

- https://arxiv.org/abs/2505.22101

Read for:

- Memory as a first-class managed resource
- Heterogeneous memory types
- Governance and migration abstractions

## Practical Work

Create:

- [ ] A lifecycle state machine
- [ ] A candidate-memory admission policy
- [ ] A correction and supersession policy
- [ ] A background consolidation workflow
- [ ] A deletion workflow

Suggested states:

```text
candidate
active
disputed
quarantined
superseded
stale
archived
deleted
```

## Completion Gate

You can explain every transformation between a raw interaction and a memory influencing a future response.

---

# Phase 3 — Memory Representations

## Goal

Understand the tradeoffs among raw events, summaries, facts, episodes, procedures, vectors, and graphs.

## Required Reading

### 1. MemGPT: Towards LLMs as Operating Systems

**Type:** Research paper  
**Why:** Establishes hierarchical memory and virtual context management.

- https://arxiv.org/abs/2310.08560
- Project page: https://research.memgpt.ai/

Focus on:

- Main context
- External context
- Paging analogy
- Agent-managed memory
- Interrupts and control flow
- Multi-session conversation

### 2. Letta Memory Documentation

**Type:** Official implementation documentation

- Memory overview: https://docs.letta.com/letta-agent/memory
- Memory blocks: https://docs.letta.com/guides/core-concepts/memory/memory-blocks
- Archival memory: https://docs.letta.com/guides/core-concepts/memory/archival-memory
- Shared memory: https://docs.letta.com/guides/core-concepts/memory/shared-memory
- Stateful agents: https://docs.letta.com/guides/core-concepts/stateful-agents

Focus on:

- Always-in-context memory
- Searchable archival memory
- Agent-editable memory
- Shared memory
- Agent identity versus conversation identity

### 3. LangGraph Persistence

- https://docs.langchain.com/oss/python/langgraph/persistence

Compare:

- Checkpoint
- State
- Store
- Memory document
- Thread scope
- Cross-thread scope

## Required Viewing

Rewatch the memory hierarchy section of:

- https://www.youtube.com/watch?v=E0k9Ppq6yXY

## Optional Deep Dives

### MemOS

- https://arxiv.org/abs/2505.22101

Use it to compare plaintext, activation, and parametric memory.

## Practical Work

Represent the same incident as:

- [ ] Raw event stream
- [ ] Conversation summary
- [ ] Atomic facts
- [ ] Episode
- [ ] Knowledge graph
- [ ] Embedding record
- [ ] Learned procedure

Then record what each representation loses.

## Completion Gate

You can choose a representation based on the retrieval and lifecycle requirement rather than convenience.

---

# Phase 4 — Production Memory Architectures

## Goal

Learn the common components of a production memory stack and how they interact.

## Required Reading

### 1. LangGraph Memory and Persistence Documentation

- https://docs.langchain.com/oss/python/langgraph/add-memory
- https://docs.langchain.com/oss/python/langgraph/persistence
- https://docs.langchain.com/oss/python/langchain/long-term-memory

Focus on separating:

- Runtime state
- Durable agent state
- Long-term memory
- Storage implementation

### 2. Mem0 Architecture and Advanced Operations

- Overview: https://docs.mem0.ai/platform/overview
- How it works: https://docs.mem0.ai/core-concepts/how-it-works
- Advanced operations: https://docs.mem0.ai/platform/advanced-memory-operations
- Graph memory: https://docs.mem0.ai/platform/features/graph-memory

### 3. Microsoft GraphRAG Overview

**Why:** Useful for understanding graph construction and retrieval, while also learning that GraphRAG is knowledge retrieval rather than a complete personal-memory lifecycle.

- Docs: https://microsoft.github.io/graphrag/
- Overview: https://microsoft.github.io/graphrag/index/overview/
- Paper: https://www.microsoft.com/en-us/research/publication/from-local-to-global-a-graph-rag-approach-to-query-focused-summarization/
- Repository: https://github.com/microsoft/graphrag

Focus on:

- Indexing pipeline
- Entity extraction
- Community detection
- Community summaries
- Local versus global retrieval
- Difference between GraphRAG and agent memory

## Required Viewing

### DeepLearning.AI Agent Memory Course

Search for:

**LLMs as Operating Systems: Agent Memory**

Use it as the hands-on implementation component for this phase.

## Optional Deep Dives

### GraphRAG Publications

- https://www.microsoft.com/en-us/research/project/graphrag/publications/

## Practical Work

Draw three architectures:

- [ ] Minimal conversational memory
- [ ] Production user-memory platform
- [ ] Full agent-memory platform

Every architecture must identify:

- Source of truth
- Canonical record
- Graph projection
- Vector projection
- Lexical projection
- Write path
- Read path
- Deletion path
- Evaluation path

## Completion Gate

You can review a stack and identify missing source-of-truth, lifecycle, retrieval, governance, or evaluation layers.

---

# Phase 5 — Retrieval and Context Assembly

## Goal

Learn how relevant memories are found, ranked, filtered, and inserted into context.

## Required Reading

### 1. Generative Agents Retrieval Model

Re-read the retrieval portions of:

- https://arxiv.org/abs/2304.03442

Focus on:

- Recency
- Importance
- Relevance
- Combined ranking
- Reflection retrieval

### 2. Mem0 Search and Evaluation

- Search: https://docs.mem0.ai/core-concepts/memory-operations/search
- Evaluation: https://docs.mem0.ai/core-concepts/memory-evaluation
- New hybrid architecture: https://docs.mem0.ai/migration/oss-v2-to-v3

Focus on:

- Semantic search
- BM25
- Entity matching
- Token efficiency
- Retrieval budget
- Benchmark caveats

### 3. GraphRAG Query Modes

- https://microsoft.github.io/graphrag/

Study:

- Local search
- Global search
- Graph context construction
- Community summaries

## Required Viewing

### LangGraph Long-Term Memory Agent

Official docs should remain the source of truth, but a walkthrough can help:

- https://www.youtube.com/watch?v=pzMiZTEqI3Q

## Optional Deep Dives

### HiGMem: A Hierarchical and LLM-Guided Memory System for Long-Term Agents

**Venue:** Findings of ACL 2026

- https://aclanthology.org/2026.findings-acl.1690/

Read for:

- Hierarchical memory
- LLM-guided retrieval
- Weaknesses of pure vector similarity

## Practical Work

Create a hybrid retrieval design that uses:

- [ ] Tenant filters
- [ ] User or agent scope
- [ ] Vector similarity
- [ ] Lexical search
- [ ] Entity matching
- [ ] Graph traversal
- [ ] Temporal filters
- [ ] Confidence
- [ ] Source authority
- [ ] Reranking
- [ ] Context budgeting

Create ten queries where pure nearest-neighbor retrieval would return a plausible but wrong memory.

## Completion Gate

You can explain why retrieval is a ranking and policy problem, not simply a vector-query problem.

---

# Phase 6 — Agent Memory, Reflection, and Learning

## Goal

Understand how agents store experience, reflect on outcomes, and derive reusable procedures.

## Required Reading

### 1. Reflexion: Language Agents with Verbal Reinforcement Learning

**Venue:** NeurIPS 2023

- Abstract: https://proceedings.neurips.cc/paper_files/paper/2023/hash/1b44b878bb782e6954cd888628510e90-Abstract-Conference.html
- Paper: https://proceedings.neurips.cc/paper_files/paper/2023/file/1b44b878bb782e6954cd888628510e90-Paper-Conference.pdf
- Code: https://github.com/noahshinn/reflexion

Focus on:

- Feedback
- Verbal reflection
- Episodic memory
- Reuse across attempts
- Evaluation
- Risks of trusting self-reflection

### 2. Generative Agents Reflection

- https://arxiv.org/abs/2304.03442

Focus on:

- Reflection trigger
- Higher-order memories
- Links from reflection back to evidence
- Planning

### 3. From Storage to Experience

- https://arxiv.org/abs/2605.06716

Focus on:

- Trajectory storage
- Reflection
- Cross-trajectory abstraction
- Experience formation

## Required Viewing

### Stateful Agents Workshop

- https://www.youtube.com/watch?v=E0k9Ppq6yXY

Watch the sections on persistent agents and learning from experience.

## Optional Deep Dives

### Agentic Memory: Learning Unified Long-Term and Short-Term Memory Management

- https://arxiv.org/abs/2601.01885

Read as a frontier approach to learned memory policy, not an established production standard.

## Practical Work

For three similar agent runs, produce:

- [ ] Raw trajectories
- [ ] Outcome labels
- [ ] Reflection for each
- [ ] Common pattern
- [ ] Candidate procedure
- [ ] Evidence threshold for promotion
- [ ] Rollback rule
- [ ] Cases where the procedure should not apply

## Completion Gate

You can distinguish raw experience, reflection, generalized knowledge, and executable procedure.

---

# Phase 7 — Temporal Memory and Contradictions

## Goal

Handle facts and relationships that change over time without destroying historical truth.

## Required Reading

### 1. Towards Lifelong Dialogue Agents via Timeline-Based Memory Management

**Venue:** NAACL 2025

- Paper page: https://aclanthology.org/2025.naacl-long.435/
- PDF: https://aclanthology.org/2025.naacl-long.435.pdf

Focus on:

- Timeline construction
- Temporal and causal links
- Why old memories should not always be deleted
- Recency bias
- Evolving user information

### 2. Evaluating the Long-Term Memory of Large Language Models

**Venue:** Findings of ACL 2025

- https://aclanthology.org/2025.findings-acl.1014/

Focus on:

- Chronological interactions
- Memory decay
- Rehearsal
- Long-term retention

### 3. Mem0 Update and Additive Extraction

- Update: https://docs.mem0.ai/core-concepts/memory-operations/update
- Architecture migration: https://docs.mem0.ai/migration/oss-v2-to-v3

Compare explicit updates with additive historical records.

## Required Viewing

No required video. Spend the time modeling timelines.

## Optional Deep Dives

### Zep / Graphiti Temporal Knowledge Graph

Use official current documentation:

- Graphiti repository and documentation: https://github.com/getzep/graphiti
- Zep documentation: https://help.getzep.com/

Study:

- Temporal edges
- Episodes
- Entity resolution
- Invalidated facts
- Current versus historical truth

## Practical Work

Model a timeline containing:

- [ ] A stable fact
- [ ] A changed preference
- [ ] A correction
- [ ] Two apparently contradictory facts that are both historically true
- [ ] An uncertain claim
- [ ] An admin-authored claim
- [ ] A tool-verified claim
- [ ] A superseded claim

Required fields:

```text
claim_id
subject
predicate
object
observed_at
valid_from
valid_to
confidence
source_type
source_event
status
supersedes
derived_from
```

## Completion Gate

You can explain the difference between false, stale, corrected, superseded, disputed, and historically true.

---

# Phase 8 — Safety, Governance, and Forgetting

## Goal

Treat persistent memory as a security, privacy, and governance surface.

## Required Reading

### 1. OWASP Top 10 for LLM Applications

Use the current official version:

- https://genai.owasp.org/llm-top-10/

Focus on:

- Prompt injection
- Sensitive information disclosure
- Excessive agency
- Data and model poisoning
- Improper output handling

Map each risk to persistent memory.

### 2. NIST AI Risk Management Framework

- Main framework: https://www.nist.gov/itl/ai-risk-management-framework
- Generative AI profile: https://www.nist.gov/itl/ai-risk-management-framework/ai-rmf-generative-artificial-intelligence-profile

Focus on:

- Provenance
- Governance
- Monitoring
- Data integrity
- Human oversight
- Risk measurement

### 3. LangGraph Persistence Documentation

- https://docs.langchain.com/oss/python/langgraph/persistence

Review persistence as an attack and privacy surface:

- Serialized state
- Checkpoint contents
- Cross-thread scope
- Store namespaces

### 4. Letta Shared Memory

- https://docs.letta.com/guides/core-concepts/memory/shared-memory

Consider authorization and blast radius when shared state is editable.

## Required Viewing

No required video. Threat-modeling is more valuable here.

## Optional Deep Dives

Research terms to explore:

- Persistent prompt injection
- RAG poisoning
- Knowledge-base poisoning
- Vector database multi-tenant isolation
- Machine unlearning
- Derived-data deletion
- Right to be forgotten in knowledge graphs

Prefer peer-reviewed papers or official security guidance.

## Practical Work

Create a threat model covering:

- [ ] Malicious memory write
- [ ] Hallucinated memory extraction
- [ ] Incorrect entity linking
- [ ] Cross-tenant retrieval
- [ ] Prompt injection persisted as memory
- [ ] Low-trust memory triggering a tool
- [ ] Admin abuse
- [ ] Incomplete deletion
- [ ] Poisoned consolidated procedure
- [ ] Unsafe shared memory

Create a deletion propagation map:

```text
Source event
  → canonical memory
  → summary
  → vector index
  → graph projection
  → cached retrieval
  → consolidated procedure
```

## Completion Gate

You can explain how a bad memory enters, persists, propagates, influences behavior, and is removed.

---

# Phase 9 — Memory Evaluation

## Goal

Evaluate writes, updates, retrieval, usage, and downstream agent performance.

## Required Reading

### 1. Evaluating Very Long-Term Conversational Memory of LLM Agents

**Venue:** ACL 2024  
**Benchmark:** LoCoMo

- Page: https://aclanthology.org/2024.acl-long.747/
- PDF: https://aclanthology.org/2024.acl-long.747.pdf

Focus on:

- Benchmark construction
- Long multi-session conversations
- Question categories
- Summarization
- RAG and long-context baselines
- Human performance gap

### 2. Evaluating Memory in LLM Agents via Incremental Multi-Turn Interactions

- OpenReview: https://openreview.net/forum?id=ZgQ0t3zYTQ
- ArXiv: https://arxiv.org/abs/2507.05257

Focus on:

- Memory competencies
- Incremental interactions
- Storage
- Update
- Retrieval
- Reasoning with memory

### 3. Mem0 Memory Evaluation

- https://docs.mem0.ai/core-concepts/memory-evaluation

Read this as a vendor evaluation methodology. Ask:

- What is measured?
- What is held constant?
- What retrieval budget is used?
- What does token efficiency mean?
- Which system-level costs are absent?

### 4. Evaluating Memory Structure in LLM Agents

- https://openreview.net/forum?id=a9vY2sJkf4

Focus on how benchmark design can reveal differences among memory structures.

## Required Viewing

No required video. Spend the time inspecting benchmark examples and writing your own.

## Optional Deep Dives

### Mem-Gallery

**Venue:** ACL 2026

- https://aclanthology.org/2026.acl-long.1892/

Use for multimodal memory evaluation.

### Survey on Evaluation of LLM-Based Agents

- https://arxiv.org/abs/2503.16416

Use to connect memory metrics to end-to-end agent evaluation.

## Practical Work

Build a small benchmark with:

- [ ] 20 stable facts
- [ ] 20 changing facts
- [ ] 10 corrections
- [ ] 10 contradictory claims
- [ ] 10 episodes
- [ ] 10 procedures
- [ ] 10 low-trust or poisoned memories
- [ ] 10 cross-tenant tests
- [ ] 10 queries with misleading semantic neighbors

Track:

- Extraction precision and recall
- Retrieval hit rate
- Ranking quality
- Stale-memory retrieval
- False-memory rate
- Correction accuracy
- Deletion completeness
- Task-success improvement
- Latency
- Token cost
- Storage and write amplification

## Completion Gate

You can make a release decision based on measured memory behavior rather than a successful demo.

---

# Phase 10 — AWS Neptune Specialization

## Goal

Understand Neptune Database and Neptune Analytics deeply enough to define their correct role in a memory platform.

## Required Reading

### 1. Neptune Database Developer Guide

Start here:

- https://docs.aws.amazon.com/neptune/latest/userguide/intro.html

Study:

- Property graph model
- openCypher
- Gremlin
- RDF/SPARQL
- Transactions
- Query behavior
- Bulk loading
- Backup and recovery
- Security
- IAM
- Encryption

### 2. openCypher in Neptune

- https://docs.aws.amazon.com/neptune/latest/userguide/access-graph-opencypher.html

Focus on:

- Supported syntax
- Query patterns
- Parameterization
- Query planning and performance considerations

### 3. Neptune Full-Text Search with OpenSearch

- https://docs.aws.amazon.com/neptune/latest/userguide/full-text-search.html

This is important because it demonstrates that Neptune is commonly complemented by a separate search substrate.

### 4. Neptune Analytics

- Introduction: https://docs.aws.amazon.com/neptune-analytics/latest/userguide/what-is-neptune-analytics.html
- Vector similarity: https://docs.aws.amazon.com/neptune-analytics/latest/userguide/vector-similarity.html
- Vector index: https://docs.aws.amazon.com/neptune-analytics/latest/userguide/vector-index.html

Focus on:

- Workload model
- Graph analytics
- Vector search
- Index constraints
- Relationship to Neptune Database
- Data movement
- Cost model

### 5. AWS Memory Architecture with Mem0 and Neptune

Search and read these official AWS resources:

- **Build persistent memory for agentic AI applications with Mem0, Amazon ElastiCache for Valkey, and Amazon Neptune Analytics**
- **Company-wise memory in Amazon Bedrock with Amazon Neptune and Mem0**

AWS Database Blog and AWS Machine Learning Blog are the preferred sources.

## Required Viewing

### AWS Neptune Analytics Deep Dive

- https://www.youtube.com/watch?v=hGg7gKLHVnY

Alternative AWS-hosted version:

- https://aws.amazon.com/video/watch/6a08afaf54a/

## Optional Deep Dives

### Amazon Neptune and Cognee Integration

- https://aws.amazon.com/about-aws/whats-new/2025/08/amazon-neptune-cognee-genai-applications/

Use this to evaluate Neptune as the graph store beneath a separate memory framework.

## Practical Work

Design and compare:

### Architecture A

```text
Canonical record store
+ OpenSearch vectors and lexical search
+ Neptune Database
```

### Architecture B

```text
Canonical record store
+ Neptune Database
+ Neptune Analytics vector and graph retrieval
```

### Architecture C

```text
Neptune as canonical graph store
+ object/event archive
+ external vector search
```

Score each on:

- Temporal modeling
- Deletion
- Replay
- Auditing
- Re-embedding
- Multiple embedding models
- Query flexibility
- Tenant isolation
- Latency
- Cost
- Operational complexity
- Schema evolution

## Completion Gate

You can explain:

- Why Neptune is useful
- Why Neptune alone is incomplete
- Whether graph data is canonical or projected
- When Neptune Analytics can replace a vector store
- When OpenSearch or another vector system remains preferable

---

# Phase 11 — Industry System Comparison

## Goal

Compare real systems without accepting their marketing categories as universal truth.

## Required Systems

### Mem0

Read:

- https://docs.mem0.ai/core-concepts/how-it-works
- https://docs.mem0.ai/core-concepts/memory-types
- https://docs.mem0.ai/platform/features/graph-memory
- https://docs.mem0.ai/core-concepts/memory-evaluation
- https://docs.mem0.ai/migration/oss-v2-to-v3

### Zep / Graphiti

Read:

- https://help.getzep.com/
- https://github.com/getzep/graphiti

Focus on temporal knowledge graphs and episodes.

### Letta

Read:

- https://docs.letta.com/letta-agent/memory
- https://docs.letta.com/guides/core-concepts/stateful-agents
- https://docs.letta.com/guides/core-concepts/memory/memory-blocks
- https://docs.letta.com/guides/core-concepts/memory/archival-memory

### LangGraph

Read:

- https://docs.langchain.com/oss/python/concepts/memory
- https://docs.langchain.com/oss/python/langgraph/persistence
- https://docs.langchain.com/oss/python/langchain/long-term-memory

### Microsoft GraphRAG

Read:

- https://microsoft.github.io/graphrag/
- https://www.microsoft.com/en-us/research/publication/from-local-to-global-a-graph-rag-approach-to-query-focused-summarization/

### Cognee

Read official documentation and repository:

- https://github.com/topoteretes/cognee
- https://docs.cognee.ai/

Evaluate its graph-centric data and memory pipelines, especially in relation to Neptune.

## Comparison Matrix

For every system record:

- [ ] Definition of memory
- [ ] Write trigger
- [ ] Memory representation
- [ ] Canonical store
- [ ] Vector search
- [ ] Lexical search
- [ ] Graph search
- [ ] Temporal handling
- [ ] Contradiction handling
- [ ] Agent-managed writes
- [ ] User and organization scope
- [ ] Provenance
- [ ] Forgetting
- [ ] Evaluation
- [ ] Operational maturity
- [ ] Self-hosting
- [ ] Lock-in
- [ ] Neptune fit

## Practical Work

Produce:

- [ ] A system comparison matrix
- [ ] A two-page recommendation on patterns worth adopting
- [ ] A list of vendor claims that require independent testing
- [ ] A build-versus-buy decision framework

## Completion Gate

You can explain why Mem0, Zep, Letta, LangGraph, GraphRAG, and Cognee solve overlapping but different problems.

---

# Phase 12 — Capstone

## Goal

Produce an ownership-ready architecture proposal for an industry-standard memory platform.

## Required Deliverables

- [ ] Executive summary
- [ ] Definition of memory
- [ ] User, agent, and organizational use cases
- [ ] Memory taxonomy
- [ ] Canonical event model
- [ ] Canonical memory model
- [ ] Episode schema
- [ ] Claim schema
- [ ] Procedure schema
- [ ] Provenance model
- [ ] Temporal model
- [ ] Lifecycle state machine
- [ ] Write-path sequence diagram
- [ ] Read-path sequence diagram
- [ ] Hybrid retrieval design
- [ ] Context assembly policy
- [ ] Neptune graph schema
- [ ] Vector and lexical indexing design
- [ ] Deletion propagation design
- [ ] Poisoned-memory threat model
- [ ] Evaluation framework
- [ ] SLOs and cost model
- [ ] Phased implementation plan
- [ ] Build-versus-buy recommendation
- [ ] Open questions and risks

## Required Architecture Principle

Start with:

```text
Source events are authoritative.
Memory records are managed derivatives.
Graphs, vectors, lexical indexes, and summaries are projections.
Prompt context is a temporary materialized view.
```

Challenge this principle only when you have a clear reason.

## Final Review Questions

Your capstone should answer:

1. What is the source of truth?
2. What becomes a memory?
3. Who may create it?
4. How is it validated?
5. How is it scoped?
6. How is it represented?
7. How does it change over time?
8. How is it retrieved?
9. How does it influence an agent?
10. How is its usefulness measured?
11. How is it corrected?
12. How is it deleted?
13. How is poisoning contained?
14. What belongs in Neptune?
15. What does not belong in Neptune?

---

# Recommended 12-Week Schedule

| Week | Phase | Required Output |
|---|---|---|
| 1 | 0 | Industry map and glossary |
| 2 | 1 | Memory taxonomy |
| 3 | 2 | Lifecycle and state machine |
| 4 | 3 | Representation comparison |
| 5 | 4 | Three reference architectures |
| 6 | 5 | Hybrid retrieval design |
| 7 | 6 | Agent learning and procedure policy |
| 8 | 7 | Temporal and contradiction model |
| 9 | 8 | Threat model and deletion design |
| 10 | 9 | Evaluation benchmark |
| 11 | 10–11 | Neptune and vendor comparison |
| 12 | 12 | Capstone architecture proposal |

---

# Fast Track

When you need meeting-level competence quickly, complete these in order:

1. Memory for Autonomous LLM Agents  
   https://arxiv.org/abs/2603.07670

2. Generative Agents  
   https://arxiv.org/abs/2304.03442

3. MemGPT  
   https://arxiv.org/abs/2310.08560

4. Reflexion  
   https://proceedings.neurips.cc/paper_files/paper/2023/hash/1b44b878bb782e6954cd888628510e90-Abstract-Conference.html

5. LoCoMo  
   https://aclanthology.org/2024.acl-long.747/

6. Timeline-Based Memory Management  
   https://aclanthology.org/2025.naacl-long.435/

7. Mem0 How It Works  
   https://docs.mem0.ai/core-concepts/how-it-works

8. LangGraph Persistence  
   https://docs.langchain.com/oss/python/langgraph/persistence

9. Neptune Analytics Vector Search  
   https://docs.aws.amazon.com/neptune-analytics/latest/userguide/vector-similarity.html

10. Complete the industry-system comparison matrix.

This fast track should be enough to participate intelligently in architecture discussions. The full curriculum is intended to prepare you to own the platform.

---

# Reading Priorities

## Must Read Fully

- Generative Agents
- MemGPT
- Reflexion
- LoCoMo
- Timeline-Based Memory Management
- Memory-agent evaluation paper

## Read for Architecture

- Current memory survey
- Mem0 documentation
- Letta memory documentation
- LangGraph persistence documentation
- GraphRAG documentation
- Neptune documentation

## Skim for Frontier Awareness

- MemOS
- AgeMem
- Storage-to-Experience survey
- HiGMem
- Multimodal memory benchmarks

---

# Curriculum Completion Criteria

You have completed the curriculum when you can:

- [ ] Define memory independently of any vendor
- [ ] Distinguish runtime state, conversation continuity, knowledge, and memory
- [ ] Design write, management, and read policies
- [ ] Choose appropriate representations
- [ ] Design hybrid retrieval
- [ ] Model temporal truth and contradictions
- [ ] Design agent experience and procedure learning
- [ ] Threat-model persistent memory
- [ ] Build a meaningful benchmark
- [ ] Explain Neptune’s precise role
- [ ] Compare major industry implementations
- [ ] Produce and defend a target-state architecture
