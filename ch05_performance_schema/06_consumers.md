In MySQL's Performance Schema, consumers are entities that consume or use events produced by instrumented instruments. These consumers allow you to collect and analyze performance-related data from various aspects of MySQL server operation. Here are some common Performance Schema consumers along with brief explanations:

1. **events_statements:**
   - Consumer for SQL statement events. Collects information about the execution of SQL statements.

2. **events_stages:**
   - Consumer for query execution stage events. Provides information about different stages of query execution.

3. **events_waits:**
   - Consumer for wait event events. Captures information about threads waiting for specific conditions.

4. **events_transactions:**
   - Consumer for transaction events. Records information about transaction-related activities.

5. **events_io:**
   - Consumer for I/O events. Captures details about file I/O operations.

6. **events_errors:**
   - Consumer for error events. Collects information about errors that occur during execution.

7. **events_system:**
   - Consumer for system events. Captures general system-related information.

8. **events_users:**
   - Consumer for user-related events. Provides information about user activity.

9. **events_hosts:**
   - Consumer for host-related events. Captures information about connections from different hosts.

To query for available consumers, you can use the `performance_schema.setup_consumers` table. Here are some example queries:

1. **List All Consumers:**
   ```sql
   SELECT * FROM performance_schema.setup_consumers;
   ```

2. **Enable a Specific Consumer:**
   ```sql
   UPDATE performance_schema.setup_consumers
   SET ENABLED = 'YES'
   WHERE NAME = 'events_statements';
   ```

   This example enables the consumer for SQL statement events.

3. **Disable a Specific Consumer:**
   ```sql
   UPDATE performance_schema.setup_consumers
   SET ENABLED = 'NO'
   WHERE NAME = 'events_waits';
   ```

   This example disables the consumer for wait events.

4. **Show Enabled Consumers:**
   ```sql
   SELECT * FROM performance_schema.setup_consumers
   WHERE ENABLED = 'YES';
   ```

   This query shows a list of currently enabled consumers.

5. **Filter Consumers by Category:**
   ```sql
   SELECT * FROM performance_schema.setup_consumers
   WHERE NAME LIKE '%statement%';
   ```

   This example filters consumers related to SQL statements.

6. **Filter Consumers by Class:**
   ```sql
   SELECT * FROM performance_schema.setup_consumers
   WHERE NAME LIKE '%stage%';
   ```

   This query filters consumers related to query execution stages.

7. **Show Consumers with Specific Name Pattern:**
   ```sql
   SELECT * FROM performance_schema.setup_consumers
   WHERE NAME LIKE 'events%';
   ```

   This query shows consumers whose names start with 'events'.

8. **Reset All Consumers to Default Settings:**
   ```sql
   UPDATE performance_schema.setup_consumers
   SET ENABLED = 'DEFAULT';
   ```

   This query resets all consumers to their default settings.

These examples demonstrate how to interact with the `performance_schema.setup_consumers` table to manage and configure the collection of performance-related data in MySQL's Performance Schema. Always refer to the documentation for your MySQL version for accurate and detailed information about Performance Schema consumers.