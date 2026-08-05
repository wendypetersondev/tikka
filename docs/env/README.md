# Environment Variable Catalog

Central reference for every environment variable read across the Tikka workspace.
Use this to answer "which service needs `SUPABASE_URL`?" without grepping through source.

**Jump to:**
- [Shared infrastructure (.env)](#0-shared-infrastructure-env)
- [Backend](#1-backend-port-3001)
- [Indexer](#2-indexer-port-3002)
- [Oracle](#3-oracle-port-3003)
- [Client (Vite)](#4-client-vite-port-5173)

> **Sources of truth** (these files define what is actually read):
> - Backend → `backend/src/config/env.schema.ts` · `backend/src/config/env.config.ts`
> - Indexer → `indexer/src/config/database.config.ts` + scattered `process.env` / `ConfigService.get` calls
> - Oracle → `oracle/src/config/config.loader.ts`
> - Client → `client/src/config/env.ts`

---

## 0. Shared infrastructure (`.env`)

Used by `docker-compose.yml` for the Postgres container. Copy `.env.example` → `.env`.

| Variable | Required | Default | Description |
|---|---|---|---|
| `POSTGRES_USER` | No | `tikka` | Postgres superuser name |
| `POSTGRES_PASSWORD` | No | `tikka-pass` | Postgres superuser password |
| `POSTGRES_DB` | No | `tikka` | Default database created on first start |

---

## 1. Backend (port 3001)

Copy `backend/.env.example` → `backend/.env.local`.
Full source: [`backend/src/config/ENV_VARS.md`](../../backend/src/config/ENV_VARS.md)

### Server

| Variable | Required | Default | Description |
|---|---|---|---|
| `PORT` | No | `3001` | HTTP listen port |
| `NODE_ENV` | No | `development` | Node environment (`development`, `production`, `test`) |
| `MAINTENANCE_MODE` | No | `false` | Toggles maintenance-mode guard (returns 503) |
| `SWAGGER_ENABLED` | No | `false` | Expose Swagger UI in non-development environments |

### Supabase

| Variable | Required | Default | Description |
|---|---|---|---|
| `SUPABASE_URL` | **Yes** | — | Supabase project base URL |
| `SUPABASE_SERVICE_ROLE_KEY` | **Yes** | — | Service-role key for server-side calls (secret) |
| `SUPABASE_DB_URL` | No | — | Full Postgres URI — used by `scripts/backup.sh` only |

### Stellar

| Variable | Required | Default | Description |
|---|---|---|---|
| `STELLAR_NETWORK` | No | `testnet` | `testnet` or `mainnet`; drives Horizon/contract defaults |
| `STELLAR_HORIZON_URL` | No | Network default | Override Horizon RPC URL |
| `STELLAR_CONTRACT_ID` | No | Network default | Override on-chain raffle contract address |

### Indexer (internal)

| Variable | Required | Default | Description |
|---|---|---|---|
| `INDEXER_URL` | Auto | Network default | Base URL of the indexer service (auto-filled from `STELLAR_NETWORK` when empty) |
| `INDEXER_TIMEOUT_MS` | No | `5000` | HTTP timeout for indexer calls (ms) |

### Redis

| Variable | Required | Default | Description |
|---|---|---|---|
| `REDIS_URL` | No | `""` | Redis connection URL; empty string disables metadata cache-aside |
| `METADATA_CACHE_TTL_SECONDS` | No | `600` | TTL for cached raffle_metadata rows (seconds) |

### Auth — JWT + SIWS

| Variable | Required | Default | Description |
|---|---|---|---|
| `JWT_SECRET` | **Yes** | — | ≥ 32 character signing secret (secret) |
| `JWT_EXPIRES_IN` | No | `7d` | Access-token lifetime (e.g. `1h`, `7d`) |
| `JWT_REFRESH_EXPIRES_IN` | No | `30d` | Refresh-token lifetime |
| `SIWS_DOMAIN` | No | `tikka.io` | Domain shown in Sign-In With Stellar challenge message |
| `SIWS_NONCE_TTL_SECONDS` | No | `300` | Nonce validity window (seconds) |

### Admin

| Variable | Required | Default | Description |
|---|---|---|---|
| `ADMIN_TOKEN` | **Yes** | — | Bearer token for `/admin/*` endpoints (secret) |
| `ADMIN_IP_ALLOWLIST` | No | `""` | Comma-separated CIDR ranges; empty = allow all IPs |

### Frontend / CORS

| Variable | Required | Default | Description |
|---|---|---|---|
| `VITE_FRONTEND_URL` | **Yes** | — | Frontend origin used for CORS (`http://localhost:5173` locally) |
| `SITE_URL` | No | `VITE_FRONTEND_URL` | Public site URL for OG meta-tag rendering |

### Push Notifications (FCM)

| Variable | Required | Default | Description |
|---|---|---|---|
| `FCM_ENABLED` | No | `false` | Enable Firebase Cloud Messaging |
| `FCM_SERVICE_ACCOUNT_JSON` | No | — | Inline JSON service-account credentials |
| `FCM_SERVICE_ACCOUNT_PATH` | No | — | File path to service-account JSON |

### IPFS / Pinata

| Variable | Required | Default | Description |
|---|---|---|---|
| `ENABLE_IPFS_PINNING` | No | `false` | Pin raffle metadata to IPFS via Pinata |
| `PINATA_JWT` | No | — | Pinata JWT (preferred auth) |
| `PINATA_API_KEY` | No | — | Pinata API key (legacy auth) |
| `PINATA_API_SECRET` | No | — | Pinata API secret (legacy auth) |
| `IPFS_GATEWAY_URL` | No | `https://ipfs.io/ipfs/` | IPFS gateway base URL for redirect links |

### Geolocation / Blocking

| Variable | Required | Default | Description |
|---|---|---|---|
| `GEO_PROVIDER_URL` | No | `http://ip-api.com/json` | IP-to-country lookup provider base URL |
| `GEO_TIMEOUT_MS` | No | `3000` | Geo lookup HTTP timeout (ms) |
| `BLOCKED_COUNTRIES` | No | `""` | Comma-separated ISO 3166-1 alpha-2 codes to block |

### Rate Limiting

| Variable | Required | Default | Description |
|---|---|---|---|
| `THROTTLE_DEFAULT_LIMIT` | No | `100` | Default requests per window (all public endpoints) |
| `THROTTLE_DEFAULT_TTL` | No | `60` | Default window size (seconds) |
| `THROTTLE_AUTH_LIMIT` | No | `5` | Auth endpoint request limit |
| `THROTTLE_AUTH_TTL` | No | `900` | Auth endpoint window (seconds) — 15 min |
| `THROTTLE_NONCE_LIMIT` | No | `10` | Nonce endpoint request limit |
| `THROTTLE_NONCE_TTL` | No | `60` | Nonce endpoint window (seconds) |
| `RAFFLE_CREATE_RATE_LIMIT` | No | `5` | Raffle creation limit per wallet |
| `RAFFLE_CREATE_RATE_WINDOW_SECONDS` | No | `600` | Raffle creation window (seconds) |

### Backfill

| Variable | Required | Default | Description |
|---|---|---|---|
| `BACKFILL_MAX_RANGE` | No | `10000` | Maximum ledger range per backfill run |
| `BACKFILL_RETRY_COUNT` | No | `3` | Retries per failed ledger fetch |
| `BACKFILL_RETRY_DELAY_MS` | No | `1000` | Fixed delay between retries (ms) |
| `BACKFILL_HORIZON_TIMEOUT_MS` | No | `10000` | Horizon request timeout for backfill (ms) |

### Backup (scripts only)

| Variable | Required | Default | Description |
|---|---|---|---|
| `R2_BUCKET_NAME` | No | — | Cloudflare R2 bucket name |
| `R2_ACCESS_KEY_ID` | No | — | R2 access key ID (secret) |
| `R2_SECRET_ACCESS_KEY` | No | — | R2 secret access key (secret) |
| `R2_ENDPOINT_URL` | No | — | R2 S3-compatible endpoint URL |

### Sentry

| Variable | Required | Default | Description |
|---|---|---|---|
| `SENTRY_DSN` | No | — | Sentry DSN; omit to disable Sentry entirely |
| `SENTRY_TRACES_SAMPLE_RATE` | No | `0.1` | Transaction sample rate (0–1) |

### Logging

| Variable | Required | Default | Description |
|---|---|---|---|
| `LOG_REDACT_FIELDS` | No | Built-in list | Comma-separated field names to redact from request logs |

---

## 2. Indexer (port 3002)

Copy `indexer/.env.example` → `indexer/.env.local`.

### Database

| Variable | Required | Default | Description |
|---|---|---|---|
| `DATABASE_URL` | **Yes*** | — | Full Postgres connection URL (preferred over individual vars) |
| `DB_HOST` | No | `localhost` | Postgres host (used when `DATABASE_URL` is unset) |
| `DB_PORT` | No | `5432` | Postgres port |
| `DB_USERNAME` | No | `postgres` | Postgres user |
| `DB_PASSWORD` | No | `postgres` | Postgres password |
| `DB_DATABASE` | No | `tikka_indexer` | Database name |
| `DB_SSL` | No | `false` | Set `true` to enable SSL (required on Supabase / Railway) |
| `DATABASE_REPLICA_URL` | No | — | Comma-separated read-replica URLs; enables master/slave replication |
| `SLOW_QUERY_THRESHOLD_MS` | No | `200` | Log queries slower than this threshold (ms) |

> *`DATABASE_URL` is required unless all `DB_*` individual vars are set.

### Redis

| Variable | Required | Default | Description |
|---|---|---|---|
| `REDIS_HOST` | No | `localhost` | Redis host (used by webhook queue and cache) |
| `REDIS_PORT` | No | `6379` | Redis port |

### Stellar / Blockchain

| Variable | Required | Default | Description |
|---|---|---|---|
| `HORIZON_URL` | No | `https://horizon.stellar.org` | Stellar Horizon SSE endpoint for ledger streaming |
| `TIKKA_CONTRACT_ID` | **Yes** | — | Deployed Tikka raffle contract address to index |
| `SOROBAN_RPC_URL` | No | — | Soroban RPC endpoint (set in `.env.example`; used for event decoding) |

### Ingestion Tuning

| Variable | Required | Default | Description |
|---|---|---|---|
| `INGESTION_BATCH_SIZE` | No | `25` | Max Soroban events processed per DB transaction |
| `REORG_SAFETY_DEPTH` | No | `5` | Ledgers to look back when checking for chain reorgs |

### Health & Alerting

| Variable | Required | Default | Description |
|---|---|---|---|
| `LAG_THRESHOLD` | No | `100` | Ledger lag above this is reported as `degraded` |
| `INDEXER_LAG_ALERT_THRESHOLD_LEDGERS` | No | `50` | Ledger lag above this triggers a critical alert |

### API / Security

| Variable | Required | Default | Description |
|---|---|---|---|
| `PORT` | No | `3002` | HTTP listen port |
| `NODE_ENV` | No | `development` | Node environment |
| `INTERNAL_API_KEY` | No | — | Bearer token protecting internal API endpoints; Swagger UI shown when set |

### Supabase (Oracle audit logs)

| Variable | Required | Default | Description |
|---|---|---|---|
| `SUPABASE_URL` | No | — | Supabase project URL (required when oracle audit log API is enabled) |
| `SUPABASE_SERVICE_ROLE_KEY` | No | — | Service-role key for Supabase access (secret) |

### Snapshots / S3

| Variable | Required | Default | Description |
|---|---|---|---|
| `SNAPSHOT_STORAGE_URL` | No | — | S3/MinIO URL for snapshot uploads/downloads |
| `AWS_REGION` | No | `us-east-1` | AWS (or MinIO) region |
| `AWS_ACCESS_KEY_ID` | No | `minioadmin` | AWS / MinIO access key ID (secret) |
| `AWS_SECRET_ACCESS_KEY` | No | — | AWS / MinIO secret key (secret) |

### Maintenance Tasks

| Variable | Required | Default | Description |
|---|---|---|---|
| `DRY_RUN` | No | `false` | Log DB operations without committing (useful for CI/CD and archive tasks) |
| `RAFFLE_EVENTS_RETENTION_DAYS` | No | `30` | Days to retain raffle events before archival |
| `BATCH_SIZE` | No | `500` | Rows per batch in archival/maintenance tasks |
| `MAX_BATCH` | No | — | Hard cap on total batches processed in one archival run |
| `MAX_DISPATCH_RETRIES` | No | `3` | Max retry attempts for event dispatch |
| `BASE_RETRY_DELAY_MS` | No | `500` | Base delay for exponential backoff on dispatch retries (ms) |

---

## 3. Oracle (port 3003)

Copy `oracle/.env.example` → `oracle/.env.local`.

### Server

| Variable | Required | Default | Description |
|---|---|---|---|
| `PORT` | No | `3003` | HTTP listen port |
| `NODE_ENV` | No | `development` | Node environment (`development`, `production`, `test`) |

### Stellar Network

| Variable | Required | Default | Description |
|---|---|---|---|
| `SOROBAN_RPC_URL` | **Yes** | `https://soroban-testnet.stellar.org` | Soroban RPC endpoint for contract interaction |
| `SOROBAN_RPC_FALLBACK_URLS` | No | `""` | Comma-separated fallback RPC URLs |
| `HORIZON_URL` | No | `https://horizon-testnet.stellar.org` | Horizon endpoint for SSE event streaming |
| `NETWORK_PASSPHRASE` | No | `Test SDF Network ; September 2015` | Stellar network passphrase |
| `RAFFLE_CONTRACT_ID` | **Yes** | — | Deployed raffle contract address to listen on |

### Key Provider

| Variable | Required | Default | Description |
|---|---|---|---|
| `KEY_PROVIDER` | No | `env` | Key backend: `env`, `aws-kms`, or `gcp-kms` |
| `ORACLE_SECRET_KEY` | Cond. | — | Oracle private key — required when `KEY_PROVIDER=env` (secret) |
| `ORACLE_PRIVATE_KEY` | Cond. | — | Alias for `ORACLE_SECRET_KEY` (secret) |
| `AWS_REGION` | Cond. | — | AWS region — required when `KEY_PROVIDER=aws-kms` |
| `AWS_KMS_KEY_ID` | Cond. | — | KMS key ARN/ID — required when `KEY_PROVIDER=aws-kms` (secret) |
| `GCP_PROJECT_ID` | Cond. | — | GCP project — required when `KEY_PROVIDER=gcp-kms` |
| `GCP_LOCATION_ID` | No | `global` | GCP KMS location |
| `GCP_KEY_RING_ID` | Cond. | — | KMS key ring — required when `KEY_PROVIDER=gcp-kms` |
| `GCP_KEY_ID` | Cond. | — | KMS key name — required when `KEY_PROVIDER=gcp-kms` (secret) |
| `GCP_KEY_VERSION` | No | `1` | KMS key version |

### Queue (Redis / Bull)

| Variable | Required | Default | Description |
|---|---|---|---|
| `REDIS_HOST` | No | `localhost` | Redis host for job queue |
| `REDIS_PORT` | No | `6379` | Redis port |
| `QUEUE_MAX_RETRIES` | No | `3` | Max job retry attempts |
| `QUEUE_INITIAL_BACKOFF_MS` | No | `2000` | Initial retry backoff (ms) |
| `QUEUE_BACKOFF_MULTIPLIER` | No | `2` | Exponential backoff multiplier |
| `QUEUE_MAX_BACKOFF_MS` | No | `60000` | Maximum retry backoff (ms) |
| `QUEUE_CONFIRMATION_TIMEOUT_MS` | No | `300000` | Transaction confirmation timeout (ms) |
| `QUEUE_MAX_CONCURRENCY` | No | `5` | Max concurrent job workers |
| `QUEUE_GENERATION_TIMEOUT_MS` | No | `30000` | VRF/PRNG generation timeout (ms) |
| `QUEUE_SUBMISSION_TIMEOUT_MS` | No | `120000` | Contract submission timeout (ms) |

### VRF

| Variable | Required | Default | Description |
|---|---|---|---|
| `VRF_THRESHOLD_XLM` | No | `500` | Prize amount (XLM) above which VRF is used instead of PRNG |

### Circuit Breaker

| Variable | Required | Default | Description |
|---|---|---|---|
| `ORACLE_CB_FAILURE_THRESHOLD` | No | `5` | Consecutive Horizon SSE failures before circuit opens |
| `ORACLE_CB_RESET_TIMEOUT_MS` | No | `60000` | Time the circuit stays open before allowing a probe (ms) |

### Priority Queue

| Variable | Required | Default | Description |
|---|---|---|---|
| `ORACLE_HIGH_VALUE_THRESHOLD_XLM` | No | `10000` | Prize ≥ this XLM → HIGH priority (Bull priority 1) |
| `ORACLE_MED_VALUE_THRESHOLD_XLM` | No | `1000` | Prize ≥ this XLM → MEDIUM priority; must be < high threshold |

### Fees

| Variable | Required | Default | Description |
|---|---|---|---|
| `ORACLE_MAX_FEE_STROOPS` | No | `100000000` | Max transaction fee in stroops (10 XLM) |
| `ORACLE_MIN_FEE_STROOPS` | No | `100` | Min transaction fee in stroops |
| `LOW_STAKES_THRESHOLD_XLM` | No | `500` | Prize below this XLM uses minimum fee strategy |

### Transaction Submission

| Variable | Required | Default | Description |
|---|---|---|---|
| `TX_SUBMIT_MAX_ATTEMPTS` | No | `5` | Max submission attempts per transaction |
| `TX_SUBMIT_INITIAL_BACKOFF_MS` | No | `1000` | Initial backoff before retry (ms) |
| `TX_SUBMIT_ALERT_WEBHOOK_URL` | No | — | Webhook URL called on repeated submission failures |

### Multi-Oracle (Advanced)

| Variable | Required | Default | Description |
|---|---|---|---|
| `ORACLE_MODE` | No | `single` | `single` or `multi` |
| `MULTI_ORACLE_ENABLED` | No | `false` | Enable multi-oracle consensus mode |
| `LOCAL_ORACLE_ID` | No | — | This oracle's ID in the multi-oracle registry |
| `ORACLE_REGISTRY` | No | — | Oracle registry endpoint |
| `ORACLE_PEERS` | No | — | Comma-separated peer oracle endpoints |
| `ORACLE_SECRETS` | No | — | Peer authentication secrets (secret) |
| `MULTI_ORACLE_THRESHOLD` | No | — | Minimum agreeing oracles; defaults to majority |
| `ORACLE_MULTI_TIMEOUT_MS` | No | `10000` | Consensus timeout (ms) |

### Supabase (Audit Logs)

| Variable | Required | Default | Description |
|---|---|---|---|
| `SUPABASE_URL` | No | — | Supabase project URL (required when audit logging is enabled) |
| `SUPABASE_SERVICE_ROLE_KEY` | No | — | Service-role key (secret) |
| `SUPABASE_ANON_KEY` | No | — | Anon key (fallback to service-role key) |

### Alerting

| Variable | Required | Default | Description |
|---|---|---|---|
| `ALERTING_PROVIDER` | No | `none` | `none`, `pagerduty`, or `opsgenie` |
| `PAGERDUTY_ROUTING_KEY` | Cond. | — | Required when `ALERTING_PROVIDER=pagerduty` (secret) |
| `OPSGENIE_API_KEY` | Cond. | — | Required when `ALERTING_PROVIDER=opsgenie` (secret) |
| `ALERT_WEBHOOK_URL` | No | — | Generic webhook URL for alerts |

### Heartbeat

| Variable | Required | Default | Description |
|---|---|---|---|
| `HEARTBEAT_INTERVAL_MS` | No | `3600000` | How often to emit a heartbeat (ms; default 1 h) |
| `HEARTBEAT_ALERT_TIMEOUT_MS` | No | `90000` | Alert if no heartbeat received within this window (ms) |

### Event Listener

| Variable | Required | Default | Description |
|---|---|---|---|
| `EVENT_LISTENER_INITIAL_RETRY_DELAY` | No | `1000` | Initial reconnect delay on SSE disconnect (ms) |
| `EVENT_LISTENER_MAX_RETRY_DELAY` | No | `60000` | Max reconnect delay (ms) |
| `ORACLE_DRAW_REQUEST_REPLAY` | No | `false` | Replay missed draw-request events on startup |

### Logging

| Variable | Required | Default | Description |
|---|---|---|---|
| `LOG_LEVEL` | No | `info` | `error`, `warn`, `info`, `debug`, or `verbose` |
| `LOG_DIR` | No | `./logs` | Directory for log file output |
| `LOG_TO_CONSOLE` | No | `true` | Echo logs to stdout |
| `LOG_MAX_SIZE` | No | `20m` | Max log file size before rotation |
| `LOG_MAX_FILES` | No | `14d` | Max log file age before deletion |
| `LOG_ZIPPED_ARCHIVE` | No | `true` | Gzip rotated log files |

---

## 4. Client / Vite (port 5173)

Copy `client/.env.example` → `client/.env.local`. All variables **must** be prefixed with `VITE_` to be exposed to the browser bundle.

### Backend API

| Variable | Required | Default | Description |
|---|---|---|---|
| `VITE_API_BASE_URL` | No | `http://localhost:3001` | Backend API base URL |
| `VITE_ADMIN_TOKEN` | No | — | Admin token for the oracle monitor dashboard (must match backend `ADMIN_TOKEN`) |

### Stellar Network

| Variable | Required | Default | Description |
|---|---|---|---|
| `VITE_STELLAR_NETWORK` | No | `testnet` | `testnet` or `mainnet` |
| `VITE_STELLAR_HORIZON_URL` | No | `https://horizon-testnet.stellar.org` | Horizon API URL |
| `VITE_STELLAR_NETWORK_PASSPHRASE` | No | `Test SDF Network ; September 2015` | Network passphrase |
| `VITE_HORIZON_URL` | No | `VITE_STELLAR_HORIZON_URL` | Alias used by `stellar.ts`; prefer `VITE_STELLAR_HORIZON_URL` |

### Soroban / Contract

| Variable | Required | Default | Description |
|---|---|---|---|
| `VITE_SOROBAN_RPC_URL` | No | `https://soroban-testnet.stellar.org` | Soroban RPC URL for contract reads |
| `VITE_RAFFLE_CONTRACT_ADDRESS` | No | — | Deployed raffle contract address (required for any on-chain interaction) |
| `VITE_CONTRACT_DEPLOYMENT_HASH` | No | — | Deployment transaction hash (informational) |

### Supabase

| Variable | Required | Default | Description |
|---|---|---|---|
| `VITE_SUPABASE_URL` | No | — | Supabase project URL (required for metadata display) |
| `VITE_SUPABASE_ANON_KEY` | No | — | Supabase anon/public key (safe to expose in browser) |
| `VITE_SUPABASE_TABLE` | No | `raffle_metadata` | Supabase table for raffle metadata |

### Wallet

| Variable | Required | Default | Description |
|---|---|---|---|
| `VITE_DEFAULT_WALLET` | No | `freighter` | Default wallet provider (`freighter`, `albedo`, `xbull`) |
| `VITE_WALLET_AUTO_CONNECT` | No | `false` | Auto-connect wallet on page load |

### Application

| Variable | Required | Default | Description |
|---|---|---|---|
| `VITE_APP_ENV` | No | `development` | `development`, `staging`, or `production` |
| `VITE_SITE_URL` | No | `http://localhost:5173` | Public site URL for OG / Twitter Card absolute URLs |
| `VITE_DEBUG_MODE` | No | `true` | Enable verbose browser console logging |
| `VITE_API_TIMEOUT` | No | `30000` | API request timeout (ms) |

### Feature Flags

| Variable | Required | Default | Description |
|---|---|---|---|
| `VITE_FEATURE_LEADERBOARD` | No | `true` | Show the leaderboard UI |
| `VITE_FEATURE_SOCIAL_SHARE` | No | `true` | Enable social-share buttons |
| `VITE_FEATURE_EMAIL_NOTIFICATIONS` | No | `false` | Enable email notification opt-in |

### Observability

| Variable | Required | Default | Description |
|---|---|---|---|
| `VITE_GA_MEASUREMENT_ID` | No | — | Google Analytics GA4 measurement ID |
| `VITE_SENTRY_DSN` | No | — | Sentry DSN for browser error tracking |

### IPFS (future)

| Variable | Required | Default | Description |
|---|---|---|---|
| `VITE_IPFS_GATEWAY` | No | — | IPFS gateway base URL for image display |
| `VITE_PINATA_API_KEY` | No | — | Pinata API key for client-side pinning |
| `VITE_PINATA_SECRET_KEY` | No | — | Pinata secret key (secret) |

### Development

| Variable | Required | Default | Description |
|---|---|---|---|
| `VITE_USE_DEMO_DATA` | No | `false` | Use mock/demo data instead of real backend |
| `VITE_SHOW_DEV_TOOLS` | No | `true` | Show dev tooling overlays |

---

## Cross-service variable map

Variables shared across multiple services — set consistently or you'll get mismatches.

| Variable | Backend | Indexer | Oracle | Client | Notes |
|---|---|---|---|---|---|
| `SUPABASE_URL` | ✅ Required | ✅ Required | Optional | `VITE_SUPABASE_URL` | Same Supabase project |
| `SUPABASE_SERVICE_ROLE_KEY` | ✅ Required | ✅ Required | Optional | — | Server-side only, never in browser |
| `REDIS_HOST` / `REDIS_PORT` | `REDIS_URL` (URL form) | ✅ | ✅ | — | Point to same Redis instance |
| `SOROBAN_RPC_URL` | — | Optional | ✅ Required | `VITE_SOROBAN_RPC_URL` | Can differ per environment |
| `HORIZON_URL` | `STELLAR_HORIZON_URL` | Optional | Optional | `VITE_STELLAR_HORIZON_URL` | — |
| `NODE_ENV` | ✅ | ✅ | ✅ | `VITE_APP_ENV` | — |
| `PORT` | `3001` | `3002` | `3003` | (Vite default `5173`) | Must not collide |
