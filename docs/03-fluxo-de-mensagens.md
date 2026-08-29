# 3. Fluxo de Mensagens

```mermaid
flowchart LR
    P[Paciente] --> W[WhatsApp]
    W --> E[Evolution API]
    E --> X[Camada de enriquecimento<br/>payload + contexto da clínica/paciente]
    X --> N[Webhook n8n]
```

A camada de enriquecimento pertence à infraestrutura da aplicação (fora do workflow principal) e adiciona ao payload os dados de contexto necessários — clínica, assistente e paciente.

Ao entrar no n8n, os dados são reorganizados em blocos conceituais de contexto:

```
Assistant Configuration
        +
Clinic Configuration
        +
Patient Context
        +
Current Message
```

## Normalização de mensagens

O sistema aceita múltiplos formatos de entrada e converte tudo para uma representação textual comum antes de qualquer processamento pelos agentes.

```mermaid
flowchart TD
    M[Incoming Message] --> T[Texto]
    M --> AU[Áudio]
    M --> MD[Mídia<br/>imagem/vídeo/documento]
    T --> NT[Normalized Text]
    AU -->|Gemini| NT
    MD -->|Gemini| NT
```

Isso evita que cada agente precise lidar individualmente com múltiplos formatos de entrada.

## Buffer de mensagens (Redis)

Usuários de WhatsApp costumam enviar várias mensagens curtas em sequência ("Oi", "queria saber", "se vocês atendem Unimed"). Processar cada uma isoladamente geraria execuções redundantes da IA e pouco contexto por execução.

Solução: as mensagens são acumuladas no **Redis** dentro de uma janela de ~30 segundos.

```mermaid
flowchart LR
    M1[Message 1] --> R[Redis Buffer]
    M2[Message 2] --> R
    M3[Message 3] --> R
    R --> WT{Última mensagem<br/>ainda é a mais recente?}
    WT -->|Sim| AG[Agrega mensagens]
    WT -->|Não, chegou nova| STOP[Interrompe execução anterior]
    AG --> AI[AI Agent]
```

Se uma mensagem mais nova chega antes da janela expirar, o processamento anterior é interrompido — evitando respostas duplicadas ou fora de ordem.

O Redis aqui tem responsabilidade diferente da memória conversacional: é **estado temporário**, não histórico.

## Memória conversacional

Implementada com o mecanismo de Chat Memory do n8n, persistido em **PostgreSQL**. Mantém uma janela de histórico recente para dar contexto aos agentes durante o atendimento.

| Componente | Responsabilidade |
|---|---|
| Redis | Buffer temporário de mensagens |
| PostgreSQL / Chat Memory | Histórico conversacional |
| Sistema externo | Dados persistentes de domínio (clínicas, pacientes, agenda) |

---

⬅ [Multi-tenancy](./02-multi-tenancy.md) · [Índice](../README.md) · Próximo → [Guardrails e agentes](./04-guardrails-e-agentes.md)
