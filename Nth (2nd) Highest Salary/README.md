# 9 Approaches To Get Nth (2nd) Highest Salary 

Finding the Nth highest salary 2nd, 3rd, or nth highest in a table is a crucial and common question asked in various interviews.

## Overview

This guide demonstrates various methods to write SQL queries for finding the 2nd highest salary in a table. The example utilizes a table called Emp, containing employee details like id, name, and salary.

All SQL query is tailored for PostgreSQL and retrieves the 2nd highest salary from the Emp table.

## Emp Table Data

| id  | name      | salary |
| --- | -------   | ------ |
| 1   | Abdullah  | 30000  |
| 2   | Umar      | 80000  |
| 3   | Jubair    | 35000  |
| 4   | Jafar     | 58000  |
| 5   | Zaied     | 40000  |
| 6   | Abid      | 45000  |
| 7   | Saad      | 38000  |
| 8   | Ahmed     | 30000  |
| 9   | Kasem     | 27000  |
| 10  | Usman     | 42000 |

## Create emp Table
```sql
CREATE TABLE IF NOT EXISTS emp(
    id serial PRIMARY KEY,
    name character varying,
    salary integer    
)

```

## Insert Data To emp Table
```sql
INSERT INTO emp(name, salary)
	VALUES ('Abdullah',30000),
			('Umar',	80000),
			('Jubair',	35000),
			('Jafar',	58000),
			('Zaied',	40000),
			('Abid',	45000),
			('Saad',	38000),
			('Ahmed',	30000),
			('Kasem',	27000),
			('Usman',	42000);  
```
## Show Data From emp Table		

```sql
SELECT * FROM emp;
```
	

## Get 2nd Highest Salary Using Limit, Subquery and NOT IN

```sql

-- Approache - 01

SELECT salary 
FROM emp 
WHERE id NOT IN (		
		SELECT id 
		FROM emp 
		ORDER BY salary DESC 
		LIMIT 1 									
	) 
ORDER BY salary DESC 
LIMIT 1; 	
		
```

## Get 2nd Highest Salary Using	MAX, Less Than and Subquery

```sql

-- Approache - 02

SELECT MAX(salary) 
FROM emp
WHERE salary < (SELECT MAX(salary) FROM emp);

```

## Get 2nd Highest Salary Using Offest and Lmit

```sql

-- Approache - 03

SELECT salary 
FROM emp 
ORDER BY salary DESC 
LIMIT 1 OFFSET 1;

```


## Get 2nd Highest Salary Using Subquery, Max and Not Equal

```sql

-- Approache - 04

SELECT MAX(salary) 
FROM emp
WHERE salary != (SELECT MAX(salary) FROM emp);

```

## Get 2nd Highest Salary Using Subquery, Max and Not In	

```sql

-- Approache - 05

SELECT MAX(salary) 
FROM emp
WHERE salary NOT IN (SELECT MAX(salary) FROM emp);

```

## Get 2nd Highest Salary Using Subquery and Limit

```sql

-- Approache - 06

SELECT salary 
FROM (
		SELECT salary 
		FROM emp 
		ORDER BY salary DESC 
		LIMIT 2	
	) 
ORDER BY salary 
LIMIT 1;

```

## Get 2nd Highest Salary Using CTE and Dense Rank

```sql

-- Approache - 07

WITH RESULT AS  
(  
	SELECT 
		salary,  
		DENSE_RANK() OVER (ORDER BY salary DESC) AS denserank  
	FROM emp  
)  

SELECT salary  
FROM RESULT  
WHERE denserank = 2;

-- You can also use RANK(), ROW_NUMER() instead of DENSE_RANK()

```

## Get 2nd Highest Salary Using CTE and Limit	

```sql

-- Approache - 08

WITH RESULT AS  
(  
	SELECT salary          
	FROM emp  
	ORDER BY salary DESC
	LIMIT 2
)  

SELECT salary  
FROM RESULT  
ORDER BY salary LIMIT 1;

```

## Get 2nd Highest Salary Using Subquery, Count, Greater Than

```sql

-- Approache - 09

SELECT 
    salary 
FROM 
    emp e1
WHERE 
    1 = (
        SELECT 
            COUNT(DISTINCT salary) 
        FROM 
            emp e2 
        WHERE 
            e2.salary > e1.salary
    );
	
```	

Evaluate these alternatives based on your specific requirements and compare their performance in different scenarios.

## Performance Testing and Alternative Methods
Now, let's put the SQL query to the test with a substantial amount of data to evaluate its performance.

### Performance Testing
To assess the query's performance, consider running it on a larger dataset within your PostgreSQL environment. Measure the execution time and resource utilization to ensure efficiency, especially as the dataset size increases. 

> [!IMPORTANT]
> Feel free to share these valuable insights with others so that they can benefit from the solutions provided. Sharing knowledge fosters a collaborative learning environment and helps the community understand various approaches to SQL problem-solving. Whether it's discussing performance testing or exploring alternative methods, spreading the information can empower others in their SQL journey. Don't hesitate to pass along this resourceful content to contribute to the collective knowledge base.
