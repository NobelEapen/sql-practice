# sql-practice
SQL query practice — joins, window functions, aggregations. Companion to my Power BI dashboard work.

SQL stands for Structured Query Language
SQL lets you access and manipulate databases
SQL became a standard of the American National Standards Institute (ANSI) in 1986, and of the International Organization for Standardization (ISO) in 1987

**RDBMS**
RDBMS stands for Relational Database Management System.
RDBMS is the basis for SQL, and for all modern database systems such as MS SQL Server, IBM DB2, Oracle, MySQL, and Microsoft Access.
The data in RDBMS is stored in database objects called tables. A table is a collection of related data entries and it consists of columns and rows.

SQL keywords are NOT case sensitive: select is the same as SELECT

A SQL query refers to a block of code that defines what data you’d like to pull from your database. For data analysts, this is generally the start of any analysis. Here is a basic SQL query breakdown:

**SELECT**: Defines columns/fields to pull | To select ALL columns, without specifying every column name, use the SELECT * syntax
  The SELECT DISTINCT statement is used to return only distinct (unique) values.// SELECT DISTINCT Country FROM Customers;
  In a table, a column may contain several duplicate values - and sometimes you want to list only the unique values.
  By using the COUNT() function with the DISTINCT keyword, we can count the number of unique countries.// SELECT COUNT(DISTINCT Country) FROM Customers;

**FROM**: Specifies table(s) to pull from

**WHERE**: Filters data on a condition (or conditions)
  The WHERE clause is used to filter records.
  The WHERE clause is used to extract only those records that fulfill a specific condition. //SELECT * FROM Customers WHERE Country = 'Mexico';
  The WHERE clause is not only used in SELECT statements, it is also used in UPDATE, DELETE, etc.
  The WHERE clause can contain one or many AND operators.
  The AND operator is used to filter records based on more than one condition.
  **Note**: The AND operator displays a record if all the conditions are TRUE.

**GROUP BY**: Group rows based on one or more columns
  The ORDER BY keyword is used to sort the result-set in ascending or descending order.
  The ORDER BY keyword sorts the result-set in ascending order (ASC) by default.
  Sort the products from lowest to highest price // SELECT * FROM Products ORDER BY Price;

**ORDER BY**: Define sort order
  The ORDER BY keyword is used to sort the result-set in ascending or descending order.
  The ORDER BY keyword sorts the result-set in ascending order (ASC) by default.
  Sort the products from lowest to highest price// SELECT * FROM Products  ORDER BY Price;
  To sort the records in descending order, use the **DESC** keyword.
  Sort the products from highest to lowest price// SELECT * FROM Products ORDER BY Price DESC;
  Select all Spanish customers that starts with either "G" or "R" // SELECT * FROM Customers WHERE Country = 'Spain' AND (CustomerName LIKE 'G%' OR CustomerName     LIKE 'R%');
  Without parenthesis, the SQL above will return all customers from Spain that starts with a "G", plus all customers that starts with an "R", regardless of the     country value // SELECT * FROM Customers WHERE Country = 'Spain' AND CustomerName LIKE 'G%' OR CustomerName LIKE 'R%';




  
**LIMIT**: Limit the total number of records returned

UPDATE - updates data in a database
DELETE - deletes data from a database
INSERT INTO - inserts new data into a database
CREATE DATABASE - creates a new database
ALTER DATABASE - modifies a database
CREATE TABLE - creates a new table
ALTER TABLE - modifies a table
DROP TABLE - deletes a table
CREATE INDEX - creates an index (search key)
DROP INDEX - deletes an index
