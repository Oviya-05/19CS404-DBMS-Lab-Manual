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
write a SQL query to create a union of two queries that shows the customer id, cities, and ratings of all customers. Those with a rating of 300 or greater will have the words 'High Rating', while the others will have the words 'Low Rating'.

customer table

cid           name          type   notnull       dflt_value  pk
------------  ------------  -----  ------------  ----------  ----------
0             customer_id   int    0                         0
1             cust_name     text   0                         0
2             city          text   0                         0
3             grade         int    0                         0
4             salesman_id   int    0                         0

![image](https://github.com/user-attachments/assets/0b24b967-3272-42fe-bca6-571ffcb7f486)


```sql
SELECT customer_id, city, grade, 'High Rating' AS Rating
FROM customer
WHERE grade >= 300

UNION

SELECT customer_id, city, grade, 'Low Rating' AS Rating
FROM customer
WHERE grade < 300;

```

**Output:**

![image](https://github.com/user-attachments/assets/890e01ea-44df-47a9-b048-ce3d900838fe)


**Question 2**
---
Write a SQL query to Delete customers from 'customer' table where 'WORKING_AREA' is 'New York'

![image](https://github.com/user-attachments/assets/9456a3c4-b397-42c2-b107-aaeb08ec6a71)


```sql
DELETE FROM customer
WHERE WORKING_AREA = 'New York';

```

**Output:**

![image](https://github.com/user-attachments/assets/657703e0-0d8e-4d9a-9b48-cc0d4dda780c)


**Question 3**
---
Write a SQL query to Delete customers with 'GRADE' 3 and whose 'CUST_NAME' contains the substring 'BBB', and 'PAYMENT_AMT' is greater than 2000

Sample table: Customer

![image](https://github.com/user-attachments/assets/d8f2a8f8-b830-431a-94b1-efba85b92818)


```sql
DELETE FROM Customer
WHERE GRADE = 3
  AND CUST_NAME LIKE '%BBB%'
  AND PAYMENT_AMT > 2000;

```

**Output:**


![image](https://github.com/user-attachments/assets/ae6a350d-e765-441f-892c-02064ab4b6cb)


**Question 4**
---
Write a SQL statement to Update the grade of all customers in Chennai city as  5. 

Customer table (customer_id,cust_name,city,grade,salesman_id)

```sql
UPDATE customer
SET grade = 5
WHERE city = 'Chennai';

```

**Output:**


![image](https://github.com/user-attachments/assets/d15799c6-1ee8-4493-a639-e46c423bb9ca)


**Question 5**
---
Write a SQL query to calculate the discount amount for each product. Return product_id, original_price, discount_percentage, and discount_amount.

Sample table: Products

product_id | original_price | discount_percentage
------------+----------------+---------------------
101 | 50.00 | 0.10
102 | 75.00 | 0.15
103 | 100.00 | 0.20

![image](https://github.com/user-attachments/assets/6fc16649-b558-4f32-b0ee-da66d64afc98)


```sql
-- SELECT 
  product_id,
  original_price,
  discount_percentage,
  original_price * discount_percentage AS discount_amount
FROM Products;

```

**Output:**

![image](https://github.com/user-attachments/assets/6dead82d-d50c-4b57-ade9-22b331506b2c)


**Question 6**
---
Write a SQL query to retrieve all employee names in lower case. 

Table name: emp

name        type
----------  ----------
empno       INT
ename       VARCHAR(100)
job         VARCHAR(50)
mgr         INT
hiredate    DATE
sal         DECIMAL(10,2)
comm        DECIMAL(10,2)
deptno      INT

![image](https://github.com/user-attachments/assets/67ef02af-836e-4ebc-bcfa-a02549596343)


```sql
SELECT LOWER(ename) AS EmpName
FROM emp;
```

**Output:**


![image](https://github.com/user-attachments/assets/84ee14a7-e09d-4830-9db7-301fc4aa613b)


**Question 7**
---
Write a SQL query to find all employees who were hired in the year 2022 from emp table.

cid         name        type        
----------  ----------  ---------- 
0           empno       INT         
1           ename       VARCHAR(100)
2           job         VARCHAR(50)
3           mgr         INT        
4           hiredate    DATE        
5           sal         DECIMAL(10,2)  
6           comm        DECIMAL(10,2)  
7           deptno      INT         
For example:

![image](https://github.com/user-attachments/assets/d9a30324-7b27-4678-8c45-afbfa62beee9)

```sql
SELECT *
FROM emp
WHERE strftime('%Y', hiredate) = '2022';

```

**Output:**

![image](https://github.com/user-attachments/assets/2270ac24-37d4-4677-a975-70a88e99e80d)


**Question 8**
---
Write a SQL query to retrieve the details of all customers whose ID belongs to any of the values 3007, 3008 or 3009. Return customer_id, cust_name, city, grade, and salesman_id.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
For example:

![image](https://github.com/user-attachments/assets/9bf49b7f-baad-4344-b898-5bca7437086d)


```sql
SELECT customer_id, cust_name, city, grade, salesman_id
FROM customer
WHERE customer_id IN (3007, 3008, 3009);

```

**Output:**

![image](https://github.com/user-attachments/assets/fd33ef6d-6f2d-440c-83ff-53ec31dce8ee)


**Question 9**
---
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is less than 2.

 
Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |

![image](https://github.com/user-attachments/assets/70b5d962-342c-492c-8bd4-083e953e3339)

```sql
DELETE FROM Customer
WHERE GRADE < 2;

```

**Output:**


![image](https://github.com/user-attachments/assets/f63edf1d-6f5a-4857-9f0b-90fb897964ad)


**Question 10**
---
Write a SQL statement to Double the salary for employees in department 20 who have a job_id ending with 'MAN'


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

![image](https://github.com/user-attachments/assets/3e9dbaad-9bb9-483e-920e-3b2867a906a4)

```

**Output:**


![image](https://github.com/user-attachments/assets/1fd58dca-a973-4dff-bbfe-28020aec6d1a)


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
