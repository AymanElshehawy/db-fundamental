### ISAM (Indexed Sequential Access Method):

1. **Data Storage:**
    - ISAM stores data in fixed-length rows, meaning that each row has a predetermined size.
    - It uses an index file to store key values and a data file to store the actual data records.

2. **Indexing:**
    - ISAM uses a B-tree (Balanced Tree) index structure to provide fast access to rows based on key values.
    - It supports both primary and secondary indexes.

3. **Transactions:**
    - ISAM supports basic transactions, allowing the grouping of multiple SQL statements into a single unit of work.
    - However, it lacks some advanced transaction features compared to more modern storage engines.

4. **Concurrency Control:**
    - ISAM uses table-level locking, which means that when a transaction modifies a row, it locks the entire table, potentially leading to contention and decreased concurrency.

5. **Crash Recovery:**
    - ISAM does not provide automatic crash recovery. In the event of a system failure, manual intervention may be required to recover data consistency.

### InnoDB:

1. **Data Storage:**
    - InnoDB stores data in a clustered index called the "primary key" index, where the data rows are stored in the leaf nodes of the index itself.
    - It uses a dynamic row format, allowing for variable-length rows, which can be more efficient in terms of storage.

2. **Indexing:**
    - InnoDB uses a B-tree structure for indexing, similar to ISAM.
    - The primary key index is the main structure for organizing data, and secondary indexes are also supported.

3. **Transactions:**
    - InnoDB fully supports ACID properties (Atomicity, Consistency, Isolation, Durability) and provides advanced transaction features.
    - It supports multi-versioning, allowing for consistent reads and writes even in the presence of concurrent transactions.

4. **Concurrency Control:**
    - InnoDB uses a combination of row-level and table-level locking to manage concurrency.
    - Row-level locking reduces contention and allows for higher concurrency compared to table-level locking.

5. **Crash Recovery:**
    - InnoDB provides automatic crash recovery. In the event of a system failure, InnoDB uses a transaction log (redo log) to bring the database back to a consistent state during the recovery process.

In summary, while ISAM is a simpler and older storage engine with fixed-length rows and basic transaction support, InnoDB is a more modern and feature-rich engine with support for variable-length rows, advanced transactions, and better concurrency control. InnoDB is the default and recommended storage engine for most MySQL applications today.