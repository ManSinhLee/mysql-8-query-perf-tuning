The sys schema in MySQL is a collection of views, functions, and procedures that provide a high-level, user-friendly interface for monitoring and managing the MySQL server. The sys schema relies on the Performance Schema and Information Schema to gather performance-related data and present it in a more accessible form.

To use and configure the sys schema in MySQL, follow these steps:

mysql> SELECT * FROM sys.sys_config;
+--------------------------------------+-------+---------------------+--------+
| variable                             | value | set_time            | set_by |
+--------------------------------------+-------+---------------------+--------+
| diagnostics.allow_i_s_tables         | OFF   | 2023-12-20 09:04:48 | NULL   |
| diagnostics.include_raw              | OFF   | 2023-12-20 09:04:48 | NULL   |
| ps_thread_trx_info.max_length        | 65535 | 2023-12-20 09:04:48 | NULL   |
| statement_performance_analyzer.limit | 100   | 2023-12-20 09:04:48 | NULL   |
| statement_performance_analyzer.view  | NULL  | 2023-12-20 09:04:48 | NULL   |
| statement_truncate_len               | 64    | 2023-12-28 20:29:21 | NULL   |
+--------------------------------------+-------+---------------------+--------+
6 rows in set (0.01 sec)

mysql> SET @query = 'SELECT * FROM world.country INNER JOIN world.city ON country.Code = city.CountryCode';
Query OK, 0 rows affected (0.00 sec)

mysql> SELECT sys.sys_get_config( 'statement_truncate_len', NULL ) AS TruncateLen\G
*************************** 1. row ***************************
TruncateLen: 64
1 row in set (0.00 sec)

mysql> SELECT sys.format_statement(@query) AS Statement\G
*************************** 1. row ***************************
Statement: SELECT * FROM world.country INNER JOIN world.city ON country.Code = city.CountryCode
1 row in set (0.00 sec)

mysql> UPDATE sys.sys_config SET value = 48 WHERE variable = 'statement_truncate_len';
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> SET @sys.statement_truncate_len = NULL;
Query OK, 0 rows affected (0.00 sec)

mysql> SELECT sys.format_statement(@query) AS Statement\G
*************************** 1. row ***************************
Statement: SELECT * FROM world.co ... ode = city.CountryCode
1 row in set (0.00 sec)

mysql> SET @sys.statement_truncate_len = 96;
Query OK, 0 rows affected (0.00 sec)

mysql> SELECT sys.format_statement(@query) AS Statement\G
*************************** 1. row ***************************
Statement: SELECT * FROM world.country INNER JOIN world.city ON country.Code = city.CountryCode
1 row in set (0.00 sec)

mysql> 