In MySQL's Performance Schema, events represent specific occurrences or activities within the MySQL server that can be monitored for performance analysis. These events are produced by instruments and consumed by consumers. Here are some common types of Performance Schema events along with brief explanations:

1. **Statement Events (`events_statements`):**
   - Events related to the execution of SQL statements.

   Examples:
   - `statement/sql/select`: Execute a SELECT statement.
   - `statement/sql/insert`: Execute an INSERT statement.

2. **Stage Events (`events_stages`):**
   - Events related to different stages of query execution.

   Examples:
   - `stage/sql/starting`: The starting stage of query execution.
   - `stage/sql/executing`: The executing stage of query execution.

3. **Wait Events (`events_waits`):**
   - Events related to threads waiting for specific conditions.

   Examples:
   - `wait/synch/mutex/sql/THD::LOCK_thd_data`: Wait for a THD data structure mutex.
   - `wait/io/table/sql/handler`: Wait for a table handler lock.

4. **Transaction Events (`events_transactions`):**
   - Events related to transaction activities.

   Examples:
   - `transaction/sql/commit`: SQL commit operation.
   - `transaction/sql/rollback`: SQL rollback operation.

5. **IO Events (`events_io`):**
   - Events related to I/O operations.

   Examples:
   - `file/sql/FRM::fseek`: File seek operation in SQL code.
   - `file/sql/FRM::fread`: File read operation in SQL code.

6. **Error Events (`events_errors`):**
   - Events related to error occurrences.

   Examples:
   - `error/sql/ER_LOCK_DEADLOCK`: Deadlock error in SQL code.
   - `error/sql/ER_TABLE_EXISTS_ERROR`: Table exists error in SQL code.

7. **System Events (`events_system`):**
   - General system-related events.

   Examples:
   - `memory/sql/malloc`: Memory allocation in SQL code.
   - `memory/sql/free`: Memory deallocation in SQL code.

8. **User Events (`events_users`):**
   - Events related to user activities.

   Examples:
   - `user/sql/connect`: User connection event.
   - `user/sql/disconnect`: User disconnection event.

To query for available events, you can use the corresponding tables in the Performance Schema, such as `events_statements`, `events_stages`, `events_waits`, `events_transactions`, `events_io`, `events_errors`, `events_system`, and `events_users`. Here are some example queries:

1. **List All Statement Events:**
   ```sql
   SHOW TABLES LIKE '%events%';
   ```

2. **List All Wait Events:**
   ```sql
   SHOW TABLES LIKE '%events_waits%';
   ```

3. **List All System Events:**
   ```sql
   SELECT * FROM performance_schema.events_system;
   ```

4. **Filter Events by Thread ID:**
   ```sql
   SELECT * FROM performance_schema.events_statements WHERE THREAD_ID = <your_thread_id>;
   ```

5. **Filter Events by Event Name:**
   ```sql
   SELECT * FROM performance_schema.events_transactions WHERE EVENT_NAME LIKE 'transaction/sql%';
   ```

These examples demonstrate how to query specific types of events and filter the results based on different criteria. Always refer to the documentation for your specific MySQL version for accurate and detailed information about Performance Schema events and their associated tables.