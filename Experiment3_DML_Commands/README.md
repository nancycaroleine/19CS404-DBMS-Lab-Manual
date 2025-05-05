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
-- Increase the reorder level by 30% for products from 'Food' category having quantity in stock less than 50% of existing reorder level in the products table

name               type

product_id         INT
product_name       VARCHAR(10)
category           VARCHAR(50)
cost_price         DECIMAL(10)
sell_price         DECIMAL(10)
reorder_lvl        INT
quantity              INT
supplier_id           INT

For example:
Test 	Result

select changes();

	

changes()
----------
4


```sql
--
update products
set reorder_lvl = round(reorder_lvl*1.30)
where category = 'Food' and quantity < (reorder_lvl*0.50);
```

**Output:**

![Screenshot (210)](https://github.com/user-attachments/assets/a1cb12c0-42ad-4635-85a4-da32956e608e)


**Question 2**
---
-- Write a SQL statement to Change the category to 'Household' where product name contains 'Detergent' in the products table.

Products Table 

name          type       
 
product_id     INT PRIMARY KEY        
product_name   VARCHAR(10) 
category       VARCHAR(50) 
cost_price     DECIMAL(10) 
sell_price     DECIMAL(10) 
reorder_lvl    INT        
quantity       INT        
supplier_id    INT           

For example:
Test 	Result

select changes();

changes()

 4


```sql
--
update Products
set category ='Household'
where product_name like '%Detergent%';
```

**Output:**
![Screenshot (211)](https://github.com/user-attachments/assets/6629c153-dc58-4c81-ad0d-e2ac98021fad)


**Question 3**
---
-- Write a SQL statement to Increase the selling price by 15% in the products table where quantity in stock is less than 50 and supplier ID is 10.

Products Table 

name          type       
 
product_id     INT PRIMARY KEY        
product_name   VARCHAR(10) 
category       VARCHAR(50) 
cost_price     DECIMAL(10) 
sell_price     DECIMAL(10) 
reorder_lv     INT        
quantity       INT        
supplier_id    INT           

For example:
Test 	Result

select changes();

changes()

4


```sql
--
update products
set sell_price = sell_price*1.15
where quantity < 50 and supplier_id = 10;
```

**Output:**
![Screenshot (212)](https://github.com/user-attachments/assets/be220d31-cc58-4c51-8f33-3fcb94b29f1b)


**Question 4**
---
-- 
 Update the total selling price to quantity sold multiplied by updated selling price per unit where product id is 10 in the sales table.

SALES TABLE

name               type

sale_id            INT
sale_date          DATE
product_id         INT
quantity           INT
sell_price         DECIMAL(10,2)
total_sell_price   DECIMAL(10,2)

For example:
Test 	Result

select changes();

changes()

3

```sql
--
update SALES
set total_sell_price = quantity*sell_price
where product_id = 10;
```

**Output:**

![Screenshot (213)](https://github.com/user-attachments/assets/f1299129-5563-4c87-8d37-b0897bafc59b)


**Question 5**
---
-- Write a SQL statement to Update the product_name to 'Premium Bread' whose product ID is 5 in the products table.

Products table

---------------
product_id
product_name
category
cost_price
sell_price
reorder_lvl
quantity
supplier_id

```sql
--
update Products
set product_name = 'Premium Bread'
where product_id = 5;
```

**Output:**

![Screenshot (214)](https://github.com/user-attachments/assets/a0b01e2f-aec4-414d-b877-789a921d2855)


**Question 6**
---
-- Write a SQL query to Delete customers with following conditions

    'CUST_COUNTRY' is not in a list of specified countries ('UK', 'USA', 'Canada')
    'GRADE' is greater than or equal to 3

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |

For example:
Test 	Result

select changes();

changes()

2


```sql
--
delete from customer
where cust_country not in ('UK','USA','Canada') and grade >=3;
```

**Output:**

![Screenshot (215)](https://github.com/user-attachments/assets/cb3e667b-d6a0-438a-bac1-5c0a3b61ba1f)


**Question 7**
---
-- Write a SQL query to Delete all Doctors whose Specialization is either 'Pediatrics' or 'Cardiology' and Last Name is Brown.

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

For example:
Test 	Result

SELECT * FROM doctors;

	

doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology

2           Emily       Johnson     Orthopedics

3           Michael     Brown       Pediatrics

doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology

2           Emily       Johnson     Orthopedics

```sql
--
delete from Doctors
where specialization in ('Pediatrics','Cardiology') and last_name='Brown';
```

**Output:**

![Screenshot (216)](https://github.com/user-attachments/assets/559ec1df-563b-4a60-bc74-c52c718f52fe)

**Question 8**
---
-- Write a SQL query to Delete customers from 'customer' table where 'GRADE' is not equal to 3.
 

Sample table: Customer

  
|CUST_CODE  |   CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE |    OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |


| C00013    |   Holmes      |   London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |


| C00001    |   Micheal     |   New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |


| C00020    |   Albert      |   New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |

For example:
Test 	Result

select distinct(grade)from customer;

	

GRADE
----------
2
3
1
0
GRADE
----------
3


```sql
--
delete from Customer 
where GRADE !=3;
```

**Output:**
![Screenshot (217)](https://github.com/user-attachments/assets/fde505b6-34bc-4ef7-85ef-838688e6bde4)

**Question 9**
---
-- Write a SQL query to Delete customers from 'customer' table where 'CUST_NAME' has exactly 6 characters.

Sample table: Customer
 
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |

| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |

| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |

| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |

For example:
Test 	Result

select changes();

	

CUST_CODE   CUST_NAME   CUST_CITY   WORKING_AREA  CUST_COUNTRY  GRADE       OPENING_AMT  RECEIVE_AMT  PAYMENT_AMT  OUTSTANDING_AMT  PHONE_NO    AGENT_CODE

C00013      Holmes      London      London        UK            2           6000         5000         7000         4000             BBBBBBB     A003

C00020      Albert      New York    New York      USA           3           5000         7000         6000         6000             BBBBSBB  

C00015      Stuart      London      London        UK            1           6000         8000         3000         11000            GFSGERS     A003

C00012      Steven      San Jose    San Jose      USA           1           5000         7000         9000         3000             KRFYGJK     A012

C00003      Martin      Torento     Torento       Canada        2           8000         7000         7000         8000             MJYURFD     A004

C00009      Ramesh      Mumbai      Mumbai        India         3           8000         7000         3000         12000            Phone No    A002

changes()

6


```sql
--
delete from Customer
where length(CUST_NAME) = 6;
```

**Output:**
![Screenshot (218)](https://github.com/user-attachments/assets/d8df3bfd-1721-4be8-a890-2fe3b2f24592)


**Question 10**
---
-- Write a SQL query to delete a specific doctor from Doctors table whose ID is 1.

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

```sql
--
delete from Doctors
where doctor_id = 1;
```

**Output:**

![Screenshot (219)](https://github.com/user-attachments/assets/81eaa3b2-f163-4bd0-8ad8-be0ed67ec2f3)

**MODULE 2 - SEB GRAGE SCREENSHOT]**

![Screenshot 2025-05-05 141549](https://github.com/user-attachments/assets/c754bf48-b600-440e-949b-de39e3dbb417)


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
