# Nth Highest Salary

Finding the Nth highest salary (2nd, 3rd, or nth highest) in a table is a crucial and common question asked in various interviews.

## Overview

This guide demonstrates various methods to write SQL queries for finding the 2nd highest salary in a table. The example utilizes a table called Emp, containing employee details like id, name, and salary.

## Emp Table Data

| id  | name    | salary |
| --- | ------- | ------ |
| 1   | Abdullah    | 30000  |
| 2   | Umar | 80000  |
| 3   | Jubair | 35000  |
| 4   | Abu | 58000  |
| 5   | Zaied   | 40000  |
| 6   | Abid  | 45000  |
| 7   | Saad | 38000  |
| 8   | Ahmed    | 30000  |
| 9   | Kasem    | 27000  |
| 10  | Usman  | 420000 |

## SQL Query Example

```sql
-- Example to find the Nth highest salary (replace N with the desired rank)
WITH RankedSalaries AS (
    SELECT 
        SALARY,
        DENSE_RANK() OVER (ORDER BY SALARY DESC) AS SalaryRank
    FROM 
        Emp
)
SELECT 
    SALARY
FROM 
    RankedSalaries
WHERE 
    SalaryRank = N;
