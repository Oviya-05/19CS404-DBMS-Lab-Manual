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
Create a table named Invoices with the following constraints:
- InvoiceID as INTEGER should be the primary key.
- InvoiceDate as DATE.
- Amount as REAL should be greater than 0.
- DueDate as DATE should be greater than the InvoiceDate.
- OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
![image](https://github.com/user-attachments/assets/169dfaa9-45e5-425a-b13c-1b2efab23c52)

```sql
CREATE TABLE Invoices (
    InvoiceID   INTEGER PRIMARY KEY,
    InvoiceDate DATE NOT NULL,
    Amount      REAL NOT NULL CHECK (Amount > 0),
    DueDate     DATE NOT NULL,
    OrderID     INTEGER NOT NULL,
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID),
    CHECK (DueDate > InvoiceDate)
);

```

**Output:**

![image](https://github.com/user-attachments/assets/9e5fe6b3-14e6-4f52-a0db-e3b72f1e01ad)


**Question 2**
---
Create a table named Employees with the following constraints:

- EmployeeID should be the primary key.
- FirstName and LastName should be NOT NULL.
- Email should be unique.
- Salary should be greater than 0.
- DepartmentID should be a foreign key referencing the Departments table.

  ![image](https://github.com/user-attachments/assets/47060038-14e9-45b2-877e-e81dc84f00e8)


```sql
CREATE TABLE Employees (
    EmployeeID   INTEGER PRIMARY KEY,
    FirstName    TEXT NOT NULL,
    LastName     TEXT NOT NULL,
    Email        TEXT UNIQUE NOT NULL,
    Salary       REAL NOT NULL CHECK (Salary > 0),
    DepartmentID INTEGER NOT NULL,
    FOREIGN KEY (DepartmentID) REFERENCES Departments(DepartmentID)
);

```

**Output:**

![image](https://github.com/user-attachments/assets/78d06100-05c1-4798-8d8c-130d7fb6a068)


**Question 3**
---
Insert all employees from Former_employees into Employee

Table attributes are EmployeeID, Name, Department, Salary

![image](https://github.com/user-attachments/assets/4dcc3073-e1a9-44d3-8a64-e6e9d6cd835f)


```sql
INSERT INTO Employee (EmployeeID, Name, Department, Salary)
SELECT EmployeeID, Name, Department, Salary
FROM Former_employees;

```

**Output:**
![image](https://github.com/user-attachments/assets/3b45b211-64d3-423f-81ef-dedafb494bb6)


**Question 4**
---
Create a table named Customers with the following columns:

- CustomerID as INTEGER
- Name as TEXT
- Email as TEXT
- JoinDate as DATETIME
  
![image](https://github.com/user-attachments/assets/ec14a0b3-3b4b-4e26-9087-06ed1704d3ce)

```sql
CREATE TABLE Customers (
    CustomerID INTEGER,
    Name       TEXT,
    Email      TEXT,
    JoinDate   DATETIME
);

```

**Output:**
![image](https://github.com/user-attachments/assets/54cbee44-7f72-45ea-a58c-57f018a7264e)



**Question 5**
Insert a student with RollNo 201, Name David Lee, Gender M, Subject Physics, and MARKS 92 into the Student_details table.
![image](https://github.com/user-attachments/assets/ab399473-0cf0-4ace-86fb-3e914335849a)

```sql
INSERT INTO Student_details (RollNo, Name, Gender, Subject, MARKS)
VALUES (201, 'David Lee', 'M', 'Physics', 92);

```

**Output:**
![image](https://github.com/user-attachments/assets/ecb0080c-009d-46a6-9d6b-cceeec8f0edf)


**Question 6**
---
Insert a new product with ProductID 101, Name Laptop, Category Electronics, Price 1500, and Stock 50 into the Products table.
![image](https://github.com/user-attachments/assets/778dd531-1bbd-4aba-ab19-0733057f16cd)

```sql
INSERT INTO Products (ProductID, Name, Category, Price, Stock)
VALUES (101, 'Laptop', 'Electronics', 1500, 50);

```

**Output:**

![image](https://github.com/user-attachments/assets/d8c02e27-053b-4245-b0c6-b73c13315718)


**Question 7**
---
Write an SQL query to add two new columns, designation and net_salary, to the table Companies. The designation column should have a data type of varchar(50), and the net_salary column should have a data type of number.

![image](https://github.com/user-attachments/assets/e52c1175-8218-4d58-9be5-c3b5f32896fc)


```sql
ALTER TABLE Companies ADD COLUMN designation varchar(50);
ALTER TABLE Companies ADD COLUMN net_salary number;

```

**Output:**

![image](https://github.com/user-attachments/assets/9fa81ae0-8cec-4adb-8ab9-73d811145f3c)


**Question 8**
---
Create a table named Products with the following constraints:
- ProductID as INTEGER should be the primary key.
- ProductName as TEXT should be unique and not NULL.
- Price as REAL should be greater than 0.
- StockQuantity as INTEGER should be non-negative.

![image](https://github.com/user-attachments/assets/5cce0853-b56a-4d4f-9ae0-eb8a7402b13f)

```sql
CREATE TABLE Products (
    ProductID      INTEGER PRIMARY KEY,
    ProductName    TEXT NOT NULL UNIQUE,
    Price          REAL NOT NULL CHECK (Price > 0),
    StockQuantity  INTEGER NOT NULL CHECK (StockQuantity >= 0)
);

```

**Output:**

![image](https://github.com/user-attachments/assets/9f5fca5f-e1ce-44b7-a71f-b4b394593ede)

**Question 9**
---
Create a table named Products with the following constraints:

- ProductID should be the primary key.
- ProductName should be NOT NULL.
- Price is of real datatype and should be greater than 0.
- Stock is of integer datatype and should be greater than or equal to 0.

![image](https://github.com/user-attachments/assets/85405fcb-b364-4ddb-8b95-cb2642d854ff)


```sql
CREATE TABLE Products (
    ProductID    INTEGER PRIMARY KEY,
    ProductName  TEXT NOT NULL,
    Price        REAL NOT NULL CHECK (Price > 0),
    Stock        INTEGER NOT NULL CHECK (Stock >= 0)
);

```

**Output:**

![image](https://github.com/user-attachments/assets/eeeca637-aca5-4eb4-a0c4-9c5efad8b158)


**Question 10**
---
Write a SQL query to Add a new ParentsNumber column  as number and Adhar_Number as Number in the Student_details table.

![image](https://github.com/user-attachments/assets/a61e0b8e-24bc-4c41-a6b4-0310996a9493)

```sql
ALTER TABLE Student_details ADD COLUMN ParentsNumber number;
ALTER TABLE Student_details ADD COLUMN Adhar_Number number;

```

**Output:**

![image](https://github.com/user-attachments/assets/0bd5cc08-ac6a-4510-8759-ef10b2884dda)



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
