# SQL Part 1

## <p id = "toc"> Table of Contents </p>
0. [Lesson 0: Before We Begin](#0)
1. [Lesson 1: Executing a Simple Query](#1)
2. [Lesson 2: Performing a Conditional Search](#2)
3. [Lesson 3: Working with Functions](#3)
4. [Lesson 4: Organizing Data](#4)
5. [Lesson 5: Retrieving Data from Multiple Tables](#5)
6. [Lesson 6: Exporting Query Results](#6)

/* -------------------------------------------------------
## <p id = "0"> LESSON 0: Before We Begin </p>
---------------------------------------------------------- */

----- 

### About the Data:  
We’ll be working with data from a publishing company that sells books to bookstores.

You can download SQL Server Management Studio(SSMS) online [here](https://www.microsoft.com/en-us/sql-server/sql-server-downloads).

The main parts of the SSMS interface are the:
- Object Explorer: Navigate through databases, tables, views, stored procedures, etc. 
    - We can hide/unhide this pane if needed.
- Query Editor: Write and run SQL queries.
- Results Pane: Ctrl + R - Toggles the results pane

```
	To Show Lines in the Query Editor:
		1. Go to Tools > Options 
		2. Expand 'Text Editor' -> Transact-SQL -> General. 
		3. Check the Line numbers box and click OK
```



> NOTE:  
> Suppose we use Task Manager to close SQL Server Management Studio (SSMS).
Reopening SSMS could cause problems, so we’ll use SQL Server 20XX Configuration Manager to start the service.  
Additional Note: Don’t use Windows Services to start SSMS.

1. Type in 'Configuration Manager' to launch the application
2. Start the service for 'SQL Server' (SQL EXPRESS)
3. Relaunch SSMS normally.

[Stack Overflow Reference](https://stackoverflow.com/questions/35630344/unable-to-connect-to-local-sql-server-after-ending-tasks)



/* -------------------------------------------------------
## <p id = "1"> LESSON 1: Executing a Simple Query | [Back to ToC](#toc) </p>
---------------------------------------------------------- */

### Our First Query

Press `CTRL + N` to launch a new query.

In SQL Server, we can run a simple statement:  
``` SELECT 1+3 ``` 

There are different ways to execute the query:  
	- Shortcuts: F5, Ctrl + E, Alt + X  
	- Click the green 'Execute' button on the toolbar.  
	- Go to Query (tab) -> Execute.  
	- Right-click anywhere in the query window and choose 'Execute SQL' from the context menu.  

> NOTE: T-SQL is a Declarative language that supports some precedural syntax.

### SQL Comments
Comments are used explain SQL code or add notes for the reader. They are ignored by the database engine and are not executed.
``` sql
-- Two -'s are used to write a single-line comment.  
-- Text after -- is ignored to the end of the line.
SELECT 1+3 -- Output: 4
```

#### SQL Multi-line Comments
Multi-line comments begin with /* and end with */. Any text between them is ignored.

``` sql
/*  
	The 
	query 
	below 
	outputs 
	4.
*/
SELECT 1 + 3
```

---

In SQL Server, you can include multiple SELECT statements in a single query batch and each will return its own result set.

``` sql
SELECT 1+3
SELECT 'After Insertion:'	-- Outputs simple text
PRINT 'Hello World! Bye!' 	-- Displays a message or a value in the 'Messages' tab and is mainly used for debugging
```

---

SQL Server provides built-in functions that format how data is displayed and can perform calculations e.g. rounding values.
``` sql
SELECT FORMAT(1+3, 'C')  				-- FORMAT Function converts the number into a string, where 'C' stands for Currency.
SELECT FORMAT(123.490000000, '0.##')	-- Output: 123.49
SELECT ROUND(235.415, 2) AS RoundValue;	-- Output: 235.420 
-- Note: MS Excel has a round function too 
-- = ROUND(D2,0) -- given that D2 = 235.415
```

---

### Selecting Data from a Database

To return all data from the `Slspers` table:  
``` sql
USE Pub1  
SELECT *  	 -- Selects ALL columns
FROM slspers -- Note: Spelling matters. Typing 'slsperson' won't execute.
```

> In SQL Server, a SELECT query can also be made from the Object Explorer:  
> Right-click the table name and choose 'Select Top 1000 Rows'.

Optional Exercise: Retrieve the data from the other 3 tables:  
``` sql
SELECT * FROM Customers  
SELECT * FROM Titles  
SELECT * FROM Sales  
```

Queries can be written to output individual columns.  

``` sql
-- Output the first and last names of everyone in the `Slspers` table.
SELECT fname, lname
FROM slspers;
```

#### SQL Prefix
A prefix can be used in front of a column or even table name to specify its source and avoid ambiguity

``` sql
-- `Slspers` is a table prefix for the column `fname`
SELECT  
	Slspers.fname, Slspers.lname  
FROM Slspers;
```

Table prefixes can also be used before the wildcard asterisk (*).
``` sql
SELECT Slspers.* FROM Slspers    
-- Same as:  
-- SELECT * FROM Slspers
```

#### Alias 'AS' Keyword 
In SQL, aliases are used to give a table or a column a temporary name and are useful when renaming long or confusing column names

``` sql
SELECT 
	fname AS [First Name], 
	lname AS 'Last Name' 
FROM Slspers; 
```

NOTE: The keyword 'AS' is not needed since it's just a formality.  
``` sql 
SELECT 
	fname, 
	lname 'Last Name' 
FROM Slspers; 
```

#### ...more to discuss in Chapter 5! [Link to Lesson 5](#5). 

---

### Calculated/Derived columns
In SQL, a new "calculated" column can be added to the query result by using a fixed value or calculation. This column appears ONLY in the results and is neither stored nor affect the actual table.

``` sql
SELECT 
	fname, 
	lname, 
	'United States' AS Country, 
	'21' AS Age  
FROM Slspers
```

#### Round Function
The ROUND() function rounds a number to however many decimal places needed.
``` sql
SELECT  
	slprice,  
	ROUND(slprice,0) -- Round to nearest number  
FROM Titles
```

ADVANCED: To create a new rounded column:
``` sql
ALTER TABLE Titles
ADD RoundedPrice INT;

UPDATE Titles
SET RoundedPrice = ROUND(slprice, 0);
```

Remember: A calculated column doesn't exist in a table, yet SQL will calculates the function for each row when the query runs. 

Another Example:
``` sql
SELECT  
	partnum,   
	bktitle,  
	slprice,  
	slprice * 1.2 AS slprice_inflation,       

	-- To Remove trailing 0's without rounding:  
	FORMAT(slprice * 1.2, '0.##') AS discounted_price, -- Good Solution:	0's removed, but some prices only have whole dollars   
	CAST(slprice * 1.2 AS DECIMAL(10,2))  AS Inflation -- Better Solution:	Force two decimal places everywhere.
FROM Titles
```

### Keyboard Shortcuts:

> Ctrl + R (Hide the Result Pane)

> Ctrl+K; Ctrl+C (comment)  
> Ctrl+K; Ctrl+U (uncomment)

> CTRL + Shift + U (Uppercase)  
> CTRL + Shift + L (Lowercase)

--- 

To create custom keyboard shortcuts for useful commands e.g.  executing queries:
1. 	Go to Tools -> Options
2. 	Navigate to:
	Environment → Keyboard
3.  In 'Show commands containing', search for: `Query.Execute` & click on it
4.  Under 'Press shortcut keys', press your desired combination (e.g., Ctrl + Shift + N)
5.  Click Assign, then OK

<img src = "./zz_add_shortcut.png" />

---

MS SQL Server holds many stored procedures that act as a saved set of SQL commands

For instance, to display a table structure:  
```
SP_HELP Slspers  
```

Additionally, in Object Explorer, right-click on the table of your choice and click “Design” to view and modify the table’s structure

``` sql 
-- Albeit advanced, the below command also outputs column names  
SELECT COLUMN_NAME  
FROM INFORMATION_SCHEMA.COLUMNS  
WHERE TABLE_NAME = 'Slspers'
```

### Create a Backup Table
``` sql
-- Excercise: Create a Backup table
SELECT *  
INTO Slspers_Backup  
FROM Slspers;  
```

- In SQL Server, once the command is executed, we will need to refresh the Object Explorer by clicking the button Refresh (F5)  
- Then, we will need to hide the folder 'Tables' & expand the folder again.  

-- When you create a new table in SQL, IntelliSense may not recognize it right away and can display a red squiggly line indicating an invalid object name.  
-- To refresh IntelliSense cache, either press (Ctrl + Shift + R) or go to Edit -> IntelliSense -> Refresh Local Cache

> Note: Not good practice to create duplicate tables unless for sandboxes & backups

Albeit advanced, we can also create a 'NewCustomers' table but with structure only  
``` sql
SELECT *  
INTO NewCustomers  
FROM Customers  
WHERE 1 = 0;  
-- To create an empty table (structure only),   
-- use WHERE 1 = 0 or similar condition.
```

To delete a table:  
``` sql
DROP TABLE IF EXISTS titles_backup  
-- (Note: This will PERMANENTLY delete the table unless you have a backup or haven’t committed the changes yet!) 
```  

To drop a table, you can also do the following:  
- Right-click the table name in Object Explorer and select 'Delete'.

Lastly, to truncate a table i.e. to remove all rows from table:   
``` TRUNCATE TABLE titles_backup  ```

---

Note: To Run T-SQL via the command line:  
```
C:\Users\student> sqlcmd -S UT-LAPTOP\SQLEXPRESS -E  
1> select 1 + 2;  
2> GO  

1> USE Pub1;  
2> SELECT * FROM Slspers;  
3> Go  
```

If a SQL Script has been saved, it can also be executed from the command line:
```
sqlcmd -S UT-LAPTOP\SQLEXPRESS -E -i "C:\Users\student\Documents\SQL Script Command Line\SQLQuery.sql"
```

/* -------------------------------------------------------
## <p id = "2"> LESSON 2: Performing a Conditional Search | [Back to ToC](#toc) </p>
---------------------------------------------------------- */


<!-- SORTING & FILTERING CHAPTER -->

In the last chapter, a connection to a server was made and a few basic queries were executed.  
This chapter will cover how to sort & filter results to reorganize and display only the data needed.

### Sorting
Sorting organizes query results in ascending or descending order.

#### Example: Sort data by a single column:  
``` sql
SELECT *  
FROM Customers   
ORDER BY state ASC -- Sorts the table by state column  
-- IN SQL SERVER, ORDER BY defaults to ASC.  
```

A multi-level sort can be applied by listing column names in sequence and separating them with commas.

#### Example of a Multi-Level Sort:  
``` sql
SELECT *  
FROM Customers  
ORDER BY state ASC, city DESC, custname ASC    
-- This means that the customer data is sorted first by State, and if some records share the same State, those records are then sorted by City.  
-- For those customers in the same city, those records are then further sorted by name.
```

The `SELECT TOP` clause limits the number of records returned. It is especially useful for large tables, as retrieving too many records can slow performance.

#### Example: Select only the top 5 rows of the Customers Table:  
``` sql
SELECT  
TOP 5  
*  
FROM Customers  
ORDER BY State ASC
```

-- In SSMS, you can use the 'Query Options' command to set the ROWCOUNT value.  
-- i.e. 'Specify the maxinum number of rows to return before the server stops processing'


### Where Clause
The SQL WHERE clause filters results by applying one or more conditions so that only records that meet the criteria are returned (or affected). A condition is a rule for finding specific data and consists of a column (or expression), an operator, and a value to compare.

#### Example of Where Clause
``` sql
SELECT *  
FROM Customers  
WHERE state = 'NY'   
-- The WHERE clause acts as a Filter. Verify that 6 people are returned.  

-- NOTE: In SQL Server, use single quotation marks (' ') for string literals.  
-- Double quotation marks (" ") are not valid for this purpose and will not work in a query.
```

> Practice Exercise: Show all people from the city 'Houston'.

Below are more examples demonstrating various ways the WHERE clause can be used:  
- WHERE clause used with numbers:
	``` sql
	-- Another Example  
	SELECT *  
	FROM  titles  
	WHERE  
	-- NOT  
	slprice      >            50  
	column    operator       value
	```

- WHERE clause used with showing book titles with dates past 1/1/2017
	``` sql 
	SELECT 
		bktitle, 
		CAST(pubdate AS DATE) -- CAST is used to truncate the time portion  
	FROM Titles  
	WHERE pubdate > '2017-01-01' -- Note: Date must be wrapped in ''  
	ORDER BY pubdate
	```

- BE CAREFUL: Computed or alias columns aren't part of the actual table, so they can't be used in the `WHERE` clause since WHERE is evaluated before SELECT.
	``` sql
	SELECT  
		partnum,  
		bktitle,  
		slprice - slprice * 0.07 AS discounted_price  
	FROM Titles  
	WHERE slprice - slprice * 0.07 >= 45  
	-- WHERE discounted_price >= 45 -- WON'T WORK!  
	ORDER BY discounted_price DESC  -- WILL WORK!  
	```

- WHERE Clause used with creating a new table from a filter:
	``` sql
	SELECT *  
	INTO CA_Customers  -- Creates a new table called 'CA_Customers'  
	FROM Customers  
	WHERE state = 'CA'  
	```

	- TO DELETE:  
	``` DROP TABLE CA_Customers ```  

- Another Example  
	``` sql
	SELECT *  
	INTO HighEarners  
	FROM Slspers  
	WHERE commrate > 0.04;  
	```

### SQL NOT Operator 
The NOT operator is used in the WHERE clause to return records that do not match a specific condition.

#### Example: Returns all customers NOT from NY:
``` sql
SELECT *  
FROM Customers  
WHERE NOT state = 'NY'    
-- ORDER BY state  
```

### NULL Values
In SQL, a `NULL` value represents void or empty data in a table field. Similar to a blank cell in Excel, in databases a `NULL` value is a placeholder that represents missing or blank data, and is different from a numeric zero or an empty string.

#### Example of WHERE clause with NULL:  
``` sql
SELECT *  
FROM Titles  
WHERE devcost IS  
-- NOT  
NULL  
```

Additionally, ISNULL() is a function that replaces `NULL` values with an alternate value. This function is similar to the Excel function ' IF( ISBLANK() ) '  
> Note: In MySQL, use the function IFNULL() instead.

For example, if a table looked like this:
```
Name	Bonus  
Alice	1000  
Bob		NULL  
Charlie	500  
```

Running the following query will replace null values with 0:  
``` sql
SELECT Name, ISNULL(Bonus, 0) AS BonusAmount  
FROM Employees;
```

Result:
```
Result:  
Name	Bonus  
Alice	1000  
Bob		0  
Charlie	500  
```

Advanced: To permanently update all `NULL` values with a generic statement:
``` sql
UPDATE Employees
SET Bonus = 0
WHERE Bonus IS NULL;
```

### AND Operator
The AND operator displays a record if all the searched conditions are TRUE.

> Remember: EVERY (All) condition MUST be true. [Similar to Excel Function]

Exercise: Show only customers from Denver, CO since there are multiple Denver cities in America.
``` sql
SELECT *  
FROM customers  
WHERE state = 'CO' AND city = 'Denver'  
```

1 MIN Optional Exercise: Show all customers that live in NY but NOT in the city of Buffalo.
``` sql
SELECT *  
FROM customers  
WHERE state = 'NY' AND NOT city = 'Buffalo'
```

Exercise: Show all sales records made by sales representative 'N02' where the quantity sold is greater than 200
``` sql
SELECT *  
FROM sales  
WHERE repid = 'N02' AND qty > 200  
ORDER BY qty 
```

Exercise: Show all book titles whose sales price is between $30 & $40.
``` sql
SELECT *  
FROM Titles  
WHERE slprice >= 30 AND slprice <= 40  
-- Also works: WHERE slprice BETWEEN 30 AND 40 -- does the same as above.  
ORDER BY slprice ASC
```

1 MIN Optional Exercise: Show all book titles that have a sales price between $30 and $40 and have a
defined (a.k.a. known) development cost.
``` sql
SELECT *
FROM Titles
WHERE slprice BETWEEN 30 AND 40 
AND devcost IS NOT NULL
```

### OR  

> Remember: ONE/ANY condition MUST be true. [Similar to Excel Function]

Exercise: Show all customers who are either in California or New York. 
``` sql
SELECT custname, city, state 
FROM Customers    
WHERE state = 'CA' OR state = 'NY'    
-- Also works: -- WHERE state IN ('CA', 'NY', 'TX');  
```

#### Activity 2.3: Find the Problem:
Q: Show me people who live either in NY or CA. Amongst those people, they MUST have a zipcode of 92704.

``` sql
SELECT *  
FROM Customers  
WHERE Customers.state = 'NY' OR state='CA' AND zipcode = '92704'  
ORDER BY zipcode  
-- This will return multiple NY resident without the zipcode 92704  
-- This is because in a SQL query, the AND operator has a higher precedence than the OR operator and is evaluated first

-- Proper Solution: 
-- WHERE (Customers.state = 'NY' OR state='CA') AND zipcode = '92704'  
```

#### omg LIKE Operator 
The LIKE operator is used in a WHERE clause to search for data based on a string pattern.

Exercise: Get all people whose first name starts with the letter 'A'  
``` sql
-- Solution
SELECT *  
FROM Slspers  
WHERE fname LIKE 'A%';
```

Optional Exercise: Show all book titles that end with 'y'
``` sql
-- Solution:
SELECT * 
FROM Titles
WHERE TRIM(bktitle) LIKE '%y';
```

Optional Example #1: Show all book titles that only begins with the word 'The'
``` sql
-- Solution
SELECT *
FROM Titles
WHERE bktitle LIKE 'The%'
```

Optional Example #2: Show all book titles that contains the word 'The'
``` sql
-- Solution
SELECT *
FROM Titles
WHERE bktitle LIKE '%The%' 
```

#### EXACT MATCH  
``` sql
SELECT * FROM Titles  
WHERE bktitle = 'Sailing' -- filters rows
```

VS.
 
#### CONTAINS MATCH
``` sql
SELECT * FROM Titles  
WHERE bktitle LIKE '%B%'  -- Show all books that contain the letter B
-- Also works: -- WHERE bktitle LIKE '%[B]%' 
```

The following 3 filters are all the same: 
``` sql
SELECT bktitle  
FROM Titles   
-- The following 3 filters are all the same:  
-- WHERE bktitle LIKE '[ABC]%' -- Replacing '[ABC]%' with '[ABR]%' only shows titles beginning with A, B, or R  
-- WHERE bktitle LIKE '[A-C]%' -- Brackets is a must; Returns titles with books that begin A-C  
-- WHERE bktitle LIKE '[A]%' OR bktitle LIKE '[B]%' OR bktitle LIKE '[C]%'  
-- WHERE partnum LIKE '401__' -- underscore represents 1 character  
ORDER BY bktitle ASC  
```


/* -------------------------------------------------------
## <p id = "3"> LESSON 3: Working with Functions | [Back to ToC](#toc)</p>
---------------------------------------------------------- */

Database functions are reusable expressions (blocks of code) used in SQL queries to compute and return values.  
There are many built-in SQL functions similar to Excel's `SUM` and `CONCATENATE`, and you can also create your own custom functions.

### Date Functions

To get todays date:
``` sql
SELECT GETDATE();  -- Similar to Excels NOW() function. 
SELECT CAST(GETDATE() AS DATE);  -- Similar to TODAY() function
```

> Note: Please do not forget to include parentheses when working with functions.


Column names can be wrapped in parentheses:
``` sql
SELECT
	bktitle, 
	(slprice * 0.9),  -- Column name works with or without () 
	(pubdate),  
	CAST(pubdate AS Date) AS 'New Pub Date'
FROM titles
```

To ouput the current year:
``` sql
SELECT YEAR( GETDATE() ); 	-- like in Excel, the functions MONTH(date) and DAY(date) are available too.  
-- Also works: -- SELECT DATEPART( year, GETDATE() )
```

<br/>

#### Filter By Year 2017
``` sql
-- Example: Filter by 2017  
SELECT  
	bktitle,  
	pubdate  
FROM Titles  
WHERE YEAR(pubdate) = 2017  -- Filter by 2017  
ORDER BY YEAR(pubdate), MONTH(pubdate)
```

#### Recap:
``` sql
SELECT  
	bktitle,   
	pubdate,  
	YEAR(pubdate) -- Use Year function to return YEAR of each record.  
FROM Titles  
WHERE YEAR(pubdate) = 2017  -- Filter by 2017  
-- Same as: -- WHERE DATEPART(year, pubdate) = 2017  
```

#### 1 Min Optional Exercise: Filter for months between May & Oct  
``` sql
SELECT  
 	bktitle, CAST(pubdate AS DATE)  
FROM Titles  
WHERE MONTH(pubdate) BETWEEN 5 AND 10  
```

#### 1 Min Optional Exercise: Show booktitles published on July 2016
``` sql
-- Solution:  
SELECT  
	bktitle, CAST(pubdate AS DATE)  
FROM Titles  
WHERE YEAR(pubdate) = 2016 AND MONTH(Pubdate) = 7  
ORDER BY pubdate
```

#### 1 Min Optional Exercise: Show titles published in 2016 or 2017
``` sql
-- Solution 1:
SELECT
	bktitle, CAST(pubdate AS Date) AS 'New Pub Date'
FROM Titles
WHERE YEAR(Pubdate) = 2017 OR YEAR(Pubdate) = 2016

-- Solution 2:
SELECT
    bktitle,
    CAST(pubdate AS DATE) AS [New Pub Date]
FROM Titles
WHERE YEAR(pubdate) IN (2016, 2017)
ORDER BY pubdate
```

#### This query below lists publication date, and extra columns depicting the next day, and one year later.
``` sql
SELECT  
	pubdate,   
	pubdate + 1 AS next_day,  
	DATEADD(YEAR, 1, pubdate) AS Pub_Deadline -- Adds 1 year later to the publication date.  
FROM Titles  
WHERE pubdate BETWEEN '1/1/1994' AND '12/31/2013'  
```



### AGGREGATE FUNCTIONS  

``` sql
SELECT	
	COUNT(*),  
	COUNT(DISTINCT pubdate) AS distinct_publish_dates  -- Count UNIQUE publish dates.
FROM	TITLES  
WHERE 	YEAR(pubdate) = 2017  
```

``` sql
SELECT  
	SUM(devcost),  
	AVG(slprice),  
	AVG(slprice * 0.9) AS AVERAGE_DISCOUNT_PRICE,  
	MAX(slprice) Highest_Price,  --  Note: AS keyword is dropped  
	MIN(slprice) Lowest  
FROM Titles  
WHERE YEAR(pubdate) = 2017  
```

``` sql
-- Notice the difference between answers
SELECT AVG( CAST(commrate AS DECIMAL(10,1)) ) FROM Slspers  -- 0.030000
SELECT AVG( CAST(commrate AS DECIMAL(10,2)) ) FROM Slspers  -- 0.037000
```

> Side Note: If a SQL column is stored as TEXT but contains numbers, you must cast it to a numeric type before doing numeric operations or comparisons.

--  
Q: Can we use a sum function across a row?

Short answer:  
No, you can't use `SUM()` to add values across columns like `Q1 + Q2` in a single total row.  
`SUM()` works vertically by adding values in one column over many rows

You can however do a row-wise sum across columns like Q1 + Q2 without the function:

``` sql
SELECT 
    id,  
    Q1,  
    Q2,  
    Q1 + Q2 AS Total  
FROM sales;  
```

<br /> 

--- 

#### Note: Wrap `SELECT` Queries in parenthesis to form nested queries (Similar to Nested Functions in Excel)

#### Query 1
``` sql
SELECT fname, commrate From Slspers  
WHERE commrate > 0.02  
-- ORDER BY commrate DESC  
```

#### Query 2  
``` sql
(  
SELECT AVG(commrate) FROM Slspers -- RESULT: 0.037  
)  
```

#### Query 3 (Combined)
> Combining the last 2 queries together...  

``` sql
SELECT fname, commrate From Slspers  
WHERE commrate > (SELECT AVG(commrate) From Slspers)  
-- ORDER BY commrate DESC  
```

Optional Exercise: Show all books that are of the maximum salesprice:
``` sql
SELECT *
FROM Titles
WHERE slprice = (
    SELECT MAX(slprice)
    FROM Titles
)
```

---

### String Functions


#### TRIM Function  

``` sql
SELECT  
	city + ', ' + state  
	-- TRIM Function removes TRAILING SPACE  
	-- Rochester           <- space ends here  
	-- Solution: -- TRIM(city) + ', ' + state  
FROM CUSTOMERS
```

> NOTE:  The TRIM function does not automatically apply to all columns in a table.  
You must specify each column you want to trim.

#### Optional Excercise: Create a column that contains the full address from the Customers table 

```sql
-- Solution:  
SELECT 
    Custname, 
    TRIM(Address) + ', ' +  
    TRIM(City) + ', ' +  
    TRIM(State) + ', ' +  
    TRIM(Zipcode)  
  AS Address  
FROM Customers;
```

#### Exercise #1: Create a 'Full Name' column by concatenating Last Name, First

``` sql
-- Solution:  
SELECT   
	TRIM(lname) + ', ' + fname AS 'Full Name'  -- Two-word Alias must be wrapped in single quotes.  
	-- Below Also Works:   
	-- CONCAT(TRIM(fname), ' ', lname) AS full_name  -- One-word Alias does not need quotes.  
FROM Slspers
```

#### Bonus: Convert Concatenated Text to Lowercase 

``` sql
-- Solution:  
SELECT   
	LOWER(  
		CONCAT(TRIM(fname), ' ', lname)  
	) AS Full_Name  
FROM Slspers;
```

#### Exercise 2: Create a fake email for each salesperson by using the format: `fname.lname@outlook.com`

``` sql
-- Solution:  
SELECT  
	TRIM(fname) + '.' + TRIM(lname) + '@outlook.com'  
FROM Slspers  
```

/* -------------------------------------------------------
## <p id = "4"> LESSON 4: Organizing Data | [Back to ToC](#toc)</p> 
---------------------------------------------------------- */



SELECT COUNT(*)  
FROM Slspers;  
-- in SSMS, Clicking on 'Messages' will display output of Count of Rows as well.


-- Show Row #'s for each row  
SELECT  
	ROW_NUMBER() OVER (ORDER BY repid) AS row_num,  	
	*  
FROM Slspers


> Remember if I want to show rows as a seperate column:

SELECT 
    ROW_NUMBER() OVER (ORDER BY repid) AS row_num,  
    *  
FROM Slspers;

 
SELECT  
  fname, 
  commrate,  
  DENSE_RANK() OVER (ORDER BY commrate DESC) AS SalaryRank  
  -- DENSE_RANK uses consecutive ranks that doesn't skip ranks after ties.  
FROM Slspers
ORDER BY commrate ASC;


#### Unpreferred
SELECT  
  fname,  
  commrate,  
  RANK() OVER (ORDER BY commrate DESC) AS SalaryRank  
  -- RANK() assigns the same rank to tied values.  
  -- It skips ranks for ties (that's why there’s no rank 2,3).  
FROM Slspers
ORDER BY commrate ASC;



> REMEMBER:  
SELECT  
	COUNT(*),   
	SUM(devcost),  
	AVG(slprice),  
	MIN(slprice),  
	MAX(slprice)  
	-- bktitle -- will run an error because it's not an aggregate function  
FROM Titles  
WHERE DATEPART(year, pubdate) = 2017  


### Group By  

-- Output each distinct customer (like Excel's UNIQUE() function)  
SELECT DISTINCT City  
FROM Customers  


-- SAME AS ABOVE --  
SELECT city  
FROM Customers  
GROUP BY city  


-- List each commission rate along with the number of salespeople who have that rate.  
SELECT	
	commrate,  
	COUNT(commrate) AS number_salespeople,  
	STRING_AGG(TRIM(fname), ', ') AS salespeople   
	-- string aggregation creates a column that aggregates the first names of salespeople into a list or array  
FROM Slspers  
GROUP BY commrate


#### For each sales person, show the number of books sold
SELECT repid, SUM(qty) as qty_total  
FROM SALES  
WHERE YEAR(sldate) = 2017  
-- WHERE DATEPART(YEAR, sldate) = 2017  
GROUP BY repid  
ORDER BY qty_total




-- Please make sure to import 'Employees' Data Set first before executing:  
SELECT 	
	Position  
	-- COUNT(*) AS NumEmployees  
FROM Employees  
GROUP BY Position;  

-- AVG Salary for each position:  
SELECT  
	Position,  
	ROUND(AVG(Salary),0) AS AVGSALARY  
	-- FORMAT(ROUND(AVG(Salary),0), '0') AS AVGSALARY -- Formatted  
FROM Employees  
GROUP BY Position;





#### HAVING
-- Acronym:   
Start Fridays With Grandmas Homemade Oatmeal  
SELECT FROM WHERE Group By Having Order By

-- Ex 1 --   
SELECT Position, AVG(Salary) AS AVGSALARY  
FROM Employees  
GROUP BY Position  
HAVING AVG(Salary) > 70000  


-- Show me which years HAVE # of books released >5  
SELECT YEAR(pubdate), COUNT(*) -- COUNT(pubdate)  
FROM Titles  
GROUP BY YEAR(pubdate) --  WITH ROLLUP  
HAVING COUNT(*) > 5  



/*
The ROLLUP operator in SQL is used to generate 
subtotals and grand totals for grouped data. 
It's especially useful in reports where 
you want to see aggregates by category, 
as well as totals across all categories.
*/

-- ROLLUP -- 
SELECT Position, AVG(Salary) AS AverageSalary
FROM Employees
GROUP BY ROLLUP(Position);
-- Also works: GROUP BY Position WITH ROLLUP;



SELECT *
FROM (
    SELECT Position, Salary
    FROM Employees
) AS SourceTable
PIVOT (
    AVG(Salary)   -- Aggregate function
    FOR POSITION IN ([Web Designer], [UX Designer])  -- Column values to become new columns
) AS PivotTable;



/* -------------------------------------------------------
## <p id = "5"> Lesson 5: Retrieving Data from Multiple Tables | [Back to ToC](#toc)</p> 
---------------------------------------------------------- */


### /* ------------ Unions Statement ------------ */
SELECT *  
FROM Titles  
UNION   
SELECT *  
FROM Obsolete_Titles
-- Optional: -- ORDER BY bktitle

-- note: when combining data, every SELECT statement within UNION must have the same number of columns in the right order!  
-- in short: -- YOU MUST OUTPUT SAME COLUMNS ON BOTH QUERIES


SELECT bktitle, slprice  
FROM Titles  
UNION ALL 	-- includes 'Clear Cupboards' twice since it allows duplicate values  
-- UNION 	-- Takes off 1 row of 'Clear Cupboards' since it removes entire duplicate rows—not just duplicates in a single column like bktitle or slprice.
-- INTERSECT 	-- only shows 'Clear Cupboards' since it's a name in both -- will return rows ONLY if there's an exact match across all columns   
-- EXCEPT 	-- tricky one. Returns rows from the first query that aren't in the second.   
		-- Since there are 92 entries in Titles (recall: header row isn't included) it outputs 91 to exclude 'Clear Cupboards'   
SELECT bktitle, slprice  
FROM Obsolete_Titles  
ORDER BY bktitle


--- 
## JOIN Statements
### /* ------------ JOINS Statement ------------ */

#### Recall: Table Aliases (Important Sidenote)

```sql
-- Works:
SELECT Sales.ORDNUM, * -- Note: Ordnum would be outputted twice in this example.
FROM Sales
WHERE Sales.qty > 300;
```

```sql
-- Works:
SELECT S.* -- Using an alias S  -- Outputting Individual Columns -- S.ordnum, S.qty
FROM Sales S
WHERE S.qty > 300;
```

```sql
-- Does NOT work:
SELECT S.*
FROM Sales S
WHERE Sales.qty > 300; -- Must change to S.qty
```

* `Sales S` assigns alias `S` to the `Sales` table.
* Remember, once an alias is declared on a table (Sales S), you must reference it as `S`, not `Sales`.

> Don't forget this! You must use the alias instead of the full table name! 

---

<br/>
<br/>


### INNER JOIN


Match rows where the key exists in both tables.
[Link](https://www.w3schools.com/sql/sql_join_inner.asp)

NOTE:
It's always a great idea to check what the contents of each table is:
```sql
SELECT S.* FROM Sales2 S
SELECT SP.* FROM Slspers2 SP
```


```sql
-- Prerequisite: Assure that both Sales2 & Slspers2 tables are created.  
-- `INNER JOIN` returns only matching rows & functionally is the same as writing just `JOIN`.
SELECT s.*, sp.fname
FROM sales2 s
INNER JOIN slspers2 sp
    ON s.repid = sp.repid;
```



### LEFT JOIN

Similar idea to VLOOKUP (matching keys), `LEFT JOIN` and `LEFT OUTER JOIN` are the same.

```sql
-- Include all rows from the left table.
SELECT s.*, sp.fname
FROM sales2 s
LEFT JOIN slspers2 sp
    ON s.repid = sp.repid;
```

Note:
* All rows from `sales2` are returned.
* Matching rows from `slspers2` are included.
* Non-matching rows show NULL values.

---

### Sample - Left Join Demo: Show All Customers with Their Salesperson

```sql
-- Returns all customers & shows assigned salesperson name if available.
SELECT C.*, S.fname
FROM Customers C
LEFT JOIN Slspers S
    ON C.repid = S.repid;
```

> Remember if you're struggling to output the two tables, use the following:  
> SELECT C.* FROM Customers C  
> SELECT S.* FROM Slspers S  

### Sample - Inner Join Demo: Show All Matching Titles with Obsolete Titles

```sql
-- Before attempting INNER JOIN, look at individual titles

-- SELECT T.* FROM Titles T  
-- SELECT O.* FROM Obsolete_Titles O
SELECT t.*  
FROM Titles t  
INNER JOIN Obsolete_Titles o  
ON t.partnum = o.partnum;  
```


### Exercise #1: One-to-Many Example

```sql
-- Sample Exercise: Show all Customers who are in the Customers Table AND Potential Customers Table

SELECT *
FROM Customers C
INNER JOIN Potential_Customers P
ON C.custnum = P.custnum

```

### Exercise #2: Calculated Column with JOIN

```sql
-- Sample Exercise: Show all titles and display matching sales if they exist (Bonus: Add TotalSales).
SELECT Titles.partnum,
       bktitle,
       qty, -- Notice that qty doesn't exist on Titles table.
       Sales.qty * Titles.slprice AS total_amount
FROM Titles
LEFT JOIN Sales
    ON Titles.partnum = Sales.partnum;
```

* Demonstrates calculated column inside SELECT.
* `Total_amount` = Quantity × selling price.

---


### Exercise #3: Multi-Join Example - Show which customers bought 500 copies of which books.

-- i.e. Find out for all sales where qty = 500, who was the customer and what did they buy.

-- To start off:  
SELECT * FROM Sales WHERE qty = 500  

> NOTE - In this simplified example, every sale corresponds to a valid customer account and a valid purchased book.
> Because of this, it doesn’t matter which JOIN type is used.

```sql
SELECT S.*, C.Custname, T.bktitle -- The order of the columns does not matter.
FROM Sales s 
JOIN Titles t
    ON s.partnum = t.partnum
JOIN Customers c
    ON s.custnum = c.custnum
WHERE s.qty >= 500;
```

This query:  
	* Starts with `Sales` Table  
	* Joins to `Title` Table to find what the purchased title was  
	* Joins to `Customers` Table to get the customer name  
	* Filters to only sales where book quantity = 500  

---


### Bonus Exercise: Count Sales Per Salesperson (Even if 0)

```sql
SELECT sp.repid,
       sp.fname,
       COUNT(s.ordnum) AS sales_count
FROM slspers2 sp
LEFT JOIN sales2 s
    ON sp.repid = s.repid
GROUP BY sp.repid, sp.fname;
```

* LEFT JOIN ensures reps with zero sales still appear.
* `COUNT(s.ordnum)` counts only matching sales rows.

---


### FULL OUTER JOIN

Include all rows from both tables, matching where possible.

Example forcing no matches:

```sql
SELECT s.*, sp.fname
FROM sales2 s
FULL OUTER JOIN slspers2 sp
    ON 1 = 0;
```

* `ON 1 = 0` forces no match.
* Returns all rows from both tables with NULLs where no match exists.

Standard FULL OUTER JOIN:

```sql
SELECT *
FROM sales2 s
FULL OUTER JOIN slspers2 sp
    ON s.repid = sp.repid;
```

* Returns all rows from both tables.
* Matches where keys align.
* Does NOT create every possible combination (not a Cartesian product).

#### Group By With Join Example
SELECT pubdate, qty  
FROM Titles  
LEFT JOIN Sales  
ON Titles.partnum = Sales.partnum  
GROUP BY pubdate  

---

/* -------------------------------------------------------
## <p id = "6"> LESSON 6: Exporting Query Results | [Back to ToC](#toc)</p> 
---------------------------------------------------------- */


EXPORTING  
Ctrl + Shift + F (Results to File): Save the query results directly to a file, such as a CSV or text file.  
You can then run the query again to save it to a file.


SELECT *  
FROM dbo.Slspers  
FOR XML AUTO, ROOT('Document')  
FOR XML AUTO, TYPE, ELEMENTS  

FOR XML, MAKE SURE YOU WRAP INFORMATION IN  
`<document>`

</document>

-- BONUS --

> Excercise: Create simple table 'Vendors' who are partners involved in publishing.  

```
CREATE TABLE Vendors (  
    VendorID INT PRIMARY KEY IDENTITY(1000,1), -- KEYWORD 'IDENTITY' AUTOINCREMENTS; FIRST ROW WILL START AT 1000 and increment 1 for each new row!  
    Name VARCHAR(100),  
    Phone VARCHAR(20),  
    Email VARCHAR(100)  
);
```

INSERT INTO Vendors(Name, Phone, Email)  
VALUES  
('Raza', '818-123-4321', 'Raza@outlook.com')

INSERT INTO Vendors (Name, Phone, Email)
VALUES  
('Global Print Solutions', '555-123-4567', 'alice.morgan@globalprint.com'),  
('BookWorks Inc.', '555-987-6543', 'robert.tan@bookworks.com'),  
('EcoPaper Co.', '555-555-1212', 'jenna.park@ecopaper.com');  

SELECT * FROM Vendors;

```
CREATE TABLE Authors (  
    AuthorID INT PRIMARY KEY,  -- must be unique and not null (Cannot insert duplicate key!)  
    FirstName VARCHAR(100) NOT NULL,  
    LastName VARCHAR(100),  
    AGE INT DEFAULT 21  
);
```

INSERT INTO AUTHORS(AuthorID, FirstName, LastName)   
VALUES    
(NULL , 'Raza', 'M'), 	-- Will return error because Primary Key can not be null 	-- Fix by changing NULL to number  
(2, NULL, 'Z'), 	-- Will return error because Firstname can not be null 		-- Fix by adding a name  
(3, 'Maria', NULL),  
(4, 'Raza');		-- Will return error because  
			-- # of columns for each row in a table value constructor must be the same. -- Solution: -- (4, 'Raza', NULL)

SELECT * FROM AUTHORS;

```
-- Good potential table 'Reviews' which stores book reviews from customers or critics:  
CREATE TABLE Reviews (  
    ReviewID INT PRIMARY KEY IDENTITY(1,1),  
    TitleID INT FOREIGN KEY REFERENCES Titles(TitleID),  
    CustomerID INT FOREIGN KEY REFERENCES Customers(CustomerID),  
    Rating INT CHECK (Rating BETWEEN 1 AND 5),  
    ReviewText TEXT,  
    ReviewDate DATE  
);  
```
-- End of Bonus Chapter --

== FAQ's: ==  

Q: How to return all columns?  
A: 
```sql
SELECT COLUMN_NAME  
FROM INFORMATION_SCHEMA.COLUMNS  
WHERE TABLE_NAME = 'Slspers'
```

Q: How to get count of rows returned?  
A: ``` SELECT COUNT(*) FROM Employees; ```
OR
```sql
SELECT COUNT(*)
FROM (
    SELECT *
    FROM Employees
    WHERE Salary > 70000
) AS Sub;
```
Q: If a table is called Employees, will ``` SELECT * FROM Employee; ``` work?  
A: NO.

Q: For string literals, can I use double quotes "" instead of single quotes ''?  
A: NO  

Q: Will ``` SELECT Fname Lname Commrate FROM Employee; ``` work?  
A: NO since commas are needed.  

Q: How to copy output into text file?  
A:  
	`Ctrl` + `Shift` + `F` (Results to File): 
	Save the query results directly to a file, such as a CSV or text file.
	You can then run the query again to save it to a file.  
OR   
	Select all the data via `CTRL` + `A` and then 
	press `Ctrl` + `Shift` + `C` to copy all data + column headers

---