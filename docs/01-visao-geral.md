# 1. Visão Geral

O **Viver** é uma plataforma SaaS multi-tenant que fornece atendimento automatizado por IA via WhatsApp para clínicas. O sistema funciona como uma secretária virtual capaz de:

- Interpretar mensagens de texto, áudio, imagem, vídeo, figurinha e documento;
- Manter contexto e memória da conversa;
- Responder dúvidas institucionais da clínica;
- Executar operações de agenda (criar, consultar, cancelar e reagendar horários).

A orquestração é feita principalmente com **n8n**, combinando serviços gerenciados e infraestrutura própria em containers.

O diferencial arquitetural não é "uma IA para clínicas", mas sim:

> Uma estrutura compartilhada de processamento, configurada dinamicamente por tenant, na qual mensagens são normalizadas e agregadas antes do processamento, agentes especializados cuidam de responsabilidades distintas, e operações críticas são delegadas a workflows determinísticos em vez de raciocínio livre da LLM.

## O problema

Sistemas de atendimento por IA costumam cair em uma de duas armadilhas:

- **Uma instância de IA por cliente** — não escala, é caro de manter e dificulta evolução conjunta do produto.
- **LLM responsável por tudo**, inclusive lógica de negócio determinística (ex.: cálculo de disponibilidade de agenda) — gera respostas inconsistentes e abre espaço para alucinação em operações que deveriam ser previsíveis.

O Viver resolve isso com uma arquitetura compartilhada + contexto dinâmico, separando claramente **interpretação de linguagem** (papel da LLM) de **execução de regras de negócio** (papel do código).

---

⬅ [Voltar ao índice](../README.md) · Próximo → [Multi-tenancy](./02-multi-tenancy.md)
