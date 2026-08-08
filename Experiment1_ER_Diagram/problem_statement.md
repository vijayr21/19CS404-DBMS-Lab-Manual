# VIJAY R (212223240178)
# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:

<img width="1202" height="762" alt="City Fitness Club Management drawio 1" src="https://github.com/user-attachments/assets/789d504f-7f57-4f39-8513-f0928a619c39" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|Member        |MemberID (PK), Name, Phone, Email |Gym members       |
|Trainer        |TrainerID (PK), Name, Specialization, Phone                    |Gym trainers       |
|Program        |ProgramID (PK), ProgramName, Description           |Fitness programs|
|Session         |SessionID (PK), SessionDate, ProgramID (FK)                    |Training sessions       |
|Payment        |PaymentID (PK), PaymentDate, Amount, PaymentMethod                    |Payment details |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|Member–Trainer|  1:N          |Mandatory for Member, Optional for Trainer           |Member assign trainer      |
|Program–Session  |  1:N          |Mandatory for Session, Optional for Program              |Program has session       |
|Member–Program  |   M:N          |Mandatory for Session, Optional for Program  |Member enrolls Program       |
|Member to Payment |   1:1        |Mandatory for Payment, Optional for Member          |Member makes payment         |

### Assumptions
- Each member has a unique MemberID.
- A member can enroll in multiple fitness programs.
- A trainer can handle multiple programs, and a program can have multiple trainers.
- Each training session belongs to only one fitness program.
- Payments are made only for enrolled programs.
---

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:

<img width="1416" height="802" alt="Screenshot 2026-07-26 225729" src="https://github.com/user-attachments/assets/73172707-3c83-474b-9455-0564b9ec3d05" />


### Entities and Attributes

| Entity  | Attributes (PK, FK)                                | Notes                            |
| ------- | -------------------------------------------------- | -------------------------------- |
| Member  | Member_ID (PK), Name, Phone                        | Library members                  |
| Book    | Book_ID (PK), Title, Category                      | Books available in the library   |
| Loan    | Loan_ID (PK), Book_ID (FK), Loan_Date, Return_Date | Book lending records             |
| Fine    | Fine_ID (PK), Loan_ID (FK), Amount                 | Fine for overdue book returns    |
| Event   | Event_ID (PK), Event_Name                          | Library events conducted         |
| Room    | Room_ID (PK), Room_Name                            | Rooms used for library events    |
| Speaker | Speaker_ID (PK), Speaker_Name                      | Speakers participating in events |

### Relationships and Constraints

| Relationship               | Cardinality | Participation  | Notes                                                                                         |
| -------------------------- | ----------- | -------------- | --------------------------------------------------------------------------------------------- |
| Member – Book (Borrows)    | M : N       | Partial        | A member can borrow multiple books, and a book can be borrowed by multiple members over time. |
| Book – Loan                | 1 : M       | Total on Loan  | Each loan is associated with exactly one book. A book can have many loan records.             |
| Loan – Fine (Generates)    | 1 : 0..1    | Partial        | A loan may or may not generate a fine. A fine belongs to only one loan.                       |
| Member – Event (Registers) | M : N       | Partial        | A member can register for multiple events, and an event can have many members.                |
| Room – Event (Hosts)       | 1 : M       | Total on Event | One room can host many events. Each event is hosted in one room.                              |
| Event – Speaker (Has)      | 1 : M       | Partial        | An event can have multiple speakers. Each speaker is assigned to one event.                   |

### Assumptions
- Each reader has a unique ReaderID.
- A reader can borrow multiple books.
- Every book is published by only one publisher.
- Each staff member has one unique login account.
- Only registered readers are allowed to borrow books.
---

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:

<img width="1192" height="757" alt="Screenshot 2026-07-26 230100" src="https://github.com/user-attachments/assets/5e70e565-50db-42e2-9412-d73bbfb8975a" />


### Entities and Attributes

| Entity      | Attributes (PK, FK)                                                                | Notes                                |
| ----------- | ---------------------------------------------------------------------------------- | ------------------------------------ |
| Customer    | Customer_ID (PK), Name                                                             | Customer details                     |
| Reservation | Reservation_ID (PK), Date, Guests, Customer_ID (FK), Table_ID (FK), Waiter_ID (FK) | Table reservations made by customers |
| Table       | Table_ID (PK), Capacity                                                            | Restaurant tables                    |
| Waiter      | Waiter_ID (PK), Name                                                               | Waiters serving customers            |
| Order       | Order_ID (PK), Order_Date, Reservation_ID (FK)                                     | Orders placed during a reservation   |
| Dish        | Dish_ID (PK), Dish_Name, Price, Category_ID (FK)                                   | Menu items served                    |
| Category    | Category_ID (PK), Category_Name                                                    | Dish categories                      |
| Bill        | Bill_ID (PK), Reservation_ID (FK), Total_Amount                                    | Final bill for a reservation         |
### Relationships and Constraints


| **Relationship**                    | **Cardinality** | **Participation**                             | **Notes**                                                                                   |
| ----------------------------------- | --------------- | --------------------------------------------- | ------------------------------------------------------------------------------------------- |
| **Customer  — Reservation**  | 1 : M           | Customer (mandatory), Reservation (mandatory) | A customer can make many reservations.                                                      |
| **Customer  — Bill**          | 1 : 1           | Both mandatory                                | One bill per customer per reservation.                                                      |
| **Reservation — Table**  | 1 : M           | Reservation (mandatory), Table (mandatory)    | One reservation uses exactly one table; a table can be used by many reservations over time. |
| **Reservation — Waiter** | 1 : M           | Reservation (mandatory), Waiter (optional)    | A reservation has one waiter; a waiter handles many reservations.                           |
| **Reservation — Order**       | 1 : M           | Reservation (mandatory), Order (optional)     | A reservation may place multiple orders.                                                    |
| **Order — Dish**          | M : M           | Optional for both                             | An order contains multiple dishes; a dish can appear in many orders.                        |
| **Dish — Category**         | M : 1           | Dish (mandatory), Category (mandatory)        | Each dish belongs to exactly one category.                                                  |
### Assumptions
- Each customer has a unique CustomerID.
- A customer can make multiple table reservations.
- Each reservation is assigned to only one table.
- A reservation can include multiple food orders.
- One bill is generated for each reservation
---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
