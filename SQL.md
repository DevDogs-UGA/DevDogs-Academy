# What is SQL/MySQL?

SQL, often pronounced either "Sequel" or "Ess Que Ell", stands for Structured Query Language and is by far one of the most common and easier languages to learn. SQL acts as an international, standardized language to communicate with relational databases in order to create, edit, delete, and obtain information. Fortunately for us, this means once we learn SQL we'll be able to apply it to pretty much any database management system that accepts SQL. 

What is a relational database? A relational database consists of tables made up of columns and rows, like an Excel spreadsheet, where each row has a unique input with its own identifying information determined by its columns. These tables are *related* to each other through *keys*, which we'll get into more later. 

MySQL, often pronounced "My Ess Que Ell" or "My Sequel", is the Relational Database Management System(RDBMS) that we'll be using. We will be learning the basics in this article and I would recommend you to download MySQL Workbench and follow along. You can find the download [here](https://dev.mysql.com/downloads/installer/).  

I am using version 8.0.34 and would recommend you use the same if you want to follow along. This is ***not*** the most recent version and there are differences between versions and some commands may be slightly different under another version.


### Very quick disclaimer
***This article is student-created and run so there may be some incorrect info and there will definitely be typos. If you notice a mistake or feel information can be conveyed in a more effective way please feel free to [open an issue](https://github.com/DevDogs-UGA/DevDogs-Academy/issues) and we'll get right on it.***

## The very basics 

This is meant as an introductory into SQL and as such we won't be delving into all the commands. The goal is that by the end of the article, you can confidently build and navigate a database on your own. 

Like Java, every command ends with a semicolon. So if I wanted to create a database called "headache" I would do it like so:
~~~~sql
CREATE DATABASE headache;
~~~~
This successfully creates an empty database called headache, but without the semicolon the command wouldn't work. Another important thing to remember about SQL is that it is **not** case sensitive and the command is also valid as:
~~~~sql
create database headache;
~~~~
And if you're feeling especially bored you can write:
~~~~sql
cReAtE dAtAbAsE headache;
~~~~



If you're trying out MySQL for the first time, two important things to note are the execute button at the top and the action output panel at the bottom of the workbench.

![mysql example](https://github.com/user-attachments/assets/f78f209f-a8e5-468f-86bf-d816639f31aa)

After hitting the execute button always check the action output panel to make sure your command went through, and if it didn't the panel will tell you why. A common mistake when starting to use SQL is running the previous command again because you've forgotten to delete it from the window. A simple way to avoid this is to highlight the section of code you want to run, so when you hit the execute button only the highlighted code runs.

An important term to know is **schema**. A schema is essentially the blueprint for how data is laid out and interconnected. As an introduction the table below has a schema that defines three columns of: a double, string, and year type. 
|DOUBLE   |STRING   |YEAR     | 
|---------|---------|---------|
|15.75    |John Doe |2023|
|22.00    |Alice Keys|2016|
|25.00    |Dania Hogforn|2013|


## What information can be stored?

In SQL the rows of a table represent individual records and these records contain data stored in columns. SQL is strict in regards to what data is allowed in each column; you can not store a float type in an int column. There are lots of different data types you can assign a column; below are common ones we'll be sticking to in this article.
| Data Type          | Description                                           |
|--------------------|-------------------------------------------------------|
| `INT`              | Integer data type, used for whole numbers.            |
| `BIGINT`           | Large integer data type, supports very large numbers. |
| `SMALLINT`         | Small integer data type, used for smaller ranges.     |
| `FLOAT`            | Floating-point number with approximate precision.     |
| `DECIMAL(p, s)`    | Exact numeric data type, specified precision (`p`) and scale (`s`). |
| `DOUBLE`           | Double-precision floating-point number.               |
| `CHAR(n)`          | Fixed-length string, where `n` is the number of characters. |
| `VARCHAR(n)`       | Variable-length string, where `n` is the maximum number of characters. |
| `TEXT`             | Large variable-length string.                         |
| `DATE`             | Date type, stores year, month, and day.               |
| `TIME`             | Time type, stores hours, minutes, and seconds.        |
| `DATETIME`         | Stores both date and time.                            |
| `TIMESTAMP`        | Stores date and time, often used for row versioning.  |
| `BOOLEAN`          | Stores `TRUE` or `FALSE` values.                      |



## Creating our first database/table

After installing and setting up your workbench we're going to create our first database, TUTDB, with the command:
~~~~sql
CREATE DATABASE TUTDB;
USE TUTDB;
~~~~
***We run "USE TUTDB;" so MySQL knows that we will be working with this database. This shouldn't be necessary unless you already have another database but we'll run it anyway.***

Once we have our database made, we're going to create our first table. When we create a table we need to specify the column names and types. *(Don't worry if you don't know all the information you want to store just yet, you can always modify the table at a later point to add on or remove columns.)*

For our purposes, we'll be creating a table to store employee data for a dealership:
~~~~sql
CREATE TABLE Employees(
EmployeeID INT,
FirstName varchar(50),
LastName varchar(50),
Pay DECIMAL(5,2)
);
~~~~

Assuming everything went smoothly and nothing is red in the action output panel, we're ready to view our first table. To do so use the command:
~~~~sql
SELECT * FROM Employees;
~~~~


## The select command

The SELECT command is your best friend, chances are you'll be running it after every other command to check on your database and make sure your tables look good. In SQL you follow the **SELECT** command with an option to specify what and how many entries you want returned. A list of some of these options can be found below. Another thing to take note of is **FROM**. This keyword is followed by the table you want to pull information from, in our case we pulled from the Employees table. For this tutorial, you should use the '*' after SELECT to see all the columns but as your table and databases grow you'll eventually want to specify which columns you want to view.
| Option           | Description                                                                 | Example                                                                 |
|------------------|-----------------------------------------------------------------------------|-------------------------------------------------------------------------|
| `*`              | Selects all columns from a table.                                           | `SELECT * FROM table_name;`                                             |
| `SELECT DISTINCT`| Returns only distinct (different) values, eliminating duplicates.           | `SELECT DISTINCT column_name FROM table_name;`                          |
| `WHERE`          | Filters records based on specified conditions.                              | `SELECT column_name FROM table_name WHERE condition;`                   |
| `ORDER BY`       | Sorts the result set in ascending (`ASC`) or descending (`DESC`) order.     | `SELECT column_name FROM table_name ORDER BY column_name ASC;`          |
| `GROUP BY`       | Groups rows that have the same values in specified columns.                 | `SELECT column_name, COUNT(*) FROM table_name GROUP BY column_name;`    |
| `HAVING`         | Filters groups based on a condition, often used with `GROUP BY`.            | `SELECT column_name, COUNT(*) FROM table_name GROUP BY column_name HAVING COUNT(*) > 1;` |
| `LIMIT`          | Restricts the number of rows returned in the result set.                    | `SELECT column_name FROM table_name LIMIT 10;`                          |
| `AS`             | Provides an alias for a column or table name, which can simplify query results or improve readability. | `SELECT column_name AS alias_name FROM table_name;`                     |


## Adding data to our new table

Now that you know what the SELECT command is and how to use it, lets play around with our table a little. A database with no data doesn't do anybody any good so let's add some employees with the **INSERT INTO** command:
~~~~sql
INSERT INTO Employees(EmployeeID, FirstName, LastName, Pay) VALUES
(1, "Hank", "Lean", 12.50),
(2, "Dean", "Smith", 14.00),
(3, "Brock", "Oli", 33.00);
~~~~
Currently, we're adding data for every column so we can omit the column names as long as we keep the data ordered the same way the schema is set up (EmployeeID, FirstName, etc)
~~~~sql
INSERT INTO Employees VALUES
(4, "Doc", "Venture", 40.00);
~~~~
After running a "SELECT * FROM Employees" your table should look like the one below. If not, I would recommend finding the section on deletion and either correct it or start over.
| EmployeeID | FirstName | LastName | Pay  |
|------------|-----------|----------|------|
| 1          | Hank      | Lean     | 12.50|
| 2          | Dean      | Smith    | 14.00|
| 3          | Brock     | Oli      | 33.00|
| 4          | Doc       | Venture  | 40.00|


## Operators

Like Java, SQL has operators that we can use in our queries and processes. Below is a handy table you can refer to if you're looking for something specific.
| Operator     | Description                                             | Example                             |
|--------------|---------------------------------------------------------|-------------------------------------|
| `=`          | Checks if two values are equal                          | `SELECT * FROM Employees WHERE Pay = 100;` |
| `<>` or `!=` | Checks if two values are not equal                      | `SELECT * FROM Employees WHERE Pay != 100;` |
| `>`          | Checks if a value is greater than another               | `SELECT * FROM Employees WHERE Pay > 100;`  |
| `<`          | Checks if a value is less than another                  | `SELECT * FROM Employees WHERE Pay < 100;`  |
| `>=`         | Checks if a value is greater than or equal to another   | `SELECT * FROM Employees WHERE Pay >= 100;` |
| `<=`         | Checks if a value is less than or equal to another      | `SELECT * FROM Employees WHERE Pay <= 100;` |
| `BETWEEN`    | Checks if a value is within a specified range           | `SELECT * FROM Employees WHERE Pay BETWEEN 50 AND 100;` |
| `IN`         | Checks if a value is within a set of specified values   | `SELECT * FROM Employees WHERE Pay IN (100, 200, 300);` |
| `LIKE`       | Searches for a specified pattern in a column            | `SELECT * FROM Employees WHERE FirstName LIKE 'H%';` |
| `IS NULL`    | Checks if a value is `NULL`                             | `SELECT * FROM Employees WHERE LastName IS NULL;` |
| `IS NOT NULL`| Checks if a value is not `NULL`                         | `SELECT * FROM Employees WHERE LastName IS NOT NULL;` |
| `AND`        | Combines multiple conditions, all must be true          | `SELECT * FROM Employees WHERE Pay > 100 AND Pay < 200;` |
| `OR`         | Combines multiple conditions, at least one must be true | `SELECT * FROM Employees WHERE Pay > 100 OR Pay < 50;`  |
| `NOT`        | Negates a condition                                     | `SELECT * FROM Employees WHERE NOT Pay = 100;`          |



### Can you leave out information?

It depends. Knowing what your table schema looks like is incredibly important and will determine if we can leave an area null or if it's even needed. In our case when we created our table we didn't specify any of our columns couldn't contain a null value so we can do:
~~~~sql
INSERT INTO Employees (EmployeeID, FirstName, LastName) VALUES
(5, "Henry", "Killenger");
~~~~
This code runs fine and now your table should look something like: 
| EmployeeID | FirstName | LastName   | Pay  |
|------------|-----------|------------|------|
| 1          | Hank      | Lean       | 12.50|
| 2          | Dean      | Smith      | 14.00|
| 3          | Brock     | Oli        | 33.00|
| 4          | Doc       | Venture    | 40.00|
| 5          | Henry     | Killenger  | NULL |

Had we modified **Pay** to not accept NULL values this would've resulted in an error. We'll discuss modifications and altering tables in the next section.


## Modifications and altering tables 


Our first modification to the table will be correcting the NULL value with the **UPDATE** command:
~~~~sql
UPDATE Employees SET Pay = 7.50 WHERE EmployeeID = 5;
~~~~
You'll notice a couple of things here. First, we have a new command, **UPDATE**, which takes in the table, column, and an identifier (EmployeeID). Second, unlike Java, the '=' can act as either a comparison operator or assignment operator.

So what if we do if we want to make it so **Pay**, or any other column can't be null? We can run the command: 
~~~~sql
ALTER TABLE Employees MODIFY COLUMN Pay DECIMAL(5,2) NOT NULL;
~~~~
Now if we try and run a command like the one below it will not execute because **Pay** can't be null:
~~~~sql
INSERT INTO Employees VALUES (6,"Jim","Bob",NULL);
~~~~
We can also set a default value to a column. For instance, we can set **Pay** to have a default value of 0.00 so if we insert data without a pay value it will default to 0.00.
~~~~sql
ALTER TABLE Employees ALTER COLUMN Pay SET DEFAULT 0.00;
~~~~
Now we can run the command below and MySQL should assign **Pay** to 0.00.
~~~~sql
INSERT INTO Employees(EmployeeID, FirstName, LastName) VALUES (6, "Jim", "Bob");
~~~~
You can check your table with the **SELECT * FROM Employees** to make sure it looks like:
| EmployeeID | FirstName | LastName | Pay  |
|------------|-----------|----------|------|
| 1          | Hank      | Lean     | 12.50|
| 2          | Dean      | Smith    | 14.00|
| 3          | Brock     | Oli      | 33.00|
| 4          | Doc       | Venture  | 40.00|
| 5          | Henry     | Killenger| 7.50 |
| 6          | Jim       | Bob      | 0.00 |


## Deletion

Now, it turns out it's not legal to pay an employee $0 an hour, so what are we going to do? Obviously, we're going to fire Jim Bob. The command the delete an entry is simple:
~~~~sql
DELETE FROM Employees WHERE EmployeeID = 6;
~~~~
This successfully fires Jim Bob from our database. However, be careful because if you forget the WHERE clause and just run "DELETE FROM Employees;" you'll end up clearing your entire table.
If you happen to want to remove a table you use:
~~~~sql
DROP TABLE name;
~~~~
Or a database:
~~~~sql
DROP DATABASE name;
~~~~

## Modifications

Primary keys are vital to databases and each table should have one. A primary key is a modifier to a column that constricts data to being ***unique*** and ***not null***. This allows the database to have a unique identifier for every entry in a table. If Jim Bob and Henry Killenger ended up having the same Employee ID they both would've been deleted. Sure you can specify both employee id and name but this is bad practice and as a company grows you'll eventually have people with the same names and if there's no way to differentiate them in the database you're going to have a bad time. To avoid this headache and create a primary key use:
~~~~sql
ALTER TABLE Employees ADD PRIMARY KEY(EmployeeID);
~~~~

If at some point you decide you want to change primary keys or if you don't want one all together you run:
~~~~sql
ALTER TABLE Employees DROP PRIMARY KEY;
~~~~
***Quick PSA: Each table has ONE primary key, but the primary key can be made up of more than one column. If you're interested in learning more you can check it out [here](https://www.w3schools.com/mysql/mysql_primarykey.asp).
You can also designate a primary key when you first create a table, we just did so after to teach SQL a piece at a time.***


Another modifier that can make life easier is **AUTO_INCREMENT** which automatically creates and adds one to a field. **We will NOT be using auto increment in the tutorial, because when you delete an entry and add another it keeps incrementing which can get funky when we keep adding and removing entries.** IF we were going to do it however we would use:
~~~~sql
ALTER TABLE Employees MODIFY EmployeeID INT AUTO_INCREMENT;
~~~~
Notice when we modify the EmployeeID column we have to specify its data type, int. This is because MySQL treats the MODIFY command as a complete redefinition of the column this means we should always redefine it with the same data type it had originally, unless you WANT to change the data type as well. If you forgot the schema for your table, two easy ways to check is by using the drop-down menu to the left and clicking on the column OR run the command "SHOW CREATE TABLE Employees;" which will give you more details details after clicking the Form Editor tab.
![mysql example2](https://github.com/user-attachments/assets/faffa393-e7c6-4782-a2a4-77d1ffd5048d)


To undo the auto-increment from a column run:
~~~~sql
ALTER TABLE Employees MODIFY EmployeeID int(10);
~~~~
***Here the 11 in int(10) is a semi-arbitrary number that represents the 'width' of an int. This does not change the range of ints that can be stored and only matters if you use ZEROFILL, in which case it would become entries like 6 would become 0000000006.***



Now what if we want to modify a column to accept only unique or non-null data without setting it as a primary key? All you need to do is run:
~~~~sql
ALTER TABLE Employees MODIFY COLUMN FirstName VARCHAR(50) NOT NULL;
~~~~
Now MySQL won't let us insert any null data into the FirstName column and if we want to remove this constraint we just re-modify the column:
~~~~sql
ALTER TABLE Employees MODIFY COLUMN FirstName VARCHAR(50);
~~~~
Making a column only accept UNIQUE inputs is very similar to NOT NULL:
~~~~sql
ALTER TABLE Employees MODIFY COLUMN FirstName VARCHAR(50) UNIQUE;
~~~~
However, it does differ when removing the UNIQUE constraint. If you try and recast it without the constraint like we did with NOT NULL it won't remove the modifier. To remove the UNIQUE restraint we run:
~~~~sql
ALTER TABLE Employees DROP INDEX FirstName;
~~~~
Now we can have multiple employees with the same first name. I don't plan on using the UNIQUE or NOT NULL constraint on the FirstName column for the rest of the tutorial, so feel free to remove it if you want.



## Adding a new column/re-naming

Looking back, it may have been overkill to have deleted Jim Bob from the database entirely and deleting employees could have impacts on other tables as we expand our database. So, we're going to create a new column that tells us if the employee is currently employed or not. 
~~~~sql
ALTER TABLE Employees ADD COLUMN Employeed BOOLEAN;
~~~~
Now we have a column that will hold True if the person is a current employee, or False if they are no longer with the organization. However, because we just added this new column all its entries are NULL. Since Jim Bob is the only person currently not employed with us we will just run: 
~~~~sql
UPDATE Employees SET Employeed = 1 WHERE EmployeeID <= 6;
~~~~
In MySQL BOOLEAN is an alias for TINYINT(1) so they store the exact same thing, however, we'll be using BOOLEAN for clarity. You'll notice that we're not explicitly storing the values True or False and instead storing 1 and 0. You can still use TRUE or FALSE when querying or setting boolean values and MySQL will understand you're looking for 0 or 1.

Now, we're going to add Jim Bob back to our table as not employed with us:
~~~~sql
INSERT INTO Employees VALUES(7, "Jim", "Bob", 0.00, 0);
~~~~
If you want to confirm Jim Bob is back you can run the following command to view all employees not currently employed by the organization:
~~~~sql
SELECT * FROM Employees WHERE Employeed = FALSE;
~~~~

Some of you may have picked up on and begrudgingly named our Employed column "Employeed". I did promise typos and to correct this and re-name the column we just run:
~~~~sql
ALTER TABLE Employees CHANGE Employeed Employed BOOLEAN;
~~~~
This is one of those commands that has been updated in more recent versions of MySQL to be more intuitive. If you are using a more recent version you can find pretty much all equivalent commands [here](https://www.w3schools.com/sql/sql_alter.asp). 
As of right now your table should look something like this:
| EmployeeID | FirstName | LastName | Pay  | Employed |
|------------|-----------|----------|------|----------|
| 1          | Hank      | Lean     | 12.50|1         |
| 2          | Dean      | Smith    | 14.00|1|
| 3          | Brock     | Oli      | 33.00|1|
| 4          | Doc       | Venture  | 40.00|1|
| 5          | Henry     | Killenger| 7.50 |1|
| 6          | Jim       | Bob      | 0.00 |0|


# Our second table
A relational database would be useless if there were no other tables to relate to, so let's create one. Our new table will be ***Sales*** and we'll be storing: TransactionID (BIGINT), EmployeeID (INT), GrossSale (DOUBLE (11,2)), TransactionDate (DATE), CustomerID (INT)
~~~~sql
CREATE TABLE Sales (
    TransactionID BIGINT,              
    EmployeeID INT,                    
    GrossSale DOUBLE(11, 2),           
    TransactionDate DATE,              
    CustomerID INT
);
~~~~
***If you're not sure of the purpose of the EmployeeID in the Sales table, it's to identify who made the sale for a transaction.***

Now, let's add some data!
~~~~sql
INSERT INTO Sales (TransactionID, EmployeeID, GrossSale, TransactionDate, CustomerID)
VALUES
    (1, 1, 250.50, '2024-01-10', 26),
    (2, 2, 500.99, '2024-02-12', 7),
    (3, 3, 150.25, '2024-03-15', 13),
    (4, 4, 300.75, '2024-04-18', 69),
    (5, 6, 1200.40, '2024-05-20', 38),
    (6, 2, 850.30, '2024-06-25', 72),
    (7, 5, 450.60, '2024-07-30', 38);
~~~~
With this table we're going to need a primary key, the most logical key we can use is the TransactionID column, so:
~~~~sql
ALTER TABLE Sales ADD PRIMARY KEY(TransactionID);
~~~~


## The foreign key
The foreign key is the constraint we'll be applying to columns to relate tables together. The foreign key can be related to either primary keys of another table or unique columns, however, relating through primary keys is much more common. For our Sales table, we'll use the EmployeeID as the foreign key to relate the Sales table to the Employees table. To do this we'll run: 
~~~~sql
ALTER TABLE Sales ADD FOREIGN KEY(EmployeeID) references Employees(EmployeeID);
~~~~
Now, our two tables are related. Notice we specified which table we were referencing "Employees" and then the specific column in "()". If we try to add a record into our Sales table with an EmployeeID that doesn't exist in our Employees table it will fail. The insert below with an EmployeeID of 100 results in an error:
~~~~sql
INSERT INTO Sales VALUES(8, 100, 3.99, '2024-10-10', 33);
~~~~
Furthermore, if we try to delete a record from our Employees table that is referenced by our Sales table it will throw an error:
~~~~sql
DELETE FROM Employees WHERE EmployeeID = 6;
~~~~
Foreign keys have names and to drop a foreign key we will want to know its name. To check the name MySQL auto-generated for our foreign key go to the schema drop-down, find the sales table, then foreign keys and you'll see the foreign key(s).
![mysql example3](https://github.com/user-attachments/assets/63efc46b-9259-4c7b-8630-e358333c6e6c)
To drop the key run:
~~~~sql
ALTER TABLE Sales DROP FOREIGN KEY name;
~~~~
When creating your foreign key you can also choose its name with a command set up like:
~~~~sql
ALTER TABLE Sales ADD CONSTRAINT name FOREIGN KEY(EmployeeID) references Employees(EmployeeID);
~~~~
For this tutorial, we'll be using a foreign key to connect our tables so if you've removed it, kindly add it back.


### ON DELETE

What if we want to be able to delete entries from our Employees table even if they occur in the Sales table? Well, two options are ON DELETE SET NULL or ON DELETE CASCADE. ON DELETE SET NULL simply sets the value in the related column to null if it's deleted from the parent column. However, ON DELETE CASCADE will delete the entire row in the child's database. Given our current Sales table below, if we delete Employee 2 from the Employees table with the foreign key set to ON DELETE SET NULL it will just change the EmployeeID value to null in transactions 2 and 6. However, if the key is set to ON DELETE CASCADE and employee 2 is deleted, all the data for transactions 2 and 6 will be deleted.
| TransactionID | EmployeeID | GrossSale | TransactionDate | CustomerID |
|---------------|------------|-----------|-----------------|------------|
| 1             | 1          | 250.50    | 2024-01-10      | 26         |
| 2             | 2          | 500.99    | 2024-02-12      | 7          |
| 3             | 3          | 150.25    | 2024-03-15      | 13         |
| 4             | 4          | 300.75    | 2024-04-18      | 69         |
| 5             | 6          | 1200.40   | 2024-05-20      | 38         |
| 6             | 2          | 850.30    | 2024-06-25      | 72         |
| 7             | 5          | 450.60    | 2024-07-30      | 38         |

If you want to add these options to a foreign key you'll first want to remove it (as we did above). Then you will recreate it with the command: 
~~~~sql
ALTER TABLE Sales ADD FOREIGN KEY(EmployeeID) references Employees(EmployeeID) ON DELETE SET NULL;
~~~~
Or for cascade:
~~~~sql
ALTER TABLE Sales ADD FOREIGN KEY(EmployeeID) references Employees(EmployeeID) ON DELETE CASCADE;
~~~~


## Joins

What are joins and what do they do? Joins are used to combine rows from two or more tables based on a related column between them. They allow you to retrieve data from multiple tables by specifying how the tables should be linked together. There a many types and below is a quick visual guide for you to refer back to:
![mysql joins2](https://github.com/user-attachments/assets/6077fce0-56a3-4203-83a3-2e9d63764df3)

Before we start using joins let's first add some more data to our tables:
~~~~sql
INSERT INTO Employees VALUES 
(7, "David", "Bowie", 12.50, 1),
(8, "Shelia", "Moppet", 14.00, 1),
(9, "Gary", "Mingle", 7.50, 1),
(10, "Billy", "White", 40.00, 1),
(11, "Hunter", "Gathers", 13.00, 1),
(12, "Timothy", "Traster", 13.00, 0),
(13, "Jah", "Bullard", 15.00, 1),
(14, "Ben", "Potter", 17.50, 0);
INSERT INTO Sales VALUES
(8, 8, 146.73, '2024-08-17', 41),
(9, 10, 299.99, '2024-08-17', 7),
(10, 8, 182.37, '2024-09-15', 12),
(11, 7, 175.69, '2024-09-18', 13),
(12, 13, 350.00, '2024-10-07', 7),
(13, 11, 239.99, '2024-10-21', 4),
(14, 9, 411.98, '2024-11-29', 39);
~~~~
Now both our tables hold twice as much info for us to work with!
When we talk about left and right joining, typically the table you use first in the command is the left and the table typed second is the right. To run a left join with Employees as the left table we'll run:
~~~~sql
SELECT * FROM Employees LEFT JOIN Sales ON Employees.EmployeeID = Sales.EmployeeID;
~~~~
Notice we used "ON Employees.EmployeeID = Sales.EmployeeID". This allows MySQL to match the records from the Employees table to the Sales table based on the EmployeeID column that they share. Also, we use table.column to tell MySQL which columns to use instead of "column name" FROM "table name". 

Now, MySQL should have pulled up a table consisting of ***at least*** one entry per employee. 
Some employees have two entries; one for each transaction they've been involved in. There are also employees that have NULL values for their Sales part of the table, this is because they're leeches and didn't make any sales.

To see which entries have no relation/overlap with the Sales table we can run:
~~~~sql
SELECT * FROM Employees LEFT JOIN Sales ON Employees.EmployeeID = Sales.EmployeeID WHERE Sales.EmployeeID IS NULL;
~~~~
This should have brought up Timothy and Ben's employee information along with null values for the Sale info. To run a right join, all we have need to do is change LEFT to RIGHT. Beucase our Sales table has an EmployeeID for each entry the information MySQL gives us won't be different.
~~~~sql
SELECT * FROM Employees RIGHT JOIN Sales ON Employees.EmployeeID = Sales.EmployeeID;
~~~~
Or:
~~~~sql
SELECT * FROM Employees RIGHT JOIN Sales ON Employees.EmployeeID = Sales.EmployeeID WHERE Sales.EmployeeID IS NULL;
~~~~

Unfortunately, MySQL doesn't have a command for FULL OUTER JOIN, so we have to create our own version consisting of the UNION between the left outer join and right outer join.
~~~~sql
SELECT * FROM Employees LEFT JOIN Sales ON Employees.EmployeeID = Sales.EmployeeID
UNION
SELECT * FROM Employees RIGHT JOIN Sales ON Employees.EmployeeID = Sales.EmployeeID;
~~~~
This output should look exactly like our left join command. This is because our foreign key in the Sales table prevents there from being NULL or an EmployeeID that doesn't belong to the Employee table.

Inner joins allow us to combine and view information that overlaps from both tables. For us that means when we run our command, MySQL should return the employee and sale information for each sale and exclude Timothy and Ben because their EmployeeIDs can't be found in the sales table. Try:
~~~~sql
SELECT * FROM Employees INNER JOIN Sales ON Employees.EmployeeID = Sales.EmployeeID;
~~~~

## Functions

MySQL has an absurd amount of functions and I would **highly** recommend giving a quick skim over them [here](https://dev.mysql.com/doc/refman/8.4/en/built-in-function-reference.html). Below is a table of some common built-in functions, however, there are plenty more that serve their own purposes. 
| **Function**      | **Description**                                                | **Example**                                               |
|-------------------|----------------------------------------------------------------|-----------------------------------------------------------|
| **`COUNT()`**      | Returns the count of non-null values in a column               | `SELECT COUNT(*) FROM Employees;`                         |
| **`SUM()`**        | Adds up the values in a numeric column                         | `SELECT SUM(Employed) FROM Employees;`                      |
| **`AVG()`**        | Calculates the average of a numeric column                     | `SELECT AVG(Pay) FROM Employees;`                      |
| **`MIN()`**        | Returns the minimum value in a column                          | `SELECT MIN(Pay) FROM Employees;`                      |
| **`MAX()`**        | Returns the maximum value in a column                          | `SELECT MAX(Pay) FROM Employees;`                      |
| **`LENGTH()`**     | Returns the length of a string (in characters)                 | `SELECT LENGTH(LastName) FROM Employees;`                     |
| **`CONCAT()`**     | Concatenates two or more strings                              | `SELECT CONCAT(FirstName, ' ', LastName) FROM Employees;` |
| **`LOWER()`**      | Converts a string to lowercase                                | `SELECT LOWER(Name) FROM Employees;`                      |
| **`UPPER()`**      | Converts a string to uppercase                                | `SELECT UPPER(Name) FROM Employees;`                      |
| **`SUBSTRING()`**  | Extracts a substring from a string                            | `SELECT SUBSTRING(Name, 1, 3) FROM Employees;`            |
| **`NOW()`**        | Returns the current date and time                             | `SELECT NOW();`                                           |
| **`CURDATE()`**    | Returns the current date                                      | `SELECT CURDATE();`                                       |
| **`DATE_FORMAT()`**| Formats a date according to a specified format                | `SELECT DATE_FORMAT(NOW(), '%Y-%m-%d');`                  |
| **`DATEDIFF()`**   | Returns the difference in days between two dates              | `SELECT DATEDIFF('2024-12-31', CURDATE());`               |
| **`IFNULL()`**     | Returns a specified value if the expression is `NULL`          | `SELECT IFNULL(Pay, 0) FROM Employees;`                |
| **`COALESCE()`**   | Returns the first non-null value in a list of expressions      | `SELECT COALESCE(Bonus, Pay, 0) FROM Employees;`       |
| **`ROUND()`**      | Rounds a numeric value to the nearest integer or decimal place | `SELECT ROUND(Pay, 2) FROM Employees;`                 |
| **`FLOOR()`**      | Returns the largest integer less than or equal to a number     | `SELECT FLOOR(Pay) FROM Employees;`                    |
| **`CEIL()`**       | Returns the smallest integer greater than or equal to a number | `SELECT CEIL(Pay) FROM Employees;`                     |
| **`RAND()`**       | Returns a random floating-point number between 0 and 1         | `SELECT RAND();`                                          |
| **`INSTR()`**      | Returns the position of the first occurrence of a substring    | `SELECT INSTR(Name, 'John') FROM Employees;`              |
| **`REPLACE()`**    | Replaces occurrences of a substring with another substring     | `SELECT REPLACE(FirstName, 'John', 'Jon') FROM Employees;`     |

A function that could help our business would be AVG() so we can find the average gross sale. We would do this as:
~~~~sql
SELECT AVG(GrossSale) FROM Sales;
~~~~
Now we know the average sale without manually adding and dividing all the entries ourselves. The column name "AVG(GrossSale)" isn't very intuitive so we'll use an alias:
~~~~sql
SELECT AVG(GrossSale) AS Average FROM Sales;
~~~~
An alias was mentioned earlier, BOOLEAN is an alias for TINYINT(1), which means it's just given a temporary name to make readability or queries easier. Another use for this would be returning the full names of employees in a single column:
~~~~sql
SELECT CONCAT(FirstName, ' ', LastName) AS Full_Name FROM Employees;
~~~~

MySQL allows you to create your own functions too if there's a very specific action you want to take. If you're interested in creating functions, which differ from procedures, there's a very informative and quick 3-minute video [here](https://www.youtube.com/watch?v=j73M7OIkEcY).

## Stored Procedures

Procedures, like functions, are meant to take the place of large chunks of code and streamline tasks. 
| **Aspect**          | **Procedure**                                               | **Function**                                                 |
|---------------------|-------------------------------------------------------------|--------------------------------------------------------------|
| **Purpose**         | Used to perform actions, such as modifying data or executing a series of operations. | Typically used to compute and return a single value or result based on inputs. |
| **Return Value**    | Does not need to return a value. Can return multiple values using `OUT` parameters. | Must return a single value using the `RETURN` statement. |
| **Invocation**      | Called using `CALL` or `EXECUTE` in SQL. Example: `CALL procedure_name();` | Called like a regular function in SQL. Example: `SELECT function_name();` |
| **Usage in Queries**| Cannot be directly used in SQL queries (e.g., `SELECT`, `WHERE`). | Can be used directly in SQL queries like `SELECT`, `WHERE`, etc. |
| **Side Effects**    | Can perform actions that modify the database (such as `INSERT`, `UPDATE`, `DELETE`). | Cannot modify the database. It's designed to compute and return values without side effects. |
| **Parameters**      | Supports `IN`, `OUT`, and `INOUT` parameters, allowing it to accept input and output multiple values. | Only supports `IN` parameters (input values) and must return a single value. |
| **Transaction Control** | Can contain and control transactions (i.e., `COMMIT`, `ROLLBACK`). | Cannot contain transaction control statements like `COMMIT` or `ROLLBACK`. |
| **Use Case**        | Use when you need to perform complex operations, possibly involving multiple steps or queries. | Use when you need to perform calculations or return a derived value in a query. |

Let's create a procedure to get our employees' full name (what we used above):
~~~~sql
DELIMITER //
CREATE PROCEDURE get_employees()
BEGIN
SELECT CONCAT(FirstName, ' ', LastName) AS Full_Name FROM Employees;
END //
DELIMITER ;
~~~~
The delimiter is how MySQL knows where the end of the command is, so when we create a new procedure we change our delimiter to something that won't be found in our code block, in this case "//". At the end of the code block we changed the delimiter back to ';'. Now when we call the function it should return the first and last names of all employees.
~~~~sql
CALL get_employees();
~~~~

For our projects, we may end up creating procedures with a little more complexity. For instance, while working on a better bus app there was a procedure that took the user's coordinates, found the distance to every stop, and then returned the 'n' closest stops. It looked like:
~~~~sql
CREATE PROCEDURE `FinalCalculate`(user_lat DOUBLE, user_lon DOUBLE, n INT)
BEGIN
    SELECT stopid, latitude, longitude,
    6371 * 2 * ASIN(
        SQRT(
            SIN(RADIANS((user_lat - latitude) / 2)) * SIN(RADIANS((user_lat - latitude) / 2)) +
            COS(RADIANS(user_lat)) * COS(RADIANS(latitude)) *
            SIN(RADIANS((user_lon - longitude) / 2)) * SIN(RADIANS((user_lon - longitude) / 2))
        )
    ) AS distance
    FROM ospdb.stopinfo
    ORDER BY distance
    LIMIT n;
END
~~~~
