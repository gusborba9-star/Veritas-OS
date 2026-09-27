# ADR-0007 — Interoperability Strategy

**Status:** Accepted — DEFINED

## Context
O Veritas deverá interoperar com sistemas externos.

## Decision
Tratar APIs, importação/exportação, FHIR e HL7 como direção arquitetural, usando adaptadores e contratos explícitos. Nenhuma integração é considerada implementada nesta execução.

## Consequences
O domínio interno não precisa ficar acoplado diretamente a formatos externos; adaptadores poderão evoluir e ser testados independentemente.

## Alternatives Considered
- Acoplamento direto do domínio a um padrão externo — aumentaria dependência.
- Ignorar interoperabilidade até produção — criaria risco de contratos incompatíveis.
