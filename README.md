# yamamote
High-throughput concurrent RSS &amp; API ingestion engine in Go, powered by worker pools, PostgreSQL, Redis, and Chi.
## Overview

**Yamanote** is an idiomatic, production-grade Go service designed to handle concurrent I/O operations safely and efficiently. 

It periodically fetches JSON and RSS feeds from multiple external endpoints using a managed worker pool, processes and deduplicates records in PostgreSQL, and serves cached responses through a lightweight Chi REST API.

### Key Features & Engineering Highlights

* **Concurrent Fetch Engine:** Utilizes Goroutines and channels to implement a configurable worker pool for non-blocking I/O.
* **Resilient Network Requests:** Enforces strict HTTP timeout constraints using Go's `context` package to eliminate lingering connections.
* **Idempotent Data Ingestion:** Deduplicates payload items via SHA-256 hashing and PostgreSQL `ON CONFLICT` upsert operations.
* **High-Performance Caching:** Leverages Redis for session management and low-latency API response caching.
* **Containerized Deployment:** Multi-stage Docker build producing a minimal static binary (<20MB container footprint).

### Tech Stack

* **Language:** Go 1.22+
* **Routing:** Chi
* **Database:** PostgreSQL (`pgx` / `sqlx`)
* **Caching & Rate Limiting:** Redis
* **Infrastructure:** Docker & Docker Compose
