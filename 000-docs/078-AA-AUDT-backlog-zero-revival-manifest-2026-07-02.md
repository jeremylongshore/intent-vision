# Backlog Zero — intentvision dormant-backlog settle & revival manifest

| Field | Value |
|---|---|
| **Campaign** | Backlog Zero, Wave 0 (dormant-repo settle) |
| **Date** | 2026-07-02 |
| **Repo** | `jeremylongshore/intent-vision` (dormant; last commit 2026-04-30) |
| **Scout provenance** | Read-only scout ran 2026-07-02 (66 open + 1 in_progress confirmed; estimated split 26 still-valid / 16 done-drift / 15 obsolete / 9 needs-human). Every scout verdict was re-verified against files on disk, git history, PRs, and AARs before any write. |
| **Runner** | db mutation-runner (skeptic pass + settle), 2026-07-02 |
| **Revival epic** | `intentvision-3pt` — "Revive or archive intentvision: settle the dormant backlog and decide the project's future" |

## Outcome

All 67 non-closed beads settled: **36 closed with evidence**, **20 deferred to 2026-10-01**, **11 kept open as needs-human**. End state: the only open beads are the revival epic and the needs-human items.

Skeptic-pass corrections to the scout's estimate:

- **More done-drift than estimated (24 vs ~16).** The TimeGPT circuit-breaker cluster, the Agent Engine CI workflows + AAR, the Phase F productization AAR, and the prod-secrets runbook (`intentvision-mgn.1`, the in_progress bead — its PR #6 content is fully subsumed by main via the PR #7 squash) all turned out shipped.
- **Scout's "AAR tasks need Jeremy" partly refuted** — the Phase D and Phase F AARs exist on disk (`000-docs/060`, `000-docs/062`), so those beads closed.
- **RTO/RPO definition deferred, not needs-human** — nothing to approve while dormant; stakeholder approval is flagged for revival.
- **Minor:** scout's quick-win path `packages/api/src/billing/usage-report.ts` is actually `packages/api/src/scripts/usage-report.ts`.

## Settled beads (all 67)

| Bead | Title | Disposition | Evidence / state |
|---|---|---|---|
| `intentvision-p88.1` | 4.1 Implement Firestore SaaS control plane schema and helpers | **closed** | Shipped in commit 9c52b3b (2025-12-15): packages/api/src/firestore/schema.ts (572 lines; Organization plan/slug, Source, DailyUsage SaaS types) + firestore/client.ts. AAR 000-docs/034-AA-AACR-phase-4-saas-control-plane-api-v1.md. |
| `intentvision-p88.2` | 4.2 Implement API key authentication middleware | **closed** | Shipped in commit 9c52b3b: packages/api/src/auth/api-key.ts (294 lines; scoped key system ingest:write / metrics:read / alerts:*). AAR 000-docs/034. |
| `intentvision-p88.3` | 4.3 Implement Public API v1 endpoints (events, forecasts, alerts) | **closed** | Shipped in commit 9c52b3b: packages/api/src/routes/v1.ts (428 lines) + routes/alerts.ts (1024 lines) + routes/me.ts + routes/internal.ts. AAR 000-docs/034. |
| `intentvision-p88.4` | 4.4 Implement Resend email alerts with user-configurable channels | **closed** | Shipped in commit 9c52b3b: packages/api/src/notifications/resend.ts (450 lines) + resend-client.ts with user-configurable channels; routes/preferences.ts. AARs 000-docs/034 + 039. |
| `intentvision-p88.5` | 4.5 Create API documentation | **closed** | Shipped: packages/api/docs/API.md (532 lines, commit 9c52b3b) + packages/api/openapi.yaml (946 lines) + src/scripts/validate-openapi.ts. |
| `intentvision-p88.6` | 4.6 Create Phase 4 AAR document | **closed** | Shipped: 000-docs/034-AA-AACR-phase-4-saas-control-plane-api-v1.md exists on origin/main (added in commit 9c52b3b). |
| `intentvision-uxb` | Phase 8: Notification Preferences + Multi-Channel Alerts (Epic) | **closed** | Shipped: 000-docs/039-AA-AACR-phase-8-notification-preferences-multi-channel-alerts.md + 040-DR-ADRC-notification-preferences-alert-routing.md; packages/api/src/notifications/resend.ts + routes/preferences.ts implement user-configurable multi-channel alerts. |
| `intentvision-7d5` | Phase 12: Stripe client stub | **closed** | Shipped: packages/api/src/billing/stripe-client.ts (236-line Stripe abstraction with stub implementation). AAR 000-docs/048-AA-AACR-phase-12-billing-plumbing.md. |
| `intentvision-uvj` | Phase 12: Billing CLI script | **closed** | Shipped: packages/api/src/scripts/billing-snapshot.ts (175-line CLI). AAR 000-docs/048. |
| `intentvision-uhc` | Phase 12: Usage snapshots model | **closed** | Shipped: BillingSnapshot type + billingSnapshots collection in packages/api/src/firestore/schema.ts; packages/api/src/scripts/usage-report.ts. AAR 000-docs/048. |
| `intentvision-8k8` | Phase 12: Owner billing UI | **closed** | Shipped: packages/web/src/pages/BillingPage.tsx (file header: "Phase 12: Owner Billing UI" - plan, usage, billing history). AAR 000-docs/048. |
| `intentvision-62k` | Phase 13: Environment config | **closed** | Shipped: packages/api/src/config/environment.ts (three-tier dev/staging/prod config). AAR 000-docs/050-AA-AACR-phase-13-production-deployment.md. |
| `intentvision-c0s` | Phase 13: Observability | **closed** | Shipped: packages/api/src/observability/metrics.ts (request/forecast/alert metrics collector). AAR 000-docs/050 documents logging/error-reporting/uptime setup. |
| `intentvision-c79` | Phase 13: Firebase hosting | **closed** | Shipped: firebase.json hosting config at repo root, wired to packages/web. AAR 000-docs/050. |
| `intentvision-nra` | Phase 13: CI/CD pipeline | **closed** | Shipped: .github/workflows/ci.yml (build/test/deploy pipeline) + arv-gate.yaml. AAR 000-docs/050. Cron schedules later disabled in commit 386817c; pipeline code remains on main. |
| `intentvision-xyq.4` | F.4 Configure secrets in Secret Manager | **closed** | Shipped: AAR 000-docs/056-AA-AACR-phase-f-cloud-deployment.md marks F.4 completed (ci.yml unified to GCP_WIF_PROVIDER/GCP_SA_EMAIL); Terraform Secret Manager resources merged via PR #4 (commit 59fb07b). |
| `intentvision-9xh.1` | D.1 Add CI steps to build and deploy ADK app to Agent Engine | **closed** | Shipped: .github/workflows/agent-engine-deploy.yml + a2a-gateway-deploy.yml + adk/service/a2a_gateway/ Dockerfile.cloudrun + cloudbuild.yaml. AAR 000-docs/060-AA-AACR-phase-d-cicd-arv.md. |
| `intentvision-9xh.3` | D.3 AAR + docs update for agent deployment | **closed** | Shipped: 000-docs/060-AA-AACR-phase-d-cicd-arv.md is the Phase D AAR + docs update (status FINAL). |
| `intentvision-mpr.3` | F.3 Final AAR summarizing agent integration and roadmap | **closed** | Shipped: 000-docs/062-AA-AACR-phase-f-productization.md (status FINAL) summarizes the ADK integration Phases A-F incl. A2A gateway client + chat routes. |
| `intentvision-4hi.1` | (api) Implement circuit breaker | **closed** | Shipped: CircuitBreaker class in packages/pipeline/src/connections/nixtla-client.ts (configurable circuitBreakerThreshold / circuitBreakerResetMs, 5-failure/30s default); statistical fallback in packages/api/src/forecast/backend-router.ts. |
| `intentvision-4hi.2` | (api) Surface clear error modes | **closed** | Shipped: packages/api/src/forecast/backend-router.ts returns backend + rationale (fallback warning) in responses; ForecastMetric.backend in packages/api/src/observability/metrics.ts tracks per-backend usage. |
| `intentvision-4hi.3` | (api) Metering for TimeGPT calls | **closed** | Shipped: DailyUsage.nixtla counter ("Nixtla/TimeGPT backend calls") in packages/api/src/firestore/schema.ts; canUseTimegpt()/timegptEnabled plan gating in packages/api/src/services/usage-service.ts. |
| `intentvision-4hi` | intentvision/resilience: TimeGPT circuit breaker | **closed** | All three children closed with on-disk evidence (circuit breaker, error modes, metering): nixtla-client.ts, backend-router.ts, metrics.ts, schema.ts, usage-service.ts - see child close reasons. |
| `intentvision-mgn.1` | (ops) Prod secrets creation + naming | **closed** | Shipped to main: 000-docs/065-AT-RNBK-secrets-management.md on origin/main (landed via PR #7 squash b91c911); SOPS+age standard (.sops.yaml, .env.sops) on main; Secret Manager Terraform merged PR #4. PR #6 content fully subsumed (git diff origin/main..HEAD shows only deletions) - recommend closing PR #6 unmerged. |
| `intentvision-91n.1` | G.1 Create apps/ directory structure | **closed** | Obsolete, never adopted: no apps/ dir exists on main; repo permanently kept packages/ layout and added infrastructure/ (PRs #3/#4/#5), adk/, services/ instead. Parent epic intentvision-91n already closed. Plan preserved at 000-docs/028-AT-ARCH-target-scaffold-phase-g.md. |
| `intentvision-91n.2` | G.2 Migrate packages/api to apps/api | **closed** | Obsolete: packages/api was never moved and remains the live API home (packages/api/src/routes, auth, firestore). Phase G apps/ restructure never adopted (no apps/ dir on main; parent epic closed). |
| `intentvision-91n.3` | G.3 Create apps/web dashboard scaffold | **closed** | Superseded: dashboard shipped at packages/web (React+Vite; pages/DashboardPage, AlertsPage, SettingsPage, BillingPage) instead of apps/web. apps/ restructure never adopted. |
| `intentvision-91n.4` | G.4 Create packages/sdk-js client SDK | **closed** | Superseded: customer SDK shipped as packages/sdk (listed in CLAUDE.md as the customer-facing TypeScript SDK) instead of packages/sdk-js. Restructure never adopted. |
| `intentvision-91n.5` | G.5 Reorganize scripts/ directory | **closed** | Obsolete: scripts/ kept its flat layout (scripts/ci/arv-check.sh pattern); the planned ci/dev/ops reorg was never adopted (parent epic closed). |
| `intentvision-91n.6` | G.6 Create infra/ deployment configs | **closed** | Superseded: deployment config landed as infrastructure/ Terraform (commits 04dc382, 59fb07b, 7bf219c via PRs #3/#4/#5) + firebase.json at root, not the planned infra/ layout. |
| `intentvision-91n.7` | G.7 Configure Firebase Hosting for web app | **closed** | Superseded: firebase.json exists at repo root configured for packages/web (Phase 13, AAR 000-docs/050), not apps/web. |
| `intentvision-91n.8` | G.8 Update root workspace and imports | **closed** | Obsolete: root package.json workspaces still packages/*; no apps/* workspace was ever added (restructure never adopted). |
| `intentvision-91n.9` | G.9 Update and verify all tests | **closed** | Obsolete: test-migration task for a restructure that never happened; tests and imports still live under packages/*. |
| `intentvision-91n.10` | G.10 Update CI/CD for new structure | **closed** | Obsolete: CI was built for the packages/ layout instead (ci.yml, arv-gate.yaml, agent-engine-deploy.yml); no apps/-based CI ever needed. |
| `intentvision-91n.11` | G.11 Update documentation and CLAUDE.md | **closed** | Obsolete: CLAUDE.md and README document the packages/ monorepo as built; there is no Phase G structure to document (restructure never adopted, parent epic closed). |
| `intentvision-91n.12` | G.12 Cleanup deprecated packages/functions | **closed** | Obsolete: packages/functions still exists in the workspace as built; this cleanup was scoped to the abandoned apps/ restructure (parent epic intentvision-91n closed). |
| `intentvision-51b` | intentvision/loadtest: Load testing and tuning | **deferred → 2026-10-01** | Still valid, no code evidence on disk; revisit on revival. |
| `intentvision-51b.1` | (test) Execute Baseline profile | **deferred → 2026-10-01** | Still valid, no code evidence on disk; revisit on revival. |
| `intentvision-51b.2` | (test) Execute Growth profile | **deferred → 2026-10-01** | Still valid, no code evidence on disk; revisit on revival. |
| `intentvision-51b.3` | (ops) Firestore index audit | **deferred → 2026-10-01** | Still valid, no code evidence on disk; revisit on revival. Note: written against GCP (Firestore/Cloud Run/Cloud Monitoring) - re-scope to the VPS platform on revival. |
| `intentvision-51b.4` | (ops) Cloud Run tuning | **deferred → 2026-10-01** | Still valid, no code evidence on disk; revisit on revival. Note: written against GCP (Firestore/Cloud Run/Cloud Monitoring) - re-scope to the VPS platform on revival. |
| `intentvision-945` | intentvision/dr: Disaster recovery and backups | **deferred → 2026-10-01** | Still valid, no code evidence on disk; revisit on revival. |
| `intentvision-945.1` | (ops) Define RTO/RPO and document | **deferred → 2026-10-01** | Still valid, no code evidence on disk; revisit on revival. RTO/RPO stakeholder approval will be needed at revival. |
| `intentvision-945.2` | (ops) Firestore scheduled exports | **deferred → 2026-10-01** | Still valid, no code evidence on disk; revisit on revival. Note: written against GCP (Firestore/Cloud Run/Cloud Monitoring) - re-scope to the VPS platform on revival. |
| `intentvision-945.3` | (ops) Firestore restore procedure test | **deferred → 2026-10-01** | Still valid, no code evidence on disk; revisit on revival. Note: written against GCP (Firestore/Cloud Run/Cloud Monitoring) - re-scope to the VPS platform on revival. |
| `intentvision-945.4` | (ops) Turso backup/restore documentation | **deferred → 2026-10-01** | Still valid, no code evidence on disk; revisit on revival. |
| `intentvision-aas` | intentvision/observability: Monitoring and alerting baseline | **deferred → 2026-10-01** | Still valid, no code evidence on disk; revisit on revival. |
| `intentvision-aas.1` | (api) Verify logging standards | **deferred → 2026-10-01** | Still valid, no code evidence on disk; revisit on revival. |
| `intentvision-aas.2` | (ops) Create Cloud Monitoring dashboard | **deferred → 2026-10-01** | Still valid, no code evidence on disk; revisit on revival. Note: written against GCP (Firestore/Cloud Run/Cloud Monitoring) - re-scope to the VPS platform on revival. |
| `intentvision-aas.3` | (ops) Configure alert policies | **deferred → 2026-10-01** | Still valid, no code evidence on disk; revisit on revival. Note: written against GCP (Firestore/Cloud Run/Cloud Monitoring) - re-scope to the VPS platform on revival. |
| `intentvision-aas.4` | (ops) Integrate Error Reporting | **deferred → 2026-10-01** | Still valid, no code evidence on disk; revisit on revival. Note: written against GCP (Firestore/Cloud Run/Cloud Monitoring) - re-scope to the VPS platform on revival. |
| `intentvision-c2y` | intentvision/webtests: Web package test coverage | **deferred → 2026-10-01** | Still valid, no code evidence on disk; revisit on revival. |
| `intentvision-c2y.1` | (test) Add test framework to packages/web | **deferred → 2026-10-01** | Still valid, no code evidence on disk; revisit on revival. |
| `intentvision-c2y.2` | (test) Add smoke tests (render, routes) | **deferred → 2026-10-01** | Still valid, no code evidence on disk; revisit on revival. |
| `intentvision-c2y.3` | (ci) Add web tests to CI | **deferred → 2026-10-01** | Still valid, no code evidence on disk; revisit on revival. |
| `intentvision-xyq.3` | F.3 Set up Turso Cloud database | **deferred → 2026-10-01** | Still valid, no code evidence on disk; revisit on revival. Turso Cloud provisioning per AAR 000-docs/056 (F.3 pending). |
| `intentvision-mgn` | intentvision/prod-cutover: Enable production deployment | **needs-human** | Prod-cutover epic targets GCP Cloud Run + WIF; prod hosting moved to the Contabo VPS 2026-05-01 (GCP exodus). Keep or kill? Recommended default: obsolete under GCP exodus; re-scope deploy to the VPS stack if the project revives. Decision by 2026-07-16. |
| `intentvision-mgn.2` | (ci) Verify WIF auth for prod deploy | **needs-human** | WIF auth verification is GCP-only - keep or drop under the GCP exodus? Recommended default: obsolete; a VPS deploy would use the Tailscale OIDC pattern instead. Decision by 2026-07-16. |
| `intentvision-mgn.3` | (ci) Audit and harden deploy-prod job | **needs-human** | deploy-prod job hardening targets Cloud Run - harden or retire? Recommended default: obsolete under GCP exodus; re-scope to a VPS deploy workflow on revival. Decision by 2026-07-16. |
| `intentvision-mgn.4` | (ci) Add smoke-prod job | **needs-human** | smoke-prod job presupposes the Cloud Run deploy - keep? Recommended default: obsolete under GCP exodus; re-create against the VPS deploy on revival. Decision by 2026-07-16. |
| `intentvision-mgn.5` | (ops) Rollback drill + documentation | **needs-human** | Rollback drill is written against Cloud Run traffic-splitting - keep? Recommended default: obsolete under GCP exodus; re-scope the rollback drill to the VPS pattern on revival. Decision by 2026-07-16. |
| `intentvision-xyq.5` | F.5 Deploy to Cloud Run | **needs-human** | Deploy to Cloud Run never happened (AAR 000-docs/056 lists F.5 pending) - do it or drop under the GCP exodus? Recommended default: obsolete; deploy to the VPS if the project revives. Decision by 2026-07-16. |
| `intentvision-9xh` | Phase D: Agent Engine Deployment | **needs-human** | Epic blocked on one remaining child (Agent Engine E2E verify, GCP-bound); CI workflows + AAR already shipped. Close as done-except-GCP? Recommended default: close once 9xh.2 is ruled obsolete under the GCP exodus. Decision by 2026-07-16. |
| `intentvision-9xh.2` | D.2 Verify E2E: HTTP -> Agent Engine -> IntentVision | **needs-human** | E2E verification HTTP -> Vertex AI Agent Engine -> IntentVision was never evidenced - pursue or drop? Recommended default: obsolete under GCP exodus (Agent Engine is GCP-only); re-scope agent hosting on revival. Decision by 2026-07-16. |
| `intentvision-mpr` | Phase F: ADK Productization | **needs-human** | Epic's remaining children (Agent Assist pricing, customer user journeys) await business decisions - hold open or defer the cluster? Recommended default: defer to revival once the children are ruled. Decision by 2026-07-16. |
| `intentvision-mpr.1` | F.1 Feature flags and pricing for Agent Assist | **needs-human** | Feature flags + pricing for Agent Assist is a business/pricing decision - set pricing now or shelve? Recommended default: shelve until revival; no pricing while dormant. Decision by 2026-07-16. |
| `intentvision-mpr.2` | F.2 User journey definition: how customers see/use agents | **needs-human** | Customer-facing agent user-journey definition is a product decision - define now or at revival? Recommended default: defer to revival. Decision by 2026-07-16. |

## In-flight residue

- **`intentvision-mgn.1` (was `in_progress`)** — "(ops) Prod secrets creation + naming". Closed with evidence: `000-docs/065-AT-RNBK-secrets-management.md` is on `origin/main` (landed via the PR #7 squash `b91c911`), the SOPS+age standard (`.sops.yaml`, `.env.sops`) is on main, and the Secret Manager Terraform merged via PR #4 (`59fb07b`).
- **Working tree** — the repo checkout sits on stale branch `feature/intentvision-mgn.1-prod-secrets` (not switched by this settle). Dirty state at settle time: deleted `.beads/dolt-monitor.pid.lock`; untracked `.beads/export-state.json`, `packages/*/tsconfig.tsbuildinfo`, `packages/web/vite.config.{js,d.ts}`; `.beads/issues.jsonl` modified by this settle (the updated copy is committed on this manifest branch).
- **Open PRs** (`gh pr list`):
  - **PR #6** — "[Task: intentvision-mgn.1] Prod secrets + rotation runbook" (open since 2026-02-03). `git diff origin/main..feature/intentvision-mgn.1-prod-secrets` shows only deletions (main is ahead) — the PR's content is fully subsumed. **Recommend: close unmerged.**
  - **PR #1** — "Phase 11: Usage metering + strict PR workflow" (open since 2026-01-30). Phase 11 shipped via later commits (AAR `000-docs/045-AA-AACR-phase-11-usage-metering.md`). **Recommend: close unmerged.**

## Needs-human digest (decision by 2026-07-16)

Context: production hosting moved to the Contabo VPS on 2026-05-01 and GCP is under exodus review, so pure-GCP deploy work is obsolete-as-written unless Jeremy re-platforms it.

| Bead | Question | Recommended default |
|---|---|---|
| `intentvision-mgn` (epic) | Prod cutover targets GCP Cloud Run + WIF — keep or kill? | Obsolete under GCP exodus; re-scope deploy to the VPS stack if the project revives |
| `intentvision-mgn.2` | WIF auth verification (GCP-only) — keep? | Obsolete; a VPS deploy would use the Tailscale OIDC pattern |
| `intentvision-mgn.3` | Harden Cloud Run deploy-prod job? | Obsolete; re-scope to a VPS deploy workflow on revival |
| `intentvision-mgn.4` | smoke-prod job (presupposes Cloud Run deploy)? | Obsolete; re-create against the VPS deploy on revival |
| `intentvision-mgn.5` | Rollback drill (Cloud Run traffic-splitting)? | Obsolete; re-scope to the VPS pattern on revival |
| `intentvision-xyq.5` | Deploy to Cloud Run (never done; AAR 056 lists F.5 pending)? | Obsolete; deploy to the VPS if the project revives |
| `intentvision-9xh` (epic) | Close as done-except-GCP (workflows + AAR shipped)? | Close once 9xh.2 is ruled obsolete |
| `intentvision-9xh.2` | E2E verify against Vertex AI Agent Engine (never evidenced)? | Obsolete (Agent Engine is GCP-only); re-scope agent hosting on revival |
| `intentvision-mpr` (epic) | Remaining children are business decisions — hold or defer? | Defer to revival once the children are ruled |
| `intentvision-mpr.1` | Set Agent Assist feature flags + pricing now? | Shelve until revival; no pricing while dormant |
| `intentvision-mpr.2` | Define customer-facing agent user journeys now? | Defer to revival |

Also awaiting Jeremy (not beads): close stale PRs #1 and #6 unmerged (see In-flight residue).
