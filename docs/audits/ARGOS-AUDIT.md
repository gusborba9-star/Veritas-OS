# Veritas OS — ARGOS Legacy Audit

**Execution:** EXECUÇÃO 02 — AUDITORIA INTEGRAL DO LEGADO E INFRAESTRUTURA  
**Phase:** PHASE 1 — ARGOS AUDIT  
**Audit date:** 2026-09-27  
**Legacy repository:** `gusborba9-star/argos-intelligence`  
**Audited branch:** `main`  
**Audited HEAD:** `a1b3c0b2d1df24008d607c7b70ee98661b60ddd0`

## 1. Objective

Determine which technical elements of the Argos legacy can reduce effort, risk, or time for Veritas OS without importing betting-domain architecture, coupling, security debt, or incompatible assumptions.

Veritas remains the architectural authority. This document is an audit, not a migration plan.

## 2. Scope

The audit covered GitHub repository metadata, the complete repository tree and commit history; application structure, APIs, libraries, dependencies, scripts, tests and configuration; Argos documentation and historical reports; GitHub Actions workflow definition and repository protection state; Supabase project, schema inventory, row counts, policies, extensions, migrations, Edge Functions and advisory findings; Supabase Auth user count and Storage bucket inventory; Vercel team/project/deployment inventory available through the connected Vercel account; environment-variable usage patterns and secret-handling risks visible in source/history; observability/logging patterns; and generic infrastructure candidates.

No destructive operation was executed.

## 3. Methodology

1. Establish immutable baseline of Veritas and Argos.
2. Inventory the complete Argos tree.
3. Inspect package/configuration/application entry points.
4. Inspect documentation inventory and core reports.
5. Search source for infrastructure/security integration patterns.
6. Inspect live Supabase metadata read-only.
7. Inspect accessible Vercel projects/deployments.
8. Classify components using REUTILIZAR / ADAPTAR / REESCREVER / DESCARTAR / PRESERVAR TEMPORARIAMENTE.
9. Record limitations instead of filling gaps with assumptions.

### Evidence baseline

- Argos contains **124 tracked blobs** at the audited HEAD.
- Main is **unprotected**; required status checks are not configured at the branch-protection endpoint.
- The audited HEAD is **unsigned**.
- Veritas HEAD before this execution: `dd46cbd9cce89a5f730a5f953d9ca959d638b6a5`.
- Veritas functional implementation remains absent.

## 4. Architecture found

Argos is a Next.js 15 / React 19 TypeScript application with a domain-specific intelligence pipeline.

```
External sports APIs
        ↓
Ingestion / discovery
        ↓
Queue / cache
        ↓
Argos orchestrator
        ↓
Feature + statistical / Monte Carlo engines
        ↓
Market normalization / value calculations
        ↓
Signal classification
        ↓
Telegram / payment / delivery
        ↓
Supabase persistence + auxiliary Redis
```

Repository inventory shows:

- `app/`: 13 files, including Argos v6 API routes and dashboard;
- `lib/`: 61 files, heavily divided between `lib/argos` and `lib/core`;
- `supabase/`: 10 SQL files;
- `tests/`: 1 explicit flow test plus unit tests under `lib/core`;
- `docs/`: 8 documentation artifacts;
- root documentation: 11 additional Markdown reports;
- TypeScript/TSX dominate the implementation.

The architecture is not a clean generic platform. Domain semantics are embedded across core services, database names, routes, middleware, configuration and persistence.

## 5. Application and API surface

Observed routes include:

- `/api/argos/v6`
- `/api/argos/v6/ingest`
- `/api/argos/v6/worker`
- `/api/argos/v6/collect-scores`
- `/api/argos/v6/collect-standings`
- `/api/argos/v6/daily-ticket`
- `/api/argos/v6/debug-sports`
- `/api/argos/v6/settle-signals`
- `/api/webhook-pix`

The API boundary is strongly coupled to Argos names, betting workflows and payment/delivery behavior.

**Veritas conclusion:** do not carry these routes or their contracts into Veritas. Generic HTTP handler patterns may be reused only as implementation inspiration.

## 6. Dependencies and tooling

The package manifest identifies Next.js, React, TypeScript, Vitest, Supabase JS, Upstash Redis, Axios, node-fetch, Google Generative AI, UUID, Tailwind/PostCSS and tsx/ts-node. The project uses pnpm lockfile/workspace conventions, while the GitHub Actions workflow still installs with `npm install` and caches npm. Historical commits document a previous npm/pnpm lockfile conflict.

**Classification:** dependency/toolchain pattern = ADAPTAR; never copy the lockfile or package manifest wholesale.

## 7. Tests

Evidence shows:

- `vitest` is declared;
- `test:quant` runs `vitest run`;
- there is a MarketNormalizer unit test;
- `tests/test_v6_flow.ts` invokes the Argos orchestrator against a mocked sports payload;
- CI performs TypeScript compilation, production build and quantitative tests.

The test architecture is useful as a pattern but the fixtures/contracts are betting-specific.

**Classification:** test/CI validation pattern = ADAPTAR.

No current independent execution of the Argos test suite was performed in this audit environment; therefore current runtime pass status is **NOT VERIFIED**.

## 8. CI/CD

Workflow `.github/workflows/argos-validation.yml` runs on pull requests to main/master and performs checkout, Node 20 setup, npm installation, TypeScript check, production build and quantitative tests.

Repository branch protection is currently disabled according to accessible branch metadata.

**Risk:** CI exists but is not sufficient by itself to enforce main-branch quality.

**Classification:** workflow structure = ADAPTAR / REESCREVER for Veritas, depending on the final Veritas toolchain.

## 9. Security findings

### 9.1 Historical secret exposure

Git history contains an explicit security commit documenting that a real `.env` had previously been tracked with service-role, sports API and Redis credentials. The commit states that historical values require manual rotation. Current tree contains `.env.example`, not the historical `.env`.

**Finding:** SECRET / CREDENTIAL FOUND — ROTATION REQUIRED.

No secret value is reproduced here.

### 9.2 Hardcoded legacy API credential

`middleware.ts` contains a legacy literal comparison for `argos_2026`.

**Risk:** a static credential remains in application source and creates unnecessary authentication debt.

**Classification:** DESCARTAR for Veritas.

### 9.3 API-key query-string authentication

Multiple Argos routes accept an API key from either a header or query parameter.

Query-string credentials can enter logs, caches, browser history and monitoring systems.

**Classification:** REESCREVER.

### 9.4 Service-role use in application code

Several server-side services create Supabase clients using `SUPABASE_SERVICE_ROLE_KEY`.

This can be valid for tightly controlled backend jobs, but the pattern must not be copied into Veritas without strict privilege boundaries.

**Classification:** REESCREVER.

### 9.5 Logging

Source searches show extensive `console.log` / `console.error` usage. Some services log operational identifiers and error payloads.

The Edge Function also returns the request body when `job_id` is missing.

**Risk:** sensitive data can enter logs or responses.

**Classification:** REESCREVER.

### 9.6 Edge Function

The active `argos-http-worker` has `verify_jwt=false` and executes a URL loaded from the database.

**Risk:** this creates a potentially privileged public HTTP execution primitive and requires strict authorization, URL allowlisting and SSRF controls.

**Classification:** DESCARTAR as-is; REESCREVER only if Veritas later requires a controlled outbound job worker.

## 10. Documentation audit

The Argos repository contains 19 Markdown documents plus an HTML blueprint artifact in the audited tree.

The documentation is extensive but internally inconsistent in maturity language. Examples include multiple documents declaring production readiness, roadmaps still containing open validation work, historical reports describing different versions and architectures, and future capabilities presented as completed in some later roadmap documents.

Therefore Argos documentation is useful as historical evidence but cannot be treated as authoritative architecture for Veritas.

**Classification:** historical documentation = PRESERVAR TEMPORARIAMENTE; Veritas source of truth = the Veritas Blueprint/Roadmap.

## 11. Technical debt

Material debt observed:

- versioned legacy modules remain side-by-side;
- duplicated ingestion/API patterns;
- domain-specific names spread through `lib/core`;
- mixed API clients and configuration patterns;
- multiple historical migration generations;
- public-role RLS policies on some tables;
- security-definer functions executable by authenticated roles according to Supabase security advisors;
- unindexed foreign keys;
- multiple permissive RLS policies;
- unused and duplicate indexes;
- hardcoded legacy API key;
- query-string authentication fallback;
- CI/tooling mismatch between pnpm and npm;
- unprotected main branch;
- stale/ambiguous documentation claims.

## 12. Generic technical value

The strongest reusable concepts are:

1. circuit breaker pattern;
2. queue processing with idempotency and retry semantics;
3. structured service boundaries;
4. deterministic calculation/test gates;
5. cache abstraction;
6. deployment/CI conventions;
7. audit/telemetry event concepts.

These should be **reimplemented or adapted**, not copied wholesale.

The betting-domain implementation itself has no direct place in Veritas.

## 13. Non-reusable components

The following are directly tied to the legacy domain and must not become Veritas functionality:

- betting signal generation;
- odds/fair-odds/EV/Kelly engines;
- market vertical registry;
- sports fixture ingestion;
- league scoring;
- bookmaker normalization;
- Telegram betting tiers;
- PropLine/API-Football betting ingestion;
- betting prediction ledger;
- betting settlement;
- Argos payment/tier logic;
- Argos-specific database schema;
- betting RAG context;
- Argos routes and middleware semantics.

## 14. Conclusions

The audit does **not** support an Argos-to-Veritas code migration.

The viable strategy is:

```
Argos infrastructure
      ↓
forensic audit
      ↓
retain evidence
      ↓
extract generic patterns
      ↓
reimplement/adapt under Veritas boundaries
      ↓
validate independently
```

The Argos Supabase project contains substantial live legacy state and must not be reset during this phase.

The accessible Vercel account does not expose a project demonstrably connected to Argos. The only listed project is `velor-api`, whose recent deployments point to `gusborba9-star-Horus-`; therefore Argos Vercel infrastructure is **NOT VERIFIED** rather than assumed.

## 15. Limitations

- Current Vercel account access did not expose an Argos-linked project; project-specific Argos environment variables, domains and deployment settings are therefore NOT VERIFIED.
- Supabase log query returned a backend error during this audit window; recent log contents are NOT VERIFIED.
- Supabase administrative secrets are not exposed by the audit tools and were not inspected by value.
- No destructive migration/reset was executed.
- No independent local build/test execution of Argos was performed.
- Dependency vulnerability scanning with a package-audit service was not executed; current vulnerability status is NOT VERIFIED.
- The audit uses the current Argos `main` HEAD and live Supabase metadata observed on 2026-09-27.

## 16. References

- [Veritas Blueprint](../blueprint/VERITAS-BLUEPRINT.md)
- [Veritas Roadmap](../roadmap/VERITAS-ROADMAP.md)
- [Reuse Matrix](./ARGOS-REUSE-MATRIX.md)
- [Infrastructure Audit](./INFRASTRUCTURE-AUDIT.md)
