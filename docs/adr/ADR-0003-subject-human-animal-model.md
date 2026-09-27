# ADR-0003 — Subject Human / Animal Model

**Status:** Accepted — DEFINED

## Context
O Veritas deve suportar contextos humanos e veterinários sem mistura implícita de regras.

## Decision
Subject terá classificação explícita mínima HUMAN ou ANIMAL. Life Stage e Species fornecem contexto adicional quando aplicável.

## Consequences
Regras deverão declarar aplicabilidade ao tipo de Subject; Species será relevante para animais; Life Stage para contexto humano e outros contextos pertinentes.

## Alternatives Considered
- Subject sem tipo — criaria ambiguidade.
- Cores separados para humano e animal — duplicaria infraestrutura.
