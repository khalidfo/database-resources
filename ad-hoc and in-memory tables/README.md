# Ad-hoc in-memory tables

Ad-hoc in-memory tables refer to temporary tables created dynamically during a session to hold intermediate or temporary data. These tables exist only for the duration of the session and are typically used for storing intermediate results, performing complex calculations, or simplifying data manipulation tasks. They are not permanently stored in the database but reside in memory.

## in-memory table with integer number

```sql
SELECT *
FROM (
  VALUES(1),(2),(3)
) t(result)
```

| result  | 
| ------- | 
|    1    | 
|    2    | 
|    3    | 

## in-memory table with character

```sql
SELECT *
FROM (
  VALUES('A'),('B'),('C')
) t(Result)
```

| result  | 
| ------- | 
|    A    | 
|    B    | 
|    C    | 

## in-memory table - mix character and integer value

```sql
SELECT * FROM (
  VALUES('A'),('B'),('C'),(1),(2)
) t(result)
```

### What will the result be for this query?