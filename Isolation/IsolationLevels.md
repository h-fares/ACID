# Isolation levels supported by the database.
 

The isolation level determines the degree of isolation of data between concurrent transactions.

The following are the standard SQL isolation levels:

1. **Read Uncommitted**: This is the lowest isolation level. In this level, a transaction can read data that has been modified by other transactions but not yet committed. This can lead to dirty reads, non-repeatable reads, and phantom reads.
2. **Read Committed**: This level prevents dirty reads. A transaction can only read data that has been committed by other transactions. However, non-repeatable reads and phantom reads can still occur.
3. **Repeatable Read**: This level prevents dirty reads and non-repeatable reads. A transaction can read the same row multiple times, and the data will not change. However, phantom reads can still occur.
4. **Serializable**: This is the highest isolation level. It prevents dirty reads, non-repeatable reads, and phantom reads. It ensures that transactions are executed in a way that is equivalent to running them one after the other.