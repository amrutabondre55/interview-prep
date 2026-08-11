Absolutely. Since you have only **1.5 days**, here is a **SQL interview-focused cheat sheet**. Don't just memorize definitions—learn the **question + answer + example + interview line**.

I'll use these two tables throughout.

### `employee`

| id | name  | salary | dept_id |
| -: | ----- | -----: | ------: |
|  1 | Amit  |  50000 |      10 |
|  2 | Rahul |  70000 |      10 |
|  3 | Priya |  60000 |      20 |
|  4 | Neha  |  90000 |      10 |
|  5 | Sneha |  60000 |      20 |

### `department`

| dept_id | dept_name |
| ------: | --------- |
|      10 | IT        |
|      20 | HR        |
|      30 | Finance   |

---

# 🔴 SQL FUNDAMENTALS

## 1. What is SELECT?

### Interview question

> What is the purpose of SELECT in SQL?

### Interview-friendly answer

> `SELECT` is used to retrieve data from one or more tables. We can select specific columns or all columns depending on our requirement.

### Example

```sql
SELECT name, salary
FROM employee;
```

Output:

```text
Amit    50000
Rahul   70000
Priya   60000
Neha    90000
Sneha   60000
```

All columns:

```sql
SELECT *
FROM employee;
```

### Interview line

> I use SELECT to retrieve the required columns or records from the database.

---

# 2. What is WHERE?

### Interview question

> What is the purpose of WHERE?

### Answer

> `WHERE` is used to filter individual rows based on a condition.

### Example

Find employees earning more than 60,000:

```sql
SELECT *
FROM employee
WHERE salary > 60000;
```

Result:

```text
Rahul  70000
Neha   90000
```

### Important

`WHERE` filters **rows before grouping**.

---

# 3. What is GROUP BY?

### Interview question

> Why do we use GROUP BY?

### Answer

> `GROUP BY` is used to group rows having the same value in one or more columns. It is commonly used with aggregate functions like COUNT, SUM, AVG, MAX and MIN.

### Example

Find employee count by department:

```sql
SELECT dept_id, COUNT(*) AS employee_count
FROM employee
GROUP BY dept_id;
```

Result:

```text
10 → 3
20 → 2
```

### Interview line

> GROUP BY creates groups, and then aggregate functions can perform calculations on each group.

---

# 4. What is HAVING?

### Interview question

> What is HAVING and how is it different from WHERE?

### Answer

> `HAVING` is used to filter groups after `GROUP BY`, whereas `WHERE` filters individual rows before grouping.

### Example

Find departments having more than 2 employees:

```sql
SELECT dept_id, COUNT(*) AS employee_count
FROM employee
GROUP BY dept_id
HAVING COUNT(*) > 2;
```

Result:

```text
10 → 3
```

### ⭐ Remember

```text
WHERE
   ↓
Filters rows

GROUP BY
   ↓
Creates groups

HAVING
   ↓
Filters groups
```

### Interview answer

> WHERE works on rows, while HAVING works on grouped results.

---

# 5. What is ORDER BY?

### Interview question

> What is ORDER BY?

### Answer

> `ORDER BY` is used to sort the result set in ascending or descending order.

### Ascending

```sql
SELECT *
FROM employee
ORDER BY salary ASC;
```

### Descending

```sql
SELECT *
FROM employee
ORDER BY salary DESC;
```

### Default

```text
ASC
```

### Interview line

> I use ORDER BY when I need the result in a specific sorting order.

---

# 6. What is DISTINCT?

### Interview question

> What is DISTINCT?

### Answer

> `DISTINCT` removes duplicate values from the result set.

### Example

```sql
SELECT DISTINCT salary
FROM employee;
```

Result:

```text
50000
60000
70000
90000
```

Without `DISTINCT`:

```text
50000
70000
60000
90000
60000
```

### Interview line

> DISTINCT removes duplicate rows from the selected result.

---

# 7. What is LIKE?

### Interview question

> How do you search for a pattern using SQL?

Use `LIKE`.

### Names starting with A

```sql
SELECT *
FROM employee
WHERE name LIKE 'A%';
```

Result:

```text
Amit
```

### Names ending with a

```sql
SELECT *
FROM employee
WHERE name LIKE '%a';
```

### Names containing "it"

```sql
SELECT *
FROM employee
WHERE name LIKE '%it%';
```

### Important wildcards

```text
% → Zero or more characters
_ → Exactly one character
```

### Interview line

> LIKE is used for pattern matching, where `%` represents multiple characters and `_` represents one character.

---

# 8. What is BETWEEN?

### Interview question

> How do you find employees whose salary is between 50,000 and 70,000?

```sql
SELECT *
FROM employee
WHERE salary BETWEEN 50000 AND 70000;
```

### Important

`BETWEEN` is generally **inclusive** of both boundaries.

So this includes:

```text
50000
60000
70000
```

### Interview line

> BETWEEN is used to filter values within a range, and the boundary values are included.

---

# 9. What is IN?

### Interview question

> How do you filter records for multiple specific values?

```sql
SELECT *
FROM employee
WHERE dept_id IN (10, 20);
```

Instead of:

```sql
WHERE dept_id = 10
   OR dept_id = 20;
```

### Interview line

> IN is useful when I want to check whether a value matches any value from a given list.

---

# 10. What is CASE in SQL?

### Interview question

> How do you implement conditional logic in SQL?

Use `CASE`.

### Example

```sql
SELECT name,
       salary,
       CASE
           WHEN salary >= 80000 THEN 'High'
           WHEN salary >= 60000 THEN 'Medium'
           ELSE 'Low'
       END AS salary_category
FROM employee;
```

Output:

```text
Amit    50000   Low
Rahul   70000   Medium
Priya   60000   Medium
Neha    90000   High
Sneha   60000   Medium
```

### Interview line

> CASE is used to implement conditional logic and derive values based on conditions.

---

# 11. What are Aggregate Functions?

### Interview question

> What are aggregate functions in SQL?

### Answer

> Aggregate functions perform calculations on multiple rows and return a single result for each group or for the entire result set.

Important functions:

```text
COUNT()
SUM()
AVG()
MAX()
MIN()
```

### Examples

```sql
SELECT COUNT(*)
FROM employee;
```

```sql
SELECT MAX(salary)
FROM employee;
```

```sql
SELECT MIN(salary)
FROM employee;
```

```sql
SELECT AVG(salary)
FROM employee;
```

```sql
SELECT SUM(salary)
FROM employee;
```

### Department-wise example

```sql
SELECT dept_id,
       COUNT(*) AS total_employees,
       AVG(salary) AS average_salary,
       MAX(salary) AS highest_salary
FROM employee
GROUP BY dept_id;
```

### Interview line

> Aggregate functions perform calculations over multiple rows, usually along with GROUP BY for department-wise or category-wise analysis.

---

# 🔥 JOINS

This is **very important for your interview**.

## 12. What is a JOIN?

### Interview question

> What is a JOIN and why do we use it?

### Interview-friendly answer

> A JOIN is used to combine data from two or more tables based on a related column. For example, an employee table may contain `dept_id`, while department information is stored in a separate department table. We can join these tables using `dept_id`.

```text
employee
   |
   | dept_id
   ↓
department
```

---

# 13. What is INNER JOIN?

### Interview question

> Explain INNER JOIN with a real example.

### Answer

> INNER JOIN returns only the records that have matching values in both tables.

### Query

```sql
SELECT e.name,
       d.dept_name
FROM employee e
INNER JOIN department d
ON e.dept_id = d.dept_id;
```

Result:

```text
Amit    IT
Rahul   IT
Priya   HR
Neha    IT
Sneha   HR
```

Finance doesn't appear because no employee belongs to department 30.

### Easy way

```text
Table A ∩ Table B
```

### Interview line

> INNER JOIN gives only matching records from both tables.

---

# 14. What is LEFT JOIN?

### Interview question

> Explain LEFT JOIN.

### Answer

> LEFT JOIN returns all records from the left table and matching records from the right table. If there is no match, columns from the right table will contain NULL.

### Query

```sql
SELECT e.name,
       d.dept_name
FROM employee e
LEFT JOIN department d
ON e.dept_id = d.dept_id;
```

Since all employees have a department in our example, all match.

But suppose:

```text
Employee:
Raj → dept_id = 40
```

There is no department 40.

Result:

```text
Raj    NULL
```

### Interview line

> LEFT JOIN keeps all records from the left table even if there is no matching record in the right table.

---

# 15. What is RIGHT JOIN?

### Answer

> RIGHT JOIN returns all records from the right table and matching records from the left table. If there is no match, the left-side columns become NULL.

### Query

```sql
SELECT e.name,
       d.dept_name
FROM employee e
RIGHT JOIN department d
ON e.dept_id = d.dept_id;
```

Result could include:

```text
Amit     IT
Rahul    IT
Priya    HR
Neha     IT
Sneha    HR
NULL     Finance
```

Finance appears even though there are no employees in it.

### Interview line

> RIGHT JOIN keeps all records from the right table even when there is no matching record in the left table.

---

# 16. What is FULL OUTER JOIN?

### Answer

> FULL OUTER JOIN returns all records from both tables. Matching records are combined, and non-matching records from either side contain NULL values.

Conceptually:

```text
LEFT JOIN
+
RIGHT JOIN
```

### Query

In databases that support it:

```sql
SELECT e.name,
       d.dept_name
FROM employee e
FULL OUTER JOIN department d
ON e.dept_id = d.dept_id;
```

Result includes:

```text
Employee matches → employee + department
Employee without department → employee + NULL
Department without employees → NULL + department
```

### Important interview note

> MySQL does not directly support `FULL OUTER JOIN`; it can be simulated using `LEFT JOIN` and `RIGHT JOIN` with `UNION`.

Example:

```sql
SELECT e.name, d.dept_name
FROM employee e
LEFT JOIN department d
ON e.dept_id = d.dept_id

UNION

SELECT e.name, d.dept_name
FROM employee e
RIGHT JOIN department d
ON e.dept_id = d.dept_id;
```

---

# 17. What is SELF JOIN?

🔥 Frequently asked.

### Interview question

> What is a SELF JOIN? Give me a real-world example.

### Answer

> A SELF JOIN is when we join a table with itself. It is useful when rows in the same table have a relationship with other rows in that table.

### Example

Suppose employee table contains:

| id | name  | manager_id |
| -: | ----- | ---------: |
|  1 | Amit  |       NULL |
|  2 | Rahul |          1 |
|  3 | Priya |          1 |

We want:

```text
Employee → Manager
```

### Query

```sql
SELECT e.name AS employee,
       m.name AS manager
FROM employee e
LEFT JOIN employee m
ON e.manager_id = m.id;
```

Result:

```text
Amit    NULL
Rahul   Amit
Priya   Amit
```

### How?

```text
employee e
    ↓
Employee

employee m
    ↓
Manager
```

Same table, different aliases.

### Interview line

> SELF JOIN is useful for hierarchical relationships such as employee-manager relationships, where both employee and manager information exists in the same table.

---

# ⭐ JOIN Cheat Sheet

Remember this picture:

```text
INNER JOIN
Only matching
       A ∩ B


LEFT JOIN
All A + matching B


RIGHT JOIN
Matching A + all B


FULL JOIN
All A + All B


SELF JOIN
Table A ↔ Same Table A
```

---

# 🔥 SUBQUERIES

## 18. What is a Subquery?

### Interview question

> What is a subquery?

### Answer

> A subquery is a query written inside another SQL query. The inner query produces a result that is used by the outer query.

Example:

```sql
SELECT *
FROM employee
WHERE salary > (
    SELECT AVG(salary)
    FROM employee
);
```

Here:

```sql
SELECT AVG(salary)
FROM employee
```

is the subquery.

---

# 19. What is a Single-Row Subquery?

### Interview question

> What is a single-row subquery?

### Answer

> A single-row subquery returns exactly one value or one row, so we can use operators like `=`, `>`, `<`, `>=` etc.

### Example

Find employees earning more than average salary:

```sql
SELECT *
FROM employee
WHERE salary > (
    SELECT AVG(salary)
    FROM employee
);
```

The inner query:

```sql
SELECT AVG(salary)
FROM employee;
```

returns one value.

Therefore:

```text
salary > average_salary
```

works.

### Interview line

> A single-row subquery returns one value, so comparison operators like `=`, `>`, `<` can be used with it.

---

# 20. What is a Multiple-Row Subquery?

### Interview question

> What is a multiple-row subquery?

### Answer

> A multiple-row subquery returns multiple values. Therefore, we generally use operators such as `IN`, `ANY`, or `ALL`.

### Example

Find employees working in IT or HR:

```sql
SELECT *
FROM employee
WHERE dept_id IN (
    SELECT dept_id
    FROM department
    WHERE dept_name IN ('IT', 'HR')
);
```

The subquery can return:

```text
10
20
```

So we use:

```sql
IN
```

### Important

Don't do:

```sql
WHERE dept_id = (
    SELECT dept_id
    ...
)
```

if the subquery can return multiple rows.

Use:

```sql
WHERE dept_id IN (...)
```

### Interview line

> A multiple-row subquery can return more than one value, so operators like IN, ANY, or ALL are generally used.

---

# 🔥 21. What is a Correlated Subquery?

This is more advanced and **very good to know for your interview**.

### Interview question

> What is a correlated subquery?

### Interview-friendly answer

> A correlated subquery is a subquery that depends on the current row of the outer query. Unlike a normal subquery, it cannot be evaluated independently because it references a column from the outer query.

### Example

Find employees whose salary is greater than the **average salary of their own department**.

```sql
SELECT e.name,
       e.salary,
       e.dept_id
FROM employee e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employee e2
    WHERE e2.dept_id = e.dept_id
);
```

### Understand this part carefully:

Outer query:

```sql
FROM employee e
```

For each employee, the subquery checks:

```sql
WHERE e2.dept_id = e.dept_id
```

So if current employee is from IT:

```text
Current employee
      ↓
IT department
      ↓
Calculate IT average
      ↓
Compare employee salary
```

Then it does the same for HR.

### Why is it called correlated?

Because inner query depends on:

```sql
e.dept_id
```

from the outer query.

### Interview line

> A correlated subquery depends on the current row of the outer query. It is useful when the comparison needs to be performed against a value calculated for each outer row, such as comparing an employee's salary with their department's average salary.

---

# ⭐ Normal vs Correlated Subquery

This is important.

### Normal Subquery

```sql
SELECT *
FROM employee
WHERE salary > (
    SELECT AVG(salary)
    FROM employee
);
```

Inner query is independent.

```text
Inner query
    ↓
One result
    ↓
Outer query
```

### Correlated

```sql
SELECT e.*
FROM employee e
WHERE salary > (
    SELECT AVG(e2.salary)
    FROM employee e2
    WHERE e2.dept_id = e.dept_id
);
```

Inner query depends on outer query.

```text
Outer row
   ↓
Inner query
   ↓
Result
   ↓
Compare
   ↓
Next outer row
   ↓
Inner query again
```

### Interview answer

> A normal subquery can execute independently, while a correlated subquery depends on values from the outer query and is logically evaluated for each outer row.

---

# 🔥 VERY IMPORTANT INTERVIEW DIFFERENCES

## WHERE vs HAVING

Say:

> WHERE filters individual rows before grouping, whereas HAVING filters groups after GROUP BY.

---

## INNER JOIN vs LEFT JOIN

Say:

> INNER JOIN returns only matching records from both tables, while LEFT JOIN returns all records from the left table and matching records from the right table.

---

## WHERE vs ON in JOIN

You may get this follow-up.

### `ON`

Defines **how tables are joined**.

```sql
SELECT *
FROM employee e
JOIN department d
ON e.dept_id = d.dept_id;
```

### `WHERE`

Filters the final rows.

```sql
SELECT *
FROM employee e
JOIN department d
ON e.dept_id = d.dept_id
WHERE e.salary > 60000;
```

---

# ⭐ SQL Interview Rapid-Fire

Practice answering these aloud:

### Q1. What is GROUP BY?

> GROUP BY groups rows having the same values and is generally used with aggregate functions.

### Q2. Why HAVING instead of WHERE?

> HAVING filters aggregated groups, while WHERE filters individual rows.

### Q3. What is DISTINCT?

> DISTINCT removes duplicate rows from the selected result.

### Q4. What is INNER JOIN?

> It returns only matching records from both tables.

### Q5. What is LEFT JOIN?

> It returns all records from the left table and matching records from the right table.

### Q6. What is SELF JOIN?

> It is joining a table with itself, commonly used for hierarchical relationships like employee-manager.

### Q7. What is a subquery?

> A query inside another query.

### Q8. Single-row vs multiple-row subquery?

> Single-row returns one value and generally uses operators like `=`, `>`, `<`; multiple-row returns multiple values and generally uses `IN`, `ANY`, or `ALL`.

### Q9. What is correlated subquery?

> A subquery that depends on the outer query's current row.

### Q10. What are aggregate functions?

> Functions such as COUNT, SUM, AVG, MAX and MIN that perform calculations over multiple rows.

---

# 🚨 For Your Smart Analytics Interview — Prioritize These

With your **1.5-day deadline**, learn these **first**:

### 🔴 Must know perfectly

```text
SELECT
WHERE
GROUP BY
HAVING
ORDER BY
DISTINCT
Aggregate Functions

INNER JOIN
LEFT JOIN
SELF JOIN

Subquery
Single-row vs Multiple-row
Correlated Subquery
```

### 🟠 Know after that

```text
RIGHT JOIN
FULL OUTER JOIN
LIKE
BETWEEN
IN
CASE
```

### ⭐ Most important SQL flow to understand

```text
SELECT
  ↓
FROM / JOIN
  ↓
WHERE
  ↓
GROUP BY
  ↓
HAVING
  ↓
ORDER BY
```

**One correction to remember:** this is the logical processing idea, not necessarily the physical execution order used internally by the database optimizer.

If the interviewer asks you **"Write a query"**, don't rush. First identify:

**What tables? → What relationship? → What rows? → Group needed? → Aggregate needed? → Filter before/after grouping? → Sort needed?**

That thought process will help you solve unfamiliar SQL questions too.
