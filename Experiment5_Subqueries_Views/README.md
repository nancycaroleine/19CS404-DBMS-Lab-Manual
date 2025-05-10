# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
-- Write a SQL query to Identify customers whose city is different from the city of the customer with the highest ID

SAMPLE TABLE: customer

name             type

id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER

For example:
Result

id     name             city             email            phone

6      Aarti Desai      Pune             aarti@gmail.com  890123456
7      Vivek Sharma     Chandigarh       vivek@gmail.com  980154021
8      Nisha Patel      Noida            nisha@gmail.com  901234567
9      Rajesh Singh     Hyderabad        rajesh@gmail.co  917654301

```sql
--
select * from customer 
where city<> ( select city from customer where id = (select max(id) from customer));
```

**Output:**

![Screenshot (230)](https://github.com/user-attachments/assets/095c6398-738e-4ad2-8fc3-29d75b1ee851)


**Question 2**
---
-- Write a SQL query to Retrieve the medications with dosages equal to the lowest dosage

Table Name: Medications (attributes: medication_id, medication_name, dosage)
![image (6)](https://github.com/user-attachments/assets/ffe30fcf-eec5-47f5-9b68-3d2ae00a9ff0)


For example:
Result

medic  medication_name  dosage

2      Ibuprofen        200mg


```sql
--
select * from Medications
where dosage = (select min(dosage) from Medications);
```

**Output:**

![Screenshot (231)](https://github.com/user-attachments/assets/192726f3-e416-41ef-8d2a-a6dc480210bf)


**Question 3**
---
-- From the following tables, write a SQL query to find those salespeople who earned the maximum commission. Return ord_no, purch_amt, ord_date, and salesman_id.

salesman table

name             type

salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

orders table

name             type
 
order_no         int
purch_amt        real
order_date       text
customer_id      int
salesman_id      int

 

For example:
Result

ord_no      purch_amt   ord_date    salesman_id

70002       65.26       2012-10-05  5001
70005       2400.6      2012-07-27  5001
70008       5760.0      2012-09-10  5001
70013       3045.6      2012-04-25  5001


```sql
--
select o.ord_no, o.purch_amt, o.ord_date, o.salesman_id
from orders o
join salesman s
on o.salesman_id = s.salesman_id
where s.commission = (select max(commission) from salesman);

```

**Output:**
![Screenshot (232)](https://github.com/user-attachments/assets/15a84b68-0f3e-4847-8d48-1d03dd0f65a4)


**Question 4**
---
-- Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY


1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000
 

For example:
Result

ID          NAME        AGE         ADDRESS     SALARY

2           Khilan      25          Delhi       1500


```sql
--
select * from CUSTOMERS
where ADDRESS ='Delhi';
```

**Output:**
![Screenshot (233)](https://github.com/user-attachments/assets/e660a96a-8c33-40a9-b9c2-0d263226838a)


**Question 5**
---
-- Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)
![image (3)](https://github.com/user-attachments/assets/bb0aa0ca-dae1-4a50-af61-54a6a3f8ea62)


For example:
Result

student_name     grade

Charlie          95
Emma             92
John             85


```sql
--
select student_name , grade from GRADES as g1
where grade =(select max(grade) from GRADES as g2 where g1.subject = g2.subject);
```

**Output:**

![Screenshot (234)](https://github.com/user-attachments/assets/c3d4085d-918e-4124-ae01-e8dccff60033)


**Question 6**
---
-- From the following tables write a SQL query to count the number of customers with grades above the average in New York City. Return grade and count.

customer table

name         type

customer_id  int
cust_name    text
city         text
grade        int
salesman_id  int

For example:
Result

grade       COUNT(*)

300         2


```sql
-- select grade, COUNT(*) from customer
   where grade>(select avg(grade) from customer where city ='New York')
   group by grade
```

**Output:**

![Screenshot (235)](https://github.com/user-attachments/assets/7a1a693c-556e-4c6c-8a6a-8ff661b423c2)


**Question 7**
---
-- From the following tables, write a SQL query to determine the commission of the salespeople in Paris. Return commission.

salesman table

name             type

salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

customer table

name         type

customer_id  int
cust_name    text
city         text
grade        int
salesman_id  int

For example:
Result

commission

0.14

```sql
-- 
select commission from salesman
where salesman_id in (select salesman_id from customer where city = 'Paris');
```

**Output:**


**Question 8**
---
-- Write a SQL query that retrieve all the columns from the table "Grades", where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)
![image (3)](https://github.com/user-attachments/assets/c578b019-40ce-47e2-b1bc-41b862ea0af5)


For example:
Result

student_id       student_name     subject          grade

3                Charlie          Math             95
5                Emma             Science          92
7                John             Social           85


```sql
--
select student_id , student_name , subject , grade from GRADES as g1
where grade = (select max(grade) from GRADES as g2 where g1.subject = g2.subject);
```

**Output:**

![Screenshot (237)](https://github.com/user-attachments/assets/0b368e96-911e-4f2e-b33c-8a9da7b1535d)


**Question 9**
---
-- Write a SQL query to Retrieve the names and cities of customers who have the same city as customers with IDs 3 and 7

SAMPLE TABLE: customer

name             type

id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER

For example:
Result

name   city

Neha   Bangalore
Rohit  Bangalore
Manoj  Bangalore
Vivek  Chandigarh


```sql
--
select name,city from customer
where city in (select city from customer where id in (3,7));
```

**Output:**

![Screenshot (238)](https://github.com/user-attachments/assets/cc638cb1-2a0b-40cb-b12d-5ef8a483bfaf)


**Question 10**
---
-- Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $1500.

Sample table: CUSTOMERS

ID          NAME        AGE          ADDRESS                   SALARY


1          Ramesh     32              Ahmedabad               2000

2          Khilan        25              Delhi                1500

3          Kaushik      23              Kota                  2000

4          Chaitali       25             Mumbai               6500

5          Hardik        27              Bhopal               8500

6          Komal         22              Hyderabad            4500

7           Muffy          24              Indore            10000
 

 
For example:
Result

ID          NAME        AGE         ADDRESS     SALARY

1           Ramesh      32          Ahmedabad   2000

3           Kaushik     23          Kota        2000

4           Chaitali    25          Mumbai      6500

5           Hardik      27          Bhopal      8500

6           Komal       22          Hyderabad   4500

7           Muffy       24          Indore      10000


```sql
-- select * from CUSTOMERS
   where salary > 1500;
```

**Output:**

![Screenshot (239)](https://github.com/user-attachments/assets/a92df883-d499-45b3-9526-5e9f5f01d0ab)

**SEB 4 GRADE SCREENSHOT**
![Screenshot (251)](https://github.com/user-attachments/assets/ecf5a667-f46b-4646-8990-88f2550fd5de)





## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
