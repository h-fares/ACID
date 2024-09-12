# Read phenomenas in MySQL

In MySQL, isolation refers to how transactions are executed independently of one another to avoid issues with concurrent transactions. There are four types of reading phenomena that occur based on the isolation level:

1. **Dirty Read**: A transaction reads data that has been written by another transaction but not yet committed. If the other transaction is rolled back, the data read by the first transaction is invalid.

```sql
-- Transaction 1: 
UPDATE accounts SET balance = balance - 500 WHERE account_id = 1;
-- Not committed yet.

-- Transaction 2:
SELECT balance FROM accounts WHERE account_id = 1;
-- Dirty read occurs if Transaction 2 reads the balance before Transaction 1 commits.
```

2. **Non-Repeatable Read**: A transaction reads the same row twice but gets different results because another transaction has modified the row in between the reads.

```sql
-- Transaction 1:
SELECT balance FROM accounts WHERE account_id = 1;

-- Transaction 2:
UPDATE accounts SET balance = balance - 500 WHERE account_id = 1;
COMMIT;

-- Transaction 1 (again):
SELECT balance FROM accounts WHERE account_id = 1;
-- Non-repeatable read occurs if the balance is different in the second read.
```

3. **Phantom Read**: A transaction reads a set of rows twice but gets different results because another transaction has inserted or deleted rows in between the reads.

```sql
-- Transaction 1:
SELECT * FROM orders WHERE status = 'pending';

-- Transaction 2:
INSERT INTO orders (order_id, status) VALUES (101, 'pending');
COMMIT;

-- Transaction 1 (again):
SELECT * FROM orders WHERE status = 'pending';
-- Phantom read occurs if the new row from Transaction 2 now appears in the result.
```

4. **Lost Update**: Two transactions read the same data, both modify it, but one of the updates is lost because the second one overwrites it.

```sql
-- Transaction 1:
SELECT balance FROM accounts WHERE account_id = 1;
UPDATE accounts SET balance = balance - 100 WHERE account_id = 1;

-- Transaction 2:
SELECT balance FROM accounts WHERE account_id = 1;
UPDATE accounts SET balance = balance + 200 WHERE account_id = 1;
-- One of the updates will be lost depending on the order of commits.
```