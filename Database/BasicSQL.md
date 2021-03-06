# Basic SQL

## Connecting to Database
```ssh
mysql --host=127.0.0.1 --user=myname --password=mypass mydb
```

## Cool Stuffs
```sql
SHOW CREATE TABLE my_table --shows the create script for the table in its current form
```

## Users
```sql
--two users are created (@'xx' is optional and will default to @'%')
CREATE USER 'username'@'domain.com' IDENTIFIED BY 'password';
CREATE USER 'username'@'%' IDENTIFIED BY 'password';

--revoke all privileges 
--do this before deleting the user
REVOKE ALL ON *.* FROM 'user'@'localhost';

--to delete a user
DROP USER 'username'@'%';
```

## Schema/Database
```sql
CREATE DATABASE my_db;

--delete database
DROP DATABASE my_db;

--show all databases
SHOW DATABASES;

--to switch default schema
USE my_db;

--show all tables in the selected database
SHOW TABLES;
```

## Create Table
```sql
CREATE TABLE books(
    book_id INT,
    title VARCHAR(50),
    author VARCHAR(50)
);

CREATE TABLE authors(
    author_id INT AUTO_INCREMENT PRIMARY KEY,
    author_last VARCHAR(255),
    author_first VARCHAR(255),
    country VARCHAR(50)
);

--delete
DROP TABLE test_table;
```
## Update Table
```sql
ALTER TABLE books
    --to update existing columns
    CHANGE COLUMN book_id book_id INT AUTO_INCREMENT PRIMARY KEY,
    CHANGE COLUMN author author_id INT,
    --to add new column
    ADD COLUMN description TEXT,
    ADD COLUMN genre ENUM('novel', 'poetry', 'drama'),
    ADD COLUMN publisher_id INT,
    ADD COLUMN pub_year VARCHAR(4),
    ADD COLUMN isbn VARCHAR(20)
;

-- add unique constraint
ALTER TABLE tpc_users
	ADD CONSTRAINT uc_tpc_user_display_name UNIQUE (display_name)
;
-- delete unique contraint
ALTER TABLE tpc_users DROP INDEX uc_tpc_user_display_name;
```

## Describe Table
```sql
DESCRIBE books;
```

## Insert Data
```sql
INSERT INTO authors (author_last, author_first, country) VALUES('Greene','Grahan','United Kingdom');
INSERT INTO authors (author_last, author_first, country) VALUES('King','Elias','Swapingdo');

INSERT INTO books (title, author_id, isbn, genre, pub_year) VALUE('The End of the Affair', 1, '099191918', 'novel', '1951');
```

## Query Data

## Update Row

## Delete Row
```sql
DELETE FROM tpc_users WHERE id=10001;
```
