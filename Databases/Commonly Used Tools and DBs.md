---
tags:
  - databases
  - tools
  - dbms
category: Databases
related: SQL, Relational vs non-Relational DBs, Model design considerations
---

# Commonly Used Tools and DBs

Database tools and systems vary by workload, team size, hosting model, and operational maturity. Choosing the right database is usually a tradeoff between structure, consistency, scalability, and ease of operations.

## Relational Database Systems

### PostgreSQL

PostgreSQL is a powerful open-source relational database with strong SQL support, advanced indexing, JSON features, and a mature ecosystem. It is often used for applications that need reliability, expressive queries, and growing data complexity.

**Good for:** transaction-heavy workloads, analytics, application backends, API-backed systems

### MySQL

MySQL is widely adopted for web workloads and is commonly used in traditional LAMP and cloud-hosted stacks. It is straightforward to deploy and familiar in many production environments.

**Good for:** web applications, CRUD-heavy systems, small to medium enterprise workloads

### SQL Server

Microsoft SQL Server is a relational database commonly used in enterprise and .NET-heavy environments. It integrates well with Microsoft tooling, security features, and enterprise reporting systems.

**Good for:** enterprise apps, Windows environments, integration-heavy business systems

### SQLite

SQLite is a lightweight file-based database embedded within applications. It is easy to use for local development, prototypes, small tools, and offline applications.

**Good for:** local apps, testing, simple internal tools, mobile or desktop local storage

## NoSQL and Alternative Databases

### MongoDB

MongoDB stores JSON-like documents and is popular for flexible schema modeling, rapid iteration, and document-centric workloads.

**Good for:** flexible product documents, content stores, catalogs, rapidly evolving APIs

### Redis

Redis is an in-memory key-value store commonly used as a cache, session store, or lightweight message broker. It focuses on speed and simple access patterns.

**Good for:** caching, rate limiting, session storage, real-time counters, queue-like patterns

### Cosmos DB

Azure Cosmos DB is a globally distributed database service that supports multiple data models and offers multi-region replication features.

**Good for:** global applications, low-latency access, multi-region distribution, large-scale user data

### Elasticsearch

Elasticsearch is optimized for search and analytics on text-heavy data. It is commonly used alongside a relational or operational database.

**Good for:** search, logs, observability, faceted retrieval, text-heavy indexing

## Database Administration Tools

| Tool | Purpose |
|------|---------|
| SSMS | SQL Server management and query tooling |
| pgAdmin | PostgreSQL administration |
| MySQL Workbench | MySQL schema and query management |
| Azure Data Studio | Cross-platform database management and SQL tooling |
| DBeaver | Multi-database client for many systems |
| MongoDB Compass | MongoDB schema and query exploration |
| Redis Insight | Redis monitoring and data browsing |

## Database Selection Checklist

Before choosing a database, evaluate:

- data shape and structure
- expected scale and concurrency
- read-write patterns and latency requirements
- consistency requirements
- reporting and querying complexity
- backup, disaster recovery, and operational cost
- security and access model
- team expertise and tooling support

## Common Architectural Pattern

```text
Application -> API -> Relational DB or NoSQL store
                       \-> Cache (Redis)
                       \-> Search index (Elasticsearch)
```

The best architecture often combines multiple systems rather than relying on one database for every problem.

## Best Practices

- Use the simplest database that satisfies the requirement.
- Separate storage concerns from presentation concerns.
- Define backups, restore plans, and retention policies.
- Measure actual query performance before adding more indexes or layers.
- Design security and access controls from the start.
- Keep operational knowledge and runbooks close to the system.

## Related Concepts

- [[SQL]] - Query language for relational databases
- [[Relational vs non-Relational DBs]] - Compare database classes
- [[Model design considerations]] - Schema design fundamentals
- [[Relationships Design]] - Define database associations
- [[Cache and Redis]] - Fast in-memory data access layer
