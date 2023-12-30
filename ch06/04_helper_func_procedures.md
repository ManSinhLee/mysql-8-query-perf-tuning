In MySQL's `sys` schema, there are helper functions and procedures that provide additional functionalities for performance monitoring and analysis. Below are some of the key helper functions and procedures available in the `sys` schema:

### Helper Functions:

1. **`sys.ps_thread_id()` Function:**
   - Returns a human-readable representation of a thread ID.
   - Example:
     ```sql
    mysql> SELECT THREAD_ID, NAME, TYPE, PROCESSLIST_ID FROM performance_schema.threads WHERE PROCESSLIST_ID IS NOT NULL;
    +-----------+--------------------------------+------------+----------------+
    | THREAD_ID | NAME                           | TYPE       | PROCESSLIST_ID |
    +-----------+--------------------------------+------------+----------------+
    |        41 | thread/sql/event_scheduler     | FOREGROUND |              5 |
    |        44 | thread/sql/compress_gtid_table | FOREGROUND |              7 |
    |        46 | thread/sql/one_connection      | FOREGROUND |              9 |
    +-----------+--------------------------------+------------+----------------+
    3 rows in set (0.00 sec)

     SELECT sys.ps_thread_id(5);
     SELECT sys.ps_thread_id(7);
     SELECT sys.ps_thread_id(9);
     ```

2. **`sys.ps_binary_id()` Function:**
   - Returns a human-readable representation of a binary ID.
   - Example:
     ```sql
     SELECT sys.ps_binary_id(0x12345678);
     ```

3. **`sys.ps_digest()` Function:**
   - Returns a human-readable representation of a digest.
   - Example:
     ```sql
    SELECT SCHEMA_NAME, DIGEST, COUNT_STAR FROM performance_schema.events_statements_summary_by_digest ORDER BY COUNT_STAR DESC LIMIT 10;
    +-------------+------------------------------------------------------------------+------------+
    | SCHEMA_NAME | DIGEST                                                           | COUNT_STAR |
    +-------------+------------------------------------------------------------------+------------+
    | sys         | 3739df6a28d2ae3a4b13e3544c908c60e6f4e123fd678ed16aa0f547682b57f1 |          6 |
    | sys         | f5f9379fdd2f199049426ccb51bcabedfca9117cc96c58f51b155f7f2390450f |          4 |
    | NULL        | 3739df6a28d2ae3a4b13e3544c908c60e6f4e123fd678ed16aa0f547682b57f1 |          4 |
    | sys         | 7ecdd898e5589c21b83d957c47396bf6b9568b4da16a462a39018c73aee363f6 |          3 |
    | NULL        | 44e35cee979ba420eb49a8471f852bbe15b403c89742704817dfbaace0d99dbb |          2 |
    | sys         | f195bf315bf891f7122592aa512f94a528eb7f862f8bcb6e8a248011608ea15d |          2 |
    | sys         | c12402ab86d7f2d1738b0075eda95a2d3605c5a6d08fbd2c72ce35306a504d46 |          2 |
    | NULL        | ce04eda080d3f5605113e1d0d47c2f20e23b091e2487ba586f07b32cda423942 |          2 |
    | sys         | dbea8921b559b8cdd4976d57d70304daa8a242fbbfe6df94427006b54ead6b0f |          2 |
    | sys         | ec47c58f16a1edbc01ec2f2c62cb3ce8662d2d23f6b2d2ea46027c3252b4b38a |          2 |
    +-------------+------------------------------------------------------------------+------------+
    10 rows in set (0.00 sec)

     SELECT sys.format_statement('SELECT * FROM performance_schema.events_statements_summary_by_digest WHERE DIGEST = "3739df6a28d2ae3a4b13e3544c908c60e6f4e123fd678ed16aa0f547682b57f1"') AS formatted_query;
    +---------------------------------------------------+
    | formatted_query                                   |
    +---------------------------------------------------+
    | SELECT * FROM performa ... 78ed16aa0f547682b57f1" |
    +---------------------------------------------------+
    1 row in set (0.15 sec)
     ```

### Helper Procedures:

1. **`sys.ps_truncate_thread_id()` Procedure:**
   - Truncates a thread ID to a specified length.
   - Example:
     ```sql
     CALL sys.ps_truncate_thread_id(1234, 5);
     ```

2. **`sys.ps_truncate_binary_id()` Procedure:**
   - Truncates a binary ID to a specified length.
   - Example:
     ```sql
     CALL sys.ps_truncate_binary_id(0x12345678, 6);
     ```

These functions and procedures in the `sys` schema help simplify the representation of various identifiers and information related to performance monitoring. They are especially useful when you want to present complex information in a more human-readable format.

Feel free to explore the `sys` schema and experiment with these functions and procedures to see how they can enhance your ability to monitor and analyze MySQL performance.