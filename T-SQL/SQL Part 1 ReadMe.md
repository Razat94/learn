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
```
	To Show Lines in the Query Editor:
		1. Go to Tools > Options 
		2. Expand 'Text Editor' -> Transact-SQL -> General. 
		3. Check the Line numbers box and click OK
```
- Results Pane: Ctrl + R - Toggles the results pane


> NOTE:  
> Suppose we use Task Manager to close SQL Server Management Studio (SSMS).
Reopening SSMS could cause problems, so we’ll use SQL Server 20XX Configuration Manager to start the service.  
Additional Note: Don’t use Windows Services to start SSMS.

1. Type in "Configuration Manager" to launch the application
2. Start the service for "SQL Server" (SQL EXPRESS)
3. Relaunch SSMS normally.

[Stack Overflow Reference](https://stackoverflow.com/questions/35630344/unable-to-connect-to-local-sql-server-after-ending-tasks)



/* -------------------------------------------------------
## <p id = "1"> LESSON 1: Executing a Simple Query | [Back to ToC](#toc) </p>
---------------------------------------------------------- */



To output simple text:
```
SELECT 'After Insertion:' 
```

To run the query, F5 is the shortcut. We could also use Ctrl+E OR Alt-X.  
You can run multiple SELECT statements at once if they are included in the same query as below:

```
SELECT 1+3; -- T-SQL is a Declarative language that supports some precedural syntax.
SELECT FORMAT(123.490000000, '0.##')	-- Output: 123.49
SELECT ROUND(235.415, 2) AS RoundValue;	-- Output: 235.420 
-- Two -'s are used to write a comment:
```

> Note: In Excel, we also have a round function = ROUND(D2,0) -- given that D2 = 235.415


USE Pub1  
SELECT *  
FROM slspers;  

-- To output only 2 columns  
SELECT fname, lname
FROM slspers;

-- This also works:  
SELECT 
	Slspers.fname, Slspers.lname
FROM Slspers;

#### WE CAN WRITE:  
SELECT Sales.*
FROM Sales

-- instead of

SELECT *
FROM Sales

#### ...more to discuss in CHAPTER 5! [Link to Lesson 5](#5). 

-- Alias 'AS' Keyword --  
SELECT fname, lname AS 'Last Name'  
FROM Slspers;


SELECT COUNT(*)  
FROM Slspers;  
-- in SSMS, Clicking on "Messages" will display output of Count of Rows as well.

-- Show Row #'s for each row  
SELECT  
	ROW_NUMBER() OVER (ORDER BY repid) AS row_num,  	
	*  
FROM Slspers


-- Adds a new column with a constant static value  
SELECT pubdate, bktitle, 'Non-Fiction' AS category, '12345' AS static_col  
FROM Titles;

### Calculated column
A calculated column doesn't exist in the table, but SQL calculates it for each row when the query runs. 

-- Calculated Column Example:  
SELECT  
	partnum,   
	bktitle,  
	slprice,  
	-- slprice * 1.2 AS slprice_inflation,   
	slprice - slprice * 0.07 AS discounted_price  
FROM Titles
	
SELECT  
	slprice,  
	ROUND(slprice,0) -- Round to nearest number  

	-- To remove trailing 0's without rounding?   
	-- FORMAT(slprice - slprice * 0.07, '0.##') AS discounted_price  
FROM TITLES


### Keyboard Shortcuts:
> Ctrl+K; Ctrl+C (comment)
> Ctrl+K; Ctrl+U (uncomment)


> CTRL + Shift + U (Uppercase)
> CTRL + Shift + L (Lowercase)


### Create a Backup Table
SELECT * INTO titles_backup  
FROM titles;  
> After completion, make sure to select 'Refresh' on Object Explorer.

-- Example from w3SCHOOLS  
SELECT * INTO CustomersBackup2017  
FROM Customers  
-- WHERE state = 'CA'  

-- Create 'NewCustomers' table but structure only  
SELECT *  
INTO NewCustomers  
FROM Customers  
WHERE 1 = 0;  
-- If you want to create an empty table (structure only),   
-- use WHERE 1 = 0 or similar condition.


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
-- Good potential table:  
-- Stores book reviews from customers or critics.  
CREATE TABLE Reviews (  
    ReviewID INT PRIMARY KEY IDENTITY(1,1),  
    TitleID INT FOREIGN KEY REFERENCES Titles(TitleID),  
    CustomerID INT FOREIGN KEY REFERENCES Customers(CustomerID),  
    Rating INT CHECK (Rating BETWEEN 1 AND 5),  
    ReviewText TEXT,  
    ReviewDate DATE  
);  
```


> To delete a table:  
DROP TABLE IF EXISTS titles_backup  

> To truncate a table i.e. to remove all rows from table:   
TRUNCATE TABLE titles_backup  



> To Run T-SQL via the command line:  

C:\Users\student>sqlcmd -S UT-LAPTOP\SQLEXPRESS -E  
1> select 1 + 2;  
2> GO  

1> USE Pub1;  
2> SELECT * FROM Slspers;  
3> Go  




```
Display the table structure  
/* Also works too */  
SP_HELP Titles  
```

```
-- Advanced Users can simply run this command below to execute the query.  
-- Below also outputs column names  
SELECT COLUMN_NAME  
FROM INFORMATION_SCHEMA.COLUMNS  
WHERE TABLE_NAME = 'Titles'
```



/* -------------------------------------------------------
## <p id = "2"> LESSON 2: Performing a Conditional Search | [Back to ToC](#toc) </p>
---------------------------------------------------------- */



<!-- SORTING & FILTERING CHAPTER -->

#### To sort data by a column  
SELECT *  
FROM Titles   
ORDER BY bktitle ASC -- Sort by bktitle  

-- Multilevel Sort  
Select *  
FROM Titles  
ORDER BY slprice DESC, bkTitle ASC  

#### To get top 5 rows  
SELECT  
TOP 5  
*  
FROM Titles  
ORDER BY bktitle ASC


-- In SSMS, you can use the 'Query Options' command to set the ROWCOUNT value.  
-- i.e. "Specify the maxinum number of rows to return before the server stops processing


#### WHERE clause acts as a Filter 
SELECT *  
FROM Customers  
WHERE state = 'NY'   
-- verify that 6 people are there.


#### NOT   
SELECT *  
FROM Customers  
WHERE NOT state = 'NY'  
-- ORDER BY state  


SELECT *  
FROM  titles  
WHERE  
-- NOT  
slprice      >            50  
column    operator       value


#### WHERE clause with dates:  
-- Show titles published past 1/1/2017  
SELECT bktitle, CAST(pubdate AS DATE) -- CAST is used to truncate the time portion  
FROM Titles  
WHERE pubdate > '2017-01-01' -- Note: Actual date must be wrapped in ''  
ORDER BY pubdate


#### WHERE clause with numbers:
SELECT *  
INTO HighEarners  
FROM Employees  
WHERE Salary > 80000;  

-- BE CAREFUL: Computed or alias columns aren't part of the actual table, so they can't be used in the `WHERE` clause since WHERE is evaluated before SELECT.

SELECT  
	partnum,  
	bktitle,  
	slprice - slprice * 0.07 AS discounted_price  
FROM Titles  
WHERE slprice - slprice * 0.07 >= 45  
-- WHERE discounted_price >= 45 -- WON'T WORK!  
ORDER BY discounted_price DESC  -- WILL WORK!  



#### WHERE clause with NULL:  
SELECT *  
FROM Titles  
WHERE devcost IS  
-- NOT  
NULL  


2:45
// Already covered:  
ISNULL() / IFNULL()	Replace nulls; Excel: IF(ISBLANK())



-- Remember, we can create a new table from a filtered table:  
SELECT   
	*  
	INTO CA_Customers  -- Creates a new table 'CA_Customers'
FROM Customers  
WHERE state = 'CA'  
ORDER BY custname

> TO DELETE:  
-- DROP TABLE CA_Customers  



### AND
EVERY (All) condition MUST be true. [Similar to Excel Function]

SELECT *  
FROM customers  
WHERE state = 'TX' AND city = 'Houston'  


SELECT *  
FROM sales  
WHERE repid = 'N02' AND qty > 200  
ORDER BY qty 


Select *  
FROM Titles  
-- WHERE slprice >= 35 AND slprice <= 70  
-- Also works: WHERE slprice BETWEEN 35 AND 70 -- does the same as above.  
ORDER BY slprice ASC



### OR  
ANY condition MUST be true. [Similar to Excel Function]


SELECT custname, city, state FROM Customers    
WHERE state = 'CA' OR state = 'NY'    
-- Also works: -- WHERE state IN ('CA', 'NY', 'TX');  


#### Activity 2.3: Find the Problem:
Q: Show me people who live either in NY or CA. Amongst those people, they MUST have a zipcode of 92704.

Select *  
from Customers  
WHERE Customers.state = 'NY' OR state='CA' AND zipcode = '92704'  
ORDER BY zipcode  
-- This will return multiple NY resident without the zipcode 92704  
-- Solution: -- WHERE (Customers.state = 'NY' OR state='CA') AND zipcode = '92704'  


#### omg LIKE Operator 
-- Get all people whose first name starts with the letter "A"  
SELECT *  
FROM Slspers  
WHERE fname LIKE 'A%';



#### EXACT MATCH 
SELECT *
FROM Titles
WHERE bktitle = 'Sailing'

VS.
 
#### CONTAINS MATCH
SELECT *
FROM Titles
WHERE bktitle LIKE '%Art%' -- filters rows


SELECT bktitle  
FROM Titles  
-- WHERE bktitle LIKE '%Art%'  
-- WHERE bktitle LIKE 'B%'  
-- Also works: -- WHERE bktitle LIKE '[B]%'  
-- The following 3 are all the same:  
-- WHERE bktitle LIKE '[ABC]%' -- Replacing '[ABC]%' with '[ABR]%' only shows titles beginning with A, B, or R  
-- WHERE bktitle LIKE '[A-C]%' -- Brackets is a must; Returns titles with books that begin A-C  
-- WHERE bktitle LIKE '[A]%' OR bktitle LIKE '[B]%' OR bktitle LIKE '[C]%'  
-- WHERE partnum LIKE '401__' -- underscore represents 1 character  
ORDER BY bktitle ASC  

> Ctrl + R -> Hide the Result Pane


-- SELECT title, director FROM movies   
-- WHERE title LIKE "Toy Story%";



/* -------------------------------------------------------
## <p id = "3"> LESSON 3: Working with Functions | [Back to ToC](#toc)</p>
---------------------------------------------------------- */



### Date Functions

#### Columns can be wrapped in ( ) 
SELECT 	
	bktitle,   
	(pubdate),  			-- This works with or without ()  
	(slprice * 0.9) 		-- Similar to EXCEL Formula = (A1 * 0.9)  
FROM Titles  


SELECT GETDATE();  
SELECT YEAR( GETDATE() ); 	-- like Excel, you also have MONTH( date ) AND DAY( date ) too.  
-- Also works: -- SELECT DATEPART( year, GETDATE() )


SELECT 
	pubdate  
FROM Titles  
-- Filter by 2011: 	-- WHERE Year(pubdate) = 2011  
-- Same as: 		-- WHERE DATEPART(year, pubdate) = 2011  
ORDER BY YEAR(pubdate), Month(pubdate)


SELECT   	
	bktitle,   
	pubdate,  
	YEAR(pubdate), -- Use Year function to return YEAR of each record.  
	-- To remove time:   -- CAST(pubdate AS DATE) AS pubdate_without_time  
FROM Titles  
WHERE YEAR(pubdate) = 2017  -- Filter by 2017


#### Filter for months between May & Oct  
SELECT  
 	CAST(pubdate AS DATE)  
FROM Obsolete_Titles  
WHERE MONTH(pubdate) BETWEEN 5 AND 10  



SELECT  
	pubdate,   
	pubdate + 1 AS next_day,  
	DATEADD(YEAR, 1, pubdate) AS Pub_Date_1_Year_Later -- Adds 1 year to the publication date  
FROM Titles  
WHERE pubdate BETWEEN '1/1/1994' AND '12/31/2013'  



### AGGREGATE FUNCTIONS  

SELECT	
	COUNT(*),  
	COUNT(DISTINCT pubdate) AS distinct_publish_dates  
FROM	TITLES  
WHERE 	YEAR(pubdate) = 2017  


SELECT  
	SUM(devcost),  
	AVG(slprice),  
	AVG(slprice * 0.9) AS AVERAGE_DISCOUNT_PRICE,  
	MAX(slprice),  
	MIN(slprice)  
FROM Titles  
WHERE YEAR(pubdate) = 2017  


-- If your column has a data type of text but contains numeric values,  
-- you must cast it as an INT  
SELECT AVG(CAST( commrate AS DECIMAL(10,1) )) FROM Slspers


--  
Q: Can we use a sum function across a row?

Short answer:  
No, you can't use `SUM()` to add values across columns like `Q1 + Q2` in a single row.  
`SUM()` works vertically by adding values in one column over many rows

You can however do a row-wise sum across columns like Q1 + Q2:

```
SELECT 
    id,  
    Q1,  
    Q2,  
    Q1 + Q2 AS Total  
    FROM sales;  
```

> Note: We can wrap SELECT QUERIES in parenthesis just like in Excel!

(  
SELECT AVG(commrate) From Slspers -- RESULT: 0.037  
)  


SELECT fname, commrate From Slspers  
WHERE commrate > 0.02  
-- ORDER BY commrate DESC  


> Combining the last 2 queries together...  

SELECT fname, commrate From Slspers  
WHERE commrate > (SELECT AVG(commrate) From Slspers)  
-- ORDER BY commrate DESC  





### String Functions


#### Concatenate text to make full name
SELECT TRIM(fname) + ', ' + lname  
-- Also works: -- SELECT CONCAT(TRIM(fname), ' ', lname) AS full_name   
FROM Slspers


#### Convert Concatenated Text to Lowercase 
SELECT   
	LOWER(  
		CONCAT(TRIM(fname), ' ', lname)  
	) AS Full_Name  
FROM Slspers;


#### TRIM Function  
SELECT city + ', ' + state  
-- TRIM Function removes TRAILING SPACE -- Rochester           <- space ends here  
-- SELECT TRIM(city) + ', ' + state  
FROM CUSTOMERS


> Optional Excercise: Create a column that contains the full address  
-- Solution:  
-- SELECT CustomerName, Address + ', ' + PostalCode + ' ' + City + ', ' + Country AS Address  
-- FROM Customers;  



/* -------------------------------------------------------
## <p id = "4"> LESSON 4: Organizing Data | [Back to ToC](#toc)</p> 
---------------------------------------------------------- */



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
FROM Slspers;


SELECT  
  fname,  
  commrate,  
  RANK() OVER (ORDER BY commrate DESC) AS SalaryRank  
  -- RANK() assigns the same rank to tied values.  
  -- It skips ranks for ties (that's why there’s no rank 2,3).  
FROM Slspers;



 > REMEMBER:
SELECT  
	COUNT(*),   
	SUM(devcost),  
	AVG(slprice),  
	MIN(slprice),  
	MAX(slprice)  
	-- bktitle -- will run an error because it's not an aggregate function  
WHERE DATEPART(year, pubdate) = 2017  


### Group By  

-- Output each distinct customer (like Excel's UNIQUE() function)  
SELECT DISTINCT City  
FROM Customers  


-- SAME AS ABOVE --  
SELECT city  
FROM Customers  
GROUP BY city  


-- Return a list of each commission rate and how many salespeople have that rate 
SELECT	
	commrate,  
	COUNT(commrate) AS number_salespeople,  
	STRING_AGG(TRIM(fname), ', ') AS salespeople   
	-- string aggregation creates a column that aggregates the first names of salespeople into a list or array  
FROM Slspers  
GROUP BY commrate



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


SELECT repid, SUM(qty) as qty_total  
FROM SALES  
WHERE YEAR(sldate) = 2017  
-- WHERE DATEPART(YEAR, sldate) = 2017  
GROUP BY repid  



-- HAVING --  
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

-- note: when combining data, every SELECT statement within UNION must have the same number of columns in the right order!  
-- in short: -- YOU MUST OUTPUT SAME COLUMNS ON BOTH QUERIES


SELECT bktitle, slprice  
FROM Titles  
UNION ALL 	-- includes 'Clear Cupboards' twice since it allows duplicate values  
-- UNION 	-- Takes off 1 row of 'Clear Cupboards' since it selects only distinct values by default.   
-- INTERSECT 	-- only shows 'Clear Cupboards' since it's a name in both   
-- EXCEPT 	-- tricky one. Returns rows from the first query that aren't in the second.   
		-- Since there are 92 entries in Titles (recall: header row isn't included) it outputs 91 to exclude 'Clear Cupboards'   
SELECT bktitle, slprice  
FROM Obsolete_Titles  
ORDER BY bktitle


### /* ------------ JOINS Statement ------------ */



-- Prerequisite Knowledge 

SELECT *  
-- Recall: -- SELECT sldate AS purchase_date  
FROM Sales


	SELECT *  
	-- Also works: -- SELECT S.*  
	-- Get order num: -- SELECT S.ordnum, S.qty
	FROM Sales S  
	-- WHERE S.qty > 300  


Note:  
	-- WORKS!  
	SELECT *  
	FROM Sales  
	WHERE Sales.qty > 300  
	

	-- DOESN'T WORK!  
	SELECT *  
	FROM Sales S  
	WHERE Sales.qty > 300  
	-- MUST BE  
	-- WHERE S.qty > 300  



### JOIN STATEMENT!!  

-- INNER JOIN – Match only where repid is present in both tables  
SELECT S.*, sp.fname  
FROM sales2 s  
INNER -- INNER JOIN WORKS functionally the same as JOIN  
JOIN slspers2 sp   
ON s.repid = sp.repid;



-- OUTER JOIN 

-- FULL OUTER JOIN with no matching keys, or more directly  
-- FULL OUTER JOIN include all rows from both table  
SELECT S.*, sp.fname  
FROM sales2 s  
FULL OUTER JOIN  
slspers2 sp   
ON 1 = 0;  -- Forces no match



-- A FULL OUTER JOIN gives all rows from both tables based on matching keys but not every possible combination of rows. 



-- All records from both tables, match where possible
SELECT *  
FROM sales2 s  
FULL OUTER  
JOIN slspers2 sp   
ON s.repid = sp.repid; -- Only statement that changes from last example.  




-- LEFT JOIN and LEFT OUTER JOIN are the same thing.

-- LEFT JOIN on Sales  
-- Optional: Include all sales, even if no matching rep exists (LEFT JOIN):  
SELECT S.*, sp.fname  
FROM sales2 s  
LEFT  
JOIN slspers2 sp   
ON s.repid = sp.repid;




-- 1 to many SHOW ME ALL SALES 
SELECT bktitle, qty  
FROM Titles   
LEFT   
OUTER JOIN Sales  
ON Titles.partnum = Sales.partnum  





Side Q: Show me all sales from each of the Salesrep  

-- Count Sales Per Salesperson (Even if 0)  
SELECT sp.repid, sp.fname, COUNT(s.ordnum) AS sales_count  
FROM slspers2 sp  
LEFT JOIN sales2 s ON sp.repid = s.repid  
GROUP BY sp.repid, sp.fname;  



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
<document>

</document



==
FAQ's:
Q: How to get all columns?
Q: How to get count of rows returned?
Q: Can I call a table plural/singular when it isn't? A: NO
Q: Can I use "" instead of ''? A: NO
Q: How to copy output into text file?
	A:
	Ctrl + Shift + F (Results to File): Save the query results directly to a file, such as a CSV or text file.
	You can then run the query again to save it to a file.
 
	OR 
	Select all the data via CTRL + A 
	Press Ctrl + Shift + C to copy all data + column headers
==
