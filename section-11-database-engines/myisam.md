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