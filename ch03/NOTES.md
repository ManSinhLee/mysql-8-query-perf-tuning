sysbench oltp_read_only --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-user=sbtest --mysql-password=password --mysql-db=sbtest --table_size=20000 --tables=4 --threads=4 prepare

sysbench oltp_read_only --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-user=sbtest --mysql-password=password --mysql-db=sbtest --table_size=20000 --tables=4 --threads=4 prewarm


SELECT AVG(id) FROM (SELECT * FROM sbtest1 FORCE KEY (PRIMARY) LIMIT 20000) t; 
SELECT COUNT(*) FROM (SELECT * FROM sbtest1 WHERE k LIKE '%0%' LIMIT 20000) t;


sysbench oltp_read_only --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-user=sbtest --mysql-password=password --mysql-db=sbtest --table_size=20000 --tables=4 --time=60 --threads=8 run

sysbench oltp_read_only --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-user=sbtest --mysql-password=password --mysql-db=sbtest --tables=4 cleanup

CREATE TABLE `sbtest101` (
`id` varchar(10) NOT NULL,
`val` bigint(20) unsigned NOT NULL DEFAULT '0',
PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

SHOW CREATE TABLE sbtest.sbtest1\G
UPDATE sbtest1 SET val = LAST_INSERT_ID(val+1) WHERE id = 'sbkey1';

CREATE TABLE users (
    id INT PRIMARY KEY,
    first_name VARCHAR(255),
    last_name VARCHAR(255),
    email VARCHAR(255),
    phone VARCHAR(255)
);


-- Insert 10 records into the users table
INSERT INTO users (first_name, last_name, email, phone) VALUES
    ('John', 'Doe', 'john.doe@mysql.com', '123-456-7890'),
    ('Jane', 'Smith', 'jane.smith@mysql.com', '987-654-3210'),
    ('Alice', 'Johnson', 'alice.johnson@mysql.com', '555-123-4567'),
    ('Bob', 'Miller', 'bob.miller@mysql.com', '111-222-3333'),
    ('Eva', 'Brown', 'eva.brown@mysql.com', '999-888-7777'),
    ('Charlie', 'White', 'charlie.white@mysql.com', '444-555-6666'),
    ('Grace', 'Lee', 'grace.lee@mysql.com', '777-666-5555'),
    ('David', 'Clark', 'david.clark@mysql.com', '222-333-4444'),
    ('Sophia', 'Taylor', 'sophia.taylor@mysql.com', '666-777-8888'),
    ('Matthew', 'Anderson', 'matthew.anderson@mysql.com', '333-444-5555');


INSERT INTO users (first_name, last_name, email, phone) VALUES('Jennifer', 'Allison', 'jennifer.Allison@mysql.com', '357-456-7890');