# 6. Technical Stack

| Layer                    | Technology                   |
| ------------------------ | ---------------------------- |
| Orchestration            | n8n                          |
| WhatsApp Integration     | Evolution API                |
| Multimodal Processing    | Gemini API                   |
| Conversational AI        | OpenAI API                   |
| Buffer / Temporary State | Redis                        |
| Conversational Memory    | PostgreSQL (n8n Chat Memory) |
| Persistent Domain Data   | Supabase                     |
| Infrastructure           | Docker Swarm                 |

## What Was Developed vs. Third-Party Components

**Developed as part of this architecture:**

* Workflow orchestration in n8n
* Multimodal message processing and normalization
* Message buffering and aggregation with Redis
* Dynamic multi-tenant context construction
* Routing and separation of specialized agents
* Agent integration with tools and sub-workflows
* Deterministic scheduling logic (availability, business hours, conflicts)
* Security guardrails
* Patient response preparation and delivery

**Provided by third parties / external infrastructure:**

* Evolution API, n8n, Gemini API, PostgreSQL, Supabase, Redis, Docker Swarm
* Application backend/system and payload enrichment layer

---

⬅ [Deterministic Execution](./05-deterministic-execution.md) · [Index](../README.md)
