# sql-practice
SQL query practice — joins, window functions, aggregations. Companion to my Power BI dashboard work.

SQL stands for Structured Query Language
SQL lets you access and manipulate databases
SQL became a standard of the American National Standards Institute (ANSI) in 1986, and of the International Organization for Standardization (ISO) in 1987

**RDBMS**
RDBMS stands for Relational Database Management System.
RDBMS is the basis for SQL, and for all modern database systems such as MS SQL Server, IBM DB2, Oracle, MySQL, and Microsoft Access.
The data in RDBMS is stored in database objects called tables. A table is a collection of related data entries and it consists of columns and rows.

**SQL keywords are NOT case sensitive: select is the same as SELECT**

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

**UPDATE** statement is used to update or modify one or more records in a table.
UPDATE Syntax:
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
Note: Be careful when updating records in a table! Notice the WHERE clause in the UPDATE statement. The WHERE clause specifies which record(s) that should be updated. If you omit the WHERE clause, all records in the table will be updated!
Before Table:
CustomerID	CustomerName	ContactName	Address	City	PostalCode	Country
1 Alfreds Futterkiste	Maria Anders	Obere Str. 57	Berlin	12209	Germany
UPDATE Table
The following SQL updates the record with CustomerID = 1, with a new contact person AND a new city.
Example
UPDATE Customers
SET ContactName = 'Alfred Schmidt', City= 'Frankfurt'
WHERE CustomerID = 1;

The selection from the "Customers" table will now look like this:
After Table:
CustomerID	CustomerName	ContactName	Address	City	PostalCode	Country
1 Alfreds Futterkiste	Alfred Schmidt	Obere Str. 57	Frankfurt	12209	Germany

++UPDATE Multiple Records++
The WHERE clause determines which records that will be updated.
The following SQL will update the ContactName to "Juan" for ALL records where country is "Mexico":

Example
UPDATE Customers
SET ContactName='Juan'
WHERE Country='Mexico';

The selection from the "Customers" table will now look like this:
CustomerID	CustomerName	ContactName	Address	City	PostalCode	Country
1 Alfreds Futterkiste	Alfred Schmidt	Obere Str. 57	Frankfurt	12209	Germany
2	Ana Trujillo Emparedados y helados	Juan	Avda. de la Constitución 2222	México D.F.	05021	Mexico
3	Antonio Moreno Taquería	Juan	Mataderos 2312	México D.F.	05023	Mexico
4 Around the Horn	Thomas Hardy	120 Hanover Sq.	London	WA1 1DP	UK
5	Berglunds snabbköp	Christina Berglund	Berguvsvägen 8	Luleå	S-958 22	Sweden

//Update Warning//
Be careful when updating records. If you omit the WHERE clause, ALL records will be updated!
The following SQL will update the ContactName to "Juan" for ALL records:
Example
UPDATE Customers
SET ContactName='Juan';

The selection from the "Customers" table will now look like this:
CustomerID	CustomerName	ContactName	Address	City	PostalCode	Country
1 Alfreds Futterkiste	**Juan**	Obere Str. 57	Frankfurt	12209	Germany
2	Ana Trujillo Emparedados y helados	**Juan**	Avda. de la Constitución 2222	México D.F.	05021	Mexico

**LIMIT**: Limit the total number of records returned

UPDATE - updates data in a database
DELETE - deletes data from a database
INSERT INTO - inserts new data into a database
CREATE DATABASE - creates a new database
ALTER DATABASE - modifies a database
CREATE TABLE - creates a new table
ALTER TABLE - modifies a table
DROP TABLE - deletes a table

**The DELETE** statement is used to delete existing records in a table.

DELETE Syntax:
DELETE FROM table_name WHERE condition;
Note: Be careful when deleting records in a table! Notice the WHERE clause in the DELETE statement. The WHERE clause specifies which record(s) should be deleted. If you omit the WHERE clause, all records in the table will be deleted!
++SQL DELETE Example++
The following SQL deletes the customer "Alfreds Futterkiste" from the "Customers" table:
Example
DELETE FROM Customers WHERE CustomerName='Alfreds Futterkiste';

Delete All Records
It is possible to delete all records in a table, without deleting the table. This means that the table structure, attributes, and indexes will be intact.
Syntax
DELETE FROM table_name;
The following SQL deletes ALL records in the "Customers" table, without deleting the table:
Example
DELETE FROM Customers;
Delete a Table
To delete the table completely, use the DROP TABLE statement:
Syntax
DROP TABLE table_name;

The following SQL drops the entire "Customers" table:
Example
Delete entire "Customers" table:
DROP TABLE Customers;

The SQL **SELECT TOP** Clause
The SELECT TOP clause is used to limit the number of records to return.
The SELECT TOP clause is useful on large tables with thousands of records. Returning a large number of records can impact performance.
The following SQL selects only the first 3 records of the "Customers" table:
Example
Select only the first 3 records of the Customers table:
SELECT TOP 3 * FROM Customers;
Note: Not all database systems support the SELECT TOP clause. MySQL supports the LIMIT clause to select a limited number of records, while Oracle uses FETCH FIRST n ROWS ONLY.

SELECT TOP with WHERE
The following SQL selects the first three records from the "Customers" table, where Country is "Germany" (for SQL Server/MS Access):
Example
SELECT TOP 3 * FROM Customers
WHERE Country = 'Germany';

SELECT TOP and ORDER BY
Add the ORDER BY keyword when you want to sort the result, and return the first 3 records of the sorted result.
For SQL Server and MS Access:
Example
Sort the result reverse alphabetically by CustomerName, and return the first 3 records:
SELECT TOP 3 * FROM Customers
ORDER BY CustomerName DESC;

**SQL Aggregate Functions**
An aggregate function is a function that performs a calculation on a set of values, and returns a single value.
Aggregate functions are often used with the GROUP BY clause of the SELECT statement. The GROUP BY clause splits the result-set into groups of values and the aggregate function can be used to return a single value for each group.

The most commonly used SQL aggregate functions are:
MIN() - returns the smallest value of a column
MAX() - returns the largest value of a column
COUNT() - returns the number of rows in a set
SUM() - returns the sum of a numerical column
AVG() - returns the average value of a numerical column
Aggregate functions ignore null values (except for COUNT(*)).

1) The SQL MIN() Function
The MIN() function returns the smallest value of the selected column.
The MIN() function works with numeric, string, and date data types.
MIN() Example
Return the lowest price in the Price column, in the "Products" table:
SELECT MIN(Price)
FROM Products;

Set Column Name (Alias)
When using MIN(), the returned column will not have a name.
Use the AS keyword to give the column a descriptive name:
Example
SELECT MIN(Price) AS SmallestPrice
FROM Products;

Use MIN() with GROUP BY
Here we use the MIN() function and the GROUP BY clause, to return the smallest price for each category in the Products table:
Example
SELECT MIN(Price) AS SmallestPrice, CategoryID
FROM Products
GROUP BY CategoryID;
Use MIN() with Date Column
The following SQL returns the earliest BirthDate in the BirthDate column, in the Employees table:
Example
SELECT MIN(BirthDate) AS EarliestBirthdate
FROM Employees;

2) The SQL MAX() Function
The MAX() function returns the largest value of the selected column.
The MAX() function works with numeric, string, and date data types.

MAX Example
Return the highest price in the Price column, in the "Products" table:
SELECT MAX(Price)
FROM Products;

Set Column Name (Alias)
When you use MAX(), the returned column will not have a name.
Use the AS keyword, to give the column a descriptive name:
Example
SELECT MAX(Price) AS HighestPrice
FROM Products;

Use MAX() with Date Column
The following SQL returns the latest BirthDate in the BirthDate column, in the Employees table:
Example
SELECT MAX(BirthDate) AS LatestBirthdate
FROM Employees;

Use MAX() with GROUP BY
Here we use the MAX() function and the GROUP BY clause, to return the highest price for each category in the Products table:
Example
SELECT MAX(Price) AS HighestPrice, CategoryID
FROM Products
GROUP BY CategoryID;

The **COUNT()** function returns the number of rows that matches a specified criterion.
COUNT() Syntax
SELECT COUNT([DISTINCT] column_name | *)
FROM table_name
WHERE condition;

The behavior of COUNT() depends on the argument used within the parentheses:
COUNT(*) - Counts the total number of rows in a table (including NULL values).
COUNT(columnname) - Counts all non-null values in the column.
COUNT(DISTINCT columnname) - Counts only the unique, non-null values in the column.
Using COUNT(*)
The following SQL uses COUNT(*), and counts the total number of rows in the "Products" table (will include NULL values):
Example
SELECT COUNT(*)
FROM Products;

Using COUNT(column_name)
The COUNT(column_name) counts all non-null values in the specified column.
The following SQL counts all non-null values of the "ProductName" column:
Example
SELECT COUNT(ProductName)
FROM Products;

Using COUNT(DISTINCT column_name)
You can ignore duplicates by using the DISTINCT keyword.
The COUNT(DISTINCT column_name) counts only the unique, non-null values in the column.
If DISTINCT is specified, rows with the same value for the specified column will be counted as one.
The following SQL counts the unique, non-null values of the "Price" column:
Example
How many different prices are there in the "Products" table:
SELECT COUNT(DISTINCT Price)
FROM Products;

Add a **WHERE** Clause
You can add a WHERE clause to specify conditions:
Example
Count the number of products where Price is higher than 20:
SELECT COUNT(ProductID)
FROM Products
WHERE Price > 20;

++Use an Alias++
When using COUNT(), the returned column will not have a name. Use the AS keyword to give the column a descriptive name.
Example
Name the "count" column "Number of records":
SELECT COUNT(*) AS [Number of records]
FROM Products;

Use COUNT() with GROUP BY
Here we use the COUNT() function and the GROUP BY clause, to return the number of records for EACH category in the "Products" table:
Example
SELECT COUNT(*) AS [Number of records], CategoryID
FROM Products
GROUP BY CategoryID;

The SQL **SUM()** Function
The SUM() function is used to calculate the total sum of values within a numeric column.
The SUM() function ignores NULL values in the column.
The following SQL returns the sum of the Quantity field in the "OrderDetails" table:
Example
SELECT SUM(Quantity)
FROM OrderDetails;

Add a WHERE Clause
You can add a WHERE clause to specify conditions.
The following SQL returns the sum of the Quantity field for the product with ProductID = 11, in the "OrderDetails" table:
Example
SELECT SUM(Quantity)
FROM OrderDetails
WHERE ProductId = 11;

Use an Alias
Give the summarized column a name by using the AS keyword.
Example
Name the column "total":
SELECT SUM(Quantity) AS total
FROM OrderDetails;

Use SUM() with GROUP BY
Here we use the SUM() function and the GROUP BY clause, to return the Quantity for EACH OrderID in the "OrderDetails" table:
Example
SELECT OrderID, SUM(Quantity) AS [Total Quantity]
FROM OrderDetails
GROUP BY OrderID;

SUM() With an Expression
The parameter inside the SUM() function can also be an expression.
If we assume that each product in the "OrderDetails" table costs 10 dollars, we can find the total earnings in dollars by multiply each quantity with 10:
Example
Use an expression inside the SUM() function:
SELECT SUM(Quantity * 10)
FROM OrderDetails;

The SQL **AVG()** Function
The AVG() function returns the average value of a numeric column.
The AVG() function ignores NULL values in the column.
Example
Find the average price of all products:
SELECT AVG(Price)
FROM Products;
++Note: NULL values are ignored++

Add a WHERE Clause
You can add a WHERE clause to specify conditions:
Example
Return the average price of products in category 1:
SELECT AVG(Price)
FROM Products
WHERE CategoryID = 1;

Use an Alias
Give the AVG column a name by using the AS keyword.
Example
Name the column "average price":
SELECT AVG(Price) AS [average price]
FROM Products;

Higher Than Average
To list all records with a higher price than average, we can use the AVG() function in a sub query:
Example
Return all products with a higher price than the average price:
SELECT * FROM Products
WHERE Price > (SELECT AVG(Price) FROM Products);

Use AVG() with GROUP BY
Here we use the AVG() function and the GROUP BY clause, to return the average price for EACH category in the "Products" table:
Example
SELECT AVG(Price) AS AveragePrice, CategoryID
FROM Products
GROUP BY CategoryID;

The **LIKE** operator is used in a WHERE clause to search for a specified pattern within a column's text data.
There are two wildcards often used in conjunction with the LIKE operator:
A percent sign % - represents zero, one, or multiple characters
A underscore sign _ - represents a single character
The following SQL selects all customers that starts with the letter "a":
Example
Select all customers that starts with the letter "a":
SELECT * FROM Customers
WHERE CustomerName LIKE 'a%';

The % Wildcard
The % wildcard represents any number of characters, even zero characters.
Example
Return all customers from a City that contains the character sequence 'on':
SELECT * FROM Customers
WHERE city LIKE '%on%';

The _ Wildcard
The _ wildcard represents one single character.
It can be any character or number, but each _ represents one, and only one, character.
Example
Return all customers from a City that starts with 'l' followed by one wildcard character, then 'nd' and then two wildcard characters:
SELECT * FROM Customers
WHERE city LIKE 'l_nd__';

Starts With
To return records that starts with a specific letter or phrase, add the % at the end of the letter or phrase.
Example
Return all customers that starts with 'La':
SELECT * FROM Customers
WHERE CustomerName LIKE 'La%';
++Tip: You can also combine any number of conditions using AND or OR operators.++
Example
Return all customers that starts with 'a' or starts with 'b':
SELECT * FROM Customers
WHERE CustomerName LIKE 'a%' OR CustomerName LIKE 'b%';

Ends With
To return records that ends with a specific letter or phrase, add the % at the beginning of the letter or phrase.
Example
Return all customers that ends with 'a':
SELECT * FROM Customers
WHERE CustomerName LIKE '%a';
Tip: You can also combine "starts with" and "ends with":
Example
Return all customers that starts with "b" and ends with "s":
SELECT * FROM Customers
WHERE CustomerName LIKE 'b%s';

Contains
To return records that contains a specific letter or phrase, add the % both before and after the letter or phrase.
Example
Return all customers that contains the phrase 'or'
SELECT * FROM Customers
WHERE CustomerName LIKE '%or%';

Combine Wildcards
Any wildcard, like **%** and **_** , can be used in combination with other wildcards.
Example
Return all customers that starts with "a" and are at least 3 characters in length:
SELECT * FROM Customers
WHERE CustomerName LIKE 'a__%';

Example
Return all customers that have "r" in the second position:
SELECT * FROM Customers
WHERE CustomerName LIKE '_r%';

Without Wildcards
If no wildcard is specified, the phrase has to have an exact match to return a result.
Example
Return all customers from Spain:
SELECT * FROM Customers
WHERE Country LIKE 'Spain';

A wildcard character is used to substitute one or more characters in a string.
Wildcard characters are used with the LIKE operator. The LIKE operator is used in a WHERE clause to search for a specified pattern in a column.
Example
Return all customers that starts with the letter 'a':
SELECT * FROM Customers
WHERE CustomerName LIKE 'a%';

Using the **%** Wildcard
The % wildcard represents any number of characters, even zero characters.
Example
Return all customers that ends with the pattern 'es':
SELECT * FROM Customers
WHERE CustomerName LIKE '%es';

Example
Return all customers that contains the pattern 'mer':
SELECT * FROM Customers
WHERE CustomerName LIKE '%mer%';

Using the **_** Wildcard
The _ wildcard represents a single character.
It can be any character or number, but each _ represents one, and only one, character.
Example
Return all customers with a City starting with any character, followed by "ondon":
SELECT * FROM Customers
WHERE City LIKE '_ondon';
Example
Return all customers with a City starting with "L", followed by any 3 characters, ending with "on":
SELECT * FROM Customers
WHERE City LIKE 'L___on';

Using the **[]** Wildcard
The [] wildcard returns a result if any of the characters inside gets a match.
Example
Return all customers starting with either "b", "s", or "p":
SELECT * FROM Customers
WHERE CustomerName LIKE '[bsp]%';

Using the **-** Wildcard
The - wildcard allows you to specify a range of characters inside the [] wildcard.
Example
Return all customers starting with "a", "b", "c", "d", "e" or "f":
SELECT * FROM Customers
WHERE CustomerName LIKE '[a-f]%';

Combine Wildcards
Any wildcard, like % and _ , can be used in combination with other wildcards.
Example
Return all customers that starts with "a" and are at least 3 characters in length:
SELECT * FROM Customers
WHERE CustomerName LIKE 'a__%';
Example
Return all customers that have "r" in the second position:
SELECT * FROM Customers
WHERE CustomerName LIKE '_r%';

Without Wildcard
If no wildcard is specified, the phrase has to have an exact match to return a result.
Example
Return all customers from Spain:
SELECT * FROM Customers
WHERE Country LIKE 'Spain';

The **IN** operator is used in the WHERE clause to check if a specified column's value matches any value within a provided list.
The IN operator functions as a shorthand for multiple OR conditions, making queries shorter and more readable.
The following SQL uses the IN operator to select all customers from Germany, France, or UK:
Example
SELECT * FROM Customers
WHERE Country IN ('Germany', 'France', 'UK');
The following SQL uses multiple OR conditions to select all customers from Germany, France, or UK (same result, but longer code):
Example
SELECT * FROM Customers
WHERE Country = 'Germany' OR Country = 'France' OR Country = 'UK';

By using the NOT IN operator, you return all records that are NOT any of the values in the list.
Example
Return all customers that are NOT from 'Germany', 'France', or 'UK':
SELECT * FROM Customers
WHERE Country NOT IN ('Germany', 'France', 'UK');

IN (SELECT)
You can also use IN with a subquery in the WHERE clause.
With a subquery you can return all records from the main query that are present in the result of the subquery.
The following SQL returns all customers who also have an order in the "Orders" table:
Example
SELECT * FROM Customers
WHERE CustomerID IN (SELECT CustomerID FROM Orders);

NOT IN (SELECT)
The result in the example above returned 74 records, that means that there are 17 customers that haven't placed any orders.
Let us check if that is correct, by using the NOT IN operator.
The following SQL returns all customers who do NOT have any orders in the "Orders" table:
Example
SELECT * FROM Customers
WHERE CustomerID NOT IN (SELECT CustomerID FROM Orders);

The **BETWEEN** operator is used in the WHERE clause to select values within a specified range.
The range is inclusive - the beginning and end values of the range are included in the results.
The values can be numbers, text, or dates.
Example
Select all products with a price between 10 and 20:
SELECT * FROM Products
WHERE Price BETWEEN 10 AND 20;

The NOT BETWEEN operator is used in the WHERE clause to select values outside a specified range.
The following SQL returns all products with a price NOT between 10 and 20:
Example
SELECT * FROM Products
WHERE Price NOT BETWEEN 10 AND 20;

BETWEEN with IN
The following SQL returns all products with a price between 10 and 20. In addition, the CategoryID must be either 1, 2 or 3:
Example
SELECT * FROM Products
WHERE Price BETWEEN 10 AND 20
AND CategoryID IN (1,2,3);

BETWEEN Text Values
The following SQL selects all products with a ProductName alphabetically between 'Geitost' and 'Louisiana Hot Spiced Okra':
Example
SELECT * FROM Products
WHERE ProductName BETWEEN 'Geitost' AND 'Louisiana Hot Spiced Okra'
ORDER BY ProductName;

NOT BETWEEN Text Values
The following SQL selects all products with a ProductName NOT between 'Geitost' and 'Louisiana Hot Spiced Okra':
Example
SELECT * FROM Products
WHERE ProductName NOT BETWEEN 'Geitost' AND 'Louisiana Hot Spiced Okra'
ORDER BY ProductName;

BETWEEN Dates
The BETWEEN operator is useful for filtering records within a specific date or time period. Ensure the date format matches the database (e.g. 'YYYY-MM-DD').
The following SQL selects all orders placed in July, 1996:
Example
SELECT * FROM Orders
WHERE OrderDate BETWEEN '1996-07-01' AND '1996-07-31';

An alias is created with the **AS** keyword, and is often used to make a column name more readable.
An alias only exists for the duration of that query.
Alias for Columns
The following SQL creates two aliases, one for the CustomerID column and one for the CustomerName column:
Example
SELECT CustomerID AS ID, CustomerName AS Customer
FROM Customers;

Aliases with Spaces
If you want your alias to contain one or more spaces, like "My Great Products", surround the aliasname with square brackets or double quotes:
Example
Using [square brackets] for aliases with space characters:
SELECT ProductName AS [My Great Products]
FROM Products;

OR:

Example
Using "double quotes" for aliases with space characters:
SELECT ProductName AS "My Great Products"
FROM Products;

Concatenate Columns
The following SQL creates an alias named "Address" that combine four columns (Address, PostalCode, City and Country):
Example
SELECT CustomerName, Address + ', ' + PostalCode + ' ' + City + ', ' + Country AS Address
FROM Customers;

The **JOIN** clause is used to combine rows from two or more tables, based on a related column between them.
Here are the different types of JOINs in SQL:
(INNER) JOIN: Returns only rows that have matching values in both tables
LEFT (OUTER) JOIN: Returns all rows from the left table, and only the matched rows from the right table
RIGHT (OUTER) JOIN: Returns all rows from the right table, and only the matched rows from the left table
FULL (OUTER) JOIN: Returns all rows when there is a match in either the left or right table

Look at an order in "Orders" table:
OrderID	CustomerID	OrderDate
10308	2	1996-09-18

Then, look at a customer in the "Customers" table:
CustomerID	CustomerName	ContactName	Country
2	Ana Trujillo Emparedados y helados	Ana Trujillo	Mexico
Here we see that the "CustomerID" column in the "Orders" table refers to the "CustomerID" in the "Customers" table. The relationship between the two tables above is the "CustomerID" column.
Then, we can create the following SQL statement (that contains an INNER JOIN), that selects records that have matching values in both tables:

Example
SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate
FROM Orders
INNER JOIN Customers ON Orders.CustomerID=Customers.CustomerID;

The **INNER JOIN** returns only rows that have matching values in both tables.
Tip: You can use just JOIN instead of INNER JOIN, as INNER is the default join type.
Example
Join "Products" and "Categories" with the INNER JOIN keyword:
SELECT ProductID, ProductName, CategoryName
FROM Products
INNER JOIN Categories ON Products.CategoryID = Categories.CategoryID;

++Note: INNER JOIN returns only rows with a match in both tables. This means that if there is a product with no CategoryID, or with a CategoryID not present in the Categories table, that row will not be returned in the result.++

Naming the Columns
It is a good practice to also include the table name when specifying columns in SQL joins:
Example
Add table name in front of column names:
SELECT Products.ProductID, Products.ProductName, Categories.CategoryName
FROM Products
INNER JOIN Categories ON Products.CategoryID = Categories.CategoryID;

The example above works without specifying table names, because none of the specified column names are present in both tables. However, if you add the CategoryID column in the SELECT statement, an error occurs, if you do not specify the table name. This is because the CategoryID column is present in both tables.

**JOIN** and **INNER JOIN** will return the same result.
INNER is the default join type for JOIN, so when you write JOIN the parser actually writes INNER JOIN.
Example
JOIN is the same as INNER JOIN:
SELECT Products.ProductID, Products.ProductName, Categories.CategoryName
FROM Products
JOIN Categories ON Products.CategoryID = Categories.CategoryID;

JOIN Multiple Tables
You can join more than two tables by adding multiple INNER JOIN clauses in your query.
The following SQL selects all orders with customer and shipper information:
Example
SELECT Orders.OrderID, Customers.CustomerName, Shippers.ShipperName
FROM Orders
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID
INNER JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID;

SQL LEFT JOIN
The **LEFT JOIN** returns all rows from the left table (table1), and only the matched rows from the right table (table2).
If there is no match in the right table, the result for the columns from the right table will be NULL.
The LEFT JOIN and LEFT OUTER JOIN keywords are equal - the OUTER keyword is optional.

SQL LEFT JOIN Examples
The following SQL returns all customers and their orders, including customers who have not placed any orders:
Example
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID
ORDER BY Customers.CustomerName;

++Tip: To find only the customers who have not placed any order, add a WHERE clause to filter for NULL values on the right table:++
Example
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID
WHERE Orders.CustomerID IS NULL;

SQL **RIGHT JOIN**
The RIGHT JOIN returns all rows from the right table (table2), and only the matched rows from the left table (table1).
If there is no match in the left table, the result for the columns from the left table will be NULL.
The RIGHT JOIN and RIGHT OUTER JOIN keywords are equal - the OUTER keyword is optional.

SQL RIGHT JOIN Example
The following SQL will return all employees, and any orders they might have placed:
Example
SELECT Orders.OrderID, Employees.LastName, Employees.FirstName
FROM Orders
RIGHT JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
ORDER BY Orders.OrderID;

Note: The RIGHT JOIN keyword returns all records from the right table (Employees), even if there are no matches in the left table (Orders).

SQL FULL JOIN
The **FULL JOIN** returns all rows when there is a match in either the left or right table.
If a row in the left table has no match in the right table, the result set includes the left row's data and NULL values for all columns of the right table.
If a row in the right table has no match in the left table, the result set includes the right row's data and NULL values for all columns of the left table.
The FULL JOIN and FULL OUTER JOIN keywords are equal - the OUTER keyword is optional.
++Note: FULL JOIN can potentially return very large result-sets!++

SQL FULL JOIN Example
The following SQL statement selects all customers, and all orders:
Example
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
FULL JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;

Note: FULL JOIN returns all matching records from both tables whether the other table matches or not. So, if there are rows in "Customers" that do not have matches in "Orders", or if there are rows in "Orders" that do not have matches in "Customers", those rows will be listed as well.

A self join is a regular join, but the table is joined with itself.
The following SQL statement matches customers that are from the same city:
Example
SELECT A.CustomerName AS CustomerName1, B.CustomerName AS CustomerName2, A.City
FROM Customers A, Customers B
WHERE A.CustomerID <> B.CustomerID
AND A.City = B.City
ORDER BY A.City;

The SQL **UNION** Operator
The UNION operator is used to combine the result-set of two or more SELECT statements.
The UNION operator automatically removes duplicate rows from the result set.
Requirements for UNION:
Every SELECT statement within UNION must have the same number of columns
The columns must also have similar data types
The columns in every SELECT statement must also be in the same order

The following SQL returns the unique (distinct) countries from both the "Customers" and the "Suppliers" table:
Example
SELECT Country FROM Customers
UNION
SELECT Country FROM Suppliers
ORDER BY Country;

Note: If some customers or suppliers have the same country, each country will only be listed once, because UNION selects only distinct values. Use UNION ALL to also select duplicate values!
Here we add a WHERE clause to only return the unique German cities from both the "Customers" and the "Suppliers" table:
Example
SELECT City, Country FROM Customers
WHERE Country='Germany'
UNION
SELECT City, Country FROM Suppliers
WHERE Country='Germany'
ORDER BY City;

Another UNION Example
The following SQL lists all customers and suppliers:
Example
SELECT 'Customer' AS Type, ContactName, City, Country
FROM Customers
UNION
SELECT 'Supplier', ContactName, City, Country
FROM Suppliers;

Notice the "AS Type" above - it is an alias. Aliases are used to give a column a temporary name. So, here we have created a temporary column named "Type", that list whether the contact person is a "Customer" or a "Supplier".


The SQL UNION ALL Operator
The **UNION ALL** operator is used to combine the result-set of two or more SELECT statements.
The UNION ALL operator includes all rows from each statement, including any duplicates.
Requirements for UNION ALL: 
Every SELECT statement within UNION ALL must have the same number of columns
The columns must also have similar data types
The columns in every SELECT statement must also be in the same order

Note: The column names in the result-set are usually equal to the column names in the first SELECT statement.

SQL UNION ALL Example
The following SQL returns all the countries (also duplicate values) from both the "Customers" and the "Suppliers" table:
Example
SELECT Country FROM Customers
UNION ALL
SELECT Country FROM Suppliers
ORDER BY Country;

SQL UNION ALL With WHERE
Here we add a WHERE clause to return all the German cities from both the "Customers" and the "Suppliers" table:
Example
SELECT City, Country FROM Customers
WHERE Country='Germany'
UNION ALL
SELECT City, Country FROM Suppliers
WHERE Country='Germany'
ORDER BY City;

The SQL GROUP BY Statement
The GROUP BY statement is used to group rows that have the same values into summary rows, like "Find the number of customers in each country".
The GROUP BY statement is almost always used in conjunction with aggregate functions, like COUNT(), MAX(), MIN(), SUM(), AVG(), to perform calculations on each group.

SQL GROUP BY Examples
The following SQL returns the number of customers in each country:
Example
SELECT Country, COUNT(CustomerID) AS [Number of Customers]
FROM Customers
GROUP BY Country;

The following SQL returns the number of customers in each country, sorted from high to low:
Example
SELECT Country, COUNT(CustomerID) AS [Number of Customers]
FROM Customers
GROUP BY Country
ORDER BY COUNT(CustomerID) DESC;

GROUP BY With JOIN Example
The following SQL returns the number of orders sent by each shipper:
Example
SELECT Shippers.ShipperName, COUNT(Orders.OrderID) AS NumberOfOrders
FROM Orders
LEFT JOIN Shippers
ON Orders.ShipperID = Shippers.ShipperID
GROUP BY ShipperName;

The SQL **HAVING** Clause
The HAVING clause is used to filter the results of a GROUP BY query based on aggregate functions.
Unlike the WHERE clause, which filters individual rows before grouping, the HAVING clause filters groups after the aggregation has been performed.

SQL HAVING Examples
The following SQL returns the number of customers in each country - but only include countries with more than 5 customers:
Example
SELECT Country, COUNT(CustomerID) AS [Number of Customers]
FROM Customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5;

The following SQL returns the number of customers in each country, sorted from high to low (and only include countries with more than 5 customers):
Example
SELECT Country, COUNT(CustomerID) AS [Number of Customers]
FROM Customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5
ORDER BY COUNT(CustomerID) DESC;

More HAVING Examples
The following SQL returns the employees that have registered more than 10 orders:
Example
SELECT Employees.LastName, COUNT(Orders.OrderID) AS NumberOfOrders
FROM Orders
INNER JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
GROUP BY LastName
HAVING COUNT(Orders.OrderID) > 10;

The following SQL returns if the employees "Davolio" or "Fuller" have registered more than 25 orders:
Example
SELECT Employees.LastName, COUNT(Orders.OrderID) AS NumberOfOrders
FROM Orders
INNER JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
WHERE LastName = 'Davolio' OR LastName = 'Fuller'
GROUP BY LastName
HAVING COUNT(Orders.OrderID) > 25;

