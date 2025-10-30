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

<img width="835" height="545" alt="image" src="https://github.com/user-attachments/assets/bcfb84cb-f9f8-4a4d-910c-3f7b93c49a87" />


**Question 2**
---
What is the most common diagnosis among patients?

Sample table:MedicalRecords Table



For example:

Result
Diagnosis              DiagnosisCount
---------------------  --------------
Childhood vaccination  3


```sql
select Diagnosis,count(*) as DiagnosisCount
from MedicalRecords
group by Diagnosis
order by DiagnosisCount desc
limit 1;
```

**Output:**

<img width="894" height="311" alt="image" src="https://github.com/user-attachments/assets/d96e8d1c-5fb0-40ac-9646-5e3d1279415f" />


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
order by DoctorID;
```

**Output:**

<img width="768" height="648" alt="image" src="https://github.com/user-attachments/assets/9186a100-ea06-433b-9c44-3f2e95c588d6" />


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

<img width="402" height="380" alt="image" src="https://github.com/user-attachments/assets/942f46d5-b10c-46d3-9771-ef55930a52b7" />


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

<img width="539" height="368" alt="image" src="https://github.com/user-attachments/assets/737a392f-ffa7-41c4-82db-805a5f9a8c25" />


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

<img width="468" height="375" alt="image" src="https://github.com/user-attachments/assets/cfd116c9-de07-490c-8466-bc256c70da17" />


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

<img width="550" height="388" alt="image" src="https://github.com/user-attachments/assets/391044ab-7401-47cc-9a65-327fb073c364" />


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

<img width="600" height="605" alt="image" src="https://github.com/user-attachments/assets/8be059dc-63ac-485c-9be5-661511a83e8c" />


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

<img width="643" height="382" alt="image" src="https://github.com/user-attachments/assets/6dd12120-8af2-489d-8ccc-b512aafefd23" />


**Question 10**
---
Write the SQL query that accomplishes the selection of product which has lowest price in each category from the "products" table and includes only those products where the minimum price is less than 10.

Sample table: products



For example:

Result
category_id  Price
-----------  ----------
3            7.5

```sql
Write the SQL query that accomplishes the selection of product which has lowest price in each category from the "products" table and includes only those products where the minimum price is less than 10.

Sample table: products



For example:

Result
category_id  Price
-----------  ----------
3            7.5
```

**Output:**

<img width="700" height="449" alt="image" src="https://github.com/user-attachments/assets/83b2be78-002f-4c70-a7ca-13f5335881af" />

<img width="1888" height="1029" alt="image" src="https://github.com/user-attachments/assets/4ae5031b-63b6-4f95-a56d-d46ea58fa140" />


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
