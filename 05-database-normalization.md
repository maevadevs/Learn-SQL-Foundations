# Database Normalization

- The process of efficiently organizing data in a database
- Ensure that data is logically stored
- 2 Reasons for doing this:
  - Eliminating redundant data (e.g. storing the same data in more than one table)
  - Ensuring data dependencies make sense
- Consists of a series of guidelines that help guide you in creating a good database structure
- There are 3 `Normal Forms`

## `First Normal Form: 1NF`

- Define the data items required
  - They become the columns in a table
  - Define the types and basic constraints for each one
  - Place related data items in a table
- Ensure that there are no repeating groups of data
  - If there are, then it's time to break them into their own table
- Ensure that there is a primary key for each record

## `Second Normal Form: 2NF`

- Be in 1NF
- No partial dependences of any of the columns on the primary key
  - All the fields must depend on all the primary key(s)
  - If there are not, then it's time to break them into their own table

## `Third Normal Form: 3NF`

- Be in 2NF
- All nonprimary fields are dependent on the primary key
  - Remove all transitive dependencies
  - The amount of data duplication is reduced and therefore your database becomes smaller
  - Data Integrity
