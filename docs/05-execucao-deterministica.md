# 5. Execução Determinística

Uma das decisões técnicas centrais: **reduzir deliberadamente o quanto a LLM precisa raciocinar sobre dados brutos**.

```mermaid
flowchart TD
    SA[Scheduling Agent] --> AT[Availability Tool]
    AT --> SW[Scheduling Workflow]
    SW --> RD[Retrieve Availability Data]
    RD --> DP[Deterministic Processing<br/>código, não LLM]
    DP --> SR[Structured Result]
    SR --> SA
```

Cálculo de próximo horário disponível, verificação de conflitos e regras de negócio são resolvidos em código dentro dos sub-workflows — não pela LLM. O agente recebe apenas o resultado estruturado e relevante para formular a resposta.

```
LLM        → interpretação e linguagem
Código     → regras determinísticas
```

Reagendamento, por exemplo, é tratado como operação composta (cancelar + criar), com a complexidade encapsulada no workflow — o agente só enxerga uma operação de alto nível.

## Arquitetura de responsabilidades

```mermaid
flowchart TD
    WA[WhatsApp] --> EV[Evolution API]
    EV --> N8N[n8n — Orquestração]
    subgraph N8N[" "]
        MP[Message Processing<br/>tipo, normalização, buffer] --> SEC[Security<br/>Guardrails]
        SEC --> ORQ[AI Orchestration<br/>Router, Service, Scheduling]
        ORQ --> TOOLS[Tools / Sub-workflows<br/>availability, scheduling,<br/>cancellation, rescheduling]
    end
    TOOLS --> EXT[External Application<br/>Supabase]
```

---

⬅ [Guardrails e agentes](./04-guardrails-e-agentes.md) · [Índice](../README.md) · Próximo → [Stack técnica](./06-stack-tecnica.md)
