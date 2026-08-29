# 1. Overview

This project presents a **multi-tenant AI-powered patient support architecture** designed for clinics operating through WhatsApp. The system functions as a virtual receptionist capable of:

* Interpreting text, audio, image, video, sticker, and document messages;
* Maintaining conversational context and memory;
* Answering clinic-related institutional questions;
* Performing scheduling operations (create, retrieve, cancel, and reschedule appointments).

The architecture is primarily orchestrated with **n8n**, combining managed services with self-hosted containerized infrastructure.

The architectural differentiator is not simply **"AI for clinics"**, but rather:

> A shared processing infrastructure dynamically configured per tenant, where messages are normalized and aggregated before processing, specialized agents handle distinct responsibilities, and critical operations are delegated to deterministic workflows instead of relying on unrestricted LLM reasoning.

## The Problem

AI-powered support systems commonly fall into one of two traps:

* **One AI instance per client** — this does not scale efficiently, is expensive to maintain, and makes coordinated product evolution more difficult.
* **The LLM responsible for everything**, including deterministic business logic (e.g., calculating appointment availability) — this can lead to inconsistent responses and create opportunities for hallucinations in operations that should be predictable.

This architecture addresses these challenges through a **shared architecture + dynamic context**, clearly separating **language interpretation** (the role of the LLM) from **business rule execution** (the role of code).

---

⬅ [Back to Index](../README.md) · Next → [Multi-Tenancy](./02-multi-tenancy.md)
