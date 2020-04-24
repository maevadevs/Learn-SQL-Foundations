# SELECT FUNCTIONS

- These functions can be used together with `SELECT` to fine-tune the `result-set`
- We can always re-assign a new column alias name to store the result using the `AS` keyword
- But remember that an alias only exists for the duration of the query

## `MIN(col)` and `MAX(col)`

- The `MIN()` function returns the smallest value of the selected column
- The `MAX()` function returns the largest value of the selected column

```sql
SELECT MIN(columnName)
FROM tableName
WHERE condition;

SELECT MIN(columnName) AS minimum
FROM tableName
WHERE condition;

SELECT MAX(columnName)
FROM tableName
WHERE condition;
```

## `COUNT(col)`

- The `COUNT()` function returns the number of rows that matches a specified criteria
- Note: `NULL` values are not counted

```sql
SELECT COUNT(columnName) AS count
FROM tableName
WHERE condition;
```

## `AVG(col)`

- The `AVG()` function returns the average value of a numeric column
- Note: `NULL` values are ignored

```sql
SELECT AVG(columnName) AS average
FROM tableName
WHERE condition;
```

## `SUM(col)`

- The `SUM()` function returns the total sum of a numeric column
- Note: `NULL` values are ignored

```sql
SELECT SUM(columnName) AS sum
FROM tableName
WHERE condition;
```
