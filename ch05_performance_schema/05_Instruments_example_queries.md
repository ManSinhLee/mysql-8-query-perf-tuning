To use Performance Schema instruments in queries, you can interact with the `performance_schema.setup_instruments` table. This table contains information about the available instruments that you can enable or disable for monitoring specific types of activities. Here are some example queries involving Performance Schema instruments:

1. **List All Instruments:**
   ```sql
   SELECT * FROM performance_schema.setup_instruments;
   ```

2. **Enable a Specific Instrument:**
   ```sql
   UPDATE performance_schema.setup_instruments
   SET ENABLED = 'YES'
   WHERE NAME LIKE 'wait/synch/mutex/sql/%';

   UPDATE performance_schema.setup_instruments
   SET TIMED = 'YES'
   WHERE NAME LIKE 'wait/synch/mutex/sql/%';
   ```

   This example enables all instruments related to mutexes in SQL.

3. **Disable a Specific Instrument:**
   ```sql
   UPDATE performance_schema.setup_instruments
   SET ENABLED = 'NO'
   WHERE NAME LIKE 'wait/io/file/%';
   ```

   This example disables all instruments related to file I/O.

4. **Show Enabled Instruments:**
   ```sql
   SELECT * FROM performance_schema.setup_instruments
   WHERE ENABLED = 'YES';
   ```

   This query shows a list of currently enabled instruments.

5. **Filter Instruments by Category:**
   ```sql
   SELECT * FROM performance_schema.setup_instruments
   WHERE CATEGORY = 'memory';
   ```

   This example filters instruments related to memory operations.

6. **Filter Instruments by Class:**
   ```sql
   SELECT * FROM performance_schema.setup_instruments
   WHERE CLASS = 'wait';
   ```

   This query filters instruments related to waiting events.

7. **Show Instruments with Specific Name Pattern:**
   ```sql
   SELECT * FROM performance_schema.setup_instruments
   WHERE NAME LIKE 'statement/sql/%';
   ```

   This query shows instruments related to SQL statements.

8. **Reset All Instruments to Default Settings:**
   ```sql
   UPDATE performance_schema.setup_instruments
   SET ENABLED = 'DEFAULT';
   ```

   This query resets all instruments to their default settings.

Remember that enabling too many instruments may have an impact on performance, so it's essential to selectively enable only the instruments that are necessary for your analysis. Adjust the queries based on your specific monitoring requirements and MySQL version. Always refer to the documentation for your MySQL version for accurate and detailed information about Performance Schema instruments.