# Veritas OS — Argos Reuse Matrix

**Audit baseline:** `gusborba9-star/argos-intelligence@a1b3c0b2d1df24008d607c7b70ee98661b60ddd0`

> Classification describes suitability for Veritas. It does not authorize migration.

| Component | Type | Domain | Dependencies | Quality | Security | Compatibility | Classification | Justification |
|---|---|---|---|---|---|---|---|---|
| Next.js application shell | Framework | Generic | Next/React/TS | Established | Needs hardening | Potential | ADAPTAR | Useful only if Veritas selects the same stack. |
| pnpm lock/workspace pattern | Tooling | Generic | pnpm/native builds | Usable | Low | Potential | ADAPTAR | Preserve concept, regenerate dependencies independently. |
| GitHub Actions validation workflow | CI | Generic | Node/npm/Vitest | Useful | Moderate | High conceptually | ADAPTAR | Validation sequence is useful; package manager and commands must be rebuilt. |
| Vitest test gate | Testing | Generic | Vitest/TS | Useful | Low | High | REUTILIZAR | Generic test technology, subject to Veritas toolchain confirmation. |
| TypeScript strict configuration | Tooling | Generic | TypeScript | Useful | Low | High | REUTILIZAR | Generic quality control; no Argos domain dependency. |
| Next standalone deployment setting | Deployment | Generic | Next/Vercel | Useful | Low | Potential | ADAPTAR | Reuse only if selected Veritas deployment requires it. |
| Supabase client factory | Infrastructure | Generic | Supabase JS | Mixed | High privilege | High conceptually | REESCREVER | Current implementation relies on service-role credentials and Argos assumptions. |
| CircuitBreaker | Resilience | Generic pattern | TS | Useful | Low | High | REESCREVER | Pattern is valuable; implementation should be rebuilt for Veritas contracts. |
| RedisCache / Upstash abstraction | Cache | Generic | Upstash | Useful | Credential-sensitive | Potential | ADAPTAR | Cache abstraction is reusable but provider and keys must be independently designed. |
| BatchQueueService | Queue | Argos | Supabase + Argos tables | Useful concept | Privileged | Low | REESCREVER | Queue/idempotency pattern useful; schema and lifecycle are Argos-specific. |
| TelemetryService | Observability | Generic-ish | In-memory + console | Partial | Logging risk | Medium | REESCREVER | Event model is useful; needs structured, privacy-aware telemetry. |
| PredictiveMaintenanceService | Operations | Argos | Argos endpoints | Partial | Moderate | Low | DESCARTAR | Endpoint inventory is hardcoded to Argos services. |
| SelfHealingSystem | Operations/AI | Argos | Argos prediction data | Unverified | High conceptual risk | Low | DESCARTAR | Autonomous correction is not a Veritas requirement and is domain-bound. |
| EdgeGatekeeper | Auth | Argos | Argos tiers/JWT | Mixed | High | Low | DESCARTAR | Encodes FREE/VIP betting access and legacy auth semantics. |
| ArgosMasterOrchestrator | Orchestration | Betting | All Argos engines | Complex | High | None | DESCARTAR | Central betting decision engine; incompatible with Veritas boundaries. |
| FeatureEngine | Statistics | Betting | Sports history | Useful pattern | Moderate | Low | REESCREVER | Feature-pipeline separation is useful; statistical semantics are not portable. |
| ModelFactory / Monte Carlo | Modeling | Betting | Sports features | Domain-specific | High | None | DESCARTAR | Betting probability generation has no direct Veritas role. |
| FairOddsCalculator | Quantitative | Betting | Bookmakers | Domain-specific | High | None | DESCARTAR | Betting-specific. |
| OddsValueEngine | Quantitative | Betting | Odds/EV/Kelly | Domain-specific | High | None | DESCARTAR | Betting-specific. |
| MarketNormalizer | Data normalization | Betting | Bookmaker schemas | Useful pattern | Moderate | Low | REESCREVER | Normalization concept is generic; market contracts are not. |
| MarketCoverageRegistry | Domain registry | Betting | Betting verticals | Domain-specific | Moderate | None | DESCARTAR | Registry is betting-market specific. |
| SignalDistributionEngine | Delivery | Betting | Telegram/tiers | Domain-specific | High | None | DESCARTAR | Distribution semantics are Argos-specific. |
| TelegramDispatcher | Integration | Betting | Telegram bot | Domain-specific | Credential-sensitive | None | DESCARTAR | No Veritas requirement and contains betting delivery semantics. |
| ValueDeliveryService | Monetization | Betting | tiers/payments | Mixed | High | Low | REESCREVER | Entitlement concept is generic; Argos tier model is not. |
| PaymentGatewayService (Efí) | Billing | Argos | Efí PIX/Supabase | Useful integration pattern | Credential-sensitive | Medium | ADAPTAR | Payment abstraction is useful, but provider and domain rules must be rebuilt. |
| DataIngestionService | Ingestion | Betting | PropLine/Supabase/Redis | Complex | High | Low | DESCARTAR | Core purpose is sports/betting ingestion. |
| ApiFootballService | External integration | Sports | API-Football | Domain-specific | Credential-sensitive | None | DESCARTAR | No Veritas role. |
| PropLineConfigManager | Configuration | Betting | PropLine | Narrow | Credential-sensitive | None | DESCARTAR | Betting provider specific. |
| NBADataIngestionService | Ingestion | Sports | NBA API | Narrow | Credential-sensitive | None | DESCARTAR | Domain-specific. |
| RAGContextEngine | AI/RAG | Betting | Gemini + sports context | Useful pattern | High | Low | REESCREVER | Provenance/retrieval ideas may inform Veritas Evidence/Research, but implementation is betting-bound. |
| RegimeSchema / regime engine | Modeling | Betting | Sports market regime | Domain-specific | Moderate | None | DESCARTAR | Not portable. |
| ContinuousLearningEngine | ML | Betting | prediction feedback | Conceptual | High | Low | REESCREVER | Controlled evaluation/learning pattern may be useful; implementation is betting-specific. |
| AutoTuningEngine | ML | Betting | prediction history | Unverified | High | Low | DESCARTAR | Automatic tuning of betting parameters is not portable. |
| FeedbackEngine | Analytics | Betting | signal outcomes | Useful pattern | Moderate | Low | REESCREVER | Feedback loop concept is generic; data contract is not. |
| ConsensusEngine | Modeling | Betting | multiple models | Useful pattern | High | Low | REESCREVER | Ensemble/consensus can be generic, but implementation must obey Veritas deterministic-first boundaries. |
| ContextualFactorsEngine | Modeling | Betting | sports context | Domain-specific | Moderate | None | DESCARTAR | Not portable. |
| QuotaOptimizationEngine | Resource control | Argos | sports API budgets | Useful concept | Moderate | Medium | REESCREVER | Usage metering is relevant to Veritas, but the current quota semantics are provider-specific. |
| PropLineIngestionWorker | Worker | Betting | PropLine | Domain-specific | High | None | DESCARTAR | No direct Veritas value. |
| SignalSnapshotService | Cache/state | Betting | Redis + signal schema | Useful pattern | Moderate | Low | REESCREVER | Snapshot/provenance pattern can inform Veritas audit/event design. |
| Supabase SQL schema | Persistence | Betting | 33 Argos tables | High domain coupling | High | None | DESCARTAR | Do not migrate tables or naming into Veritas. |
| Supabase RPCs | Database logic | Betting | Argos tables | Mixed | High | None | DESCARTAR | Current functions are tied to Argos and include security-definer risk. |
| Supabase RLS patterns | Security | Generic-ish | Postgres Auth | Mixed | High | Medium | REESCREVER | RLS is relevant, but existing policies have documented weaknesses. |
| Supabase Edge worker | Infrastructure | Argos | service-role + arbitrary URL | Unsafe as-is | High | Low | DESCARTAR | Public JWT bypass and outbound URL execution require a complete redesign. |
| Supabase migrations | Persistence | Betting | Argos schema history | Useful as evidence only | High | None | PRESERVAR TEMPORARIAMENTE | Needed as forensic evidence; not a migration source for Veritas. |
| Argos documentation/reports | Documentation | Betting | Historical versions | Valuable as evidence | Mixed | Low | PRESERVAR TEMPORARIAMENTE | Keep intact for audit history; do not treat as Veritas authority. |
| Dashboard UI primitives | UI | Generic-ish | React/Lucide/Tailwind | Partial | Low | Medium | ADAPTAR | Generic visual patterns may help, but no direct copy is justified. |
| Argos dashboard | UI | Betting | Argos signal schema | Domain-specific | Medium | None | DESCARTAR | Product semantics are incompatible. |
| Middleware auth | Security | Betting | API keys/tiers | Weak | High | None | REESCREVER | Veritas needs scope/permission architecture from its own Blueprint. |
| `.env.example` | Configuration | Argos | provider secrets | Useful as inventory | Sensitive | Low | PRESERVAR TEMPORARIAMENTE | Variable inventory is evidence; never copy values or names blindly. |
| README / roadmap claims | Documentation | Betting | Historical state | Inconsistent | Mixed | Low | PRESERVAR TEMPORARIAMENTE | Useful for forensic chronology, not authority. |

## Classification summary

- **REUTILIZAR:** generic TypeScript strictness and Vitest technology, subject to Veritas toolchain confirmation.
- **ADAPTAR:** application shell, package tooling, CI shape, deployment settings, Redis abstraction, Efí/payment abstraction, UI patterns.
- **REESCREVER:** resilience, queueing, telemetry, Supabase client boundary, normalization pattern, entitlement concept, controlled learning/feedback/consensus patterns, quota/metering concept, snapshot/provenance pattern, RLS strategy, auth.
- **DESCARTAR:** betting engines, sports ingestion, odds/EV/Kelly, market registries, Telegram delivery, Argos orchestrator, Argos database/RPCs, Argos Edge Function, sports-specific services and betting UI.
- **PRESERVAR TEMPORARIAMENTE:** Argos migration history and documentation required as audit evidence.

No component is classified REUTILIZAR at the domain/business-logic level.
