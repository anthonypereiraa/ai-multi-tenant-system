# 1. Overview

**Viver** is a multi-tenant SaaS platform that provides AI-powered patient support via WhatsApp for clinics. The system operates as a virtual receptionist capable of:

* Interpreting text, audio, image, video, sticker, and document messages;
* Maintaining conversational context and memory;
* Answering clinic-related institutional questions;
* Performing scheduling operations (create, retrieve, cancel, and reschedule appointments).

The system is primarily orchestrated with **n8n**, combining managed services with self-hosted containerized infrastructure.

The architectural differentiator is not simply **"AI for clinics"**, but rather:

> A shared processing infrastructure dynamically configured per tenant, where messages are normalized and aggregated before processing, specialized agents handle distinct responsibilities, and critical operations are delegated to deterministic workflows instead of relying on unrestricted LLM reasoning.

## The Problem

AI-powered support systems commonly fall into one of two traps:

* **One AI instance per client** — this does not scale efficiently, is expensive to maintain, and makes coordinated product evolution more difficult.
* **The LLM responsible for everything**, including deterministic business logic (e.g., calculating appointment availability) — this can lead to inconsistent responses and creates opportunities for hallucinations in operations that should be predictable.

Viver addresses this with a **shared architecture + dynamic context**, clearly separating **language interpretation** (the role of the LLM) from **business rule execution** (the role of code).

---

⬅ [Back to Index](../README.md) · Next → [Multi-tenancy](./02-multi-tenancy.md)
