---
tags:
  - databases
  - schema-design
  - data-modeling
category: Databases
related: SQL, Relationships Design, Relational vs non-Relational DBs
---

# Model Design Considerations

Database modeling is the process of deciding how business information should be stored, related, validated, and queried. A good data model balances clarity, integrity, performance, maintainability, and cost.

## Core Design Questions

Before creating tables and columns, answer:

- What facts must be stored?
- Which values must be unique or required?
- How do entities relate to each other?
- Which queries must be fast?
- Which data can be updated and which should be immutable?
- How will the data change over time?
- What are the failure and recovery expectations?

## Entity and Attribute Design

An entity is a thing of interest, such as Customer, Order, Product, or Employee. An attribute is a property of that entity.

Example:

```text
Customer
- CustomerId
- FirstName
- LastName
- Email
- CreatedAt
```

Choose attribute names that are clear, stable, and consistent. Avoid mixing business status, display formatting, and database-specific implementation details in the same column.

## Primary Keys and Surrogate Keys

A primary key identifies a row uniquely. Common approaches include:

- **Natural key** - an existing business value such as email or employee number
- **Surrogate key** - generated database ID such as `INT IDENTITY` or UUID

Surrogate keys are often easier for internal references, while natural keys may be useful when the business already defines a stable identity.

## Foreign Keys and Referential Integrity

Foreign keys create explicit relationships between tables. They help maintain consistency and can prevent orphan records.

```sql
ALTER TABLE Orders
ADD CONSTRAINT FK_Orders_Customers
FOREIGN KEY (CustomerId) REFERENCES Customers(CustomerId);
```

Use foreign keys whenever a record should only exist in relation to another valid record.

## Normalization

Normalization reduces redundancy and data anomalies by organizing data logically. It helps ensure updates and deletes do not corrupt facts or duplicate information across many rows.

Example problems addressed by normalization:

- repeated customer address info in many orders
- inconsistent naming between similar records
- updates causing conflicting versions of the same fact

Use normalization as a default design strategy, then denormalize only when performance or reporting requires it.

## Indexing

Indexes speed up lookup and retrieval patterns. They are especially valuable on columns used in:

- search filters
- joins
- ordering
- grouping

```sql
CREATE INDEX IX_Orders_CustomerId
ON Orders(CustomerId);
```

Tradeoffs:

- more indexes can slow writes
- too many indexes can increase storage and maintenance cost
- indexes should reflect actual query patterns

## Data Types and Validation

Choose data types that match the business meaning of the value.

Examples:

- `INT` for IDs and counts
- `DECIMAL(10,2)` for money values
- `DATETIME` or `TIMESTAMP` for temporal data
- `NVARCHAR` for user-visible strings
- `BIT` or boolean-like types for flags

Add validation rules with constraints, checks, and application-level validation where appropriate.

## Null Handling

`NULL` means “unknown, not provided, or not applicable.” It is not the same as zero or an empty string. Decide intentionally whether a column should permit nulls.

Good questions:

- Is this required for every record?
- Is an empty value semantically different from missing data?
- Does the application logic handle nulls consistently?

## Versioning and Schema Evolution

Schemas change over time. Plan for:

- adding columns with safe defaults
- handling old rows after a migration
- preserving backward compatibility for reading or writing
- testing upgrades against realistic data
- documenting breaking changes

## Design for Query Patterns

The best schema is usually shaped around what the application needs to ask. For example:

- a dashboard may need summary data and efficient grouping
- an ecommerce system may need orders by customer and date
- a user profile system may need fast user lookup by email

Model the schema around real access patterns and mixing concerns intentionally.

## Common Anti-Patterns

- Storing all data in one giant table
- Creating table-per-attribute without a clear need
- Duplicating business facts in multiple locations
- Using free-form text where a structured column is required
- Relying on application code instead of database constraints
- Creating indexes before measuring the workload

## Best Practices

- Start with the core entities and relationships.
- Validate against real use cases before adding complexity.
- Prefer explicit constraints to implicit assumptions.
- Review schema decisions when the system changes.
- Keep data models documented with diagrams or notes.
- Use migration tools and versioned schema changes.

## Related Concepts

- [[SQL]] - Query and define relational structures
- [[Relationships Design]] - How entities connect
- [[Relational vs non-Relational DBs]] - Choose the right data model class
- [[File IO]] - Data persistence outside the database layer
