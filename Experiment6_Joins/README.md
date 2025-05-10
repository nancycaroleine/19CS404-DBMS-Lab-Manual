# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
-- write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.

Sample table: salesman

 salesman_id |    name    |   city   | commission 

        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 

        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005

For example:
Result

Salesman         cust_name        city

Bob Emily        Brad Davis       New York

Nail Knite       Fabian Johns     Paris

Pit Alex         Brad Guzan       London

Pit Alex         Julian Green     London

Mc Lyon          Fabian Johns     Paris


```sql
--
select s.name as Salesman,c.cust_name,c.city from salesman s
join customer c
on s.city = c.city;

```

**Output:**

![Screenshot (252)](https://github.com/user-attachments/assets/d97239b0-e96c-4448-90a7-04a123e7b09a)


**Question 2**
---
-- Write a SQL statement to make a report with customer name, city, order number, order date, and order amount in ascending order according to the order date to determine whether any of the existing customers have placed an order or not.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 

        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007

For example:
Result

cust_name        city             ord_no           ord_date         Order Amount

Nick Rimando     Chennai          70013            2012-04-25       3045.6
Julian Green     London           70012            2012-06-27       250.45
Brad Davis       New York         70005            2012-07-27       2400.6
Geoff Cameron    Berlin           70004            2012-08-17       110.5
Jozy Altidore    Moscow           70011            2012-08-17       75.29
Nick Rimando     Chennai          70008            2012-09-10       5760.0
Graham Zusi      California       70007            2012-09-10       948.5
Brad Guzan       London           70009            2012-09-10       270.65
Nick Rimando     Chennai          70002            2012-10-05       65.26
Graham Zusi      California       70001            2012-10-05       150.5
Fabian Johns     Paris            70010            2012-10-10       1983.43
Geoff Cameron    Berlin           70003            2012-10-10       2480.4


```sql
--
select c.cust_name,c.city,o.ord_no,o.ord_date,o.purch_amt as 'Order Amount' from customer c
left join orders o
on c.customer_id = o.customer_id
order by o.ord_date asc;
```

**Output:**

![Screenshot (253)](https://github.com/user-attachments/assets/20d43042-94b1-4513-abc0-c03470de00b7)


**Question 3**
---
-- Write the SQL query that achieves the selection of the date of birth from the "patients" table (aliased as "p") and all columns from the "appointments" 
   table (aliased as "a"), with an inner join on the "patient_id" column and a condition filtering for patients with the first name 'Alice'.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id
![unnamed](https://github.com/user-attachments/assets/282143f4-dbe8-48d0-a661-b3560dda0c6e)

APPOINTMENTS TABLE:

ATTRIBUTES - appointment_id, patient_id, doctor_id, appointment_date
![unnamed](https://github.com/user-attachments/assets/a38cb063-315e-471a-ae02-1574adc9a694)

For example:
Result

date_of_birth    appointment_id   patient_id       doctor_id        appointment_date

1980-05-12       1                1                1                2024-01-05 10:00:00

```sql
--
select p.date_of_birth, a.appointment_id,a.patient_id,a.doctor_id,a.appointment_date from appointments a
inner join patients p
on a.patient_id=p.patient_id
where p.first_name='Alice';
```

**Output:**

![Screenshot (254)](https://github.com/user-attachments/assets/d104d75b-76a7-49aa-988a-04d7920e829c)


**Question 4**
---
-- Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id"     column and a condition filtering for customers in the city 'London'.

Customer Table:
![unnamed](https://github.com/user-attachments/assets/0f16b663-5bbc-4da6-9324-99220f2863c9)

Salesmen Table:
![unnamed](https://github.com/user-attachments/assets/d27311c6-4292-4c18-acec-57e77e67e05f)

For example:
Result

name
---------------
Pit Alex
Nail Knite

```sql
--
select s.name as name from Salesman s
left join Customer c
on c.salesman_id=s.salesman_id
where c.city = 'London';

```

**Output:**

![Screenshot (255)](https://github.com/user-attachments/assets/4e2a4477-a35d-49fa-8fe8-c1aaea282a6d)


**Question 5**
---
-- SQL statement to generate a report with customer name, city, order number, order date, order amount, salesperson name, and commission to determine if any of the existing customers have not placed orders or if they have placed orders through their salesman or by themselves.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 

        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001

Sample table: salesman

 salesman_id |    name    |   city   | commission 

        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12

For example:
Result

cust_name        city             ord_no           ord_date         Order Amount  name        commission

Nick Rimando     Chennai          70002            2012-10-05       65.26         Bob Emily   0.15
Nick Rimando     Chennai          70008            2012-09-10       5760.0        Bob Emily   0.15
Nick Rimando     Chennai          70013            2012-04-25       3045.6        Bob Emily   0.15
Graham Zusi      California       70001            2012-10-05       150.5         Nail Knite  0.13
Graham Zusi      California       70007            2012-09-10       948.5         Nail Knite  0.13
Brad Guzan       London           70009            2012-09-10       270.65        Pit Alex    0.11
Fabian Johns     Paris            70010            2012-10-10       1983.43       Mc Lyon     0.14
Brad Davis       New York         70005            2012-07-27       2400.6        Bob Emily   0.15
Geoff Cameron    Berlin           70003            2012-10-10       2480.4        Lauson Hen  0.12
Geoff Cameron    Berlin           70004            2012-08-17       110.5         Lauson Hen  0.12
Julian Green     London           70012            2012-06-27       250.45        Nail Knite  0.13
Jozy Altidore    Moscow           70011            2012-08-17       75.29         Paul Adam   0.13


```sql
--
select c.cust_name,c.city,o.ord_no,o.ord_date,o.purch_amt as 'Order Amount',s.name,s.commission
from customer c
left join orders o
on c.customer_id=o.customer_id
left join salesman s
on s.salesman_id=o.salesman_id;
```

**Output:**

![Screenshot (256)](https://github.com/user-attachments/assets/8ae81435-18f7-40a8-9dd5-a6019384dc62)

**Question 6**
---
-- Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column and a condition filtering for patients admitted between '2024-01-01' and '2024-01-31'.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id
![unnamed](https://github.com/user-attachments/assets/ccd74658-316f-4468-bfd1-5761de81fd0a)

TEST_RESULT TABLES:

ATTRIBUTES - result_id, patient_id, test_name, result, test_date
![unnamed](https://github.com/user-attachments/assets/4b830143-2cee-4135-928e-8021a864645e)

For example:
Result

patient_name     result_id        patient_id       test_name        result      test_date

Alice            1                1                Blood Pressure   120/80      2024-01-20


```sql
--
select p.first_name as patient_name,t.result_id,t.patient_id,t.test_name,t.result,t.test_date from test_results t
inner join patients p
on t.patient_id=p.patient_id
where t.test_date between '2024-01-01' and '2024-01-31';
```

**Output:**

![Screenshot (257)](https://github.com/user-attachments/assets/da2a8fcf-029b-4de9-9116-e9a6cbb402ec)


**Question 7**
---
-- Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column and a condition filtering for customers in the city 'New York'.

Customer Table:
![unnamed](https://github.com/user-attachments/assets/cbf534df-c824-4f3e-bcd8-93bb1f2f9d26)

Salesmen Table:
![unnamed](https://github.com/user-attachments/assets/5699f18a-20b9-4aa0-89f5-343c22e8cff3)

For example:
Result

name
Bob Emily


```sql
--
select s.name from Salesman s
left join Customer c
on c.salesman_id=s.salesman_id
where c.city='New York';
```

**Output:**

![Screenshot (258)](https://github.com/user-attachments/assets/31627f1f-4b50-4a09-84e6-050732783cb4)


**Question 8**
---
-- From the following tables write a SQL query to find the details of an order. Return ord_no, ord_date, purch_amt, Customer Name, grade, Salesman, commission. 

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 

        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005

Sample table: salesman

 salesman_id |    name    |   city   | commission 

        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12

For example:
Result

ord_no           ord_date         purch_amt        Customer Name    grade       Salesman    commission

70001            2012-10-05       150.5            Graham Zusi      200         Nail Knite  0.13
70009            2012-09-10       270.65           Brad Guzan       100         Pit Alex    0.11
70002            2012-10-05       65.26            Nick Rimando     100         Bob Emily   0.15
70004            2012-08-17       110.5            Geoff Cameron    100         Lauson Hen  0.12
70007            2012-09-10       948.5            Graham Zusi      200         Nail Knite  0.13
70005            2012-07-27       2400.6           Brad Davis       200         Bob Emily   0.15
70008            2012-09-10       5760.0           Nick Rimando     100         Bob Emily   0.15
70010            2012-10-10       1983.43          Fabian Johns     300         Mc Lyon     0.14
70003            2012-10-10       2480.4           Geoff Cameron    100         Lauson Hen  0.12
70012            2012-06-27       250.45           Julian Green     300         Nail Knite  0.13
70011            2012-08-17       75.29            Jozy Altidore    200         Paul Adam   0.13
70013            2012-04-25       3045.6           Nick Rimando     100         Bob Emily   0.15


```sql
--
select o.ord_no,o.ord_date,o.purch_amt,c.cust_name as 'Customer Name',c.grade,s.name as 'Salesman',s.commission
from orders o
join customer c 
on o.customer_id=c.customer_id
join salesman s
on c.salesman_id=s.salesman_id;
```

**Output:**

![Screenshot (259)](https://github.com/user-attachments/assets/20a08a9f-6d11-4204-a9e3-0bc73e91d633)


**Question 9**
---
-- From the following tables write a SQL query to locate those salespeople who do not live in the same city where their customers live and have received a commission of more than 12% from the company. Return Customer Name, customer city, Salesman, salesman city, commission.  

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 

        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005

Sample table: salesman

 salesman_id |    name    |   city   | commission 

        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12

For example:
Result

Customer Name    city             Salesman         city             commission

Nick Rimando     Chennai          Bob Emily        New York         0.15
Graham Zusi      California       Nail Knite       Paris            0.13
Julian Green     London           Nail Knite       Paris            0.13
Jozy Altidore    Moscow           Paul Adam        Rome             0.13


```sql
--
select c.cust_name as 'Customer Name',c.city,s.name as Salesman, s.city,s.commission from customer c
join salesman s
on c.salesman_id=s.salesman_id
where c.city != s.city and s.commission>0.12;
```

**Output:**

![Screenshot (260)](https://github.com/user-attachments/assets/51bcb0af-d65b-4658-a344-16705b4ef53a)


**Question 10**
---
-- Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and a condition filtering for appointments with an appointment date between '2024-02-01' and '2024-02-28'.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id
![unnamed](https://github.com/user-attachments/assets/e46835fc-0f51-41f2-bb81-4057a9c03700)

APPOINTMENTS TABLE:

ATTRIBUTES - appointment_id, patient_id, doctor_id, appointment_date
![unnamed](https://github.com/user-attachments/assets/e28585bb-5768-4cb8-828c-a153c1413cdb)

For example:
Result

patient_id       first_name       last_name        date_of_birth    admission_date  discharge_date  doctor_id

2                Bob              Miller           1995-08-23       2024-02-15      2024-03-01      2


```sql
--
select p.* from patients p
inner join appointments a
on p.patient_id = a.patient_id
where a.appointment_date between '2024-02-01' and '2024-02-28';
```

**Output:**

![Screenshot (261)](https://github.com/user-attachments/assets/a408ad67-8add-4f68-8ebc-94235c0a2e51)

**SEB-5 GRADE SCREENSHOT**
![Screenshot (262)](https://github.com/user-attachments/assets/9ed04831-59ca-483a-98db-c6ad67e989cf)




## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
