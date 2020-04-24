# Basics

- SQL - Structured Query Language for RDBMS
- RDBMS - Relational DataBase Management System
- Example of RDBMS - MS SQL Server, MySQL, MariaDB, Oracle, Postgre, Sybase, Informix
- Different Dialects
  - T-SQL (MSSQL)
  - PL/SQL (Oracle)
  - ANSI SQL (Standard)

## Why SQL

- Access data in RDBMS
- Describe bata
- Define and manipulate data
- Embed within other programs using SQL modules and libraries
- Create and drop databases and tables
- Create *Views*, *Stored Procedures*, *Functions*
- Set permissions on *Tables*, *Stored Procedures*, *Views*

## Components in The Process

- Query Dispatcher
- Optimization Engines
- Classic Query Engine: Handles all non-SQL queries
- SQL Query Engine

## SQL Architecture

```format
[SQL Query] --> [Query Language Processor] --> [DBMS Engine] --> [Physical Database]
                            +                       +
                         [Parser]              [File Manager]
                        [Optimizer]            [Transact SQL]
```
