# SQL Constraints

- `constraints` are the rules enforced on data columns on table
- Used to limit the type of data that can go into a table
- Ensures the accuracy and reliability of the data in the database
- Could be at the *column-level* or *table-level*

## Commonly Used Constraints

- `NOT NULL`    -- Column cannot have a `NULL` value
- `DEFAULT`     -- Provide a default value for a column
- `UNIQUE`      -- All values in the column must be unique
- `PRIMARY KEY` -- Key used to uniquely identify each records in a table
- `FOREIGN KEY` -- Key used to relate a record to another record in another table
- `CHECK`       -- Ensures that all values in a column satisfy certain conditions
- `INDEX`       -- Use to create and retrieve data from the database very quickly

## Example In Action

```sql
/* Create a table customer with fields: id, name, age, address, salary
 * PRIMARY KEY field: id
 * NOT NULL fields: id, name, age
 * DEFAULT: salary=5000.00
 */
CREATE TABLE customers(
  id INT NOT NULL,
  name VARCHAR (20) NOT NULL,
  age INT NOT NULL CHECK (age >= 18),
  address CHAR (25) ,
  salary DECIMAL (18, 2) DEFAULT 5000.00,
  driverLicenseNum INT NOT NULL UNIQUE,
  PRIMARY KEY (id)
);
```

### `NOT NULL`

- By default, a column can hold `NULL` values
- `NULL` is not allowed for a column with this constraint
- If a table is already created and a column has already been set without a `NOT NULL` constraint but need to be changed, we can use `ALTER`

```sql
/* Alter a field in an existing table
 * TABLE: Customer
 * Constraint 'salary' field to NOT NUll
 */
ALTER TABLE customers
  MODIFY salary DECIMAL (18, 2) NOT NULL;
```

- If a table is already created and a column needs to go from `NOT NULL` to be nullable, we can simply set `NULL` as a constraint using `ALTER`

```sql
/* Alter a field in an existing table
 * TABLE: Customer
 * Remove NOT NUll constraint from 'salary' field
 */
ALTER TABLE customers 
  ALTER COLUMN salary DECIMAL (18, 2) NULL;
```

### `DEFAULT`

- Provides a default value to a column when the `INSERT INTO` statement does not provide
a value
- If a table is already created and a column has already been set without a `DEFAULT` constraint but need to be changed, we can use `ALTER`

```sql
/* Alter a field in an existing table
 * TABLE: Customer
 * Change 'salary' field default to 10000.00
 */
ALTER TABLE customers
  MODIFY salary DECIMAL (18, 2) DEFAULT 10000.00;
```

- If a `DEFAULT` constraint needs to be removed from a field, we can use the `DROP` command

```sql
/* Drop a default constraint from a field in an existing table
 * TABLE: Customer
 * Drop the default constraint from 'salary' field
 */
ALTER TABLE customers
  ALTER COLUMN salary DROP DEFAULT;
```

### `UNIQUE`

- Prevents two records from having identical values in a particular column
- If a table is already created and a column needs to be `UNIQUE`, we can simply set `UNIQUE` as a constraint using `ALTER`

```sql
/* Alter a field in an existing table
 * TABLE: Customer
 * Set UNIQE constraint on 'age' field
 */
ALTER TABLE customers
 MODIFY age INT NOT NULL UNIQUE;
```

- If a `UNIQUE` constraint needs to be removed from a field, we can use the `DROP` command

```sql
/* Drop a unique constraint from a field in an existing table
 * TABLE: Customer
 * Drop unique constraint from 'age' field
 */
ALTER TABLE customers
  ALTER COLUMN age DROP UNIQUE;
```

### `PRIMARY KEY`

- A field in a table which uniquely identifies each row/record in a database table
- *Primary keys* must contain unique values
- *Primary keys* cannot be nullable
- A table can only have 1 primary key, but this can be a single field or a combination of fields
  - When using multiple fields, they are called *composite key*
- *Primary Keys* must be set during the creation of the table
- If a table is already created and a primary key needs to be added, we can simply set `ADD PRIMARY KEY` using `ALTER`. Note that the new field must have been decalred with `NOT NULL`

```sql
/* Add an additional primary key (create a composite key) in an existing table
 * TABLE: Customer
 * Make `name` field into a Primary Key
 */
ALTER TABLE customer
  ADD PRIMARY KEY (name);
```

- We can also declare multiple columns as composite keys during creation time

```sql
PRIMARY KEY (id, name)
```

- If a table is already created and a column needs to be a `PRIMARY KEY`, we can simply set `CONSTRAINT PK_CUSTID PRIMARY KEY` as a constraint using `ALTER`

```sql
/* Make id and name into primary keys
 * TABLE: Customer
 */
ALTER TABLE customers
  ADD CONSTRAINT PK_CUSTID PRIMARY KEY (id, name);
```

- We can delete the primary key of a table with `ALTER` and `DROP`

```sql
/* Drop the primary key constraint on a table
 * TABLE: Customer
 */
ALTER TABLE customers
  DROP PRIMARY KEY;
```

### `FOREIGN KEY`

- A key used to link two tables together
- Sometimes called a *Referencing Key* so we uses `references` when creating the table
- A column or a combination of columns whose values match a Primary Key in a different table

```sql
CREATE TABLE orders (
 id INT NOT NULL,
 date DATETIME,
 FOREIGN KEY customerId INT references customers (id),
 amount double,
 PRIMARY KEY (id)
);
```

- If the table is already created and a column needs to be a `FOREIGN KEY`, we can simply set `ADD FOREIGN KEY` as a constraint using `ALTER`

```sql
ALTER TABLE orders
  ADD FOREIGN KEY (customer_id) REFERENCES customers (id);
```

- We can delete the foreign key of a table with `ALTER` and `DROP`

```sql
ALTER TABLE orders
  DROP FOREIGN KEY;
 ```

### `CHECK`

- Enables a condition to check the value being entered into a record
- If the condition evaluates to `false`: the record violates the constraint and isn’t entered into the table
- If the table is already created and a column needs to have a `CHECK`, we can simply set `MODIFY` the field with the new constraint using `ALTER`

```sql
ALTER TABLE customers
  MODIFY age INT NOT NULL CHECK (age >= 18 );
```

- We can delete the check on a table's field with `ALTER` and `DROP`

```sql
ALTER TABLE CUSTOMERS
  ALTER age DROP CONSTRAINT CHECK (age >= 18 );
```

### `INDEX`

- Used to create and retrieve data from the database very quickly
- Can be created by using single or group of columns in a table
- When index is created, it is assigned a `ROWID` for each row before it sorts out the data
- Proper indexes are good for performance in large databases
- However, be careful while creating index: Selection of fields depends on what you are using in your SQL queries
- Indexes are assigned after creating a table

```sql
/* Adding an index to a specific field
 * TABLE: Customer
 * Make `address` into an indexable field
 */
CREATE INDEX idx_address
  ON customers (address);
```

- We can delete the index on a table's fields with `ALTER` and `DROP`

```sql
ALTER TABLE CUSTOMERS
  DROP INDEX idx_address;
```
