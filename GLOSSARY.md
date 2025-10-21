# Glossary

This glossary provides definitions for key terms and concepts used throughout the High Performance PostgreSQL Workbook.

---
### Associations
Active Record model methods that describe model relationships. e.g. `has_many`, `belongs_to`, `has_one`, and `has_and_belongs_to_many`.

### Backend
A backend process with a `pid` and query

### Data Manipulation Language (DML)
A subset of SQL commands used to retrieve and manipulate data within database tables. Common DML commands include `SELECT`, `INSERT`, `UPDATE`, and `DELETE`.

### Data Definition Language (DDL)
A subset of SQL commands used to define and modify the structure of database objects, such as tables

### Declarative Model
Users write SQL statements that describe what data they want. The database management system determines how to execute the statements efficiently.

### Meta-command
A special command in `psql` that starts with a backslash (`\`). Meta-commands are used to perform various tasks, such as listing tables, describing table structures, and managing database connections.

### Migration
A set of instructions that modify the database schema. These are timestamped and committed to version control.

### Object Relational Database
A database that integrates object-oriented programming principles with relational database concepts. Database objects include tables, views, indexes, and sequences. These objects can have dependencies and use inheritance.

### Object Relational Mapping (ORM)
A programming technique that bridges object-oriented programming (OOP) languages and relational databases. It allows developers to use the syntax from the OOP language to interact with the database without needing to write raw SQL.

### Optimizer
A component of a database management system that analyzes SQL queries and determines the most efficient way to execute them. The optimizer considers various factors, such as available indexes, data distribution, and join strategies, to generate an optimal execution plan.

### Query Execution Plan
A detailed breakdown of how a database management system intends to execute a SQL query. It includes information about the order of operations, join methods, and index usage.

### Relation
Also known as `relname`, it typically refers to a table in a relational database.

### System Catalog
A PostgreSQL table or view that tracks internal information about the database objects, configurations, and states. System catalogs usually start with the prefix `pg_`.

### Transaction
A sequence of one or more SQL operations that are executed as a single logical unit of work.

### Validations
Active Record model methods that describe and enforce data correctness. e.g. `validates_presence_of`, `validates_uniqueness_of`, and `validates_numericality_of`.