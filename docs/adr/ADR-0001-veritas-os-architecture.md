# ADR-0001 — Veritas OS Architecture

**Status:** Accepted — DEFINED

## Context
O Veritas deve ser uma infraestrutura de inteligência profissional multiprofissional, com Core compartilhado e módulos especializados.

## Decision
Adotar um Veritas Core comum, extensível por Domain Packs, mantendo contexto, evidência, computação, protocolos, segurança, inteligência e governança como capacidades separáveis.

## Consequences
Profissões e domínios podem evoluir sem duplicar o Core. Boundaries deverão permanecer explícitos.

## Alternatives Considered
- Um sistema independente por profissão — não atende ao requisito de Core compartilhado.
- Uma arquitetura centrada exclusivamente em LLM — contradiz Deterministic First.
