# SQL Part 2

## <p id = "toc"> Table of Contents </p>
0. [Lesson 0: Before We Begin](#0)
1. [Lesson 1: Using Nested Queries](#1)
2. [Lesson 2: Manipulating Table Data](#2)
3. [Lesson 3: Manipulating Table Structure](#3)
4. [Lesson 4: Working with Views](#4)
4. [Bonus Lesson: Procedures](#procedure)
5. [Lesson 5: Indexing Data](#5)
6. [Lesson 6: Managing Transactions](#6)

/* -------------------------------------------------------
## <p id = "0"> LESSON 0: Before We Begin </p>
---------------------------------------------------------- */

Remember the helpful Mnemonic: 
Start Fridays With Grandma's Homemade Oatmeal

/* -------------------------------------------------------
## <p id = "1"> LESSON 1: Using Nested Queries | [Back to ToC](#toc) </p>
---------------------------------------------------------- */


SELECT * FROM Slspers  
WHERE commrate >   
	(SELECT AVG(commrate) FROM Slspers)


-- Exercise: Show all titles that are cheaper to develop than the cheapest obsolete title.  
SELECT *  
FROM Titles  
WHERE devcost < (SELECT MIN(devcost) FROM Obsolete_Titles);


-- Same as if we use ALL Statement  
SELECT *  
FROM Titles  
WHERE devcost < ALL (Select devcost from Obsolete_Titles)  


-- ## Exercise: Show me all salespersons who have never made a sale.
SELECT *  
FROM Slspers  
WHERE repid NOT IN  
(  
    SELECT repid  
    FROM Sales  
    GROUP BY repid  
)  


-- Returns all rows from Titles where a matching partnum exists in Sales.  
SELECT * FROM Titles  -- This statement alone will return 92 rows.  
WHERE partnum IN  
	(SELECT partnum    
	FROM Sales) -- Executes what's in parenthesis first  


-- Alternate Solution: Inner Join Statement  
SELECT DISTINCT t.*  
FROM Titles t  
INNER JOIN Sales s  
    ON t.partnum = s.partnum;  


-- For each row in Titles, output each row in Obsolete_Titles with the same partnum  
SELECT *  
FROM Titles  
WHERE EXISTS  
	(SELECT partnum  
	FROM Obsolete_Titles  
	WHERE partnum = Titles.partnum)  


-- Alternate Solution: INNER JOIN Statement  
SELECT DISTINCT t.*  
FROM Titles t  
INNER JOIN Obsolete_Titles o  
    ON t.partnum = o.partnum;  



-- ### Additional Example:  
SELECT *  
FROM Customers  
WHERE Custnum IN  
(  
    SELECT custnum  
    FROM Sales  
    WHERE partnum IN  
    (  
        SELECT partnum  
        FROM Titles  
        WHERE slprice >= 49  
    )  
);  



/* -------------------------------------------------------
## <p id = "2"> LESSON 2: Manipulating Table Data | [Back to ToC](#toc) </p>
---------------------------------------------------------- */


===== END OF SIDE EXAMPLE =====

-- Create a backup copy of  Slspers
SELECT * INTO Slspers_Backup  
FROM Slspers  


-- Exercise: Create a backup table of Titles  
-- Solution:  
SELECT *
INTO TitlesRevised
FROM Titles


-- Trick to create a new table (Cust2025) with the same structure as Customers, but copies no data.
SELECT *
INTO Cust2025
FROM Customers
WHERE 1 = 0


> Now that we have a backup table, we can modify it freely.
> Be sure to make changes to the backup table, not the original.


-- Recall that the Object Explorer must be refreshed to see the new table.
-- Additionally, refresh IntelliSense to avoid the red error underline on the table name by going to:
-- Edit -> IntelliSense -> Refresh Local Cache (Ctrl + Shift + R)


> Remember CRUD: Create - Read - Update - Delete

/* ------------ CRUD statement ------------ */
-- C -- Create	
		/* 
		INSERT INTO 
		table_name (column1, column2, column3, ...)
		VALUES (value1, value2, value3, ...); 
		*/
-- R -- Read	-- SELECT * FROM table_name;
-- U -- Update	-- UPDATE table_name SET column1 = value1 WHERE condition;
-- D -- Delete	-- DELETE FROM table_name WHERE condition;



/* ------------ C: INSERT INTO statement ------------ */

#### Adding ONE value
INSERT INTO Slspers_Backup  
--optional -- (repid, fname, lname, commrate)  
VALUES  
('J01', 'Jane', 'Doe' , 0.05)


#### Add One Value with Null values
INSERT INTO Slspers_Backup (repid, fname)  
VALUES  
('N01', 'Nickki')


#### Adding MANY values  
INSERT INTO Slspers_Backup  
VALUES  
('P01', 'Paul', 'Smith' , 0.05),  
('P01', 'Steven', 'Stone' , 0.05),  -- Duplicate REPID 'P01' is intentional as it is a setup for a deletion example.  
('A01', 'Angie', 'Lopez' , 0.05)  



-- Exercise: Add the following information into SQL Table 'Titles'

```
partnum bktitle                                  devcost               slprice               pubdate
------- ---------------------------------------- --------------------- --------------------- -----------------------
12345   The Role of SQL in Big Data              8000.00               45.00                 2017-01-01 00:00:00
```

-- Solution:  
INSERT INTO Titles_Revised
-- optional -- (partnum, bktitle, devcost, slprice, pubdate)
VALUES
(12345, 'The Role of SQL in Big Data', 8000, 45, '2017-01-01')



-- Insert data from one table into another.
    INSERT INTO Customers
    SELECT *
    FROM Potential_Customers
    WHERE State = 'CA';


/* ------------ R: SELECT statement ------------ */

#### Output the table
SELECT *
FROM Slspers_Backup
WHERE commrate = 0.05


#### Output another table.
SELECT *
FROM Titles_Revised
WHERE partnum BETWEEN 39906 AND 39909 -- Check table with WHERE condition



/* ------------ U: Update Table ------------ */

-- Update all salesperson commission from 0.3 -> 0.6
UPDATE Slspers_Backup
SET commrate = 0.06
WHERE commrate = 0.03

-- Check:  
-- SELECT * FROM Slspers_Backup WHERE commrate = 0.06


-- Exercise: Fix the spelling mistake of 'Anne' on RepID W02 to 'Annie'  
-- Solution:
UPDATE Slspers_Backup
SET fname = 'Annie'
WHERE REPID = 'W02'
-- Bad Practice -- WHERE fname = 'Anne' -- Since there could be multiple 'Anne', this is bad practice.


-- UPDATE Titles where partnum b/w 39904 & 39906  
UPDATE Titles_Revised
SET devcost = 21000
WHERE partnum BETWEEN 39904 AND 39906
-- WHERE partnum BETWEEN 40123 AND 40124


-- Check Updated Table  
SELECT *  
FROM Titles_Revised
WHERE partnum BETWEEN 39904 AND 39906
-- WHERE partnum BETWEEN 40123 AND 40124


-- Update Table w/Multiple Parameters
UPDATE Titles_Revised
SET 	bktitle = 'Alex loves Windsurfing',
	devcost = 5000,
	slprice = 22,
	pubdate = '2017/11/01'
WHERE partnum='40123'


-- Check Updated Table
SELECT *
FROM Titles_Revised
WHERE partnum = 40123


/* ------------ D: Delete Rows ------------ */
DELETE Titles_Revised  
WHERE partnum = 40123


-- Check Updated Table
SELECT *
FROM Titles_Revised
-- WHERE partnum = 40123


-- Exercise: Attempt to delete one of the Salespeople Paul that was added earlier.
('P01', 'Paul', 'Smith' , 0.05)

-- Solution:
DELETE Slspers_Backup
WHERE REPID = 'P01' AND fname = 'Paul'


-- To Truncate All Rows
TRUNCATE TABLE Slspers_Backup;

-- To Delete ALL Rows
DELETE FROM Slspers_Backup;



===== End of Chapter Exercise =====

-- Task #1 Exercise: Insert a new book into the Titles_Revised table with the following details  

```
partnum 	bktitle				devcost 	slprice 	pubdate
---------- 	------------------------------ 	---------- 	---------- 	----------
98765 		Learn to Play the Violin 	5000.00 	45.00 		2025-01-01
```

-- Task #1 Solution: Insert a Record
INSERT INTO Titles_Revised 
-- Optional -- (partnum, bktitle ,devcost, slprice, pubdate) 
VALUES (98765, 'Learn to Play the Violin', 5000, 45, '2010-05-11')


-- Verify Insertion
SELECT * 
FROM Titles_Revised  
WHERE partnum = 98765


-- Task #2 Exercise: Update the book title with part number 98765 to: 'Learn to Play the Viola'  
-- Task #2 Solution: Update the Record
UPDATE Titles_Revised  
SET bktitle = 'Learn to Play the Viola'  
WHERE partnum = '98765'


-- Verify Update
SELECT *  
FROM Titles_Revised  
WHERE partnum = '98765'  


-- Task #3 Exercise: Delete the record with part number 98765.
-- Task #3 Solution:
DELETE Titles_Revised  
WHERE partnum= '98765'  


-- Verify Deletion  
SELECT *  
FROM Titles_Revised   
WHERE partnum = '98765'



/* -------------------------------------------------------
## <p id = "3"> LESSON 3: Manipulating Table Structure | [Back to ToC](#toc)</p>
---------------------------------------------------------- */


-- Learn more about field Data types by going to the  
[Learn Microsoft Page](https://learn.microsoft.com/en-us/sql/t-sql/data-types/data-types-transact-sql?view=sql-server-ver17)



-- Create the table
CREATE TABLE ProduceInventory (
    ProduceName VARCHAR(50),
    PricePerPound DECIMAL(5,2), -- Exactly 2 decimal places that goes up to 999.99
    InStock BIT NOT NULL
);


-- Insert the data
INSERT INTO ProduceInventory (ProduceName, PricePerPound, InStock)
VALUES 
('Cantaloupe', 0.50, 1),
('Cucumbers', 0.25, 1),
('Pumpkin', 0.33, 1),
('Ginger', 0.99, 0);


/* Output */
Produce		Price ($/lb)	In Stock?
Cantaloupe	$0.50 		TRUE
Cucumbers	$0.25 		TRUE
Pumpkin		$0.33 		TRUE
Ginger		$0.99 		FALSE
/* End of Output */



-- Suggestion: Create a new query for retrieving the data but make sure you're on correct database.

/* ------------ Check Info ------------ */
sp_help ProduceInventory


/* ------------ Truncate Table ------------ */
TRUNCATE TABLE ProduceInventory


/* ------------ DROP (Delete) Table ------------ */
DROP TABLE ProduceInventory


/* ------------ Create & Verify Duplicate Table ------------ */
SELECT * 
INTO Slspers_Copy
FROM Slspers



### Recall  
-- The Object Explorer must be refreshed to see the new table.
-- Additionally, refresh IntelliSense to avoid the red error underline on the table name by going to:
-- Edit -> IntelliSense -> Refresh Local Cache (Ctrl + Shift + R)



/* ------------ ADD Column to ALTER TABLE ------------ */

ALTER TABLE Slspers_Copy 
ADD email varchar(40)
-- NOTE: Every column will contain NULL 

SELECT * FROM Slspers_Copy

-- Check Info on ALTERED Table
sp_help Slspers_Copy


-- Fill every salesperson with generic email
UPDATE Slspers_Copy
SET email = 'test@outlook.com'
WHERE email IS NULL;


-- Change Anna's email
UPDATE Slspers_Copy
SET email = 'annarules@outlook.com'
WHERE fname = 'anna';

SELECT * FROM Slspers_Copy

-- DROP Column IF EXISTS
ALTER TABLE Slspers_Copy  
DROP COLUMN IF EXISTS email


-- Check Info on ALTERED Table
sp_help Slspers_Copy



/* ------------ Change Column property ------------ */

Task: Change the fname column so it can hold up to 10 characters and is required (it cannot be left blank or NULL)

-- Check TO VERIFY the Table.
sp_help Slspers_Copy


-- First, verify that we can enter a NULL value for Fname
INSERT INTO Slspers_Copy
VALUES ('N01', NULL, 'Nguyen', 0.05)


-- Alter the Table
ALTER TABLE Slspers_Copy 
ALTER COLUMN fname varchar(10) NOT NULL


-- Check TO VERIFY the change.
sp_help Slspers_Copy
-- Under the column "Nullable", we see that the fname column says 'No' 


-- Executing the above query should now throw an error:
``` 
Cannot insert the value NULL into column 'fname', table 'Pub1.dbo.Slspers_Copy'; column does not allow nulls. INSERT fails.
The statement has been terminated.
```
INSERT INTO Slspers_Copy
VALUES ('N01', NULL, 'Nguyen', 0.05)



/* To revert the column back to the way it was.
ALTER TABLE Slspers_Copy 
ALTER COLUMN fname VARCHAR(40) NULL;



/* ------------ CONSTRAINTS  i.e. Create a constraint after a table is already created. ------------ */

Constraints are rules that limit data. Inserting invalid data will fail if the constraint is active.
In SQL Server, constraints are separate objects, so we drop/remove the constraint to allow invalid data again.


Task: Add a rule (constraint) to make sure commission values are between 0 and 10% (0 to 0.1).
To enforce a value range like 0 <= commrate <= 0.1, we'll use a CHECK constraint.


-- Invalid data can be initially be inserted since there are no constraints
INSERT INTO Slspers_Copy
VALUES (1, 'Finnie', 'Nguyen', 0.25);


-- Adding the constraint to enforce Commission between 0 and 10%
ALTER TABLE Slspers_Copy
ADD CONSTRAINT chk_commrate CHECK (commrate >= 0 AND commrate <= 0.1);


-- To verify constraint
EXEC sp_help 'Slspers_Copy';

-- Running the previous insertion will now fail 
INSERT INTO Slspers_Copy
VALUES (1, 'Finnie', 'Nguyen', 0.25); -- Invalid Insertion Data since 0.25 is greater than 0.1 (10%)


> Use DROP CONSTRAINT to remove the Constraint to allow any commission value


-- Remove the commission constraint
ALTER TABLE Slspers_Copy
DROP CONSTRAINT chk_commrate;


-- Re-inserting data will now work after removing the constraint
INSERT INTO Slspers_Copy
VALUES (1, 'Finnie', 'Nguyen', 0.25);





/* ------------ ADDING A DEFAULT CONSTRAINT ------------ */

-- DEFAULT keyword sets a value for future inserts only
-- It does NOT change existing rows with 'some value'


ALTER TABLE Slspers_Copy
ADD CONSTRAINT df_commrate DEFAULT 0.02 FOR commrate;


-- To verify constraint
EXEC sp_help 'Slspers_Copy';


-- This works:  
INSERT INTO Slspers_Copy 
VALUES (1, 'Alice', 'Smith', 0.05);

-- This also works since we added a DEFAULT constraint:
INSERT INTO Slspers_Copy (repid, fname, lname)
VALUES (1, 'Alice', 'Smith');


-- This does NOT work:
INSERT INTO Slspers_Copy 
-- (repid, fname, lname) -- SQL Server expects values for all columns in the table
VALUES (1, 'Alice', 'Smith');

-- Verify: 
SELECT * FROM Slspers_Copy 



-- Notice about DROPPING CONSTRAINT!

-- If a column has a constraint, dropping the column won't work: 
ALTER TABLE YourTableName 
DROP COLUMN commrate -- won't work


-- Step 1: First drop the default constraint
ALTER TABLE Slspers_Copy
DROP CONSTRAINT df_commrate; -- remember to use 'sp_help YourTableName' if you forget the constraints name.


-- Step 2: Then drop the column
ALTER TABLE Slspers_Copy
DROP COLUMN commrate


-- Verify
sp_help YourTableName



/* ------------ Exercise: Try to add a default constraint  ------------ */

CONSTRAINT generic_email DEFAULT 'iloveSQL@gmail.com';

-- Using SSMS,  Verify constraint via Design View by right-click the table -> Design View 
Once the view is open, make sure to click on "Email"
In the column properties pane, see the default under "Default Value or Binding".

-- Make a new query to test
-- Test Constraint
INSERT INTO
YourTableName (repid, fname, lname, commrate)
Values
('E04', 'Raza', 'Tahir', 0.01)


 
/* ------------ Primary KEY Constraint!!! ------------ */


-- we can add primary key constraints 
-- A Primary Key is a unique identifier for each record in a table and cannot contain duplicates or NULL values!
-- You can have only 1 primary key per table unless it's a composite.
-- NOTE: Make sure we effect the DIFFERENT TABLE

SP_HELP Slspers_Copy


-- Warning - We can not make a column a primary key if it contains duplicates.
TRUNCATE TABLE Slspers_Copy

-- SQL Server refuses to make it a primary key because NULLs are allowed
ALTER TABLE Slspers_Copy
ALTER COLUMN repid varchar(6) NOT NULL; -- Exercise: Make the Slspers_Copy to be a NON null value.



ALTER TABLE Slspers_Copy
ADD CONSTRAINT pk_slspers PRIMARY KEY (repid);


-- To verify constraint
EXEC sp_help 'Slspers_Copy';


INSERT INTO Slspers_Copy
VALUES (1, 'Raza', 'Tahir', 0.05) 


-- To Remove Constraint
ALTER TABLE Slspers_Copy
DROP CONSTRAINT pk_slspers;


-- How to AutoIncrement Primary Key Constraint
-- Note: IDENTITY can only be set when the column is created
ALTER TABLE Slspers_Copy
ADD repid_new INT IDENTITY(1,1) PRIMARY KEY;




/* -------------------------------------------------------
## <p id = "4"> LESSON 4: Working with Views | [Back to ToC](#toc)</p> 
---------------------------------------------------------- */



> SQL can execute basic logic  

IF 1 = 1
    PRINT 'This is true';


> IF statements can only be used inside T-SQL blocks (e.g., stored procedures, scripts)  

'''
SELECT COUNT(*) From Slspers -- Output: 10

IF ( ( SELECT COUNT(*) From Slspers ) > 5 )
	PRINT 'More than 5'
ELSE
	PRINT 'Less than or equal to 5'
'''
 

> BEGIN/END block defines a statement block which is a group of T-SQL statements executed as a single unit in procedural logic.

-- This code will NOT work
IF (3+3) != 6
	PRINT 'Condition is true'; 
	PRINT 'Do more things here'; -- Statement becomes printed when it shouldn't.

-- Nothing becomes printed as it should.
IF (3+3) != 6
BEGIN
    PRINT 'Condition is true';
    PRINT 'Do more things here';
END 



### Another Example

```
-- This code will NOT execute.
IF ( ( SELECT COUNT(*) From Slspers ) > 5 )
	PRINT 'More than 5'
	PRINT 'Hooray!'
ELSE
	PRINT 'Less than or equal to 5'
	PRINT 'Oh no!'
```

```
-- This code WILL execute.
IF ( ( SELECT COUNT(*) From Slspers ) > 5 )
	BEGIN
		PRINT	'More than 5'
		PRINT	'Hooray!'
	END
ELSE
	BEGIN
		PRINT 'Less than or equal to 5'
		PRINT 'Oh no!'
	END
```


### Views
View is essentially a SAVED QUERY.
Think: A SQL View is a virtual table.

A view does not "physically" store data — it just stores the query.

Since a view doesn’t store data itself and is just a saved query on a table,
So if we delete data through the view, we'll actually be deleting it from the underlying table, because that’s where the real data is stored.
 

Views can be based on:
- One entire table
- A few columns from 1 table
- Multiple joined tables
- Subqueries
- Functions


Why Views Matter
- Security
	- DBAs can restrict access to tables but grant access to views.
	- A view can expose only specific rows and columns.
Efficiency
	- It’s much faster. Instead of loading all 100 columns of a table, you only retrieve the 3 you need.


Difference between VIEWS & PROCEDURES
- Can’t store/accept parameters (no input).
- Doesn’t contain procedural logic (no IF, loops, etc.).


-- After a View is created, Expand the views folder in the object explorer to now see your view.
-- When creating the view, make sure to refresh Intellisense
-- Edit -> Intellisense -> Refresh Local Cache


> -- You can make views VIA THE OBJECT EXPLORER AS WELL


-- Task #1: Create a view to show only people from state 'CA'
CREATE VIEW CA_Cust AS
SELECT custname, city, state
FROM Customers
WHERE state = 'CA';
-- Note: The ORDER BY clause is invalid in views

-- Result: If you refresh the views folder, you can see the view there.

-- A view can be queried like a table.
SELECT * FROM CA_Cust
WHERE city = 'Quebec'-- also works as an addition


-- Syntax to Delete (Drop) a View
DROP VIEW CA_Cust;


-- Task: #2
-- Create a virtual table called Top_Salesperson that shows only repid and fname
CREATE VIEW Top_Salesperson AS
SELECT repid, fname 
FROM Slspers_Copy
WHERE commrate > 0.04

-- Displays the SQL code used to define the view.
sp_helptext Top_Salesperson

-- INSERT INTO Top_Salesperson VALUES (1, 'John', 'Smith', 0.5); -- Won't Work
-- INSERT INTO Top_Salesperson VALUES (1, 'John');  -- Will Work

-- SELECT * FROM Top_Salesperson



-- Subtask: Alter the Salesperson view to now display repid, fname & lname
ALTER VIEW Top_Salesperson AS  -- Change ALTER VIEW with CREATE VIEW to update the view instead of making a new one.
SELECT repid, fname, lname
FROM Slspers_Copy


SELECT * FROM Top_Salesperson


DROP VIEW Top_Salesperson


SELECT * FROM  Top_Salesperson -- Won't work





/* ------------ EXERCISE SNIPPET: Activity 4-1 Step 3B ------------ */
```
CREATE VIEW mediumprice AS
SELECT TOP 15 partnum, bktitle, slprice
FROM Titles
WHERE slprice BETWEEN 20 AND 30
ORDER BY slprice


-- Verify that View works.
SELECT * FROM mediumprice


-- Insert 2 titles via the View
INSERT mediumprice (partnum, bktitle, slprice)
VALUES ('40256', 'How to Play Violin (Intermediate)', 22)


INSERT mediumprice (partnum, bktitle, slprice)
VALUES ('40257', 'How to Play Violin (Advanced)', 23)


-- Verify that Insertions have worked
SELECT * 
FROM mediumprice
WHERE partnum IN ('40256', '40257')


-- Will update price in both the view & table
UPDATE mediumprice
SET slprice=30
WHERE partnum='40121'


-- Check Update (Both queries are the same)
SELECT * FROM mediumprice WHERE partnum='40121'
SELECT * FROM Titles WHERE partnum='40121'


-- Use the View to delete a specific Title.
DELETE mediumprice
WHERE partnum='40121'


-- Chcek that it got deleted.
SELECT *
FROM mediumprice
WHERE partnum='40121'


-- Finish the exercise by dropping the view.
DROP VIEW mediumprice
```


/* -------------------------------------------------------
## <p id = "procedures"> Bonus Lesson: Procedures | [Back to ToC](#toc)</p> 
---------------------------------------------------------- */


Recall that a View:
- Can’t accept parameters (no input).
- Doesn’t run conditional logic (e.g. no IFs)
- Can't use loops


A view is a saved query - it doesn’t execute logic.
A stored procedure can run logic, like IF, SET, or UPDATE statements.


sp_help is a built-in stored procedure


> Since Procedures add PROGRAMMABILITY, they are more like FUNCTIONS.



Task:
Write a stored procedure that accepts a @State parameter, 
retrieves all matching records from the PotentialCustomers table, 
and inserts those records into the Customers table.


CREATE PROCEDURE InsertPotentialCustomersByState
    @State NVARCHAR(50)
AS
BEGIN
   	-- Optional -- SET NOCOUNT ON;
	-- Always add SET NOCOUNT ON; at the top of your stored procedures unless you specifically need the row count messages.

    INSERT INTO Customers
    SELECT *
    FROM Potential_Customers
    WHERE State = @State;
END;

-- TO DELETE
DROP PROCEDURE InsertPotentialCustomersByState;

-- I CAN VIEW THIS STORED PROCEDURE UNDER:
	Pub1 -> Programmability -> Stored Precedures


EXEC InsertPotentialCustomersByState @State = 'CA';

-- CHECK
SELECT * FROM Customers
WHERE STATE = 'CA'


-- To delete
DELETE FROM Customers
WHERE custnum = 31004;

-- Another delete example
DELETE FROM Slspers_Copy
WHERE repid = '1';


Task: Write a procedure to update 2 tables.
```
If a view is updateable, you can only insert into one underlying (base) table through it.
If you need to insert into multiple tables, the view alone won’t handle that. You could use a trigger to do extra inserts automatically.
But it’s usually better to use a stored procedure, because a procedure can easily insert two rows — one in each table — in a clear and controlled way.
```


/* -------------------------------------------------------
## <p id = "5"> Lesson 5: Indexing Data | [Back to ToC](#toc)</p> 
---------------------------------------------------------- */

Speeds up sorts & searches especially common ones


/* -------------------------------------------------------
## <p id = "6"> LESSON 6: Managing Transactions | [Back to ToC](#toc)</p> 
---------------------------------------------------------- */

Transactions protects your database from partial updates.

When I need to run multiple queries, transactions ensure that a series of operations are executed as a single unit of work 
> Think of it as 'ALL OR NOTHING'. Either all succeed (committed) or all fail (rolled back)

Once a transaction is committed or rolled back, the transaction ends. You can't roll back a committed transaction.

Common Examples of Transactions could be

	- Bank Transfers from Saving -> Checking
		Step 1: Subtract amount from Account A (Saving).
		Step 2: Add amount to Account B (Checking).

		BEGIN TRANSACTION;
			UPDATE accounts SET savingBalance = savingBalance - 500 WHERE account_id = '123';
			UPDATE accounts SET checkingBalance = checkingBalance + 500 WHERE account_id = '123';
		COMMIT;

	- Inventory Management
		Step 1: Insert a new record into the Orders table.
		Step 2: Deduct items from Inventory table.
		Step 3: Update customer’s balance in Accounts table.



#### Example #1


-- Create a transaction that inserts two salesperson records. 
-- This is a good way to test for errors before the code becomes implemented.

BEGIN TRANSACTION;
INSERT INTO Slspers_Backup VALUES ('N123', 'Nickki', 'Nguyen', 0.05)
INSERT INTO Slspers_Backup VALUES ('L123', 'Lena', 'Duong', 0.05)
ROLLBACK TRANSACTION; -- Switch 'ROLLBACK' with 'COMMIT' TRANSACTION when ready to implement

-- Check
SELECT * FROM Slspers


#### Example #2

-- First create a table to start off this example:
CREATE TABLE person (
    name VARCHAR(100) UNIQUE
);

-- Now try inserting these names (without a transaction):
INSERT INTO person (name) VALUES ('Alice');
INSERT INTO person (name) VALUES ('Bob');
INSERT INTO person (name) VALUES ('Alice'); -- duplicate

The first two inserts will work, but the third will fail because name must be unique. i.e. the table becomes only partially filled.  

-- Execute the code below to view the contents of the Person table.
SELECT * FROM person;

Output:
```
Alice
Bob
```

> To reset the table for the solution:  
TRUNCATE TABLE Person 

> Note: Using a transaction ensures that if the third insert fails, no rows are saved.

-- Solution
BEGIN TRANSACTION;

INSERT INTO person (name) VALUES ('Alice');
INSERT INTO person (name) VALUES ('Bob');
INSERT INTO person (name) VALUES ('Alice');  -- duplicate name (violates UNIQUE constraint)

COMMIT TRANSACTION;

The transaction will not execute any of the statements until everything (particularly the 3rd line) is correct.
All or nothing becomes executed.


#### Example #3

-- Use a TRY/CATCH block as a way of Exception Handling

How it works:  
If all operations in the TRY block succeed, then the COMMIT block is then executed.    
If any error occurs, control moves to the CATCH block and ROLLBACK TRAN is executed instead.


Make sure a table has been created
CREATE TABLE person (
	name VARCHAR(100) UNIQUE
);



BEGIN TRANSACTION;
BEGIN TRY
	-- Some SQL statements
	INSERT INTO perso VALUES ('Alice'); -- Table 'Person' misspelled on purpose.
END TRY
BEGIN CATCH
	ROLLBACK TRANSACTION;
	SELECT * FROM Person
	PRINT('Log Error')
END CATCH





-- Bonus Chapter --
/* ------------ Check Tables ------------ */
SELECT *
FROM Pub2.INFORMATION_SCHEMA.TABLES


/* ------------ Drop Tables & Confirm ------------ */
DROP TABLE Obsolete_Titles1
DROP TABLE Potential_Customers1

SELECT *
FROM Pub2.INFORMATION_SCHEMA.TABLES



-- Bonus Comments --
In SQL Server, when you run a query like INSERT, UPDATE, or DELETE, SQL Server by default returns a message like:

``` (3 rows affected) ```

This message is informational, but in some scenarios (like stored procedures or loops), it can clutter the output.  
Solution:  
SET NOCOUNT ON -- WILL THEN SUPPRESS THE MESSAGE


-- Example  
SET NOCOUNT ON;  
UPDATE Customers SET State = 'CA' WHERE State = 'California';



-- Additional  --
CREATE A PIVOTTABLE FROM SQL SERVER TABLE
Create a custom shortcut key for useful commands
Create a new database?
Create a backup database?
If you delete a table from a backup, how to restore.
Transaction log
If you want to hide the column but still support inserts, use a trigger - LEARN!!!
SQL P2.txt
Displaying SQL P2.txt.