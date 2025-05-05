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

![image](https://github.com/user-attachments/assets/bf8ff99f-71eb-4d40-84b4-e06a945d3b2a)

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

![image](https://github.com/user-attachments/assets/e4e775f2-63a0-4866-b520-0b0294f33519)

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

![image](https://github.com/user-attachments/assets/67ef02af-836e-4ebc-bcfa-a02549596343)
![image](https://github.com/user-attachments/assets/f5b655a0-7e24-4cc2-8676-36f41db5e05c)


```sql
SELECT LOWER(ename) AS EmpName
FROM emp;
```

**Output:**


![image](https://github.com/user-attachments/assets/84ee14a7-e09d-4830-9db7-301fc4aa613b)


**Question 7**
---
Write a SQL query to find all employees who were hired in the year 2022 from emp table.
![image](https://github.com/user-attachments/assets/948eb8b7-c0d8-41cb-bac4-f6501939736c)

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
![image](https://github.com/user-attachments/assets/459bcf6b-2a02-4a09-ae98-bf6ef3bdd82f)


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

 

![image](https://github.com/user-attachments/assets/0f84f1ce-55c9-4c07-a9bc-a24fc68834c5)

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
![image](https://github.com/user-attachments/assets/afcc8253-fb5e-4a5d-ac41-97a65e4e0102)


```sql
UPDATE Employees
SET salary = salary * 2
WHERE department_id = 20
  AND job_id LIKE '%MAN';

```

**Output:**


![image](https://github.com/user-attachments/assets/1fd58dca-a973-4dff-bbfe-28020aec6d1a)


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
