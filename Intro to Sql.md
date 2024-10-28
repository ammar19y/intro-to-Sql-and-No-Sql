# **SQL Basics Guide**

## **What is SQL?**
**SQL** (Structured Query Language) is a programming language used to interact with relational databases. It allows you to **create, read, update, and delete** data. SQL is the foundation for many database systems, including MySQL, PostgreSQL, SQL Server, and SQLite.

---

## **Table of Contents**
- [**SQL Basics Guide**](#sql-basics-guide)
  - [**What is SQL?**](#what-is-sql)
  - [**Table of Contents**](#table-of-contents)
    - [**Introduction to Databases**](#introduction-to-databases)
  - [**Basic SQL Commands**](#basic-sql-commands)
    - [**1. SELECT - Querying Data**](#1-select---querying-data)
      - [**Basic Syntax:**](#basic-syntax)
      - [Example:](#example)
      - [Notes:](#notes)
    - [**2. INSERT - Adding New Data**](#2-insert---adding-new-data)
      - [**Basic Syntax:**](#basic-syntax-1)
      - [Example:](#example-1)
      - [Notes:](#notes-1)
  - [Ensure the **number of values** inserted matches the **number of specified columns**](#ensure-the-number-of-values-inserted-matches-the-number-of-specified-columns)
    - [**3.UPDATE - Modifying Data**](#3update---modifying-data)
      - [**Basic Syntax:**](#basic-syntax-2)
      - [Example:](#example-2)
      - [Notes:](#notes-2)
    - [**4.DELETE  - Removing Data**](#4delete----removing-data)
      - [**Basic Syntax:**](#basic-syntax-3)
      - [Example:](#example-3)
      - [Notes:](#notes-3)
    - [**5.DELETE  - JOIN - Linking Different Tables**](#5delete----join---linking-different-tables)
      - [Types of JOIN:](#types-of-join)
      - [**Basic Syntax:**](#basic-syntax-4)
      - [Example:](#example-4)
      - [Notes:](#notes-4)
- [**Additional Learning Resources**](#additional-learning-resources)
    - [Study Tips:](#study-tips)

---

### **Introduction to Databases**

Relational databases are structured around **tables** that consist of **rows** and **columns**. This data organization allows for logical storage that is both flexible and easy to understand.

---

## **Basic SQL Commands**

### **1. SELECT - Querying Data**
The `SELECT` statement is used to retrieve data from a specific table.

#### **Basic Syntax:**
```sql
SELECT column1, column2 
FROM table_name 
WHERE condition;
```

#### Example:
Suppose we have a table called employees with columns (name, department, salary), and we want to display the names and departments of employees with a salary greater than 5000

```sql
SELECT name, department 
FROM employees 
WHERE salary > 5000;
```

#### Notes:
**SELECT * FROM table_name;** to display **all columns.**

**WHERE** to specify **certain conditions.**

---

### **2. INSERT - Adding New Data**

The `INSERT` Used to add a row (new data) to a table.

#### **Basic Syntax:**
```sql
INSERT INTO table_name (column1, column2)
VALUES (value1, value2);
```

#### Example:
We want to add a new employee named "Sara" who works in the HR department with a salary of 6000
```sql
INSERT INTO employees (name, department, salary)
VALUES ('Sara', 'HR', 6000);
```

#### Notes:
Ensure the **number of values** inserted matches the **number of specified columns**
---

### **3.UPDATE - Modifying Data**

The `UPDATE ` Used to update specific data in a table

#### **Basic Syntax:**
```sql
UPDATE table_name 
SET column1 = value1, column2 = value2 
WHERE condition;
```

#### Example:
We want to increase the salaries of employees in the sales department by 10%.

sql
```sql
UPDATE employees 
SET salary = salary * 1.1 
WHERE department = 'Sales';
```

#### Notes:
Be sure to specify the ` WHERE` condition **to avoid updating all data in the table**.

---
### **4.DELETE  - Removing Data**

The `DELETE ` Used to delete specific data from a table

#### **Basic Syntax:**
```sql
DELETE FROM table_name 
WHERE condition;
```

#### Example:
We want to delete the data of the employee named "Ahmed".

```sql
DELETE FROM employees 
WHERE name = 'Ahmed';
```

#### Notes:
Be cautious when using` DELETE `, as it permanently **removes rows from the table**.

---
### **5.DELETE  - JOIN - Linking Different Tables**

The ` JOIN ` Used to combine data from different tables based on a relationship between them.
#### Types of JOIN:
1. ` INNER JOIN `
 
  *  Returns rows that have matches in both tables

1. ` LEFT JOIN `
  
  * Returns all rows from the left table, and matched rows from the right table

2. ` RIGHT JOIN `

  * Returns all rows from the right table, and matched rows from the left table

#### **Basic Syntax:**
```sql
SELECT table1.column, table2.column 
FROM table1 
JOIN table2 ON table1.common_column = table2.common_column;
```

#### Example:
Assuming there are two tables: employees and projects. We want to retrieve employee names and the projects they are working on

```sql
SELECT employees.name, projects.project_name 
FROM employees 
JOIN projects ON employees.id = projects.employee_id;

```

#### Notes:
`JOIN` helps **manage related data across different tables** and provides a comprehensive view.

---
# **Additional Learning Resources**
* [W3Schools SQL Tutorial](https://www.w3schools.com/sql/) : A comprehensive course for beginners explaining the basics and advanced SQL 

* [SQLBolt](https://sqlbolt.com/) : An interactive site offering lessons and practical exercises to practice SQL

* [Mode Analytics SQL Tutorial](https://mode.com/sql-tutorial) : Advanced SQL lessons for those interested in analytics and reporting

* [LeetCode SQL Practice](https://leetcode.com/studyplan/top-sql-50/) : Practice common SQL questions asked in interviews
  
---

### Study Tips:

Try **writing queries** on direct SQL training platforms.
**Don’t just read the examples**; attempt to **modify values and conditions** to see different results.**Practice** writing each type of query using small databases (like a database for students, employees, or products) to solidify practical understanding