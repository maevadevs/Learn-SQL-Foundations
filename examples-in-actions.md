# Example In Action

```sql
/* Create a table customer with fields: id, name, age, address, salary
 * PRIMARY KEY field: id
 * NOT NULL fields: id, name, age
 * DEFAULT: salary=5000.00
 */
CREATE TABLE customers(
  id INT NOT NULL,
  name VARCHAR (20) NOT NULL,
  age INT NOT NULL,
  address CHAR (25) ,
  salary DECIMAL (18, 2) DEFAULT 5000.00,
  PRIMARY KEY (id)
);

/* Alter a field in an existing table
 * TABLE: Customer
 * Constraint 'salary' field to NOT NUll
 */
ALTER TABLE customers
  MODIFY salary DECIMAL (18, 2) NOT NULL;

/* Alter a field in an existing table
 * TABLE: Customer
 * Remove NOT NUll constraint from 'salary' field
 */
ALTER TABLE customers
  ALTER COLUMN salary DECIMAL (18, 2) NULL;

/* Alter a field in an existing table
 * TABLE: Customer
 * Change 'salary' field default to 10000.00
 */
 ALTER TABLE customers
  MODIFY salary DECIMAL (18, 2) DEFAULT 10000.00;

/* Drop a default constraint from a field in an existing table
 * TABLE: Customer
 * Drop default constraint from 'salary' field
 */
 ALTER TABLE customers
  ALTER COLUMN salary DROP DEFAULT;

/* Alter a field in an existing table
 * TABLE: Customer
 * Set UNIQE constraint on 'age' field
 */
ALTER TABLE customers
 MODIFY age INT NOT NULL UNIQUE;

/* Drop a unique constraint from a field in an existing table
 * TABLE: Customer
 * Drop unique constraint from 'age' field
 */
 ALTER TABLE customers
  ALTER COLUMN age DROP UNIQUE;

/* Add an additional primary key (create a composite key) in an existing table
 * TABLE: Customer
 * Make `name` field into a Primary Key
 */
ALTER TABLE customer
  ADD PRIMARY KEY (name);

/* Make id and name into primary keys
 * TABLE: Customer
 */
ALTER TABLE customers
  ADD CONSTRAINT PK_CUSTID PRIMARY KEY (id, name);
```
