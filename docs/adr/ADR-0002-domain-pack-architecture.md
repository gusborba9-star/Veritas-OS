# ADR-0002 — Domain Pack Architecture

**Status:** Accepted — DEFINED

## Context
O Veritas precisa suportar múltiplas profissões e domínios sem duplicar infraestrutura.

## Decision
Usar Domain Packs para especialização de conteúdo, regras, protocolos, cálculos, segurança e workflows sobre o Core comum.

## Consequences
Novos domínios reutilizam infraestrutura; conteúdo especializado permanece isolado e contextualizado.

## Alternatives Considered
- Fork completo por profissão — duplicaria o Core.
- Um módulo monolítico com todas as regras — aumentaria acoplamento.
