---
tag:
  - databases
  - sql
  - relational
category: Databases
related: Relational vs non-Relational DBs, Relationships Design, Model design considerations
---

# SQL

> Structured Query Language

SQL is the standard language used to define, query, manipulate, and manage relational databases. It allows developers and data professionals to create schemas, add records, update data, and retrieve information with a consistent syntax.

## Core SQL Categories

### Data Definition Language (DDL)

DDL defines the structure of the database.

```sql
CREATE TABLE Customers (
    CustomerId INT PRIMARY KEY,
    FirstName NVARCHAR(50) NOT NULL,
    Email NVARCHAR(100) UNIQUE,
    CreatedAt DATETIME DEFAULT GETDATE()
);
```

Common statements:

- `CREATE TABLE`
- `ALTER TABLE`
- `DROP TABLE`
- `CREATE INDEX`

### Data Manipulation Language (DML)

DML reads and changes rows of data.

```sql
SELECT FirstName, Email
FROM Customers
WHERE CreatedAt >= '2024-01-01';

INSERT INTO Customers (CustomerId, FirstName, Email)
VALUES (1, 'Ana', 'ana@email.com');

UPDATE Customers
SET Email = 'new@email.com'
WHERE CustomerId = 1;

DELETE FROM Customers
WHERE CustomerId = 1;
```

### Data Control Language (DCL)

DCL manages access and permissions.

```sql
GRANT SELECT, INSERT ON Customers TO AnalystRole;
REVOKE INSERT ON Customers FROM AnalystRole;
```

### Transaction Control Language (TCL)

TCL manages transaction boundaries.

```sql
BEGIN TRANSACTION;
UPDATE Accounts SET Balance = Balance - 50 WHERE Id = 1;
UPDATE Accounts SET Balance = Balance + 50 WHERE Id = 2;
COMMIT;
```

## Query Patterns

### SELECT

```sql
SELECT *
FROM Orders
WHERE Total > 100
ORDER BY OrderDate DESC;
```

### Filtering and Conditions

```sql
SELECT *
FROM Products
WHERE Category = 'Books' AND Price < 30;
```

### Joins

Joins combine rows across tables based on relationships.

```sql
SELECT c.FirstName, o.OrderId, o.Total
FROM Customers c
INNER JOIN Orders o ON c.CustomerId = o.CustomerId;
```

Common joins:

- `INNER JOIN` - only matching rows
- `LEFT JOIN` - all rows from the left table, matching rows from the right
- `RIGHT JOIN` - all rows from the right table
- `FULL OUTER JOIN` - all rows from both sides

### Grouping and Aggregation

```sql
SELECT CustomerId, COUNT(*) AS TotalOrders, SUM(Total) AS TotalSpent
FROM Orders
GROUP BY CustomerId
HAVING SUM(Total) > 500;
```

## Constraints

Constraints help protect data quality.

- **PRIMARY KEY** - unique identifier for each row
- **FOREIGN KEY** - link to a row in another table
- **UNIQUE** - no duplicate values in a column or group
- **NOT NULL** - required field
- **CHECK** - verifies a condition
- **DEFAULT** - default value when not provided

```sql
CREATE TABLE Orders (
    OrderId INT PRIMARY KEY,
    CustomerId INT NOT NULL,
    Total DECIMAL(10,2) CHECK (Total >= 0),
    CONSTRAINT FK_Orders_Customers FOREIGN KEY (CustomerId)
        REFERENCES Customers(CustomerId)
);
```

## Normalization

Normalization organizes data to reduce duplication and improve integrity. It aims to store each fact in one logical place.

Typical stages:

- 1NF - atomic values and no repeating groups
- 2NF - no partial dependency on a composite key
- 3NF - no transitive dependency

## Performance Considerations

SQL performance improves with:

- proper indexes on frequent search columns
- limiting result sets with filtering and pagination
- avoiding unnecessary joins and repeated subqueries
- keeping transactions small and focused
- using execution plans to inspect slow queries

```sql
CREATE INDEX IX_Orders_CustomerId
ON Orders(CustomerId);
```

## Best Practices

- Use clear table and column names.
- Prefer constraints over ad hoc validation.
- Keep business rules in the database where they matter for integrity.
- Write readable queries instead of overly clever ones.
- Test queries against realistic data volumes.
- Avoid returning more data than the client needs.

## Related Concepts

- [[Relational vs non-Relational DBs]] - Choose the right database model
- [[Relationships Design]] - Model how tables relate to each other
- [[Model design considerations]] - Design for integrity and performance
- [[REST API]] - APIs often read from or write to SQL databases

