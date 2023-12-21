# Aria
- Aria is a storage engine used in the MariaDB relational database management system. MariaDB is a fork of MySQL and was created by the original developers of MySQL after concerns arose over the acquisition of MySQL by Oracle Corporation. Aria is designed to be a replacement for the MyISAM storage engine, providing enhanced features and improvements.

- Key features and characteristics of the Aria storage engine include:

1. **Transactional Support:**
    - Aria is a transactional storage engine, meaning it supports the principles of ACID (Atomicity, Consistency, Isolation, Durability). This allows for reliable and consistent database transactions.

2. **Crash Recovery:**
    - Aria includes crash-safe capabilities, which means it can recover the database to a consistent state after an unexpected system failure or crash.

3. **Table-level Locking:**
    - Similar to MyISAM, Aria uses table-level locking rather than row-level locking. This can impact concurrency in certain scenarios, as multiple transactions may need to wait for access to the entire table.

4. **Storage Format:**
    - Aria uses a storage format that supports dynamic row length and can handle both variable-length and fixed-length rows.

5. **Internal Temporary Tables:**
    - Aria is often used for internal temporary tables in MariaDB. Internal temporary tables are temporary tables that are created and managed by the database engine to support certain query operations.

6. **Non-Transactional Mode:**
    - Aria can be used in a non-transactional mode, similar to MyISAM. However, the transactional features are a significant improvement over MyISAM, making it a more robust choice in many scenarios.

It's worth noting that while Aria provides certain advantages over MyISAM, MariaDB also supports the InnoDB storage engine, which is the default and widely used storage engine for many modern applications. InnoDB offers additional features such as support for foreign keys, row-level locking, and more advanced transaction support.

When choosing a storage engine in MariaDB, the decision often depends on specific application requirements, workload characteristics, and desired features. Both Aria and InnoDB are commonly used in different scenarios within the MariaDB ecosystem.