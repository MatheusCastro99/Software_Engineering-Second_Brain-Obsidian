---
tags:
  - databases
  - relationships
  - schema-design
category: Databases
related: SQL, Model design considerations, Relational vs non-Relational DBs
---

# Relationships Design

Relationships describe how records in one table connect to records in another table. In relational databases, relationships are usually implemented with foreign keys and well-defined constraints.

## One-to-Many

One record in one table relates to many records in another table.

```text
Customer 1 ----< Orders
```

Example:

- One customer may have many orders.
- Each order belongs to one customer.

```sql
CREATE TABLE Customers (
    CustomerId INT PRIMARY KEY,
    Name NVARCHAR(100)
);

CREATE TABLE Orders (
    OrderId INT PRIMARY KEY,
    CustomerId INT NOT NULL,
    Total DECIMAL(10,2),
    CONSTRAINT FK_Orders_Customers FOREIGN KEY (CustomerId)
        REFERENCES Customers(CustomerId)
);
```

This is one of the most common database designs.

## Many-to-One

Many-to-one is the same relationship viewed from the child side.

```text
Many Orders -> One Customer
```

An order has one customer, while a customer may have many orders. In practice, many-to-one and one-to-many are the same structural concept described from different perspectives.

## Many-to-Many

Many-to-many relationships require a junction table.

```text
Students --< StudentCourses >-- Courses
```

Example:

- A student can enroll in many courses.
- A course can have many students.

```sql
CREATE TABLE Students (
    StudentId INT PRIMARY KEY,
    Name NVARCHAR(100)
);

CREATE TABLE Courses (
    CourseId INT PRIMARY KEY,
    Title NVARCHAR(100)
);

CREATE TABLE StudentCourses (
    StudentId INT NOT NULL,
    CourseId INT NOT NULL,
    PRIMARY KEY (StudentId, CourseId),
    FOREIGN KEY (StudentId) REFERENCES Students(StudentId),
    FOREIGN KEY (CourseId) REFERENCES Courses(CourseId)
);
```

This pattern prevents duplicate information and keeps the relationship explicit.

## One-to-One

One record in one table is associated with exactly one record in another table.

```text
User 1 -- 1 Profile
```

Use cases:

- User profile data stored separately from authentication data
- Additional metadata stored in a dedicated table
- Rare or optional large data that should not bloat the main table

## Self-Referencing Relationships

A table can relate to itself.

```text
Employee manages many Employees
```

Example:

```sql
CREATE TABLE Employees (
    EmployeeId INT PRIMARY KEY,
    ManagerId INT NULL,
    Name NVARCHAR(100),
    FOREIGN KEY (ManagerId) REFERENCES Employees(EmployeeId)
);
```

This is common in organizational hierarchies and recursive structures.

## Other Relationship Types

### One-to-Zero-or-One

A row may have a related row or none at all.

Example:

- A user may have a profile, or may not.
- A product may have a discount record, or may not.

### Many-to-Many with Payload

In some cases, the junction table adds its own attributes.

```text
OrderItems connects Orders and Products and stores quantity and price
```

This is especially common in ecommerce applications.

## Design Guidance

- Use foreign keys to enforce referential integrity.
- Prefer a junction table for many-to-many relationships.
- Add unique constraints when a relationship should be singular.
- Consider performance and indexing on relationship columns.
- Avoid deep chains of unnecessary relationships when a simpler model works.
- Document whether optional or required relationships are intended.

## Best Practices

- Keep identifiers stable and meaningful.
- Choose keys that are not likely to change frequently.
- Add indexes on foreign key columns.
- Model a relationship only when it represents real business meaning.
- Denormalize intentionally, not accidentally.
- Use naming conventions that clearly describe each relationship.

## Related Concepts

- [[SQL]] - Query and validate relational structures
- [[Model design considerations]] - Design a schema for integrity and scalability
- [[Relational vs non-Relational DBs]] - Choose a database model
- [[REST API]] - APIs often expose related records as nested or referenced data
