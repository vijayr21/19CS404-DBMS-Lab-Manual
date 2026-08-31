# Experiment 10: PL/SQL – Triggers

## AIM
To write and execute PL/SQL trigger programs for automating actions in response to specific table events like INSERT, UPDATE, or DELETE.

---

## THEORY

A **trigger** is a stored PL/SQL block that is automatically executed or fired when a specified event occurs on a table or view. Triggers can be used for enforcing business rules, auditing changes, or automatic updates.

### Types of Triggers:
- **Before Trigger**: Executes before the operation (INSERT, UPDATE, DELETE).
- **After Trigger**: Executes after the operation.
- **Row-level Trigger**: Executes for each affected row.
- **Statement-level Trigger**: Executes once for the triggering statement.

**Basic Syntax:**
```sql
CREATE OR REPLACE TRIGGER trigger_name
BEFORE|AFTER INSERT|UPDATE|DELETE ON table_name
[FOR EACH ROW]
BEGIN
   -- trigger logic
END;
```

## 1. Write a trigger to log every insertion into a table.
**Steps:**
- Create two tables: `employees` (for storing data) and `employee_log` (for logging the inserts).
- Write an **AFTER INSERT** trigger on the `employees` table to log the new data into the `employee_log` table.

### PROGRAM
```
SET SERVEROUTPUT ON;

-- 1. Create employees table
CREATE TABLE employees_log_test (
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    salary NUMBER
);

-- 2. Create employee_log table
CREATE TABLE employee_log (
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    salary NUMBER,
    log_date DATE
);

-- 3. Create AFTER INSERT trigger
CREATE OR REPLACE TRIGGER trg_employee_insert
AFTER INSERT ON employees_log_test
FOR EACH ROW
BEGIN
    INSERT INTO employee_log
    VALUES (
        :NEW.emp_id,
        :NEW.emp_name,
        :NEW.salary,
        SYSDATE
    );
END;
/

-- 4. Insert employee record
INSERT INTO employees_log_test
VALUES (101, 'Akshaya', 5000);

COMMIT;

-- 5. Display employee table
SELECT * FROM employees_log_test;

-- 6. Display employee log
SELECT * FROM employee_log;
```

**Expected Output:**
- A new entry is added to the `employee_log` table each time a new record is inserted into the `employees` table.
<img width="946" height="249" alt="Screenshot 2026-08-24 092512" src="https://github.com/user-attachments/assets/4128960a-fa1f-434d-8fc0-b71ae54798b0" />

---

## 2. Write a trigger to prevent deletion of records from a sensitive table.
**Steps:**
- Write a **BEFORE DELETE** trigger on the `sensitive_data` table.
- Use `RAISE_APPLICATION_ERROR` to prevent deletion and issue a custom error message.

### PROGRAM
```
SET SERVEROUTPUT ON;

CREATE TABLE sensitive_data (
    id NUMBER,
    data VARCHAR2(100)
);

INSERT INTO sensitive_data VALUES (1, 'Confidential Data');
COMMIT;

CREATE OR REPLACE TRIGGER trg_prevent_delete
BEFORE DELETE ON sensitive_data
FOR EACH ROW
BEGIN
    RAISE_APPLICATION_ERROR(
        -20001,
        'ERROR: Deletion not allowed on this table.'
    );
END;
/

-- Test the trigger
DELETE FROM sensitive_data;
```

**Expected Output:**
- If an attempt is made to delete a record from `sensitive_data`, an error message is raised, e.g., `ERROR: Deletion not allowed on this table.`
<img width="729" height="255" alt="Screenshot 2026-08-24 092642" src="https://github.com/user-attachments/assets/da7d8433-324b-43a7-b7c1-949ef6312e81" />

---

## 3. Write a trigger to automatically update a `last_modified` timestamp.
**Steps:**
- Add a `last_modified` column to the `products` table.
- Write a **BEFORE UPDATE** trigger on the `products` table to set the `last_modified` column to the current timestamp whenever an update occurs.

### PROGRAM
```
SET SERVEROUTPUT ON;

-- 1. Create products table
CREATE TABLE products (
    product_id NUMBER,
    product_name VARCHAR2(50),
    price NUMBER
);

-- 2. Add last_modified column
ALTER TABLE products
ADD last_modified TIMESTAMP;

-- 3. Insert sample product
INSERT INTO products
VALUES (1, 'Laptop', 50000, SYSTIMESTAMP);

COMMIT;

-- 4. Create BEFORE UPDATE trigger
CREATE OR REPLACE TRIGGER trg_product_update
BEFORE UPDATE ON products
FOR EACH ROW
BEGIN
    :NEW.last_modified := SYSTIMESTAMP;
END;
/

-- 5. Update the product
UPDATE products
SET price = 55000
WHERE product_id = 1;

COMMIT;

-- 6. Display the result
SELECT * FROM products;
```

**Expected Output:**
- The `last_modified` column in the `products` table is updated automatically to the current date and time when any record is updated.
<img width="907" height="215" alt="Screenshot 2026-08-24 092806" src="https://github.com/user-attachments/assets/a68c86b1-6852-4b24-90a1-f18f4447e10f" />

---

## 4. Write a trigger to keep track of the number of updates made to a table.
**Steps:**
- Create an `audit_log` table with a counter column.
- Write an **AFTER UPDATE** trigger on the `customer_orders` table to increment the counter in the `audit_log` table every time a record is updated.

### PROGRAM
```
SET SERVEROUTPUT ON;

-- 1. Create customer_orders table
CREATE TABLE customer_orders (
    order_id NUMBER,
    customer_name VARCHAR2(50),
    amount NUMBER
);

-- 2. Create audit_log table
CREATE TABLE audit_log (
    table_name VARCHAR2(50),
    update_count NUMBER
);

-- 3. Insert initial value into audit_log
INSERT INTO audit_log
VALUES ('CUSTOMER_ORDERS', 0);

-- 4. Insert sample order
INSERT INTO customer_orders
VALUES (1, 'Akshaya', 5000);

COMMIT;

-- 5. Create AFTER UPDATE trigger
CREATE OR REPLACE TRIGGER trg_order_update
AFTER UPDATE ON customer_orders
FOR EACH ROW
BEGIN
    UPDATE audit_log
    SET update_count = update_count + 1
    WHERE table_name = 'CUSTOMER_ORDERS';
END;
/

-- 6. Update an order
UPDATE customer_orders
SET amount = 6000
WHERE order_id = 1;

COMMIT;

-- 7. Display the audit log
SELECT * FROM audit_log;
```

**Expected Output:**
- The `audit_log` table will maintain a count of how many updates have been made to the `customer_orders` table.
<img width="640" height="185" alt="Screenshot 2026-08-24 092930" src="https://github.com/user-attachments/assets/b5b1e781-6963-40f9-8b63-f38510d67ae2" />

---

## 5. Write a trigger that checks a condition before allowing insertion into a table.
**Steps:**
- Write a **BEFORE INSERT** trigger on the `employees` table to check if the inserted salary meets a specific condition (e.g., salary must be greater than 3000).
- If the condition is not met, raise an error to prevent the insert.

### PROGRAM
```
SET SERVEROUTPUT ON;

-- 1. Create employees table
CREATE TABLE employees_salary (
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    salary NUMBER
);

-- 2. Create BEFORE INSERT trigger
CREATE OR REPLACE TRIGGER trg_check_salary
BEFORE INSERT ON employees_salary
FOR EACH ROW
BEGIN
    IF :NEW.salary < 3000 THEN
        RAISE_APPLICATION_ERROR(
            -20001,
            'ERROR: Salary below minimum threshold.'
        );
    END IF;
END;
/

-- 3. Insert a valid employee
INSERT INTO employees_salary
VALUES (101, 'Akshaya', 5000);

COMMIT;

-- 4. Display valid employee
SELECT * FROM employees_salary;

-- 5. Test invalid salary
INSERT INTO employees_salary
VALUES (102, 'Priya', 2500);
```
**Expected Output:**
- If the inserted salary in the `employees` table is below the condition (e.g., salary < 3000), the insert operation is blocked, and an error message is raised, such as: `ERROR: Salary below minimum threshold.`
<img width="783" height="245" alt="Screenshot 2026-08-24 093056" src="https://github.com/user-attachments/assets/f0402034-44bc-4426-a8e6-9785370f495a" />

## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.
