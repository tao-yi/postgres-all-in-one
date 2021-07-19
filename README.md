## PostgreSQL Database Objects

**Databases**

- A database is a container of other objects such as `tables`, `views`, `functions` and `indexes`.

**Tables**

- Tables store data. A table belongs to a database and each database has multiple tables.
- A special feature of PostgreSQL is table inheritance.

**Schemas**

- A schema is a logical container of tables and other objects inside a table.

**Tablespaces**

- Tablespaces are where PostgreSQL stores the data physically.

**Views**

- Views are named queries stored in the database. Besides the read-only views, PostgreSQL supports updatable views.

**Functions**

- A function is a reusable block of SQL code that returns a scalar value of a set of rows.

**Operators**

- Operators are symbolic functions. PostgreSQL allows you to define custom operators.

**Sequences**

- Sequences are used to manage auto-increment columns defined in a table as a serial column or an identity column.

**Foreign tables and foreign data wrapper**

- Foreign tables are virtual tables lined to data outside a PostgreSQL database. Once you've configured the link, you can query them like any other tables.

**Triggers and trigger functions**

- You will find triggers in all enterprise-level databases; triggers detect data-change events. When PostgreSQL fires a trigger, you have the opportunity to exectue trigger functions in response. A trigger can run in response to particular types of statements or in response to changes to particular rows, and can fire before or after a data-change event.

**Catalog**

Catalogs are system schemas that store PostgreSQL built-in functions and metadata. Every database contains two catalogs:

- `pg_catalog`, which holds all functions, tables, system views, casts and types packaged with PostgreSQL;
- `information_schema`, which offers views exposing metadata in a format dictated by the ANSI SQL standard

The `information_schema` catalog is one you’ll find in MySQL and SQL Server as well. The most commonly used views in the PostgreSQL information_schema are

- columns, which lists all table columns in a database;
- tables, which lists all tables (including views) in a database;
- and views, which lists all views and the associated SQL to build rebuild the view.

**Types**

Type is short for data type. Every database product and every programming language has a set of types that it understands: integers, characters, arrays, blobs, etc. PostgreSQL has composite types, which are made up of other types. Think of complex numbers, polar coordinates, vectors, or tensors as examples.

Whenever you create a new table, PostgreSQL automatically creates a composite type based on the structure of the table. This allows you to treat table rows as objects in their own right.

## Configuration Files

Three main configuration files control operations of a PostgreSQL server:

- `postgresql.conf`: controls general settings, such as memory allocation, default storage location for new databases, the IP addresses that PostgreSQL listens on, location of logs, etc.
- `pg_hba.conf`: controls access to the server, dictating which users can log in to which databases, which IP addresses can connect, and which authentication schema to accept.
- `pg_ident.onf`: If present, this file maps an authenticated OS login to a PostgreSQL user. People sometimes map the OS root account to the PostgresSQL superuser account, postgres.

## Roles = Users

PostgreSQL officially refers to users as roles.

### How to install psql

```bash
brew install libpq

echo 'export PATH="/usr/local/opt/libpq/bin:$PATH"' >> ~/.zshrc
```

### How to use psql

```bash
# using psql to connet to pg
psql -h localhost -p 5432 -d "postgres" -U postgres

# list all database
\l

# connect to database test
\c test

# create database
CREATE DATABASE test;

# drop database
DROP DATABASE test;

# list all tables and relations
\d

# list all tables
\dt

# describe database person
\d person

# delete table
DROP TABLE person

# execute command from a file
\i /Users/yitao/github/postgresql-material/person.sql
```

### How to create table

```sql
CREATE TABLE person (
  -- SERIAL = autoincrementing four-byte integer
  id SERIAL PRIMARY KEY,
  first_name VARCHAR(50) NOT NULL,
  last_name VARCHAR(50) NOT NULL,
  gender VARCHAR(6) NOT NULL,
  date_of_birth TIMESTAMP NOT NULL,
  email VARCHAR(255)
);

INSERT INTO person(first_name,last_name,gender,date_of_birth)
VALUES('Anne','Smith','FEMALE',DATE '1988-01-09');

INSERT INTO person(first_name,last_name,gender,date_of_birth,email)
VALUES('Jake','Jones','MALE',DATE '1981-02-09', 'jake.jones@hotmail.com');
```
