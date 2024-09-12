# What is SQL/MySQL?

SQL, often pronounced either "Sequel" or "Ess Que Ell", stands for Structured Query Language and is by far one of the most common and easier languages to learn. SQL acts as an international, standardized language to communicate with relational databases in order to create, edit, delete, and obtain information. Fortunately for us, this means once we learn SQL we'll be able to apply it to pretty much any database management system that accepts SQL. 

What is a relational database? A relational database consists of tables made up of columns and rows, like an Excel spreadsheet, where each row has a unique input with its own identifying information determined by its columns. These tables are *related* to each other through *keys*, which we'll get into more later. 

MySQL, often pronounced "My Ess Que Ell" or "My Sequel", is the Relational Database Management System(RDBMS) that we'll be using. We will be learning the basics in this article and I would recommend you to download MySQL and follow along. You can find the download [here](https://dev.mysql.com/downloads/installer/).  


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

The SELECT command is your best friend, chances are you'll be running it after every other command to check on your database and make sure your tables look good. In SQL you follow the **SELECT** command with an option to specify what and how many entries you want returned. A list of some of these options can be found below. Another thing to take note of is **FROM**. This keyword is followed by the table you want to pull information from, in our case we pulled from the Employees table.
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
***Quick PSA: Each table has ONE primary key, but the primary key can be made up of more than one column. If you're interested in learning more you can check it out [here](https://www.w3schools.com/mysql/mysql_primarykey.asp).***


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
