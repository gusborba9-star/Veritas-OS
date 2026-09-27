# Veritas OS — Infrastructure Audit

**Audit date:** 2026-09-27  
**Scope:** Argos legacy infrastructure only  
**Rule:** read-only audit; no destructive operation performed.

## 1. Supabase

### 1.1 Project

- Project: `argos-intelligence`
- Project ref: `mhdwqskmkyhtpwusgikc`
- Region: `sa-east-1`
- Status: `ACTIVE_HEALTHY`
- PostgreSQL: 17.x / release channel GA
- Created: 2026-05-22

### 1.2 Database inventory

The live public schema contains:

- **33 base tables**
- **0 public views**
- **182 public functions**
- **1 non-internal public trigger**
- **12 public RLS policies**

All 33 listed public tables currently have RLS enabled.

Observed row-bearing tables include Argos matches, queue, signals, anomaly logs, team form, processed score events, API budgets, payments, user tiers and delivery tracking.

The largest observed relation is `argos_batch_queue`, approximately 36.4 MiB at audit time. The listed public relations together occupy approximately **43.6 MiB** by the queried relation-size snapshot.

### 1.3 Auth

Read-only query observed:

- `auth.users`: **0 users**.

Detailed Auth configuration was not exposed by the connected audit surface.

**Status:** PARTIAL.

### 1.4 Storage

Read-only query returned **no Storage buckets**.

**Status:** AUDITED.

### 1.5 Edge Functions

One active Edge Function was found:

- `argos-http-worker`
- version 15
- status ACTIVE
- `verify_jwt=false`

Its source uses the Supabase service-role key and executes an outbound request based on `job.url` from `argos_http_queue`.

Security implications:

- unauthenticated function endpoint;
- privileged database client;
- arbitrary outbound destination sourced from database state;
- request-body echo in one error path.

**Recommendation:** do not reuse this function. If an outbound worker is required in Veritas, design a new worker with explicit authorization, destination allowlisting, SSRF protection, least privilege and structured auditing.

### 1.6 Extensions

The database has a large extension footprint. Relevant installed extensions include:

- `pgcrypto`;
- `plpgsql`;
- `vector`;
- `pg_cron`;
- `pg_net`;
- `pg_stat_statements`;
- `pgsodium`;
- `postgis`;
- `pgmq`;
- `pg_graphql`;
- `supabase_vault`;
- `pgaudit`;
- `http`;
- `pg_jsonschema`;
- and many additional available/uninstalled extensions.

This is substantially broader than a minimal Veritas foundation should assume.

**Recommendation:** preserve the project during this audit, but do not inherit the extension footprint. A future cleanup/restructure should retain only extensions justified by approved Veritas capabilities.

### 1.7 Migrations

The live project reports migrations from July through September 2026, including v7/v8/v9 pipeline changes, RLS enablement, queue/cron hardening, team-form and score-event infrastructure, anomaly logging, API-Football budgets, signal provenance, standings infrastructure and cron.

This confirms an evolving legacy schema rather than a clean baseline.

**Classification:** PRESERVAR TEMPORARIAMENTE.

### 1.8 RLS/security findings

Supabase security advisors reported multiple `SECURITY DEFINER` functions executable by the `authenticated` role, including Argos dispatch/cron-related functions.

Performance/security advisors also reported:

- unindexed foreign keys;
- RLS auth init-plan warnings;
- multiple permissive policies;
- 33 unused indexes;
- a duplicate index.

The audit did not modify any of these findings.

**Recommendation:** before any reuse, perform a dedicated security/schema restructuring pass under CTO approval.

### 1.9 Data state

The database contains live Argos records, including:

- 24 `argos_matches`;
- 34 `argos_batch_queue`;
- 35 `argos_signal_ledger`;
- 22k+ `argos_anomaly_log` records;
- 1,089 `argos_team_form` records;
- 1,448 `argos_processed_score_events`;
- 619 `argos_api_football_teams`;
- 31 `argos_api_football_leagues`.

This is non-trivial legacy state.

**Recommendation:** do not reset or drop anything during this execution.

### 1.10 Supabase action matrix

| Resource | Exists? | Current use | Argos dependency | Veritas value | Action |
|---|---|---|---|---|---|
| Project | Yes | Argos DB/backend | Total | Infrastructure only | PRESERVAR |
| Public tables | 33 | Betting pipeline | Total | Schema patterns only | RESTRUCTURE |
| RLS | Yes | Argos access | High | High conceptually | REWRITE |
| RPCs | Yes | Queue/dispatch/cron | Total | Low | REPLACE |
| Extensions | Many | Mixed | High | Selective | RESTRUCTURE |
| Auth | Yes / 0 users | Legacy auth surface | High | High conceptually | RESTRUCTURE |
| Storage | No buckets | None observed | None | Potential future | DO NOT TOUCH |
| Edge Function | 1 | HTTP worker | Total | Generic worker pattern only | REPLACE |
| Realtime | Not verified | NOT VERIFIED | NOT VERIFIED | Potential | NOT VERIFIED |
| Logs | Query attempted; backend error | NOT VERIFIED | NOT VERIFIED | High | NOT VERIFIED |
| Secrets/Vault values | Values not exposed | NOT VERIFIED | High | High | DO NOT EXPOSE / CTO review |

## 2. Vercel

### 2.1 Accessible account inventory

The connected Vercel team is `Gustavo Borba 's projects`.

Only one project was returned:

- `velor-api`
- project id: `prj_xQDty1690tXrnIWH4IIHOOXWF7CG`

Its deployment metadata points to repository `gusborba9-star-Horus-`, not `gusborba9-star/argos-intelligence`.

Therefore the accessible Vercel account does **not** provide evidence of an Argos-linked Vercel project.

### 2.2 Deployments

The listed `velor-api` deployments include READY/CANCELED states and production targets, but their Git metadata is tied to the Horus repository and Arena Forge-related commits.

These deployments are outside this Argos audit.

### 2.3 Argos Vercel status

| Resource | State | Argos dependency | Reuse possible | Action |
|---|---|---|---|---|
| Argos Vercel project | NOT VERIFIED | Unknown | Unknown | CTO verification required |
| Argos production domain | NOT VERIFIED | Unknown | Unknown | CTO verification required |
| Argos environment variables | NOT VERIFIED | Unknown | Unknown | CTO verification required |
| Argos integrations | NOT VERIFIED | Unknown | Unknown | CTO verification required |
| Argos deployment history | NOT VERIFIED | Unknown | Unknown | CTO verification required |
| Accessible `velor-api` | AUDITED but unrelated | Horus | None established | DO NOT TOUCH |

No Vercel project, domain, deployment, variable or integration was deleted or modified.

## 3. GitHub

### 3.1 Argos repository

- Repository: `gusborba9-star/argos-intelligence`
- Visibility: private
- Default branch: main
- HEAD: `a1b3c0b2d1df24008d607c7b70ee98661b60ddd0`
- Tree inventory: 124 blobs
- Main branch protection: disabled in accessible metadata.

### 3.2 Workflow

`.github/workflows/argos-validation.yml` validates pull requests with Node 20, npm install, TypeScript check, production build and Vitest quantitative suite.

The workflow is useful as a process pattern, not as a Veritas implementation.

### 3.3 GitHub secrets

Repository secret values were not accessible through the audit surface.

Source/history search did confirm a historical secret exposure incident. Values are intentionally not reproduced.

**Status:** configuration values NOT VERIFIED; historical exposure CONFIRMED.

### 3.4 GitHub action matrix

| Resource | State | Argos dependency | Reuse possible | Action |
|---|---|---|---|---|
| Repository | Active | Total | Evidence only | PRESERVAR |
| Main branch | Active/unprotected | Total | Process lesson | ADAPTAR |
| Validation workflow | Present | Medium | Yes | ADAPTAR |
| Repository secrets | Values inaccessible | Unknown | Unknown | NOT VERIFIED |
| Documentation | Present | High | Evidence | PRESERVAR TEMPORARIAMENTE |
| Source tree | Present | High | Generic patterns only | AUDIT / no migration |

## 4. Environment/configuration audit

Observed environment variables include Supabase credentials, Google AI, sports data provider keys, Argos internal API key, Telegram credentials, Upstash Redis credentials, Efí credentials/certificate and NBA API key.

The current source references environment variables in many places, but the historical `.env` incident demonstrates that configuration hygiene was not consistently safe over the project lifetime.

**Rule for Veritas:** no Argos environment file, secret name, credential, endpoint or provider configuration is copied automatically.

## 5. Infrastructure recommendation

```
CURRENT ARGOS INFRA
        ↓
KEEP LIVE DURING AUDIT
        ↓
SEPARATE DATA / SECURITY / DOMAIN BOUNDARIES
        ↓
CONTROLLED CLEANUP
        ↓
RESTRUCTURE ONLY AFTER CTO APPROVAL
        ↓
VERITAS INFRASTRUCTURE
```

For the Supabase free-tier constraint, reusing the existing project may be technically possible, but **only after** domain isolation, schema replacement strategy, security review, data-retention decision and rollback/backup plan are approved.

The audit does not authorize cleanup.

## 6. Infrastructure limitations

- Vercel Argos project was not exposed by the connected account.
- Supabase Realtime state was not independently verified.
- Supabase log query failed at backend level; logs remain NOT VERIFIED.
- Secret values and administrative credentials were not inspected.
- No backup/restore test was executed.
- No destructive operation was performed.
