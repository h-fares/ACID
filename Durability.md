# Durability in the ACID
Durability is the guarantee that once a transaction has been committed, it will remain committed even in the case of a system failure (e.g., power loss or crash). This is usually achieved by writing the transaction's log to a non-volatile storage before acknowledging the commit. In the event of a system failure, the system can recover the transaction by replaying the log.

## Durability techniques

### Write-ahead logging (WAL)
In the write-ahead logging technique, the database writes the log records to the log file before writing the actual data to the database. This ensures that the log records are durable even if the system crashes before the data is written to the database. When the system recovers from a crash, it can replay the log records to restore the database to a consistent state.

### Asynchronous snapshot replication
In asynchronous snapshot replication, the database periodically takes snapshots of the data and replicates them to a remote server. This provides a backup of the data that can be used to recover the database in the event of a failure. However, there may be a delay between the snapshot and the actual data, so some data may be lost in the event of a failure.

### AOF (Append-Only File)
In the AOF technique, the database writes every change to the data to an append-only file. This file can be used to recover the database in the event of a failure by replaying the changes. This technique is commonly used in NoSQL databases like Redis.