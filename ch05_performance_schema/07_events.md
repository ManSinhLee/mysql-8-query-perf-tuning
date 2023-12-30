In MySQL 8, the Performance Schema is a powerful tool that provides detailed information about server performance and resource usage. Performance Schema events represent various activities within the MySQL server, and you can use these events to monitor and analyze different aspects of the server's operation. Below are some common categories of Performance Schema events available in MySQL 8:

1. **Statement Events (`events_statements`):**
   - `statement/sql/*`: Events related to SQL statement execution.
   - `statement/com/*`: Events related to communication between the client and the server.

2. **Stage Events (`events_stages`):**
   - `stage/sql/*`: Events related to different stages of SQL statement execution.

3. **Wait Events (`events_waits`):**
   - `wait/io/*`: Events related to I/O operations.
   - `wait/synch/*`: Events related to synchronization and locking.
   - `wait/lock/*`: Events related to various types of locks.

4. **Transaction Events (`events_transactions`):**
   - `transaction/*`: Events related to transaction operations.

5. **I/O Events (`events_io`):**
   - `wait/io/file/*`: Events related to file I/O operations.
   - `wait/io/socket/*`: Events related to socket I/O operations.

6. **Error Events (`events_errors`):**
   - `error/*`: Events related to errors that occurred during execution.

7. **User Events (`events_users`):**
   - `user/*`: User-defined events.

8. **Host Events (`events_hosts`):**
   - `host/cache/*`: Events related to host cache operations.

To query for available events, you can use the corresponding Performance Schema tables. Below are some example queries:

1. **List All Events:**
   ```sql
   SELECT * FROM performance_schema.events_statements;
   ```

   This query shows all statement events. You can replace `events_statements` with the appropriate event category table for other types of events.

2. **Filter Events by a Specific User:**
   ```sql
   SELECT * FROM performance_schema.events_statements
   WHERE USER = 'your_username';
   ```

   Replace `'your_username'` with the MySQL username you are interested in.

3. **Show Recent Statement Events:**
   ```sql
   SELECT * FROM performance_schema.events_statements_history
   ORDER BY EVENT_ID DESC
   LIMIT 10;
   ```

   This query shows the most recent statement events.

4. **List I/O Wait Events:**
   ```sql
   SELECT * FROM performance_schema.events_waits
   WHERE EVENT_NAME LIKE 'wait/io%';
   ```

   This query shows events related to I/O waits.

5. **Show Recently Waited Events:**
   ```sql
   SELECT * FROM performance_schema.events_waits_history
   ORDER BY TIMER_START DESC
   LIMIT 10;
   ```
   This query shows the most recent wait events.

6. **The correspondence between consumer and table names:**:
  ```sql
   SELECT TABLE_NAME FROM performance_schema.setup_consumers c 
   INNER JOIN information_schema.TABLES t ON t.TABLE_NAME = c.NAME 
   WHERE t.TABLE_SCHEMA = 'performance_schema' AND c.NAME LIKE 'events%' ORDER BY c.NAME;
  ```

These examples demonstrate how to query Performance Schema events in MySQL 8. Always refer to the MySQL documentation for your specific version for accurate and detailed information about Performance Schema events and tables.