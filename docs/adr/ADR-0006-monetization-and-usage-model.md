# ADR-0006 — Monetization and Usage Model

**Status:** Accepted — DEFINED

## Context
Monetização deve ser considerada desde a arquitetura, mas não será implementada nesta fundação.

## Decision
Reservar suporte para Individual, Clinic, Enterprise e API, com Monthly, Annual, Credits, Usage Metering, Add-ons, Additional Seats e Enterprise Contracts.

## Consequences
Billing, plans, entitlements, quotas, usage e créditos deverão possuir boundaries próprios e auditáveis. Nada disso é declarado implementado.

## Alternatives Considered
- Adiar qualquer boundary comercial até o final — perderia requisitos arquiteturais relevantes.
- Misturar billing com regras de domínio — aumentaria acoplamento.
