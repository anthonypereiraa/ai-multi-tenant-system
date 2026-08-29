# 6. Stack Técnica

| Camada | Tecnologia |
|---|---|
| Orquestração | n8n |
| Integração WhatsApp | Evolution API |
| Compreensão multimodal | Gemini API |
| Buffer / estado temporário | Redis |
| Memória conversacional | PostgreSQL (n8n Chat Memory) |
| Dados persistentes de domínio | Supabase |
| Infraestrutura | Docker Swarm |

## O que foi desenvolvido vs. componentes de terceiros

**Desenvolvido nesta arquitetura:**
- Orquestração dos fluxos no n8n
- Processamento e normalização de mensagens multimodais
- Buffer e agregação de mensagens com Redis
- Construção dinâmica de contexto multi-tenant
- Roteamento e separação entre agentes especializados
- Integração dos agentes com tools e sub-workflows
- Lógica determinística de agenda (disponibilidade, horários, conflitos)
- Guardrails de segurança
- Preparação e envio de respostas ao paciente

**Fornecido por terceiros / infraestrutura externa:**
- Evolution API, n8n, Gemini API, PostgreSQL, Supabase, Redis, Docker Swarm
- Backend/sistema da aplicação e camada de enriquecimento de payload

---

⬅ [Execução determinística](./05-execucao-deterministica.md) · [Índice](../README.md) · Próximo → [Limitações e roadmap](./07-limitacoes-e-roadmap.md)
