# SELECT Statements

- Used to select data from a database
- The data returned is stored in a result table, called the `result-set`
- Select the column names and return all their values from the given table
- We can also select all columns at once with `*` and return all their values

```sql
SELECT column1, column2...columnN
FROM tableName;

SELECT *
FROM tableName;
```

## SELECT...DISTINCT

- By default, `SELECT` returns all the values
- Using `DISTINCT` returns *only distinct (different) values*, without duplicates, from the given table
- If multiple columns given, the distinct part will be the combination (as in, if you hash each record, they will all be different)
- Note: `DISTINCT` is not bound to `SELECT` but to the columns

```sql
SELECT DISTINCT column1, column2...columnN
FROM tableName;
```

## SELECT...WHERE

- Used to extract only those records that fulfill a specified condition and basically appending a filter on the query
- Condition requires strings with single quotes, number or boolean
- Possible Operators: `=`, `>`, `<`, `>=`, `<=`, `<> | !=`, `IN`, `BETWEEN`, `LIKE`

```sql
SELECT column1, column2...columnN
FROM tableName
WHERE condition=something;
```

## SELECT...WHERE EXISTS

- The `EXISTS` operator is used to test for the existence of any record in a subquery
- The `EXISTS` operator returns true if the subquery returns one or more records
- We can also use it with `NOT` to run the non-existence of any record in a subquery

```sql
SELECT column1, column2...columnN
FROM tableName
WHERE EXISTS (
  SELECT columnName
  FROM tableName
  WHERE condition
);

SELECT column1, column2...columnN
FROM tableName
WHERE NOT EXISTS (
  SELECT columnName
  FROM tableName
  WHERE condition
);
```

Example: Fetch the first and last name of the customers who placed at least one order

```sql
SELECT fname, lname
FROM Customers
WHERE EXISTS (
  SELECT *
  FROM Orders
  WHERE Customers.customerId = Orders.customerId
);
```

## SELECT...HAVING

- The `HAVING` clause was added to SQL because the `WHERE` keyword could not be used with aggregate functions (`COUNT`, `MAX`, `MIN`, `SUM`, `AVG`)

```sql
SELECT column1, column2...columnN
FROM tableName
WHERE condition /* Using simple condition here */
HAVING condition /* Using Aggregate function condition here */
```

## SELECT...WHERE/HAVING...ANY/ALL

- `ANY` and `ALL` operators are used with a `WHERE` or `HAVING`
- `ANY` operator returns `true` if any of the subquery values meet the condition
- `ALL` operator returns `true` if all of the subquery values meet the condition
- The operator must be a standard comparison operator: `=`, `<>`, `!=`, `>`, `>=`, `<`, `<=`

```sql
SELECT column1, column2...columnN
FROM tableName
WHERE columnName [operator] ANY (
  SELECT columnName FROM tableName WHERE condition
);

SELECT column1, column2...columnN
FROM tableName
WHERE columnName [operator] ALL (
  SELECT columnName FROM tableName WHERE condition
);
```

## SELECT...WHERE...AND/OR/NOT

- Used to combine conditions in `WHERE`
- The `AND` operator displays a record if all the conditions separated by `AND` are TRUE
- The `OR` operator displays a record if any of the conditions separated by `OR` is TRUE
- The `NOT` operator displays a record if the condition(s) is `NOT` TRUE
- Note: These operators should only be used on a one-table basis

```sql
SELECT column1, column2...columnN
FROM tableName
WHERE condition1 AND condition2;

SELECT column1, column2...columnN
FROM tableName
WHERE condition1 OR condition2;

SELECT column1, column2...columnN
FROM tableName
WHERE NOT condition;
```

## SELECT...WHERE...IN/NOT IN

- The `IN` operator allows to specify multiple values in a `WHERE` clause
- It is a shorthand for multiple `OR` conditions
- We can also combine it with `NOT` for negation

```sql
SELECT column1, column2...columnN
FROM tableName
WHERE columnName IN (val1, val2,..valN);

SELECT column1, column2...columnN
FROM tableName
WHERE columnName NOT IN (val1, val2,..valN);
```

## SELECT...WHERE...BETWEEN

- The `BETWEEN` operator selects values within a given range
- The values can be numbers, text, or dates
  - Dates format: #01/07/1996# or '1996-07-01'
- The `BETWEEN` operator is **inclusive**: `[begin, end]`
- We can also combine it with `NOT` for negation

```sql
SELECT column1, column2...columnN
FROM tableName
WHERE columnName BETWEEN val1 AND val2;

SELECT column1, column2...columnN
FROM tableName
WHERE columnName NOT BETWEEN val1 AND val2;
```

## SELECT...WHERE...LIKE

- The `LIKE` operator is used in a `WHERE` clause to search for a specified pattern in a column
- We can use wildcards for the pattern (Check out sql-select-wildcards)
- We can also combine any number of conditions using `AND` or `OR` operators
- We can also combine it with `NOT` for negation

```sql
SELECT column1, column2...columnN
FROM tableName
WHERE columnName LIKE pattern;

SELECT column1, column2...columnN
FROM tableName
WHERE columnName NOT LIKE pattern;
```

## SELECT...WHERE...IS NULL/IS NOT NULL

- The `IS NULL` operator is used to test for empty values (`NULL` values)
- The `IS NOT NULL` operator is used to test for non-empty values (not `NULL` values)
- It is not possible to test for `NULL` values with comparison operators
- We will use the `IS NULL` and `IS NOT NULL` operators instead

```sql
SELECT column1, column2...columnN
FROM tableName
WHERE columnName IS NULL;

SELECT column1, column2...columnN
FROM tableName
WHERE columnName IS NOT NULL;
```

## SELECT...ORDER BY

- The `ORDER BY` keyword is used to sort the result-set in ascending or descending order by a specific column
- It sorts the records in ascending order by default
  - Use `DESC` for changing the order
  - `ASC` can always be specified as well when needed

```sql
SELECT column1, column2...columnN
FROM tableName
ORDER BY columnName;

SELECT column1, column2...columnN
FROM tableName
WHERE condition
ORDER BY columnName DESC;
```

## SELECT...GROUP BY

- The `GROUP BY` statement group rows that have the same values into summary rows
- The `GROUP BY` statement is often used with aggregate functions (`COUNT`, `MAX`, `MIN`, `SUM`, `AVG`) to group the result-set by one or more columns

```sql
SELECT SUM(columnName) AS sum
FROM tableName
WHERE condition
GROUP BY columnName;
```

## SELECT TOP

- Used to specify the number of records to return
- Useful on large tables with thousands of record
  - Returning a large number of records can impact performance
- Note: Not all RDBMS support `TOP`
  - In other RDBMS, it could be `LIMIT` or `ROWNUM`

```sql
/* MSSQL */
SELECT TOP [number | x PERCENT] column1, column2...columnN
FROM tableName
WHERE condition;
/* MySQL */
SELECT column1, column2...columnN
FROM tableName
WHERE condition
LIMIT [number];
/* Oracle */
SELECT column1, column2...columnN
FROM tableName
WHERE ROWNUM <= [number];
```

## SELECT...AS

- Used to give a table, or a column in a table, a temporary alias name
- Aliases are often used to make column names more readable
- Note: An alias only exists for the duration of the query
- Note: It requires double quotation marks or square brackets if the alias name contains spaces
- We can concatenate field names (sometimes need CONCAT()) to create a summary field
- We can also alias tables to make `JOIN` easy to operate
- Aliases can be useful when:
  - There are more than one table involved in a query
  - Functions are used in the query
  - Column names are big or not very readable
  - Two or more columns are combined together

```sql
SELECT column1 AS alias1, column2 AS alias2...columnN AS aliasN
FROM tableName as tb;

SELECT customerName, address + ', ' + postalCode + ' ' + city + ', ' + country AS address
FROM Customers;

SELECT tb1.column1 AS alias1, tb2.column1 AS alias2
FROM tableName1 as tb1, tableName2 as tb2
INNER JOIN ...
WHERE alias1='xyz';
```
