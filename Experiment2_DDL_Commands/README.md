# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
-- Insert a customer with CustomerID 301, Name Michael Jordan, Address 123 Maple St, City Chicago, and ZipCode 60616 into the Customers table.

For example:

Test	Result
SELECT * FROM Customers WHERE CustomerID = 301;
CustomerID  Name            Address       City        ZipCode
----------  --------------  ------------  ----------  ----------
301         Michael Jordan  123 Maple St  Chicago     60616

```sql
-- INSERT INTO Customers(CustomerID, Name,Address,City,ZipCode)
VALUES
(301,'Michael Jordan','123 Maple St','Chicago',60616)
```

**Output:**
<img width="585" height="132" alt="image" src="https://github.com/user-attachments/assets/953a5b68-9f0d-41c1-b012-c31c08f14a39" />



**Question 2**
---
-- Create a table named Reviews with the following columns:

ReviewID as INTEGER
ProductID as INTEGER
Rating as REAL
ReviewText as TEXT
For example:

Test	Result
pragma table_info('Reviews');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           ReviewID    INTEGER     0                       0
1           ProductID   INTEGER     0                       0
2           Rating      REAL        0                       0
3           ReviewText  TEXT        0                       0


```sql
-- CREATE TABLE Reviews(
ReviewID INTEGER,
ProductID INTEGER,
Rating REAL,
ReviewText TEXT
);
```

**Output:**
<img width="602" height="267" alt="image" src="https://github.com/user-attachments/assets/0b352f85-5d77-415e-baca-90b2105eb340" />



**Question 3**
---
--Create a table named ProjectAssignments with the following constraints:
AssignmentID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
AssignmentDate as DATE should be NOT NULL.
For example:

Test	Result
INSERT INTO ProjectAssignments (AssignmentID, EmployeeID, ProjectID, AssignmentDate) VALUES (2, 99, 1, '2024-01-03');
Error: FOREIGN KEY constraint failed


```sql
-- CREATE TABLE ProjectAssignments(
AssignmentID INTEGER PRIMARY KEY,
EmployeeID INTEGER,
ProjectID INTEGER,
AssignmentDate DATE NOT NULL,
FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID),
FOREIGN KEY (ProjectID) REFERENCES Projects(ProjectID)
)
```

**Output:**

<img width="581" height="178" alt="image" src="https://github.com/user-attachments/assets/03c12fef-d6df-446d-a9f2-21875ac30cf8" />


**Question 4**
---
-- Create a table named Products with the following constraints:

ProductID should be the primary key.
ProductName should be NOT NULL.
Price is of real datatype and should be greater than 0.
Stock is of integer datatype and should be greater than or equal to 0.
For example:

Test	Result
INSERT INTO Products
VALUES (1, NULL,0,5);
Error: NOT NULL constraint failed: Products.ProductName


```sql
-- CREATE TABLE Products(
ProductID INTEGER PRIMARY KEY,
ProductName NOT NULL,
Price REAL CHECK (Price>0),
Stock INTEGER CHECK (Stock>=0)
);
```

**Output:**

<img width="582" height="173" alt="image" src="https://github.com/user-attachments/assets/ba3de46b-bf49-429d-9ac3-d37c23331d29" />


**Question 5**
---
-- Write a SQL query to Add a new column Mobilenumber as number in the Student_details table.

Sample table: Student_details

 cid              name             type             notnu  dflt_value  pk
---------------  ---------------  ---------------  -----  ----------  ----------
0                RollNo           int              0                  1
1                Name             VARCHAR(100)     1                  0
2                Gender           TEXT             1                  0
3                Subject          VARCHAR(30)      0                  0
4                MARKS            INT (3)          0                  0
For example:

Test	Result
pragma table_info('Student_details');
cid    name             type             notnu  dflt_value  pk
-----  ---------------  ---------------  -----  ----------  ----------
0      RollNo           int              0                  1
1      Name             VARCHAR(100)     1                  0
2      Gender           TEXT             1                  0
3      Subject          VARCHAR(30)      0                  0
4      MARKS            INT (3)          0                  0
5      Mobilenumber     number           0                  0

```sql
-- alter table Student_details
add column Mobilenumber number

```

**Output:**

<img width="585" height="233" alt="image" src="https://github.com/user-attachments/assets/6d4120b7-8c76-4f91-af83-90a44dfe8e2a" />


**Question 6**
---
--Create a new table named contacts with the following specifications:
contact_id as INTEGER and primary key.
first_name as TEXT and not NULL.
last_name as TEXT and not NULL.
email as TEXT.
phone as TEXT and not NULL with a check constraint to ensure the length of phone is at least 10 characters.
For example:

Test	Result
INSERT INTO contacts (contact_id, first_name, last_name, email, phone) VALUES (1, 'John', 'Doe', 'john.doe@example.com', '1234567890');
SELECT * FROM contacts;

```sql
-- CREATE TABLE contacts(
contact_id INTEGER PRIMARY KEY,
first_name TEXT NOT NULL,
last_name TEXT NOT NULL,
email TEXT,
phone TEXT NOT NULL CHECK (length(phone)=10)
);
```

**Output:**
<img width="602" height="197" alt="image" src="https://github.com/user-attachments/assets/0fcf1fce-acba-4053-ba18-d3ebab2a418c" />



**Question 7**
---
-- In the Cusomers table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

CustomerID  Name          Address      City        ZipCode
----------  ------------  ----------   ----------  ----------
306         Diana Prince  Themyscira
307         Bruce Wayne   Wayne Manor  Gotham      10007
308         Peter Parker  Queens                   11375
 

For example:

Test	Result
SELECT * FROM Customers;
CustomerID  Name          Address     City        ZipCode
----------  ------------  ----------  ----------  ----------
306         Diana Prince  Themyscira
307         Bruce Wayne   Wayne Mano  Gotham      10007
308         Peter Parker  Queens                  11375


```sql
--INSERT INTO Customers(CustomerID,Name,Address,City,Zipcode)
VALUES
(306,'Diana Prince','Themyscira',NULL,NULL),
(307,'Bruce Wayne','Wayne Manor','Gotham',10007),
(308,'Peter Parker','Queens',NULL,11375);
```

**Output:**

<img width="592" height="175" alt="image" src="https://github.com/user-attachments/assets/3839b124-59f3-4bea-9629-19fe48b9b8ee" />

**Question 8**
---Write a SQL query to Add a new column named "discount" with the data type DECIMAL(5,2) to the "customer" table.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
 

For example:

Test	Result
pragma table_info('customer');
cid         name         type                               notnull     dflt_value  pk
----------  -----------  ---------------------------------  ----------  ----------  ----------
0           customer_id  integer primarykey auto increment  0                       0
1           cust_name    varchar2(30)                       0                       0
2           city         varchar(30)                        0                       0
3           grade        number                             0                       0
4           salesman_id  number                             0                       0
5           discount     DECIMAL(5,2)                       0                       0

-- 

```sql
--alter table customer
add column discount DECIMAL(5,2); 
```

**Output:**

<img width="577" height="203" alt="image" src="https://github.com/user-attachments/assets/5d70cf82-6266-437d-9423-9181695c9007" />


**Question 9**
---
--Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should cascade updates and deletes.
item_desc and rate should not accept NULL.
For example:

Test	Result
INSERT INTO item VALUES("ITM5","Charlie Gold",700,"COM4");
UPDATE company SET com_id='COM5' WHERE com_id='COM4';
SELECT * FROM item;
item_id     item_desc     rate        icom_id
----------  ------------  ----------  ----------
ITM5        Charlie Gold  700         COM5

```sql
-- CREATE TABLE item(
item_id TEXT PRIMARY KEY,
item_desc TEXT,
rate INTEGER,
icom_id TEXT CHECK (length(icom_id=4)),
FOREIGN KEY (icom_id) REFERENCES company(com_id)
ON UPDATE CASCADE
ON DELETE CASCADE
);
```

**Output:**


<img width="602" height="188" alt="image" src="https://github.com/user-attachments/assets/0069ed89-d857-4c4e-a0f1-6a305abb2f0e" />


**Question 10**
---
-- Insert all employees from Former_employees into Employee

Table attributes are EmployeeID, Name, Department, Salary

For example:

Test	Result
select * from Employee;
EmployeeID  Name        Department  Salary
----------  ----------  ----------  ----------
201         John Doe    HR          50000
202         Jane Smith  Engineerin  75000
203         Emily Davi  Marketing   60000

```sql
-- INSERT INTO Employee(EmployeeID, Name, Department, Salary)
SELECT EmployeeID, Name, Department, Salary
FROM Former_employees;
```

**Output:**


<img width="596" height="157" alt="image" src="https://github.com/user-attachments/assets/8e68102e-01e7-47d6-9189-ccedeb1fc51a" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
