sysbench oltp_read_only --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-user=sbtest --mysql-password=password --mysql-db=sbtest --table_size=20000 --tables=4 --threads=4 prepare

sysbench oltp_read_only --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-user=sbtest --mysql-password=password --mysql-db=sbtest --table_size=20000 --tables=4 --threads=4 prewarm


SELECT AVG(id) FROM (SELECT * FROM sbtest1 FORCE KEY (PRIMARY) LIMIT 20000) t; 
SELECT COUNT(*) FROM (SELECT * FROM sbtest1 WHERE k LIKE '%0%' LIMIT 20000) t;


sysbench oltp_read_only --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-user=sbtest --mysql-password=password --mysql-db=sbtest --table_size=20000 --tables=4 --time=60 --threads=8 run

sysbench oltp_read_only --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-user=sbtest --mysql-password=password --mysql-db=sbtest --tables=4 cleanup

SHOW CREATE TABLE sbtest.sbtest1\G
UPDATE sbtest1 SET val = LAST_INSERT_ID(val+1) WHERE id = 'sbkey1';