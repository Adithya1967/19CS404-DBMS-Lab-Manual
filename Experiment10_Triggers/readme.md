# Experiment 10: PL/SQL – Triggers

## AIM
To write and execute PL/SQL trigger programs for automating actions in response to specific table events like INSERT, UPDATE, or DELETE.

---

## THEORY

A **trigger** is a stored PL/SQL block that is automatically executed or fired when a specified event occurs on a table or view. Triggers can be used for enforcing business rules, auditing changes, or automatic updates.

### Types of Triggers:
- **Before Trigger**: Executes before the operation (INSERT, UPDATE, DELETE).
- **After Trigger**: Executes after the operation.
- **Row-level Trigger**: Executes for each affected row.
- **Statement-level Trigger**: Executes once for the triggering statement.

**Basic Syntax:**
```sql
CREATE OR REPLACE TRIGGER trigger_name
BEFORE|AFTER INSERT|UPDATE|DELETE ON table_name
[FOR EACH ROW]
BEGIN
   -- trigger logic
END;
```

## 1. Write a trigger to log every insertion into a table.
**Steps:**
- Create two tables: `employees` (for storing data) and `employee_log` (for logging the inserts).
- Write an **AFTER INSERT** trigger on the `employees` table to log the new data into the `employee_log` table.
### Program:
![image](https://github.com/user-attachments/assets/d1bece84-76df-4e9c-8bc1-4477d7b961d5)

**Expected Output:**
- A new entry is added to the `employee_log` table each time a new record is inserted into the `employees` table.

### Output:
![image](https://github.com/user-attachments/assets/9f84e30f-f682-425c-8e8b-8392a916acaf)
![image](https://github.com/user-attachments/assets/4f1544c6-d118-47fa-9118-a2493cbc70cf)

---

## 2. Write a trigger to prevent deletion of records from a sensitive table.
**Steps:**
- Write a **BEFORE DELETE** trigger on the `sensitive_data` table.
- Use `RAISE_APPLICATION_ERROR` to prevent deletion and issue a custom error message.

### Program:
![image](https://github.com/user-attachments/assets/b8abc814-dc0f-4bbf-9927-194097e97405)

**Expected Output:**
- If an attempt is made to delete a record from `sensitive_data`, an error message is raised, e.g., `ERROR: Deletion not allowed on this table.`
### Output:
![image](https://github.com/user-attachments/assets/c3411f26-292e-469b-b9fc-6049c55cd45f)

---

## 3. Write a trigger to automatically update a `last_modified` timestamp.
**Steps:**
- Add a `last_modified` column to the `products` table.
- Write a **BEFORE UPDATE** trigger on the `products` table to set the `last_modified` column to the current timestamp whenever an update occurs.

### Program:
![image](https://github.com/user-attachments/assets/24274c9d-9f8e-4037-a0d9-45b65c13e1df)

**Expected Output:**
- The `last_modified` column in the `products` table is updated automatically to the current date and time when any record is updated.

### Output:
![image](https://github.com/user-attachments/assets/189a0522-5278-4d4c-ae03-06006626975b)

---

## 4. Write a trigger to keep track of the number of updates made to a table.
**Steps:**
- Create an `audit_log` table with a counter column.
- Write an **AFTER UPDATE** trigger on the `customer_orders` table to increment the counter in the `audit_log` table every time a record is updated.

### Program:
![image](https://github.com/user-attachments/assets/05dcb8a2-2430-454f-aff5-0b7f4975d21f)


**Expected Output:**
- The `audit_log` table will maintain a count of how many updates have been made to the `customer_orders` table.

### Output:
![image](https://github.com/user-attachments/assets/385d97a3-ce79-4f0a-81fc-d8ed81a93c1d)


---

## 5. Write a trigger that checks a condition before allowing insertion into a table.
**Steps:**
- Write a **BEFORE INSERT** trigger on the `employees` table to check if the inserted salary meets a specific condition (e.g., salary must be greater than 3000).
- If the condition is not met, raise an error to prevent the insert.

### Program:
![image](https://github.com/user-attachments/assets/acb85b28-0e5d-4934-b734-b34ed27ea660)

**Expected Output:**
- If the inserted salary in the `employees` table is below the condition (e.g., salary < 3000), the insert operation is blocked, and an error message is raised, such as: `ERROR: Salary below minimum threshold.`

### Output:
![image](https://github.com/user-attachments/assets/6dbbc1c1-4150-4160-877e-45761018f104)


## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.
