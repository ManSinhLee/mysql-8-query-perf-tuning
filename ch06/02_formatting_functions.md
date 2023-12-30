The `sys` schema in MySQL includes formatting functions that allow you to format and present data in a more human-readable way. These functions are particularly useful for presenting performance-related information in a clear and understandable format. Here are some key formatting functions available in the `sys` schema:

### 1. **`format_statement()` Function:**
   - Formats a SQL statement, making it more readable by breaking it into lines and indenting.
   - Example:

     ```sql
     SELECT sys.format_statement('SELECT * FROM employees WHERE salary > 50000');
     ```

### 2. **`format_bytes()` Function:**
   - Formats a byte value into a human-readable string.
   - Example:

     ```sql
     SELECT sys.format_bytes(1024);
     ```

### 3. **`format_time()` Function:**
   - Formats a time duration in seconds into a human-readable string.
   - Example:

     ```sql
     SELECT sys.format_time(3600);
     ```

### 4. **`format_pico_time()` Function:**
   - Formats a time duration in picoseconds into a human-readable string.
   - Example:

     ```sql
     SELECT sys.format_pico_time(1000000000000);
     ```

### 5. **`format_memory()` Function:**
   - Formats a memory size in bytes into a human-readable string.
   - Example:

     ```sql
     SELECT sys.format_memory(1048576);
     ```

### 6. **`format_ps_thread_id()` Function:**
   - Formats a thread ID in a performance schema thread event into a human-readable string.
   - Example:

     ```sql
     SELECT sys.format_ps_thread_id(1234);
     ```

### 7. **`format_ps_binary_id()` Function:**
   - Formats a binary ID in a performance schema thread event into a human-readable string.
   - Example:

     ```sql
     SELECT sys.format_ps_binary_id(0x12345678);
     ```

### 8. **`format_ps_digest()` Function:**
   - Formats a digest in a performance schema statement event into a human-readable string.
   - Example:

     ```sql
     SELECT sys.format_ps_digest('d6be448db610dc4fc7a4a826858a2736b9f281b47ce3f51f9d7a8a36f278b710');
     ```

These functions are designed to help present complex information, such as SQL statements, time durations, and memory sizes, in a format that is easier to understand. Use these functions in combination with other `sys` schema views and functions for effective performance monitoring and analysis in MySQL.


mysql> SELECT sys.format_bytes(5000) AS SysBytes, FORMAT_BYTES(5000) AS P_SBytes;
+----------+----------+
| SysBytes | P_SBytes |
+----------+----------+
| 4.88 KiB | 4.88 KiB |
+----------+----------+
1 row in set (0.00 sec)

mysql> SELECT @@global.datadir AS DataDir, sys.format_path('/var/lib/mysql/binlog.000001') AS binlog_000001\G
*************************** 1. row ***************************
      DataDir: /var/lib/mysql/
binlog_000001: @@datadir/binlog.000001
1 row in set (0.00 sec)

mysql> SELECT sys.format_statement('SELECT * FROM world.country INNER JOIN world.city ON country.Code = city.CountryCode') AS Statement\G
*************************** 1. row ***************************
Statement: SELECT * FROM world.country IN ... ountry.Code = city.CountryCode
1 row in set (0.00 sec)

mysql> SELECT sys.format_time(123456789012) AS SysTime, FORMAT_PICO_TIME(123456789012) AS P_STime\G
*************************** 1. row ***************************
SysTime: 123.46 ms
P_STime: 123.46 ms
1 row in set (0.00 sec)

mysql> SELECT ROUTINE_NAME AS Function_Name,ROUTINE_DEFINITION AS Function_Code FROM INFORMATION_SCHEMA.ROUTINES WHERE ROUTINE_SCHEMA = 'sys' AND ROUTINE_TYPE = 'FUNCTION'  AND ROUTINE_NAME LIKE 'format_%'\G;