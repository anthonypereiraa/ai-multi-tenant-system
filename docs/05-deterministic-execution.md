# 5. Deterministic Execution

One of the core technical decisions was to **deliberately reduce how much the LLM needs to reason about raw data**.

```mermaid id="j2x5r1"
flowchart TD
    SA[Scheduling Agent] --> AT[Availability Tool]
    AT --> SW[Scheduling Workflow]
    SW --> RD[Retrieve Availability Data]
    RD --> DP[Deterministic Processing<br/>code, not LLM]
    DP --> SR[Structured Result]
    SR --> SA
```

Calculating the next available appointment, checking conflicts, and enforcing business rules are handled in code within the sub-workflows — not by the LLM. The agent receives only the relevant structured result needed to formulate the response.

```text id="p6r2mk"
LLM        → interpretation and language
Code       → deterministic rules
```

## Responsibility Architecture

```mermaid id="4n2w8k"
flowchart TD
    WA[WhatsApp] --> EV[Evolution API]
    EV --> N8N[n8n — Orchestration]
    subgraph N8N[" "]
        MP[Message Processing<br/>type, normalization, buffering] --> SEC[Security<br/>Guardrails]
        SEC --> ORQ[AI Orchestration<br/>Router, Service, Scheduling]
        ORQ --> TOOLS[Tools / Sub-workflows<br/>availability, scheduling,<br/>cancellation, rescheduling]
    end
    TOOLS --> EXT[External Application<br/>Supabase]
```

---

⬅ [Guardrails and Agents](./04-guardrails-and-agents.md) · [Index](../README.md) · Next → [Technical Stack](./06-technical-stack.md)
