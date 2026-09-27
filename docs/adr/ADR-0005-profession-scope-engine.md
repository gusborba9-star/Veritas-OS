# ADR-0005 — Profession, Specialty and Scope/Permission Engine

**Status:** Accepted — DEFINED

## Context
Identidade profissional, profissão, especialidade, organização, jurisdição e permissões representam dimensões diferentes de autorização.

## Decision
Separar Profession, Specialty, Organization, Jurisdiction, Permissions e Scope. A autorização futura deve ser contextual e verificável.

## Consequences
O acesso a Subjects e capacidades dependerá de escopo explícito; organizações e profissionais não serão tratados como equivalentes.

## Alternatives Considered
- Controle somente por papel global — insuficiente para escopo contextual.
- Controle somente por organização — insuficiente para diferenciar contexto profissional.
