The MySQL Performance Schema provides a `threads` table that contains information about server threads. This table is a valuable resource for understanding the state and behavior of threads in the MySQL server. Here are some example queries that you can use to gather information about threads using the `performance_schema.threads` table:

1. **List All Threads:**
   ```sql
   SELECT * FROM performance_schema.threads;
   ```

2. **Filter Threads by Connection Type:**
   ```sql
   SELECT * FROM performance_schema.threads WHERE PROCESSLIST_ID IS NOT NULL;
   ```

3. **Show Thread Details with Process List:**
   ```sql
   SELECT
       THREAD_ID,
       NAME,
       PROCESSLIST_ID,
       PROCESSLIST_USER,
       PROCESSLIST_HOST,
       PROCESSLIST_DB,
       PROCESSLIST_COMMAND
   FROM
       performance_schema.threads
   WHERE
       PROCESSLIST_ID IS NOT NULL;
   ```

4. **Show Information about Background Threads:**
   ```sql
   SELECT * FROM performance_schema.threads WHERE TYPE = 'BACKGROUND';
   ```

5. **Show Details for a Specific Thread ID:**
   ```sql
   SELECT * FROM performance_schema.threads WHERE THREAD_ID = <your_thread_id>;
   ```

6. **Show Running Threads with Query Information:**
   ```sql
   SELECT
       p.ID,
       p.USER,
       p.HOST,
       p.DB,
       p.COMMAND,
       p.TIME,
       p.STATE,
       t.THREAD_ID,
       t.NAME,
       t.TYPE
   FROM
       performance_schema.threads t
   JOIN
       information_schema.PROCESSLIST p ON t.PROCESSLIST_ID = p.ID;
   ```

7. **Show Information about Mutexes for Each Thread:**
   ```sql
    SELECT
        t.THREAD_ID,
        t.NAME,
        m.NAME AS MUTEX_NAME,
        m.LOCKED_BY_THREAD_ID
    FROM
        performance_schema.threads t
    LEFT JOIN
        performance_schema.mutex_instances m ON t.THREAD_ID = m.LOCKED_BY_THREAD_ID;
   ```

8. **Show Thread State Transitions:**
   ```sql
    SELECT
        EVENT_ID,
        THREAD_ID,
        EVENT_NAME,
        SOURCE,
        TIMER_START,
        TIMER_END,
        TIMER_WAIT
    FROM
        performance_schema.events_waits_history_long
    WHERE
        THREAD_ID IS NOT NULL
    ORDER BY
        TIMER_START DESC
    LIMIT 10;
   ```

These queries provide insights into various aspects of threads, such as their states, process list details, background threads, and mutex-related information. You can customize these queries based on your specific monitoring and diagnostic needs.

Keep in mind that the availability of certain columns or tables may vary between MySQL versions, so refer to the documentation corresponding to your MySQL version for accurate information.