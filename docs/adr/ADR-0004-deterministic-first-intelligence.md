# ADR-0004 — Deterministic First Intelligence

**Status:** Accepted — DEFINED

## Context
A LLM não deve ser tratada como autoridade profissional quando uma tarefa pode ser resolvida por mecanismos determinísticos.

## Decision
Priorizar Deterministic First → Evidence → Computation → Safety → Generative AI.

## Consequences
Cálculos devem ser reproduzíveis; evidência deve preservar proveniência; Safety permanece uma camada própria; o Copilot opera sobre contexto autorizado.

## Alternatives Considered
- LLM-first — incompatível com o princípio definido.
- Geração sem rastreabilidade — incompatível com auditabilidade.
