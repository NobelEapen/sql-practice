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
  The **NOT** operator is used in the WHERE clause to return all records that DO NOT match the specified criteria. It reverses the result of a condition from true   to false and vice-versa.
  The following SQL selects all customers that are NOT from Spain:
  Select only the customers that are NOT from Spain // SELECT * FROM Customers WHERE NOT Country = 'Spain';
  The NOT operator is also used in combination with other operators to exclude data, such as:
 **NOT LIKE**
  **NOT BETWEEN**
  **NOT IN**
  **IS NOT NULL**
 **NOT EXISTS**

1) The NOT LIKE operator is used in the WHERE clause to exclude rows that match a specified character pattern.
There are two wildcards often used in conjunction with the NOT LIKE operator:
**A percent sign %**- represents zero, one, or multiple characters
**A underscore sign _**- represents a single character
The following SQL selects all customers that do NOT start with the letter "A" // SELECT * FROM Customers WHERE CustomerName NOT LIKE 'A%';

2) The NOT BETWEEN operator is used in the WHERE clause to select rows where a value falls outside a specified inclusive range.
The NOT BETWEEN operator can be used with numeric, text, or date values.
The following SQL selects all customers with a CustomerID NOT between 10 and 60// SELECT * FROM Customers WHERE CustomerID NOT BETWEEN 10 AND 60;

3) The NOT IN operator is used in the WHERE clause to exclude rows that match any value in a specified list or a subquery result set.
The following SQL selects all customers with City NOT IN "Paris" or "London"// SELECT * FROM Customers WHERE City NOT IN ('Paris', 'London');

4) The "NOT Greater Than" condition is expressed with the NOT operator in conjunction with the standard greater than or equal to (>=) operator.
The following SQL selects all customers with a CustomerID not greater than 50 // SELECT * FROM Customers WHERE NOT CustomerID > 50;

5) The "NOT Less Than" condition is expressed with the NOT operator in conjunction with the standard less than or equal to (<=) operator.
The following SQL selects all customers with a CustomerID not less than 50 // SELECT * FROM Customers WHERE NOT CustomerId < 50;

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
  Without parenthesis, the SQL above will return all customers from Spain that starts with a "G", plus all customers that starts with an "R", regardless of the      country value // SELECT * FROM Customers WHERE Country = 'Spain' AND CustomerName LIKE 'G%' OR CustomerName LIKE 'R%';

**The INSERT INTO** statement is used to insert new records in a table.
It is possible to write the INSERT INTO statement in two ways:

**Syntax 1:** Specify both the column names and the values to be inserted:
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);

**Syntax 2:** If you insert values for ALL the columns of the table, you can omit the column names.
However, the order of the values must be in the same order as the columns in the table:
INSERT INTO table_name
VALUES (value1, value2, value3, ...);

Here we insert values for ALL the columns of the table, so we omit the column names.
CustomerID	CustomerName	ContactName	Address	City	PostalCode	Country
89	White Clover Markets	Karl Jablonski	305 - 14th Ave. S. Suite 3B	Seattle	98128	USA
90  Wilman Kala	Matti Karttunen	Keskuskatu 45	Helsinki	21240	Finland
91  Wolski	Zbyszek	ul. Filtrowa 68	Walla	01-012	Poland

The following SQL inserts a new record in the "Customers" table:
INSERT INTO Customers
VALUES ('Cardinal', 'Tom B. Erichsen', 'Skagen 21', 'Stavanger', '4006', 'Norway');

++Insert Data Only in Specific Columns++
Here we insert values only in some specific columns of the table.
The following SQL inserts a new record - but only inserts data in the "CustomerName", "City", and "Country" columns (CustomerID will be updated automatically):

Example
INSERT INTO Customers (CustomerName, City, Country)
VALUES ('Cardinal', 'Stavanger', 'Norway');

The last record in the "Customers" table will now look like this:
CustomerID	CustomerName	ContactName	Address	City	PostalCode	Country
92	Cardinal	null	null	Stavanger	null	Norway

**NULL VALUE**
If a field in a table is optional, it is possible to insert or update a record without adding any value to this field. This way, the field will be saved with a NULL value.
A NULL value represents an unknown, missing, or inapplicable data in a database field. It is not a value itself, but a placeholder to indicate the absence of data.
Note: A NULL value is different from zero (0) or an empty string (''). A field with a NULL value is one that has been left blank upon record creation.
It is not possible to test for NULL values with comparison operators, such as =, <, or <>.
We will have to use the IS NULL and IS NOT NULL operators instead.
++The IS NULL Operator++
The IS NULL operator is used to test for empty values (NULL values).
The following SQL lists all customers with a NULL value in the "Address" field:
Example
SELECT CustomerName, ContactName, Address
FROM Customers
WHERE Address IS NULL;
Tip: Always use IS NULL to look for NULL values.

++The IS NOT NULL Operator++
The IS NOT NULL operator is used to test for non-empty values (NOT NULL values).
The following SQL lists all customers with a value in the "Address" field:
Example
SELECT CustomerName, ContactName, Address
FROM Customers
WHERE Address IS NOT NULL;







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
