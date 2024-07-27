# Preparing for a SQL Interview

## 1. Understanding Various Types of Joins

### Inner Join
- **Description**: Returns only the rows that have matching values in both tables.
- **Example**: 
  ```sql
  SELECT * 
  FROM Employees 
  INNER JOIN Departments 
  ON Employees.DepartmentID = Departments.DepartmentID;
  ```

### Left Join (or Left Outer Join)
- **Description**: Returns all rows from the left table and the matched rows from the right table. If there is no match, NULL values are returned for columns from the right table.
- **Example**: 
  ```sql
  SELECT * 
  FROM Employees 
  LEFT JOIN Departments 
  ON Employees.DepartmentID = Departments.DepartmentID;
  ```

### Right Join (or Right Outer Join)
- **Description**: Returns all rows from the right table and the matched rows from the left table. If there is no match, NULL values are returned for columns from the left table.
- **Example**: 
  ```sql
  SELECT * 
  FROM Employees 
  RIGHT JOIN Departments 
  ON Employees.DepartmentID = Departments.DepartmentID;
  ```

### Full Join (or Full Outer Join)
- **Description**: Returns all rows when there is a match in one of the tables. If there is no match, NULL values are returned for columns from the table without a match.
- **Example**: 
  ```sql
  SELECT * 
  FROM Employees 
  FULL JOIN Departments 
  ON Employees.DepartmentID = Departments.DepartmentID;
  ```

### Cross Join
- **Description**: Returns the Cartesian product of both tables, i.e., every combination of rows from both tables.
- **Example**: 
  ```sql
  SELECT * 
  FROM Employees 
  CROSS JOIN Departments;
  ```

### Self Join
- **Description**: A regular join, but the table is joined with itself.
- **Example**: 
  ```sql
  SELECT A.EmployeeName, B.EmployeeName 
  FROM Employees A, Employees B 
  WHERE A.ManagerID = B.EmployeeID;
  ```

## 2. Window Functions & Their Variations

### ROW_NUMBER()
- **Description**: Assigns a unique sequential integer to rows within a partition of the result set.
- **Example**: 
  ```sql
  SELECT EmployeeName, 
         ROW_NUMBER() OVER (PARTITION BY DepartmentID ORDER BY Salary DESC) AS RowNum
  FROM Employees;
  ```

### RANK()
- **Description**: Assigns a rank to each row within a partition of the result set, with gaps in the ranking for ties.
- **Example**: 
  ```sql
  SELECT EmployeeName, 
         RANK() OVER (PARTITION BY DepartmentID ORDER BY Salary DESC) AS Rank
  FROM Employees;
  ```

### DENSE_RANK()
- **Description**: Assigns a rank to each row within a partition of the result set, without gaps in the ranking for ties.
- **Example**: 
  ```sql
  SELECT EmployeeName, 
         DENSE_RANK() OVER (PARTITION BY DepartmentID ORDER BY Salary DESC) AS DenseRank
  FROM Employees;
  ```

## 3. Distinguishing 'WHERE' vs 'HAVING'

### WHERE
- **Description**: Filters rows before any groupings are made.
- **Example**: 
  ```sql
  SELECT * 
  FROM Employees 
  WHERE Salary > 50000;
  ```

### HAVING
- **Description**: Filters rows after groupings are made, typically used with aggregate functions.
- **Example**: 
  ```sql
  SELECT DepartmentID, AVG(Salary) 
  FROM Employees 
  GROUP BY DepartmentID 
  HAVING AVG(Salary) > 50000;
  ```

## 4. Query Order of Execution

- **Description**: Understanding the order of operations in a SQL query helps in writing accurate and efficient queries.
- **Order**:
  1. **FROM**: Determines the tables and joins.
  2. **WHERE**: Filters rows.
  3. **GROUP BY**: Groups rows.
  4. **HAVING**: Filters groups.
  5. **SELECT**: Selects columns.
  6. **ORDER BY**: Orders the result.

## 5. Creating and Utilizing CTEs (Common Table Expressions)

### CTE
- **Description**: Allows you to define a temporary result set that you can reference within a SELECT, INSERT, UPDATE, or DELETE statement.
- **Example**: 
  ```sql
  WITH EmployeeCTE AS (
      SELECT EmployeeID, Salary
      FROM Employees
  )
  SELECT * 
  FROM EmployeeCTE
  WHERE Salary > 50000;
  ```

## 6. Aggregation Functions as Window Functions

### Example
- **Description**: You can use aggregation functions within window functions to perform advanced analytical queries.
- **Example**: 
  ```sql
  SELECT EmployeeName, 
         Salary, 
         SUM(Salary) OVER (PARTITION BY DepartmentID) AS TotalDepartmentSalary
  FROM Employees;
  ```

## 7. Commonly Asked Queries

### Finding Nth Highest Salary
- **Example**: 
  ```sql
  SELECT DISTINCT Salary
  FROM Employees
  ORDER BY Salary DESC
  OFFSET 2 ROWS FETCH NEXT 1 ROW ONLY;
  ```

### Calculating Cumulative Totals
- **Example**: 
  ```sql
  SELECT EmployeeName, 
         Salary, 
         SUM(Salary) OVER (ORDER BY Salary) AS CumulativeSalary
  FROM Employees;
  ```

### Implementing Self-Joins
- **Example**: 
  ```sql
  SELECT A.EmployeeName, B.EmployeeName 
  FROM Employees A
  JOIN Employees B 
  ON A.ManagerID = B.EmployeeID;
  ```

## 8. Subqueries and their Application

### Nested Queries
- **Description**: Queries within queries for performing complex data manipulations or filtering.
- **Example**: 
  ```sql
  SELECT EmployeeName
  FROM Employees
  WHERE Salary > (
      SELECT AVG(Salary)
      FROM Employees
  );
  ```

## 9. Indexing and its Importance in Query Performance

### Indexes
- **Description**: Indexes improve data retrieval speed by creating a faster search pathway.
- **Example**: 
  ```sql
  CREATE INDEX idx_salary
  ON Employees (Salary);
  ```

## 10. Handling NULL Values in SQL

### Techniques
- **Description**: Managing and working with NULL values to ensure accurate data processing.
- **Example**: 
  ```sql
  SELECT EmployeeName, 
         COALESCE(Salary, 0) AS Salary
  FROM Employees;
  ```

## 11. Joins vs. Subqueries

### Joins
- **Description**: Combine rows from two or more tables based on a related column.
- **Example**: 
  ```sql
  SELECT Employees.EmployeeName, Departments.DepartmentName
  FROM Employees
  JOIN Departments
  ON Employees.DepartmentID = Departments.DepartmentID;
  ```

### Subqueries
- **Description**: Nested queries that provide a result set to be used by the main query.
- **Example**: 
  ```sql
  SELECT EmployeeName
  FROM Employees
  WHERE DepartmentID IN (
      SELECT DepartmentID
      FROM Departments
      WHERE DepartmentName = 'Sales'
  );
  ```
