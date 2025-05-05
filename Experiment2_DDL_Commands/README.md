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
-- Insert all products from Discontinued_products into Products.

  Table attributes are ProductID, ProductName, Price, Stock
  For example:
	

  ProductID         ProductName          Price            Stock

  101              Old Smartphone       199.99             0
  
  102              Vintage Laptop       399.99             10
  
  103              Classic Tablet       149.99             5


```sql
--

  INSERT INTO Products(ProductID, ProductName, Price, Stock)
  select ProductID, ProductName, Price, Stock
  from Discontinued_products
```

**Output:**

![Screenshot (194)](https://github.com/user-attachments/assets/661fdbdf-3f16-4cbf-90ae-37a6bc696304)


**Question 2**
---
-- Create a table named Department with the following constraints:

    DepartmentID as INTEGER should be the primary key.
    DepartmentName as TEXT should be unique and not NULL.
    Location as TEXT.

INSERT INTO Department (DepartmentID, DepartmentName, Location)      VALUES (1, 'Human Resources', 'New York'); select * from Department;

	

DepartmentID       DepartmentName        Location


1                  Human Resources       New York


```sql
--

   create table Department( DepartmentID integer primary key, DepartmentName text unique not null,
   Location text
);
```

**Output:**

![Screenshot (195)](https://github.com/user-attachments/assets/f972a887-520a-426c-a688-3d8b9c94235b)


**Question 3**
---
-- Insert a student with RollNo 201, Name David Lee, Gender M, Subject Physics, and MARKS 92 into the Student_details table.

For example:
Test 	Result

SELECT * FROM Student_details WHERE RollNo = 201;

	

RollNo               Name              Gender            Subject            MARKS


201                  David Lee          M                Physics            92


```sql
--

   insert into Student_details(RollNO,Name,Gender,Subject,MARKS)
   values(201,'David Lee','M','Physics',92)
```

**Output:**

![Screenshot (196)](https://github.com/user-attachments/assets/6182c405-b8ca-4f2a-b73a-b6e22beb18da)


**Question 4**
---
-- Create a table named Events with the following columns:

    EventID as INTEGER
    EventName as TEXT
    EventDate as DATE

For example:
Test 	Result

pragma table_info('Events');

	

cid               name              type              notnull                 dflt_value  pk

0                 EventID           INTEGER           0                       0


1                 EventName         TEXT              0                       0


2                 EventDate         DATE              0                       0


```sql
--

   create table Events(EventID INTEGER, EventName TEXT, EventDate DATE);
```

**Output:**

![Screenshot (197)](https://github.com/user-attachments/assets/e41025b8-5a17-43c5-b770-2c9f14f1ae09)


**Question 5**
---
-- Write an SQL query to add a new column email of type TEXT to the Student_details table, and ensure that this column cannot contain NULL values and make default value as 'Invalid'

 For example:
Test 	Result

INSERT INTO Student_details (RollNo, Name, Gender, Subject, email) 
VALUES (1, 'John Doe', 'M', 'Math', 'john@example.com');
select * from Student_details;

	

RollN  Name   Gen  Subject     email

1      John   M    Math        john@example.com


```sql
--

   ALTER TABLE Student_details
   ADD COLUMN email TEXT NOT NULL DEFAULT 'Invalid'; 
```

**Output:**
![Screenshot (198)](https://github.com/user-attachments/assets/0c511c98-1c1d-4d01-89bc-6193fd5fa7c3)


**Question 6**
---
-- Write a SQL query to add a column named Date_of_birth as Date in the Student_details table.

For example:
Test 	Result

pragma table_info('Student_details');

	

cid    name             type             notnu  dflt_value  pk

0      RollNo           int              0                  1
1      Name             VARCHAR(100)     1                  0
2      Gender           TEXT             1                  0
3      Subject          VARCHAR(30)      0                  0
4      MARKS            INT (3)          0                  0
5      Date_of_birth    Date             0                  0

	
```sql
--
alter table Student_details
add column Date_of_birth Date
```

**Output:**
![Screenshot (204)](https://github.com/user-attachments/assets/be64f1d9-7b03-4838-830d-fdb839f97a68)



**Question 7**
---
Create a table named Bonuses with the following constraints:

    BonusID as INTEGER should be the primary key.
    EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
    BonusAmount as REAL should be greater than 0.
    BonusDate as DATE.
    Reason as TEXT should not be NULL.

For example:
Test 	Result

INSERT INTO Bonuses (BonusID, EmployeeID, BonusAmount, BonusDate, Reason) VALUES (1, 6, 1000.0, '2024-08-01', 'Outstanding performance');
SELECT * FROM Bonuses;

	

BonusID      EmployeeID   BonusAmount   BonusDate    Reason

1            6            1000.0        2024-08-01   Outstanding performance



```sql
--

create table Bonuses(
BonusID integer primary key,
EmployeeID integer,
BonusAmount real check(BonusAmount>0),
BonusDate date,
Reason text not null,
foreign key (EmployeeID) references Employees(EmployeeID)
)  
```

**Output:**

![Screenshot (205)](https://github.com/user-attachments/assets/e4da7ec3-915f-4a9f-8c23-462207727c55)



**Question 8**
---
--In the Products table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

ProductID     Name                Category      Price         Stock

106           Fitness Tracker     Wearables
107           Laptop              Electronics    999.99        50
108           Wireless Earbuds    Accessories                  100

 

For example:
Test 	Result

SELECT * FROM Products;

	  
ProductID     Name               Category      Price         Stock

106           Fitness Tracker    Wearables
107           Laptop             Electronic    999.99        50
108           Wireless Earbud    Accessorie                  100


```sql
--

   insert into Products(ProductID,Name,Category,Price,Stock)
   values(106,'Fitness Tracker','Wearables',null,null);
  insert into Products(ProductID,Name,Category,Price,Stock)
  values(107,'Laptop','Electronics',999.99,50);
  insert into Products(ProductID,Name,Category,Price,Stock)
  values(108,'Wireless Earbuds','Accessories',null,100);

```

**Output:**

![Screenshot (206)](https://github.com/user-attachments/assets/fc23e68a-8afb-4b08-a157-7e93c02b76a8)



**Question 9**
---
-- reate a table named Orders with the following constraints:

    OrderID as INTEGER should be the primary key.
    OrderDate as DATE should be not NULL.
    CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).

For example:
Test 	Result

INSERT INTO Customers (CustomerID, FirstName, LastName, Email) VALUES (1, 'Alice', 'Johnson', 'alice.johnson@example.com');
INSERT INTO Orders (OrderID, OrderDate, CustomerID) VALUES (1, '2024-08-01', 1);
select * from orders;

	

OrderID       OrderDate     CustomerID

1             2024-08-01    1

```sql
-- 

 create table Orders(
 OrderID integer primary key,
 OrderDate date not null,
 CustomerID integer,
 foreign key (CustomerID) references  Customers(CustomerID)
 );

```

**Output:**
![Screenshot (207)](https://github.com/user-attachments/assets/25f961ae-286e-4150-86d1-cbe8e9cc6509)



**Question 10**
---
-- 
Create a table named Invoices with the following constraints:

    InvoiceID as INTEGER should be the primary key.
    InvoiceDate as DATE.
    Amount as REAL should be greater than 0.
    DueDate as DATE should be greater than the InvoiceDate.
    OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

For example:
Test 	Result

INSERT INTO Orders (OrderID, OrderDate, CustomerID) VALUES (1, '2024-08-01', 1);
INSERT INTO Invoices (InvoiceID, InvoiceDate, Amount, DueDate, OrderID) VALUES (1, '2024-08-01', 100.0, '2024-09-01', 1);
SELECT * FROM Invoices;

	

InvoiceID     InvoiceDate    Amount        DueDate       OrderID

1             2024-08-01     100.0         2024-09-01    1

	
```sql
--

create table Invoices(
InvoiceID integer primary key,
InvoiceDate date,
Amount real check(Amount>0),
DueDate date check(DueDate> InvoiceDate),
OrderID integer,
foreign key (OrderID) references Orders(OrderID)
);
```

**Output:**

![Screenshot (208)](https://github.com/user-attachments/assets/955f838d-6f41-43d8-968c-37bcb6eb30b8)



**MODULE 1 - SEB GRADE SCREENSHOT:**

![Screenshot 2025-05-05 114635](https://github.com/user-attachments/assets/b90f3850-1e92-4234-9b3b-54e74b171838)


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
