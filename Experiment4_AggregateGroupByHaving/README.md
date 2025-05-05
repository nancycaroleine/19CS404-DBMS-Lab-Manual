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
-- Write the SQL query that accomplishes the grouping of data by addresses, calculates the sum of salaries for each address, and excludes addresses where the total salary sum is not greater than 2000.

Sample table: customer1
![unnamed](https://github.com/user-attachments/assets/77e34818-4a82-4ece-957a-ab51413da1c2)


For example:
Result

address     SUM(salary)

Bhopal      8500
Hyderabad   4500
Indore      10000
Mumbai      6500


```sql
--select address,SUM(salary) from customer1
group by address
having sum(salary)>2000;

```

**Output:**
![Screenshot (229)](https://github.com/user-attachments/assets/36fc065e-d76f-436c-9411-02d17249771e)



**Question 2**
---
-- How many prescriptions were written by each doctor?

Sample tablePrescriptions Table

For example:
![image (8)](https://github.com/user-attachments/assets/093b6770-1033-4afd-b7df-15fe67013871)

Result

DoctorID     TotalPrescriptions

1            1
2            1
3            1
4            1
5            1
6            1
7            1
8            1
9            1
10           1


```sql
--
select DoctorID,count(PrescriptionID) as TotalPrescriptions
from Prescriptions
group by DoctorID;
```

**Output:**
![Screenshot (221)](https://github.com/user-attachments/assets/0ea4e2a6-8c48-47a3-90d4-701eb3041732)


**Question 3**
---
-- How many doctors specialize in each medical specialty?

Sample table:Doctors Table

For example:
![image (4)](https://github.com/user-attachments/assets/4c189041-4818-40c8-bfd7-ad35e6698ac2)

Result

Specialty          TotalDocto

Gastroenterology   1

Neurology          1

Obstetrics         3

Ophthalmology      1

Orthopedics        1

Pediatrics         2

Urology            1


```sql
--
select Specialty,count(DoctorID) as TotalDocto from Doctors
group by Specialty;
```

**Output:**

![Screenshot (222)](https://github.com/user-attachments/assets/68b38c85-3bd4-4e09-9974-029cfaa5413f)


**Question 4**
---
-- Write a SQL query to return the total number of rows in the 'customer' table where the city is not Noida.

Sample table: customer
![image (3)](https://github.com/user-attachments/assets/d80ab2f4-608b-4462-a906-c9bb2b029c45)

For example:
Result

COUNT

9


```sql
--
select count(id) as COUNT from customer
where city !='Noida';
```

**Output:**

![Screenshot (223)](https://github.com/user-attachments/assets/6f01ae36-7281-4077-a954-a89d661d261c)


**Question 5**
---
-- Write a SQL query to find the minimum purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id



70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

 

For example:
Result

MINIMUM

65.26


```sql
--
select min(purch_amt) as MINIMUM from orders;
```

**Output:**

![Screenshot (224)](https://github.com/user-attachments/assets/d67867c8-bcd6-47c2-915b-887ee0666fc7)


**Question 6**
---
-- Write a SQL query to calculate the total number of working hours of all employees

Sample table: employee1

 ![image (2)](https://github.com/user-attachments/assets/e98c10cb-7fae-459f-a18a-a28e2b442515)


For example:
Result

Total working hours

111

```sql
--
select sum(workhour) as 'Total working hours'
from employee1;
```

**Output:**

![Screenshot (225)](https://github.com/user-attachments/assets/5c38ba9f-1ee1-44ae-9925-542a61f1d38e)


**Question 7**
---
-- Write a SQL query to calculate total available amount of fruits that has a price greater than 0.5 . Return total Count. 

Note: Inventory attribute contains amount of fruits

Table: fruits

name        type

id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL

 

For example:
Result

total_available_amount

160


```sql
--
select sum(inventory) as 'total_available_amount'
from fruits
where price >0.5;
```

**Output:**
![Screenshot (226)](https://github.com/user-attachments/assets/5c375c95-c963-4e33-86c4-e30870152bb3)


**Question 8**
---
-- Write the SQL query that accomplishes the grouping of data by age intervals using the expression (age/5)5, calculates the minimum age for each group, and excludes groups where the minimum age is not less than 25.

Sample table: customer1
![unnamed](https://github.com/user-attachments/assets/b3e160bf-4479-4e89-a686-68c6ab45f52b)


For example:
Result

age_group   MIN(age)

20          22


```sql
--
select (age/5)*5 as age_group,MIN(age) from customer1
group by age_group
having min(age) <25;
```

**Output:**

![Screenshot (227)](https://github.com/user-attachments/assets/39dbf571-4b0a-4603-bc96-de014bf7d6c2)


**Question 9**
---
-- Write the SQL query that accomplishes the grouping of data by age, calculates the maximum income for each age group, and includes only those age groups where the maximum income is greater than 2,000,000.

Sample table: employee
![unnamed](https://github.com/user-attachments/assets/c8eaccb3-50d3-4c9f-b6e0-9b8c7a353409)


For example:
Result

age         MAX(income)

35          5000000


```sql
--
select age,MAX(income) from employee
group by age
having max(income)>2000000;
```

**Output:**

![Screenshot (228)](https://github.com/user-attachments/assets/1e0c1b1f-4447-44c4-8159-348edecff809)


**Question 10**
---
-- Write SQL query to extract the email domain from each patient's email address and count the number of patients with the same email domain.

Sample table: Patients Table
![image (3)](https://github.com/user-attachments/assets/379ec86b-fc75-46ba-909f-dfc4833b6003)


For example:
Result

EmailDomain    TotalPatients

example.com    10


```sql
-- select substr(email,instr(email))
```

**Output:**
![Screenshot (220)](https://github.com/user-attachments/assets/c57f7e4b-bb7f-46e8-8567-76de0239b0a8)

**SEB-3 GRADE SCREENSHOT**
![Screenshot 2025-05-05 222957](https://github.com/user-attachments/assets/514f802c-a5ad-4ed2-a677-39861c2a50eb)




## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
