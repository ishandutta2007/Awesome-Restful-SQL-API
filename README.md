# Awesome-Restful-SQL-API

# Top RESTful SQL API Ecosystem

**Curated List of SaaS Products & Open-Source GitHub Projects**  
*Focused on Auto-Generated REST Endpoints, Schema Introspection & Self-Hosted SQL-to-API Gateways*  
**Last updated: November 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **RESTful SQL APIs**. These tools enable developers to expose SQL databases as RESTful endpoints—automatically generating CRUD APIs, handling authentication, and enforcing row-level security—without writing custom backend code for every table.

**Examples** include Snowflake SQL API, PostgREST, Hasura Cloud, Supabase REST API, Prisma Accelerate, Cube Cloud SQL API, AWS Data API for Aurora, SurrealDB Cloud, SingleStore Data API, and ClickHouse HTTP API (the category leaders).

**Open-source emphasis**: RESTful SQL API is a domain where open-source tooling is **exceptionally mature and production-proven**, with clear leaders for different philosophies. **PostgREST** remains the gold standard for PostgreSQL—a single binary that turns your schema directly into a RESTful API, with permissions and constraints in the database determining endpoints and operations . **Faucet** is the most compelling modern alternative, supporting **seven databases** (PostgreSQL, MySQL, MariaDB, SQL Server, Oracle, Snowflake, SQLite) from a single Go binary with a built-in admin UI, OpenAPI 3.1 spec, RBAC, row-level security filters, and a **built-in MCP server for AI agents** . **Supabase REST API** builds on PostgREST to provide auto-generated APIs with Postgres Row Level Security, realtime subscriptions, and a managed platform . The critical caveat: **PostgREST is PostgreSQL-only**, while **Faucet trades PostgREST's database-native purity for multi-database breadth**—and neither matches the managed convenience of Snowflake's SQL API or AWS Data API for Aurora, which handle infrastructure, scaling, and credential management for you .

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents
- [SaaS/Hosted Platforms](#saas-products)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **[Snowflake SQL API](https://docs.snowflake.com/en/developer-guide/sql-api/about-endpoints)**  
  REST API for submitting SQL statements to Snowflake and retrieving results; endpoints include `/api/v2/statements/` for submission, `statementHandle` for status checking, and `statementHandle/cancel` for cancellation . Removes concurrency limits, enabling multi-threaded result retrieval . **Best for Snowflake-native applications** wanting programmatic SQL execution without a driver—but it is a query execution API, not an auto-generated CRUD layer over your schema.

- **[PostgREST (Managed Hosting)](https://postgrest.org/)**  
  While PostgREST itself is open-source, managed hosting is available through platforms like Supabase and various PaaS providers.

- **[Hasura Cloud](https://hasura.io/)**  
  Managed GraphQL engine (not REST-first) that connects to databases and provides a unified GraphQL API; includes caching, monitoring, and enterprise features . **Note**: Hasura is **GraphQL-first**, not REST—included for context as the most prominent instant-API alternative.

- **[Supabase REST API](https://supabase.com/docs/guides/api)**  
  Auto-generated RESTful API built on PostgREST, exposed at `https://<project_ref>.supabase.co/rest/v1/` . **Instant and auto-generated** from your database schema; **self-documenting** via the Dashboard; **secure** with Postgres Row Level Security and API gateway key-auth; **fast** (300%+ faster than Firebase for basic reads per Supabase benchmarks); **scalable** for serverless workloads . Supports CRUD, arbitrary relationships, views, materialized views, foreign tables, and Postgres functions . **Best for teams wanting a managed, batteries-included Postgres API** with auth, storage, and realtime alongside REST.

- **[Prisma Accelerate](https://www.prisma.io/)**  
  Managed connection pool and global cache for Prisma ORM (formerly Data Proxy); provides up to 1000x faster queries with 5ms latency via distributed caching in ~280 locations . **Not a REST API generator**—it optimizes Prisma queries, not auto-generates endpoints from schemas.

- **[Cube Cloud SQL API](https://cube.dev/)**  
  SQL API within Cube's semantic layer; Cube Core is open-source (17,000+ GitHub stars), while Cube Cloud provides managed hosting . **Best for teams wanting a semantic layer** over SQL databases rather than raw CRUD.

- **[AWS Data API for Aurora](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/data-api.html)**  
  HTTP-based API for Aurora Serverless v1 (not v2); executes SQL without persistent database connections; credentials stored in Secrets Manager with IAM tag-based access control . **Best for serverless AWS-native applications**—but limited to Aurora Serverless v1 and requires IAM/Secrets Manager configuration.

- **[SurrealDB Cloud](https://surrealdb.com/)**  
  Managed SurrealDB with HTTP API at `/sql`; query via SurrealQL with bearer token auth, namespace/database headers, and JSON responses . **Best for teams using SurrealDB's multi-model database**—not a general SQL-to-REST gateway.

- **[SingleStore Data API](https://docs.singlestore.com/)**  
  Built-in HTTP server for executing SQL; `/ping` for health checks, `/query/rows` for queries via POST with JSON body and basic auth . **Best for SingleStore users** wanting HTTP SQL execution.

- **[ClickHouse HTTP API](https://clickhouse.com/)**  
  Native HTTP interface on port 8123 (or 8443 for HTTPS); query via HTTP POST with SQL in the body . **Best for ClickHouse users** wanting direct HTTP SQL access—not an auto-generated CRUD layer.

## Open-Source GitHub Projects

### PostgreSQL-Native REST APIs

- **[PostgREST](https://github.com/PostgREST/postgrest)**  
  The **gold standard for PostgreSQL-to-REST** (MIT). A standalone web server that turns your PostgreSQL database directly into a RESTful API—**the structural constraints and permissions in the database determine the API endpoints and operations** . **Philosophy**: database as single source of truth; declarative programming (let Postgres join data and enforce permissions rather than writing imperative code); leak-proof abstraction (no ORM involved) . Used in production by Catarse, Drip Depot, Image-charts, and Supabase . **Best for PostgreSQL teams wanting database-native API generation**—but it is PostgreSQL-only, has no built-in admin UI, and requires understanding Postgres roles/grants to secure endpoints.

### Multi-Database REST APIs (PostgREST Alternatives)

- **[Faucet](https://github.com/faucetdb/faucet)**  
  The most compelling **multi-database REST API generator** (MIT, single Go binary ~22MB). Supports **seven databases**: PostgreSQL, MySQL, MariaDB, SQL Server, Oracle, Snowflake, and SQLite . Features: **full CRUD REST API** with filtering, ordering, and pagination; **OpenAPI 3.1 spec** auto-generated at `/openapi.json`; **RBAC** with per-table verb permissions and **row-level security filters**; **built-in admin UI** (Preact + Tailwind) with schema explorer and API tester; **embedded MCP server** (8 tools + 2 resources) for Claude, Cursor, and other AI agents—governed by the same RBAC rules . **Configuration stored in embedded SQLite**—no external database required . Install via `npx @faucetdb/faucet`, Homebrew, Docker, or `go install` . **Best for teams wanting PostgREST-like capabilities across heterogeneous databases**—but it is newer than PostgREST and the admin UI is embedded rather than a separate platform.

### GraphQL-First (Adjacent)

- **[Hasura GraphQL Engine](https://github.com/hasura/graphql-engine)**  
  Open-source GraphQL engine (Apache 2.0) that makes data instantly accessible over GraphQL; connects to databases, REST, and GraphQL endpoints to provide a unified, real-time, secured API . **Not REST-first**—included for context as the most prominent instant-API alternative. Community Edition available via Docker; Cloud and Enterprise editions add managed infrastructure and observability .

### Additional Strong Open-Source Options

- **DreamFactory** — Open-source (Apache 2.0) REST API platform for many SQL and NoSQL sources; PHP/Laravel application with web admin app . **Best for teams wanting a broader enterprise API platform**—but it is a PHP application rather than a single binary.
- **Supabase (self-hosted)** — The open-source Supabase stack (Postgres, PostgREST, GoTrue auth, Realtime, Storage) can be self-hosted via Docker; the managed Supabase REST API is built on PostgREST . **Best for teams wanting the full Supabase experience** with auth and realtime—but it is a multi-service stack, not a single-purpose API gateway.

**Frameworks for building custom systems**: For **PostgreSQL-native REST with database-enforced permissions**, PostgREST is the mature standard . For **multi-database REST with an admin UI and MCP support**, Faucet provides the broadest coverage . For **GraphQL instead of REST**, Hasura . For **managed Postgres API with auth and realtime**, Supabase . No open-source project matches the **managed infrastructure and credential management** of Snowflake SQL API or AWS Data API for Aurora—those handle scaling and security for you .

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- RESTful SQL API gateways expose database access over HTTP; **security misconfiguration can expose entire tables or allow unauthorized writes**—row-level security, RBAC, and API key management are critical. Faucet's security notes explicitly warn that role rules were historically stored but not enforced for API-key requests in older versions—verify you are running a version that enforces RBAC .
- **Open-source RESTful SQL APIs are mature for PostgreSQL and emerging for multi-database**—PostgREST is battle-tested , and Faucet provides broad database support with MCP for AI agents . However, **no open-source project matches the managed infrastructure and credential management** of Snowflake SQL API or AWS Data API for Aurora—organizations requiring managed convenience should evaluate commercial platforms.
- Verify license terms for commercial use; PostgREST uses MIT , Faucet uses MIT , and Hasura GraphQL Engine uses Apache 2.0 .

---

**Made for backend developers, platform engineers, and teams building data APIs.**  
Let's make RESTful SQL APIs more open, but with clear eyes about the security configuration and managed infrastructure trade-offs that define each path.
