# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
Write a SQL query to reduce the reorder level by 30% where cost price is more than 50 and quantity in stock is less than 100 in the products table.

Products Table 

name          type       
----------    ---------- 
product_id     INT PRIMARY KEY        
product_name   VARCHAR(10) 
category       VARCHAR(50) 
cost_price     DECIMAL(10) 
sell_price     DECIMAL(10) 
reorder_lvl    INT        
quantity       INT        
supplier_id    INT               

```sql
UPDATE products set reorder_lvl = reorder_lvl*0.7 where cost_price>50 and quantity<100;
```

**Output:**

<img width="1237" height="664" alt="image" src="https://github.com/user-attachments/assets/3e5df21d-e58b-4842-86f4-395253860a52" />
<img width="1255" height="641" alt="image" src="https://github.com/user-attachments/assets/5578953d-47c4-406e-be40-7edbce4f914f" />


**Question 2**
---
Write a SQL statement to Increase the salary by 500 and email as 'updated' for employees with job ID 'SA_REP' and commission percentage greater than 0.15

Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id

```sql
UPDATE Employees set salary=salary+500,email='updated' where job_id='SA_REP' and commission_pct>0.15;
```

**Output:**

<img width="1217" height="735" alt="image" src="https://github.com/user-attachments/assets/b1194657-d3a4-434a-9a8d-3b02efadaa48" />


**Question 3**
---
Write a SQL statement to Update the hire_date of employees in department 50 to 2024-01-24.

Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id

```sql
update Employees set hire_date ='2024-01-24' where department_id=50;
```

**Output:**

<img width="1234" height="449" alt="image" src="https://github.com/user-attachments/assets/e715f76e-d648-47d5-8237-a2c709ac8aad" />


**Question 4**
---
Write a SQL statement to change the email column of employees table with 'Unavailable' for all employees in employees table.

Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id

```sql
update Employees set email='Unavailable';
```

**Output:**

<img width="1217" height="637" alt="image" src="https://github.com/user-attachments/assets/8f2489ee-0716-44f5-a7f1-f9b397f04e4c" />


**Question 5**
---
Update the 'Selling_Price' to add 10% extra margin for all products supplied by the supplier with id 6.

PRODUCTS TABLE

name               type
-----------------  ---------------
product_id         INT
product_name       VARCHAR(100)
category           VARCHAR(50)
cost_price         DECIMAL(10,2)
sell_price         DECIMAL(10,2)
reorder_lvl        INT
quantity           INT
supplier_id        INT

```sql
update Products set sell_price=sell_price*110/100 where supplier_id=6;
```

**Output:**

<img width="1251" height="746" alt="image" src="https://github.com/user-attachments/assets/e6b5c8af-4c86-4d33-80c0-0b761eb08816" />
<img width="1182" height="734" alt="image" src="https://github.com/user-attachments/assets/74e63a24-9d74-4928-aeb5-a466b6cc527b" />


**Question 6**
---
Write a SQL query to Delete All Doctors with a NULL Specialization

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

```sql
delete from Doctors where specialization is NULL;
```

**Output:**

<img width="1247" height="631" alt="image" src="https://github.com/user-attachments/assets/2829226c-4367-484c-b0e4-ef5af8f8a3bf" />
<img width="1215" height="761" alt="image" src="https://github.com/user-attachments/assets/dd0fc173-5582-4e0c-b9ac-77675b05f01b" />


**Question 7**
---
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is exactly 2.

 
Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |

```sql
delete from customer where grade=2;
```

**Output:**

<img width="851" height="732" alt="image" src="https://github.com/user-attachments/assets/21113b19-e835-48cc-b0ba-b1bf74662998" />


**Question 8**
---
Write a SQL query to Delete All Doctors with a NULL Last Name

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

```sql
delete from Doctors where last_name is null;
```

**Output:**

<img width="1190" height="756" alt="image" src="https://github.com/user-attachments/assets/6342795f-2741-43a5-b42c-51cb63654b3d" />


**Question 9**
---
Write a SQL query to remove rows from the table 'customer' with the following condition -

1. 'cust_city' should begin with the letter 'L',

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |

```sql
delete from customer where cust_city like 'L%';
```

**Output:**

<img width="1193" height="726" alt="Screenshot 2026-08-29 191018" src="https://github.com/user-attachments/assets/ba0ce971-fdd3-48a1-8b50-296443798b2c" />
<img width="1226" height="701" alt="Screenshot 2026-08-29 191022" src="https://github.com/user-attachments/assets/f47ffad7-841a-435d-8e2d-45540b8c3dcf" />
<img width="1159" height="589" alt="Screenshot 2026-08-29 191042" src="https://github.com/user-attachments/assets/a2063089-4eaa-4b28-a6c7-4fc0baadbf49" />
<img width="1213" height="681" alt="Screenshot 2026-08-29 191048" src="https://github.com/user-attachments/assets/42eb00e5-b913-439b-9266-3c6b5931f23a" />


**Question 10**
---
Write a SQL query to Delete a Specific Surgery which was made on 28th Feb 2024.

Sample table: Surgeries

attributes: surgery_id, patient_id, surgeon_id, surgery_date


```sql
delete from Surgeries where surgery_date= '2024-02-28'
```

**Output:**

<img width="1231" height="550" alt="image" src="https://github.com/user-attachments/assets/ef31b51d-6369-4182-9e11-ebe86f0d5f72" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
