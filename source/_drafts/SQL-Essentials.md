---
title: SQL Essentials
tags:
---

## Database
- To show the list of database we use `SHOW DATABASES;`.
- To create a database we run `CREATE DATABASE <database-name>;`.
- To change to a database we run the command `USE DATABASE <database-name>;`.
- To show the tables in a database we run `SHOW TABLES;`.

## Table
- To create a table we run the following command.
```sql
CREATE TABLE employees(
	name VARCHAR(30),
	age INTEGER,
	designation VARCHAR(30)
);
```
- To show the structure of a table we run `DESC <table-name>;`. 
- We can also use the command `DESCRIBE <table-name>`.
- We can also use the command `EXPLAIN <table-name>;`.

## Inserting records
- `INSERT INTO employees VALUES("Raj Abishek",20,"Staff Member");`. If we use this command we have to specify all the values in the same order as the columns were created.
- To not specify all values or to not pass the values in the same order we have to use `INSERT INTO employees(designation,name) VALUES("Staff Member","Raj Abishek");`. The values for the non entered columns will be `NULL`.

## Selecting
- `SELECT * FROM employees;` will show all the records and columns. 
- To restrict the columns `SELECT name FROM employees;`.

## Data types
