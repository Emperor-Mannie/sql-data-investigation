# sql-data-investigation
SQL examples and investigation techniques for troubleshooting data-related application issues.
# SQL Data Investigation

A collection of practical SQL examples and investigation techniques for identifying and troubleshooting data-related issues.

## Investigation Principles

Before making changes to production data:

1. Understand the reported issue.
2. Identify the relevant records.
3. Run a SELECT query to verify the data.
4. Confirm the scope of affected records.
5. Use targeted changes only where authorised.
6. Verify the outcome after the change.

## Example 1: Finding Records with Missing Values

```sql
SELECT CustomerID, CustomerName, AccountNumber
FROM Customers
WHERE AccountNumber IS NULL;
```

This query can help identify records where a required value is missing.

## Example 2: Comparing Related Records

```sql
SELECT
    c.CustomerID,
    c.CustomerName,
    t.TransactionReference,
    t.Status
FROM Customers c
LEFT JOIN Transactions t
    ON c.CustomerID = t.CustomerID
WHERE t.TransactionReference IS NULL;
```

A LEFT JOIN can be useful when investigating whether records in one system have corresponding records in another table.

## Example 3: Verify Before Updating

Before making an authorised update, first confirm the exact records affected:

```sql
SELECT *
FROM Customers
WHERE CustomerID = 'SAMPLE001';
```

After confirming the scope and receiving appropriate authorisation, changes should be targeted and followed by a verification query.

## Key Lesson

A structured data investigation should prioritise accuracy and verification. A query that changes data should never be the first step when the issue can be investigated safely with a SELECT statement.
