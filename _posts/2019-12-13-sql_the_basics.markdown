---
layout: post
title:      "SQL the Basics"
date:       2019-12-13 13:53:15 -0500
permalink:  sql_the_basics
---


SQL(Structured Query Language) is a language for managing data in a database When creating tables be sure to use lowercase and snake case (snake_case). 

## creating a database 
```sqlite3 database_name.db```

To create a table we must also be sure to include colmun names as well. For instance **CREATE TABLE table_name ( id INTEGER PRIMARY KEY, name TEXT, age INTEGER);** 

`.schema` will allow you to look at the structure of the database. 

**ALTER TABLE** allows you to **ADD COLUMN** or **REMOVE COLUMN** 

**DROP TABLE** will delete the whole table

To exit the command prompt use `.quit`

*If you happen to get stuck in the sql command prompt and keep seeing this `..>` just type in a semicolon. 
*

To create a database create a file (filename.db). Then create a sql file (01_create_table) Insert whatever column information is needed. Save and add this to the database by doing this **filename.db < 01_create_table.sql**. You can confirm the table is created by opening the sql command prompt (sqlite3 filename.db) and running the schema command. Once you've confirmed it updated, exit.

## SQL datatypes 

TEXT - alphanumeric characters
INTEGER - whole number
REAL - decimal number 
BLOB - stores binary data

## Inserting, Updating, and Selecting

INSERT INTO command, followed by the name of the table followed by the VALUES keyword ('Maru', 3, 'Scottish Fold');

SELECT [names of columns we are going to select] FROM [table we are selecting from];

To retrieve:
SELECT * FROM cats;
*this returns the same as above, but with more typing:
(SELECT id, name, age, breed FROM cats;) 

Can also be written like:
SELECT cats.name FROM cats;

To select more then one table  but not all include a comma in between table names.

Use WHERE to retrieve specific table row. **SELECT * FROM table_name WHERE column_name = some_value;**

To update **UPDATE [table name] SET [column name] = [new value] WHERE [column name] = [value];**

To delete **UPDATE [table name] SET [column name] = [new value] WHERE [column name] = [value];**

## SQL queries 
ORDER BY. This modifier allows us to order the table rows returned by a certain SELECT statement:
**SELECT column_name FROM table_name ORDER BY column_name ASC|DESC;
**

LIMIT is used to determine the number of records you want to return from a dataset. For example:
**SELECT * FROM cats ORDER BY age DESC LIMIT 1;**

BETWEEN allows us to find information in between a certan range: 
**SELECT column_name(s) FROM table_name WHERE column_name BETWEEN value1 AND value2;**

NULL can be used to set data that has no value yet:
**INSERT INTO cats (name, age, breed) VALUES (NULL, NULL, "Tabby");**
You can also retrieve a NULL value:
**SELECT * FROM cats WHERE name IS NULL;**

COUNT will count the number of records that meet certain condition:
**SELECT COUNT(owner_id) FROM cats WHERE owner_id = 1;** *=> 2*

GROUP BY groups your results by a given column:
**SELECT breed, COUNT(breed) FROM cats GROUP BY breed;**
This should return:

breed               COUNT(breed)
------------------  ------------
American Shorthair  1           
Calico                             1           
Scottish Fold               1           
Tabby                              3           


## Aggregators

AVG(), - average value of a column:
**SELECT AVG(column_name) FROM table_name;**

**AS** keyword to rename the column. This is called "aliasing the return value".

SUM(),- sum of all of the values in a particular column:
**SELECT SUM(column_name) FROM table_name;**

MIN() and MAX() - minimum and maximum values from a specified column:
**SELECT MIN(column_name) FROM table_name;
SELECT MAX(column_name) FROM table_name;**

COUNT() - count function returns the number of rows that meet a certain condition:
**SELECT COUNT(column_name) FROM table_name;** => returns integer

