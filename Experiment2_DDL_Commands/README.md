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
Create a table named Departments with the following columns:

DepartmentID as INTEGER
DepartmentName as TEXT

```sql
create table Departments(
DepartmentID INTEGER,
DepartmentName TEXT
);
```

**Output:**

<img width="1244" height="287" alt="image" src="https://github.com/user-attachments/assets/6ee53448-d509-4db9-8b26-42e5273062ad" />


**Question 2**
---
-- Create a table named Products with the following constraints:
ProductID as INTEGER should be the primary key.
ProductName as TEXT should be unique and not NULL.
Price as REAL should be greater than 0.
StockQuantity as INTEGER should be non-negative.

```sql
create table Products(
ProductID INTEGER primary key,
ProductName TEXT unique NOT NULL,
Price REAL check(Price>0),
StockQuantity INTEGER check(StockQuantity>=0));
```

**Output:**

<img width="1166" height="170" alt="image" src="https://github.com/user-attachments/assets/7abbe813-c121-48f6-8a11-56b1eaec6684" />


**Question 3**
---
Insert a new product with ProductID 101, Name Laptop, Category Electronics, Price 1500, and Stock 50 into the Products table.

```sql
insert into Products(ProductID,Name,Category,Price,Stock) values(101,"Laptop","Electronics",1500,50);
```

**Output:**

<img width="1283" height="227" alt="image" src="https://github.com/user-attachments/assets/2c4f9c8f-c720-481d-9124-e304a463e26d" />


**Question 4**
---
--Create a table named Department with the following constraints:
DepartmentID as INTEGER should be the primary key.
DepartmentName as TEXT should be unique and not NULL.
Location as TEXT.

```sql
create table Department(
DepartmentID INTEGER primary key,
DepartmentName TEXT unique NOT NULL,
Location TEXT);
```

**Output:**

<img width="1216" height="172" alt="image" src="https://github.com/user-attachments/assets/3611fd80-182f-4215-a808-a1afad521013" />


**Question 5**
---
-- Insert all customers from Old_customers into Customers

Table attributes are CustomerID, Name, Address, Email

```sql
insert into Customers(CustomerID, Name, Address, Email) 
select CustomerID, Name, Address, Email from Old_customers;
```

**Output:**

<img width="1252" height="264" alt="image" src="https://github.com/user-attachments/assets/bc4761f0-da31-4b2a-a7ee-fb1e31017c75" />


**Question 6**
---
-- In the Books table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

ISBN             Title                      Author           Publisher   Year
---------------  -------------------------  ---------------  ----------  ----------
978-1234567890   Introduction to AI         John Doe
978-9876543210   Deep Learning              Jane Doe         TechPress   2022
978-1122334455   Cybersecurity Essentials   Alice Smith                  2021

```sql
insert into Books(ISBN,Title,Author,Publisher,Year) values("978-1234567890","Introduction to AI","John Doe","",""),("978-9876543210","Deep Learning","Jane Doe","TechPress",2022),("978-1122334455","Cybersecurity Essentials","Alice Smith","",2021);
```

**Output:**

<img width="1188" height="203" alt="image" src="https://github.com/user-attachments/assets/a5acf51c-e1db-4be0-a920-5b0290f51ae4" />


**Question 7**
---
-- Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```sql
create table Shipments(
ShipmentID INTEGER primary key,
ShipmentDate DATE,
SupplierID INTEGER,
OrderID INTEGER,
foreign key(SupplierID) references Suppliers(SupplierID),
foreign key(OrderID) references Orders(OrderID)
);
```

**Output:**

<img width="1203" height="308" alt="image" src="https://github.com/user-attachments/assets/b4941948-dcc1-4651-8457-c630ed2dce58" />


**Question 8**
---
--Write a SQL query to add a new column MobileNumber of type NUMBER and a new column Address of type VARCHAR(100) to the Student_details table.

```sql
alter table Student_details add MobileNumber NUMBER;
alter table Student_details add Address VARCHAR(100);
```

**Output:**

<img width="1265" height="229" alt="image" src="https://github.com/user-attachments/assets/2893d4f7-53ea-467a-a2c0-293816dc7ddc" />


**Question 9**
---
-- Write an SQL query to add two new columns, designation and net_salary, to the table Companies. The designation column should have a data type of varchar(50), and the net_salary column should have a data type of number.

```sql
 alter table Companies add designation varchar(50);
alter table Companies add net_salary number;
```

**Output:**

<img width="1251" height="305" alt="image" src="https://github.com/user-attachments/assets/3f98bc5e-8b90-426b-9a14-7aeeb0bbfa0d" />


**Question 10**
---
-- Create a table named ProjectAssignments with the following constraints:
AssignmentID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
AssignmentDate as DATE should be NOT NULL.

```sql
create table ProjectAssignments(
AssignmentID INTEGER primary key,
EmployeeID INTEGER,
ProjectID INTEGER,
AssignmentDate DATE NOT NULL,
foreign key(EmployeeID) references Employees(EmployeeID),
foreign key(ProjectID) references Projects(ProjectID));
```

**Output:**

<img width="1112" height="166" alt="image" src="https://github.com/user-attachments/assets/7ebd3559-ef08-4db2-a9ca-48e6256ea281" />

<img width="1468" height="92" alt="image" src="https://github.com/user-attachments/assets/e0ea8b90-a46e-4147-beb8-1491b62f2f6e" />


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
