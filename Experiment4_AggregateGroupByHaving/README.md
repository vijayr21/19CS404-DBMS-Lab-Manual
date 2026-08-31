# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
How many patients are covered by each insurance company?

Sample table:Insurance Table

name               type
-----------------  ----------
InsuranceID        INTEGER
PatientID          INTEGER
InsuranceCompany   TEXT
PolicyNumber       TEXT
PolicyHolder       TEXT
ValidityPeriod     TEXT

```sql
SELECT InsuranceCompany, count(PatientID) as TotalPatients from Insurance group by InsuranceCompany;
```

**Output:**

<img width="972" height="741" alt="image" src="https://github.com/user-attachments/assets/e29fc002-26d5-49a2-a923-b657196f871f" />


**Question 2**
---
<img width="1224" height="757" alt="image" src="https://github.com/user-attachments/assets/56ccad1f-534d-4e39-ba4f-2790d1ad2444" />


```sql
select DoctorID, count(PrescriptionID) as TotalPrescriptions from Prescriptions group by DoctorID;
```

**Output:**

<img width="954" height="761" alt="image" src="https://github.com/user-attachments/assets/2eea3786-4534-464e-996e-a7c1a5aabe16" />


**Question 3**
---
How many patients have insurance coverage valid in each year?

Sample table:Insurance Table

name               type
-----------------  ----------
InsuranceID        INTEGER
PatientID          INTEGER
InsuranceCompany   TEXT
PolicyNumber       TEXT
PolicyHolder       TEXT
ValidityPeriod     TEXT

```sql
select SUBSTR(ValidityPeriod,1,4) as ValidityYear,count(PatientID) as TotalPatients from Insurance group by SUBSTR(ValidityPeriod,1,4) order by ValidityYear;
```

**Output:**

<img width="855" height="568" alt="image" src="https://github.com/user-attachments/assets/7c4447d8-2b31-40fb-9927-3f675112b544" />


**Question 4**
---
Write a SQL query to find the total amount of fruits with a unit type of 'LB'.

Note: Inventory attribute contains amount of fruits

Table: fruits

name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL

```sql
select SUM(inventory) as total from fruits where unit='LB';
```

**Output:**

<img width="621" height="476" alt="image" src="https://github.com/user-attachments/assets/e58521a0-1896-4d6f-bddb-f5167dae73ba" />


**Question 5**
---
Write a SQL query to find the total income of employees aged 40 or above.

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER

```sql
select SUM(income) as total_income from employee where age>=40;
```

**Output:**

<img width="584" height="476" alt="image" src="https://github.com/user-attachments/assets/89133897-cf85-410a-8d8b-6efb55d45030" />


**Question 6**
---
Write a SQL query to Calculate the average email length (in characters) for people who lives in Mumbai city

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT   
city        TEXT
email       TEXT
phone       INTEGER

```sql
select AVG(LENGTH(email)) as avg_email_length_below_30 from customer where city='Mumbai';
```

**Output:**

<img width="820" height="521" alt="image" src="https://github.com/user-attachments/assets/dc626181-4a4c-4517-94a0-dbecc8d3d48d" />


**Question 7**
---
<img width="1210" height="600" alt="image" src="https://github.com/user-attachments/assets/4170ae70-0b52-45b5-b270-b562c45f81ad" />


```sql
select count(*) as COUNT from customer where city<> 'Noida';
```

**Output:**

<img width="575" height="477" alt="image" src="https://github.com/user-attachments/assets/5edf7126-86c2-421f-8516-7a606fb02e13" />


**Question 8**
---
<img width="1205" height="622" alt="image" src="https://github.com/user-attachments/assets/e602e64b-02bb-4f9a-a2e8-19a9c65c496d" />


```sql
select age,MAX(income) from employee group by age having max(income)>2000000;
```

**Output:**

<img width="778" height="536" alt="image" src="https://github.com/user-attachments/assets/cfe53047-3f76-4783-9cb3-a931533350eb" />


**Question 9**
---
<img width="1167" height="677" alt="image" src="https://github.com/user-attachments/assets/67519377-1f5d-4aae-98e5-070f45bd72a1" />


```sql
select city,SUM(income) as Income from employee group by city having SUM(income)>200000;
```

**Output:**

<img width="801" height="723" alt="image" src="https://github.com/user-attachments/assets/4d8c3a3f-e7ed-4ce8-b3a1-e6217d038dc0" />


**Question 10**
---
<img width="1203" height="635" alt="image" src="https://github.com/user-attachments/assets/d591e0a1-e322-4ffc-81a0-1db009f7b02a" />


```sql
select occupation,AVG(workhour) from employee1 group by occupation having AVG(workhour) between 10 and 12;
```

**Output:**

<img width="875" height="578" alt="image" src="https://github.com/user-attachments/assets/0c5bc072-6226-4034-bd4e-ab619fe7bc4d" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
