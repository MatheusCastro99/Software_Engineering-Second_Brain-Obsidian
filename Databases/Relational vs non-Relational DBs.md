---
tags:
  - databases
  - relational
  - nosql
category: Databases
related: SQL, Relationships Design, Model design considerations
---

# Relational vs Non-Relational Databases

Databases are usually grouped into relational and non-relational systems. The difference is not only about storage format, but about how the system models data, enforces integrity, scales, and handles consistency.

## Relational Databases

Relational databases store data in tables with rows and columns. They strongly emphasize structure, relationships, consistency, and query power.

### Characteristics

- Data is modeled with tables, rows, and columns.
- Relationships are expressed through primary and foreign keys.
- Schema is usually defined upfront.
- Data integrity is enforced by constraints.
- Querying is performed with SQL.
- Commonly support ACID transactions.

### Good Fit

- Financial systems and banking
- Order processing and inventory
- Reporting and analytical workloads
- Data with clear relationships and strong validation needs

**Examples:** PostgreSQL, MySQL, SQL Server, Oracle

## Non-Relational Databases

Non-relational databases cover a broad range of database systems, often grouped under the term NoSQL. They emphasize flexibility, scale, schema evolution, and specialized access patterns.

### Common Types

| Type | Typical use | Example |
|------|-------------|---------|
| Document | JSON-like records and nested payloads | MongoDB |
| Key-value | Cache or simple lookup | Redis |
| Wide-column | Large-scale distributed data | Cassandra |
| Graph | Highly connected entities | Neo4j |
| Time series | Metrics and event streams | InfluxDB |

### Characteristics

- Flexible schemas or no fixed schema
- Often built for horizontal scaling
- Better suited for large-scale and rapidly changing data
- Trade consistency for speed and availability in some architectures
- Queries vary by database type and may be less standardized than SQL

### Good Fit

- Real-time analytics
- User activity logs
- Large event streams
- Flexible product catalogs
- Rapidly changing or semistructured data

## ACID vs BASE

### ACID

Relational databases often follow ACID principles:

- **Atomicity** - transactions succeed or fail as a unit
- **Consistency** - data remains valid after each transaction
- **Isolation** - concurrent operations do not corrupt each other
- **Durability** - committed data is not lost

This is especially valuable for financial and transactional systems.

### BASE

Many NoSQL systems lean toward BASE:

- **Basically Available** - the system remains available even under failures
- **Soft state** - data may change without explicit writes
- **Eventual consistency** - data becomes consistent over time

This favors availability and scale over immediate consistency.

## When to Choose Which

| Requirement | Prefer relational | Prefer non-relational |
|-------------|------------------|----------------------|
| Structured data with strong integrity | Yes | Sometimes |
| Complex reporting and joins | Yes | Less common |
| Fast horizontal scaling | Sometimes | Yes |
| Flexible schema changes | Less ideal | Yes |
| High write throughput | Maybe | Often |
| Strong transactional guarantees | Yes | Not always |
| Semistructured or nested documents | Less ideal | Often yes |

## Hybrid Models

Many modern systems use both relational and non-relational databases together:

- SQL database stores accounts, orders, and inventory
- Redis caches frequently accessed values
- MongoDB stores flexible document content
- Elasticsearch handles full-text search

The right architecture depends on the problem, not a one-size-fits-all rule.

## Best Practices

- Model the data to match the problem, not the database hype.
- Use relational databases when correctness and relationships matter most.
- Use NoSQL when flexibility, scale, and specialized access patterns matter more.
- Keep system boundaries explicit.
- Measure performance at realistic workloads.
- Design with observability, backup, and recovery in mind.

## Related Concepts

- [[SQL]] - Query language for relational systems
- [[Relationships Design]] - Model associations in relational data
- [[Model design considerations]] - Designing schema and data rules
- [[Cache and Redis]] - A common NoSQL-style key-value store
