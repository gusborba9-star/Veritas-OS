# Veritas OS — Roadmap Oficial

> Fonte oficial do progresso estrutural. Nenhuma fase pode ser VALIDATED sem evidência registrada.

## Estados permitidos
PLANNED · AUDITING · DESIGNED · IMPLEMENTING · TESTING · CI_PENDING · CI_FAILED · CORRECTING · AUDIT_DIFF · VALIDATED · BLOCKED

## Regra de execução
AUDITAR → DEFINIR MENOR ESCOPO → IMPLEMENTAR → TESTAR → CORRIGIR → TESTAR NOVAMENTE → AUDITAR DIFF → VALIDAR → REGISTRAR EVIDÊNCIA → ATUALIZAR ROADMAP

## Estado global
- Produto: Veritas OS
- Execução: EXECUÇÃO 01 — FUNDAÇÃO DOCUMENTAL
- Implementação funcional: não iniciada
- Auditoria profunda do Argos: não iniciada
- Fase atual: PHASE 0 — FOUNDATION

## PHASE 0 — FOUNDATION
**Objetivo:** estabelecer Blueprint, Roadmap e ADRs como fonte de verdade, sem implementar produto.
**Dependências:** nenhuma.
**Entregáveis:** Blueprint; Roadmap; ADR-0001 a ADR-0007.
**Critérios de aceitação:** documentação coerente; distinção DEFINED/PLANNED/IMPLEMENTED/VALIDATED; Markdown e links validados; diff sem código funcional; Argos não tocado; commit e evidências registrados; Roadmap atualizado na mesma execução.
**Estado:** VALIDATED.
**Evidência:** repositório inicialmente vazio; documentação criada em docs/; validação documental executada; commits registrados; nenhuma funcionalidade de produto criada.

## PHASE 1 — ARGOS AUDIT
**Objetivo:** auditoria integral posterior do legado Argos.
**Dependências:** PHASE 0.
**Entregáveis:** inventário; matriz REUSE/ADAPT/REWRITE/DISCARD; riscos e evidências.
**Critérios de aceitação:** auditoria completa e independente, sem reutilização presumida.
**Estado:** VALIDATED.
**Evidência:** EXECUÇÃO 02 — auditoria documental e técnica registrada em `docs/audits/ARGOS-AUDIT.md`, `docs/audits/ARGOS-REUSE-MATRIX.md` e `docs/audits/INFRASTRUCTURE-AUDIT.md`; Argos permaneceu intocado; Supabase foi auditado somente em leitura; Vercel foi auditado até o limite de acesso disponível; riscos de segurança e limitações foram registrados; diff do Veritas foi auditado; commit de fechamento registrado no próprio repositório.
**Limitações:** projeto Vercel explicitamente ligado ao Argos não foi exposto pelo acesso disponível; logs Supabase não puderam ser consultados por erro do backend; segredos não foram lidos; nenhuma afirmação foi inferida para preencher essas lacunas.

## PHASE 2 — ARCHITECTURE
**Objetivo:** detalhar boundaries, contratos, dependências e arquitetura executável do Veritas.
**Dependências:** PHASE 0; resultados relevantes da PHASE 1.
**Entregáveis:** contratos, boundaries, ADRs adicionais quando necessários.
**Critérios de aceitação:** coerência com Blueprint e revisão arquitetural.
**Estado:** PLANNED.
**Evidência esperada:** artefatos arquiteturais versionados.

## PHASE 3 — VERITAS CORE
**Objetivo:** implementar infraestrutura compartilhada.
**Dependências:** PHASE 2.
**Entregáveis:** Core mínimo aprovado.
**Critérios de aceitação:** testes, CI e auditoria do diff.
**Estado:** PLANNED.
**Evidência esperada:** código + testes + CI terminal + diff.

## PHASE 4 — IDENTITY / TENANCY / SCOPE
**Objetivo:** identidade, organizações, membership, tenancy e permissões.
**Dependências:** PHASE 3.
**Entregáveis:** Identity Engine e Scope/Permission Engine.
**Critérios de aceitação:** autorização e isolamento testados.
**Estado:** PLANNED.
**Evidência esperada:** testes positivos/negativos + CI.

## PHASE 5 — DOMAIN MODEL
**Objetivo:** Profession, Specialty, Subject, Species, Life Stage, Organization, Jurisdiction, Permissions e Domain Pack.
**Dependências:** PHASE 3–4.
**Entregáveis:** modelo de domínio versionado.
**Critérios de aceitação:** HUMAN/ANIMAL e contexto de espécie/estágio explicitamente separados.
**Estado:** PLANNED.
**Evidência esperada:** contratos + testes de domínio + CI.

## PHASE 6 — EVIDENCE ENGINE
**Objetivo:** evidência, proveniência, versionamento e aplicabilidade.
**Dependências:** PHASE 5.
**Entregáveis:** Evidence Engine.
**Critérios de aceitação:** proveniência e aplicabilidade reproduzíveis.
**Estado:** PLANNED.
**Evidência esperada:** código + testes + CI.

## PHASE 7 — CALCULATION ENGINE
**Objetivo:** cálculos determinísticos e reproduzíveis.
**Dependências:** PHASE 5.
**Entregáveis:** Calculation Engine.
**Critérios de aceitação:** entradas, resultados e versões testáveis.
**Estado:** PLANNED.
**Evidência esperada:** testes determinísticos + CI.

## PHASE 8 — PROTOCOL ENGINE
**Objetivo:** protocolos versionados e contextuais.
**Dependências:** PHASE 5–7.
**Entregáveis:** Protocol Engine.
**Critérios de aceitação:** aplicabilidade e rastreabilidade.
**Estado:** PLANNED.
**Evidência esperada:** testes + CI + auditoria.

## PHASE 9 — SAFETY ENGINE
**Objetivo:** camada de segurança profissional.
**Dependências:** PHASE 5–8.
**Entregáveis:** Safety Engine.
**Critérios de aceitação:** regras, conflitos, limites, bloqueios e escalonamento verificáveis.
**Estado:** PLANNED.
**Evidência esperada:** testes positivos/negativos + CI.

## PHASE 10 — INTELLIGENCE / COPILOT
**Objetivo:** Intelligence Engine e AI Copilot subordinados às camadas estruturadas.
**Dependências:** PHASE 6–9.
**Entregáveis:** Intelligence Engine e Copilot.
**Critérios de aceitação:** separação entre geração, evidência, cálculo, protocolo e safety.
**Estado:** PLANNED.
**Evidência esperada:** testes de contrato + avaliação controlada + CI.

## PHASE 11 — TIMELINE / WORKFLOW
**Objetivo:** timeline longitudinal e workflows profissionais.
**Dependências:** PHASE 3–5.
**Entregáveis:** Timeline e Workflow.
**Critérios de aceitação:** temporalidade, proveniência, contexto e transições consistentes.
**Estado:** PLANNED.
**Evidência esperada:** testes de consistência temporal/workflow.

## PHASE 12 — LENS
**Objetivo:** apresentação e interpretação contextual.
**Dependências:** PHASE 10–11.
**Entregáveis:** Lens.
**Critérios de aceitação:** contexto autorizado sem redefinir regras do Core.
**Estado:** PLANNED.
**Evidência esperada:** testes de escopo e integração.

## PHASE 13 — IMMUNIZATION
**Objetivo:** Domain Pack de imunização.
**Dependências:** PHASE 5–9 e PHASE 11.
**Entregáveis:** conteúdo e workflows especializados.
**Critérios de aceitação:** regras versionadas, contextualizadas e auditáveis.
**Estado:** PLANNED.
**Evidência esperada:** testes especializados + revisão documental.

## PHASE 14 — PERFORMANCE
**Objetivo:** Domain Pack de performance.
**Dependências:** PHASE 5–9 e PHASE 11.
**Entregáveis:** capacidades especializadas.
**Critérios de aceitação:** reutilização do Core sem duplicação.
**Estado:** PLANNED.
**Evidência esperada:** testes de domínio + CI.

## PHASE 15 — VETERINARY
**Objetivo:** Domain Pack veterinário.
**Dependências:** PHASE 5–9 e PHASE 11.
**Entregáveis:** capacidades veterinárias.
**Critérios de aceitação:** ANIMAL e espécie explícitos; regras humanas não vazam para o domínio veterinário.
**Estado:** PLANNED.
**Evidência esperada:** testes HUMAN/ANIMAL/Species + CI.

## PHASE 16 — INTEROPERABILITY
**Objetivo:** APIs, importação/exportação e integrações; FHIR/HL7 quando efetivamente implementados.
**Dependências:** PHASE 2–5.
**Entregáveis:** adaptadores e contratos de interoperabilidade.
**Critérios de aceitação:** contratos versionados e testes de integração.
**Estado:** PLANNED.
**Evidência esperada:** testes de contrato/integração.

## PHASE 17 — BILLING / CREDITS
**Objetivo:** planos, assinaturas, credits, usage metering, add-ons, seats e enterprise contracts.
**Dependências:** PHASE 4 e API architecture.
**Entregáveis:** billing e entitlements.
**Critérios de aceitação:** consumo comercial reproduzível e auditável.
**Estado:** PLANNED.
**Evidência esperada:** testes de billing/entitlements/usage + CI.

## PHASE 18 — SECURITY / LGPD / GOVERNANCE
**Objetivo:** controles de segurança, privacidade e governança.
**Dependências:** PHASE 4 e módulos relevantes.
**Entregáveis:** controles e políticas técnicas.
**Critérios de aceitação:** evidência técnica dos controles; nenhuma declaração jurídica sem suporte.
**Estado:** PLANNED.
**Evidência esperada:** testes + revisão de segurança.

## PHASE 19 — OBSERVABILITY
**Objetivo:** logs, métricas, tracing e observabilidade de governança.
**Dependências:** PHASE 3–18 conforme eventos.
**Entregáveis:** observabilidade operacional.
**Critérios de aceitação:** sinais críticos observáveis e correlacionáveis.
**Estado:** PLANNED.
**Evidência esperada:** execução instrumentada + testes.

## PHASE 20 — PRODUCT VALIDATION
**Objetivo:** validar fluxos e aderência à proposta de produto.
**Dependências:** fases funcionais relevantes.
**Entregáveis:** validação de produto.
**Critérios de aceitação:** fluxos prioritários reproduzíveis e aceitos.
**Estado:** PLANNED.
**Evidência esperada:** testes de produto + revisão CTO.

## PHASE 21 — PRODUCTION READINESS
**Objetivo:** verificar prontidão operacional.
**Dependências:** PHASE 18–20.
**Entregáveis:** checklist operacional, segurança, observabilidade, recuperação e governança.
**Critérios de aceitação:** pacote completo de evidências e validação final.
**Estado:** PLANNED.
**Evidência esperada:** evidências de produção + aprovação CTO.

## Registro da EXECUÇÃO 02
- Escopo: auditoria integral do legado Argos e infraestrutura acessível.
- Argos: `gusborba9-star/argos-intelligence` permaneceu intocado.
- Supabase Argos: auditado em modo somente leitura; nenhuma alteração destrutiva executada.
- Vercel: inventário acessível auditado; nenhum projeto, deployment, domínio ou variável alterado.
- Classificação: REUTILIZAR / ADAPTAR / REESCREVER / DESCARTAR / PRESERVAR TEMPORARIAMENTE registrada na matriz de reutilização.
- Segurança: histórico de exposição de credenciais, API key legada, autenticação por query string, service-role usage, RLS/security-definer e Edge Function privilegiada registrados.
- Evidências: baseline Argos `a1b3c0b2d1df24008d607c7b70ee98661b60ddd0`; Veritas baseline `dd46cbd9cce89a5f730a5f953d9ca959d638b6a5`; dados Supabase observados em 2026-09-27.
- Limitações: Vercel Argos não verificado, logs Supabase não verificados, secrets não lidos e dependency audit externo não executado.
- Estado de fechamento: VALIDATED.

## Registro da EXECUÇÃO 01
- Escopo: fundação documental.
- Repositório: gusborba9-star/Veritas-OS.
- Estado inicial: repositório Git vazio.
- Arquivos funcionais: nenhum.
- Argos: fora do escopo e não alterado.
- Blueprint: criado e revisado.
- ADRs: criados e revisados.
- Roadmap: atualizado nesta mesma execução.
- Próxima etapa: PHASE 1 — ARGOS AUDIT, somente mediante nova delegação do CTO.


## Evidência de fechamento — EXECUÇÃO 01

- Validação estrutural: os 9 arquivos documentais previstos existem nos caminhos definidos.
- Validação de conteúdo: Blueprint, Roadmap e ADRs foram relidos após criação.
- Validação de escopo: não há implementação funcional do Veritas nesta execução.
- Validação de nomenclatura: estados DEFINED, PLANNED, IMPLEMENTED e VALIDATED foram distinguidos.
- Validação do Roadmap: PHASE 0 é a única fase VALIDATED; PHASE 1–21 permanecem PLANNED.
- Auditoria de diff: alterações desta execução são exclusivamente documentais dentro de docs/.
- Argos: não alterado e não incluído na execução.
- Commit de fechamento: este commit.
