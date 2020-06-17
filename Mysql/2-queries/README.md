To download mysql, type in this command:
` sudo apt-get install mysql-server `

To download workbench:
sudo apt-get install mysql-workbench


CREATE TABLE tablename ( );


CREATE TABLE tablename ( id INT, name TEXT, age INT );



How to sign in using my computer:
Open Terminal;
Type in: 'mysql -u root -p';
you will then be prompted with this message: 'Enter password: '
The password is: 'root'.

If successful. you should be displayed this message:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 6
Server version: 5.7.24-0ubuntu0.16.04.1 (Ubuntu)

Copyright (c) 2000, 2018, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> 



MYSQL Commands
SHOW WARNINGS;
CREATE DATABASE database_name
CREATE DATABASE IF NOT EXISTS my_database;
SHOW DATABASES;
SELECT DATABASE();
DROP DATABASE mydatabase;
DROP DATABASE IF EXISTS mydatabase;

tables
USE tablename;
SHOW TABLES;
DESCRIBE tablename; == SHOW COLUMNS FROM tablename;
CREATE TABLE tablename ( );
DROP TABLE tablename;

SELECT queries commands
SELECT * FROM tablename;
SELECT * FROM tablename LIMIT number;
SELECT * FROM tablename
	ORDER BY column1, column2 ... ASC|DESC;
SELECT column AS col FROM tablename
SELECT * FROM Products
	WHERE (Price BETWEEN 10 AND 20)
	AND NOT CategoryID IN (1,2,3);

SELECT	column1, column2
	FROM table
	WHERE column LIKE pattern;

Aggregate functions
SELECT MIN|MAX|COUNT|AVG|SUM (column_name) FROM tablename;

INSERT INTO tablename VALUES ( ... );
UPDATE tablename 
	SET column1 = value1
	WHERE condition;

DELETE FROM tablename WHERE condition;

ALTER TABLE table_name
ADD column_name datatype;

ALTER TABLE table_name
DROP COLUMN column_name;

ALTER TABLE table_name
MODIFY COLUMN column_name datatype;

Syntax
The syntax to rename a table in MySQL is:

ALTER TABLE table_name
  RENAME TO new_table_name;


IF YOU WANT TO RUN MYSQL SCRIPT FROM COMMAND LINE:

https://stackoverflow.com/questions/8940230/how-to-run-sql-script-in-mysql

If you’re at the MySQL command line mysql>
just declare the SQL file as source.

mysql> source \home\user\Desktop\test.sql;






mysql> CREATE TABLE person2 ( id INT AUTO_INCREMENT primary key NOT NULL, age INT );
Query OK, 0 rows affected (0.30 sec)

/*
Set the auto increment field to NULL or 0 if you want it to be auto magically assigned...
*/

in which case^
CREATE TABLE person2 ( id INT AUTO_INCREMENT primary key, age INT );

(BTW, you could've also swapped AUTO_INCREMENT WITH primary key like so:

CREATE TABLE person2 ( id INT primary key AUTO_INCREMENT, age INT );

and to insert...
INSERT INTO person2 values ( NULL , [just type in a value] );

