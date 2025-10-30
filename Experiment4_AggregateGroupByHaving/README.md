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
How many appointments are scheduled in each hour of the day?

Sample table:Appointments Table

name                              type
--------------------          ----------
AppointmentID               INTEGER
PatientID                         INTEGER
DoctorID                         INTEGER
AppointmentDateTime   DATETIME
Purpose                           TEXT
Status                              TEXT     

```sql
select strftime('%H',AppointmentDateTime) as HourOfDay,count(*) as TotalAppointments 
from Appointments
group by strftime('%H',AppointmentDateTime)
order by HourOfDay;
```

**Output:**

<img width="713" height="530" alt="image" src="https://github.com/user-attachments/assets/c13bd407-83c6-4916-a139-e6045a6b9576" />


**Question 2**
---
What is the most common diagnosis among patients?

Sample table:MedicalRecords Table



For example:

Result
Diagnosis              DiagnosisCount
---------------------  --------------
Childhood vaccination  3

```sqlselect Diagnosis,count(*) as DiagnosisCount
from MedicalRecords
group by Diagnosis
order by DiagnosisCount desc
limit 1;
```

**Output:**

<img width="841" height="324" alt="image" src="https://github.com/user-attachments/assets/29478f86-938a-4af0-a0f6-31673934a072" />


**Question 3**
---
What is the total number of appointments scheduled by each doctor?

Sample table:Appointments Table



For example:

Result
DoctorID    TotalAppointments
----------  -----------------
1           1
2           3
5           3
9           2
10          1

```sql
select DoctorID,count(*) as TotalAppointments
from Appointments
group by DoctorID
order by DoctorID;-- Paste your SQL code below for Question 3
```

**Output:**

<img width="750" height="619" alt="image" src="https://github.com/user-attachments/assets/6cd40ee7-e73f-4a25-ac13-02ecdd2ac075" />


**Question 4**
---
Write a SQL query to find the total amount of fruits with a unit type of 'LB'.

Note: Inventory attribute contains amount of fruits

Table: fruits

name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL
 

```sql
select sum(inventory) as total from fruits where unit='LB';
```

**Output:**

<img width="478" height="370" alt="image" src="https://github.com/user-attachments/assets/a2bfd5e6-273f-4218-8048-948585c49831" />


**Question 5**
---
Write a SQL query to return the total number of rows in the 'customer' table where the city is Noida.

Sample table: customer



 

For example:

Result
COUNT
----------
1

```sql
select count(*) as COUNT from customer where city='Noida';
```

**Output:**

<img width="488" height="384" alt="image" src="https://github.com/user-attachments/assets/107239d1-520b-4aeb-bb65-b74b06041137" />


**Question 6**
---
Write a SQL query to calculate the average purchase amount of all orders. Return average purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

```sql
select avg(purch_amt) as AVERAGE from orders;
```

**Output:**

<img width="404" height="369" alt="image" src="https://github.com/user-attachments/assets/87adda07-747e-4d80-a028-939794034840" />


**Question 7**
---
Write a SQL query to find the number of employees whose age is greater than 32.

Sample table: employee

id

name

age

address

salary

1

Paul

32

California

20000

4

Mark

25

Richtown

65000

5

David

27

Texas

85000

 

```sql
select count(*) as COUNT from employee where age>32;
```

**Output:**

<img width="394" height="380" alt="image" src="https://github.com/user-attachments/assets/8973984a-f457-439c-9c50-a357e0cfa19c" />


**Question 8**
---
Write the SQL query that achieves the grouping of data by city, calculates the total income for each city, and includes only those cities where the total income sum is greater than 200,000.

Sample table: employee



For example:

Result
city        Income
----------  ----------
Alaska      450000
Arizona     1000000
California  5300000
Florida     5350000
Georgia     250000

```sql
select city,sum(income) as Income from employee
group by city
having sum(income)>200000;
```

**Output:**

<img width="593" height="535" alt="image" src="https://github.com/user-attachments/assets/d0347bf5-fd85-44d0-85e8-b94fdaf737b5" />


**Question 9**
---
Write the SQL query that achieves the grouping of data by age intervals using the expression (age/5)5, calculates the average age for each group, and excludes groups where the average age is not less than 24.

Sample table: customer1



For example:

Result
age_group   AVG(age)
----------  ----------
20          23.0

```sql
select (age/5)*5 as age_group,avg(age) as 'AVG(age)' from customer1 group by (age/5)*5
having avg(age)<24;
```

**Output:**

<img width="667" height="375" alt="image" src="https://github.com/user-attachments/assets/ec47c11c-6ee3-4f6d-b8ca-1148467cc3fd" />


**Question 10**
---
Write the SQL query that accomplishes the selection of product which has lowest price in each category from the "products" table and includes only those products where the minimum price is less than 10.

Sample table: products



For example:

Result
category_id  Price
-----------  ----------
3            7.5
Answer:(penalty regime

```sql
select category_id,min(price) as Price from products group by category_id having min(price)<10;
```

**Output:**

<img width="635" height="420" alt="image" src="https://github.com/user-attachments/assets/03a144d6-58b2-44d2-9911-3b5ce94d8761" />

<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/f10b416f-d4b8-413a-b698-8970290d4dd7" />


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
