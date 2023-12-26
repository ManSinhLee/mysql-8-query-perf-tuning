In MySQL 8, as in previous versions, threads play a crucial role in the operation of the database server. Threads in MySQL handle various tasks concurrently to ensure efficient execution of queries and other operations. Here are some key types of threads in MySQL 8 along with examples:

1. **Connection Handling Threads:**
   - MySQL uses threads to handle client connections. Each connection is typically associated with a separate thread. Connection threads manage tasks related to client communication, query execution, and result processing.

   ```sql
   -- Example: Show information about active connections
   SHOW PROCESSLIST;
   ```

2. **Storage Engine Threads:**
   - Storage engines in MySQL use threads to perform tasks related to data retrieval and storage. Different storage engines may have their own threads for handling specific operations.

   ```sql
   -- Example: InnoDB threads
   SHOW ENGINE INNODB STATUS;
   ```

3. **Replication Threads:**
   - MySQL replication involves several threads for tasks like reading the binary log, sending events to replica servers, and applying changes on replica servers.

   ```sql
   -- Example: Show information about replication status
   SHOW SLAVE STATUS;
   ```

4. **I/O Threads:**
   - MySQL uses I/O threads for handling tasks related to reading and writing data to disk. For example, InnoDB may use I/O threads for flushing dirty pages to disk.

   ```sql
   -- Example: Show information about InnoDB I/O threads
   SHOW ENGINE INNODB STATUS;
   ```

5. **Utility Threads:**
   - There are various utility threads in MySQL that handle tasks such as signal handling, background maintenance, and cleanup.

   ```sql
   -- Example: Show information about background threads
   SELECT * FROM performance_schema.threads;
   ```

6. **Query Execution Threads:**
   - MySQL uses threads to execute queries concurrently. The number of query execution threads can be configured based on system resources and workload.

   ```sql
   -- Example: Configure the number of query execution threads
   SET GLOBAL max_execution_time = 1000;
   ```

7. **Event Scheduler Threads:**
   - MySQL includes an event scheduler that uses threads to execute scheduled events.

   ```sql
   -- Example: Show information about scheduled events
   SHOW EVENTS;
   ```

8. **Mutex and Lock Threads:**
   - Threads related to mutexes and locks are responsible for managing access to shared resources to ensure data consistency and integrity.

   ```sql
   -- Example: Show information about mutexes
   SELECT * FROM performance_schema.mutex_instances WHERE OBJECT_INSTANCE_BEGIN IS NOT NULL;
   ```

These are just a few examples, and MySQL uses threads for various other tasks as well. It's important to note that the specifics of thread usage can vary based on the MySQL configuration, storage engines in use, and the nature of the workload.

To gather more detailed information about threads and their activities, you can use queries against the `performance_schema` database, as demonstrated in the examples above. Additionally, the MySQL documentation for your specific version provides detailed information about thread types and their functionalities.

Let's break down the components of the query:

```sql
SELECT
    THREAD_ID AS TID,
    SUBSTRING_INDEX(NAME, '/', -2) AS THREAD_NAME,
    IF(TYPE = 'BACKGROUND', '*', '') AS B,
    IFNULL(PROCESSLIST_ID, '') AS PID
FROM
    performance_schema.threads;

mysql> SELECT THREAD_ID AS TID, SUBSTRING_INDEX(NAME, '/', -2) AS THREAD_NAME, IF(TYPE = 'BACKGROUND', '*', ") AS B, IFNULL(PROCESSLIST_ID, ") AS PID FROM performance_schema.threads;
+-----+--------------------------------------+---------------------------------+
| TID | THREAD_NAME                          | PID                             |
+-----+--------------------------------------+---------------------------------+
|   1 | sql/main                             | *                               |
|   3 | innodb/io_ibuf_thread                | *                               |
|   4 | innodb/io_read_thread                | *                               |
|   5 | innodb/io_read_thread                | *                               |
|   6 | innodb/io_read_thread                | *                               |
|   7 | innodb/io_read_thread                | *                               |
|   8 | innodb/io_write_thread               | *                               |
|   9 | innodb/io_write_thread               | *                               |
|  10 | innodb/io_write_thread               | *                               |
|  11 | innodb/io_write_thread               | *                               |
|  12 | innodb/page_flush_coordinator_thread | *                               |
|  13 | innodb/log_checkpointer_thread       | *                               |
|  14 | innodb/log_flush_notifier_thread     | *                               |
|  15 | innodb/log_flusher_thread            | *                               |
|  16 | innodb/log_write_notifier_thread     | *                               |
|  17 | innodb/log_writer_thread             | *                               |
|  18 | innodb/log_files_governor_thread     | *                               |
|  21 | innodb/srv_lock_timeout_thread       | *                               |
|  22 | innodb/srv_error_monitor_thread      | *                               |
|  23 | innodb/srv_monitor_thread            | *                               |
|  24 | innodb/buf_resize_thread             | *                               |
|  25 | innodb/srv_master_thread             | *                               |
|  26 | innodb/dict_stats_thread             | *                               |
|  27 | innodb/fts_optimize_thread           | *                               |
|  28 | mysqlx/acceptor_network              | *                               |
|  29 | mysqlx/worker                        | *                               |
|  31 | mysqlx/worker                        | *                               |
|  34 | innodb/buf_dump_thread               | *                               |
|  35 | innodb/clone_gtid_thread             | *                               |
|  36 | innodb/srv_purge_thread              | *                               |
|  37 | innodb/srv_worker_thread             | *                               |
|  38 | innodb/srv_worker_thread             | *                               |
|  39 | innodb/srv_worker_thread             | *                               |
|  40 | sql/event_scheduler                  | ) AS B, IFNULL(PROCESSLIST_ID,  |
|  41 | sql/signal_handler                   | *                               |
|  42 | sql/compress_gtid_table              | ) AS B, IFNULL(PROCESSLIST_ID,  |
|  43 | mysqlx/acceptor_network              | *                               |
|  46 | sql/one_connection                   | ) AS B, IFNULL(PROCESSLIST_ID,  |
+-----+--------------------------------------+---------------------------------+
38 rows in set (0.09 sec)

mysql> 
```

Here's an explanation of each part of the query:

- **`SELECT THREAD_ID AS TID`**: Select the `THREAD_ID` column from the `performance_schema.threads` table and alias it as `TID`.

- **`SUBSTRING_INDEX(NAME, '/', -2) AS THREAD_NAME`**: Extract the second-to-last segment of the `NAME` column using the '/' delimiter. This is often used to obtain a more human-readable thread name. It is then aliased as `THREAD_NAME`.

- **`IF(TYPE = 'BACKGROUND', '*', '') AS B`**: If the value in the `TYPE` column is equal to 'BACKGROUND', then the character '*' is returned; otherwise, an empty string is returned. This is used to mark background threads. The result is aliased as `B`.

- **`IFNULL(PROCESSLIST_ID, '') AS PID`**: If the value in the `PROCESSLIST_ID` column is not null, then it is returned; otherwise, an empty string is returned. This is used to show the process ID associated with the thread. The result is aliased as `PID`.

- **`FROM performance_schema.threads`**: Specifies the source table for the query, which is `performance_schema.threads`.

In summary, the query retrieves information from the `performance_schema.threads` table and presents it in a more readable format, including the thread ID (`TID`), a human-readable thread name (`THREAD_NAME`), a '*' character if the thread is a background thread (`B`), and the process ID (`PID`). This type of query is often used to inspect and analyze the active threads in a MySQL server, especially when looking at background and user threads.

mysql> SHOW PROCESSLIST;
+----+-----------------+---------------------+------+---------+------+------------------------+------------------+
| Id | User            | Host                | db   | Command | Time | State                  | Info             |
+----+-----------------+---------------------+------+---------+------+------------------------+------------------+
|  5 | event_scheduler | localhost           | NULL | Daemon  | 1262 | Waiting on empty queue | NULL             |
| 11 | dbadmin         | 104.28.249.55:55201 | NULL | Query   |    0 | init                   | SHOW PROCESSLIST |
+----+-----------------+---------------------+------+---------+------+------------------------+------------------+
2 rows in set, 1 warning (0.12 sec)

mysql> SELECT CONNECTION_ID(), PS_THREAD_ID(11), PS_CURRENT_THREAD_ID()\G
*************************** 1. row ***************************
       CONNECTION_ID(): 11
      PS_THREAD_ID(11): 48
PS_CURRENT_THREAD_ID(): 48
1 row in set (0.11 sec)

# Querying the threads table for the current connection
mysql> SELECT * FROM performance_schema.threads WHERE THREAD_ID = PS_CURRENT_THREAD_ID()\G
*************************** 1. row ***************************
            THREAD_ID: 48
                 NAME: thread/sql/one_connection
                 TYPE: FOREGROUND
       PROCESSLIST_ID: 11
     PROCESSLIST_USER: dbadmin
     PROCESSLIST_HOST: 104.28.249.55
       PROCESSLIST_DB: NULL
  PROCESSLIST_COMMAND: Query
     PROCESSLIST_TIME: 0
    PROCESSLIST_STATE: statistics
     PROCESSLIST_INFO: SELECT * FROM performance_schema.threads WHERE THREAD_ID = PS_CURRENT_THREAD_ID()
     PARENT_THREAD_ID: NULL
                 ROLE: NULL
         INSTRUMENTED: YES
              HISTORY: YES
      CONNECTION_TYPE: SSL/TLS
         THREAD_OS_ID: 2018
       RESOURCE_GROUP: USR_default
     EXECUTION_ENGINE: PRIMARY
    CONTROLLED_MEMORY: 39056
MAX_CONTROLLED_MEMORY: 46176
         TOTAL_MEMORY: 109486
     MAX_TOTAL_MEMORY: 117970
     TELEMETRY_ACTIVE: NO
1 row in set (0.11 sec)

mysql> 