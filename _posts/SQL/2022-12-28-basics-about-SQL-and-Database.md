---
layout: post
title: Basics about SQL
date: 2022-12-28
categories: [SQL]
tags: [SQL, Database]
---

# SQL
SQL is a declarative programming language.
## Declarative languages
In declarative languages such as SQL & Prolog:
* A "program" is a description of the desired result 
* The interpreter figures out how to generate the result
* (The computational processes are decided by Database management systems.)

In imperative languages such as Python & Scheme:
* A "program" is a description of computational processes 
* The interpreter carries out execution/evaluation rules

## basics
In SQL, every statement should be ended with `;`.
### select
A select statement always includes a comma-separated list of column descriptions.
A column description is an expression, optionally followed by as and a column name
```shell
sqlite> SELECT * FROM first_tb WHERE city = "new york";
new york|US
```

In practice, `select` statements are compounds of many other keywords that describe what you want more specifically and thus make it possible to solve more complicated problems.

`SELECT [columns] FROM [tables] WHERE [condition] ORDER BY [columns] LIMIT [limit];`

* `SELECT [columns]` tells SQL that we want to include the given columns in our output table; `[columns]` is a comma-separated list of column names, and * can be used to select all columns 
* `FROM [table]` tells SQL that the columns we want to select are from the given table
* `WHERE [condition]` filters the output table by only including rows whose values satisfy the given [condition], a boolean expression 
* `ORDER BY [columns]` orders the rows in the output table by the given comma-separated list of columns, add keyword `DESC` if you want descreasing order 
* `LIMIT [limit]` limits the number of rows in the output table by the integer `[limit]`

### create and drop
You can use `select` to create a table from scratch. Every `select` clause will create a row for the table. The first row should define the column names with `as`, while other rows should not repeat it. `union` is used to connect these rows together.


```shell
CREATE TABLE [table_name] AS
  SELECT [val1] AS [column1], [val2] AS [column2], ... UNION
  SELECT [val3]             , [val4]             , ... UNION
  SELECT [val5]             , [val6]             , ...;
```

The result of a `select` statement is displayed to the user, but not stored. A `create table` statement gives the result a name.
But when you use `union`, the order of the rows in the table might be different from the order of inputting. It's up to the DBMS. 


To delete the all table, use `drop table [table_name]`.
### insert and update
If you want to insert a new row with all column values, `insert into [table_name] values (col1_val, col2_val, ...);`. If you just want to insert a row with specific columns, `insert into [table_name] (col1, col5) values (col1_val, col5_val);`, the column values that are not assigned for the added row will be `null`.

In order to modify specific column values of existing rows in the table, `update [table_name] set [col1 = val1, col2 = val2] where [conditions]`

### Operators
* comparison operators: =, >, <, <=, >=, <> or != ("not equal")
* boolean operators: AND, OR 
* arithmetic operators: +, -, *, / 
* concatenation operator: ||
## Join
* `(INNER) JOIN`: Returns records that have matching values in both tables
* `LEFT (OUTER) JOIN`: Returns all records from the left table, and the matched records from the right table 
* `RIGHT (OUTER) JOIN`: Returns all records from the right table, and the matched records from the left table 
* `FULL (OUTER) JOIN`: Returns all records when there is a match in either left or right table
### inner join
To perform an inner join on two on more tables, simply list them all out in the `FROM` clause of a `SELECT` statement.
`SELECT [columns] FROM [table1], [table2], ..`. This is a shorthand for `JOIN`. A more general way is `SELECT [columns] FROM table1 INNER JOIN table2 ON table1.column_name=table2.column_name;`.

The keyword `ON` is used to specify the columns connecting tables.
## Aggregation
### Builtin aggregation functions

#### avg
The avg() function returns the average value of all non-NULL X within a group, e.g. `select avg(weight) from animals;`.
#### count
The count(X) function returns a count of the number of times that X is not NULL in a group, e.g. `select count(kind) from animals where weight > 10;`.

The count(*) function (with no arguments) returns the total number of rows in the group.

The count(distinct X) function returns a count of row with unique values for column X.

#### group_concat
The group_concat() function returns a string which is the concatenation of all non-NULL values of X. If parameter Y is present then it is used as the separator between instances of X. A comma (",") is used as the separator if Y is omitted. The order of the concatenated elements is arbitrary.

Example:
`select group_concat(kind, ";") from animals where weight > 10;`
#### max and min
The max() aggregate function returns the maximum value of all values in the group. The maximum value is the value that would be returned last in an ORDER BY on the same column. Aggregate max() returns NULL if and only if there are no non-NULL values in the group.

`select max(weight) from animals where legs > 2;`

#### sum and total
The sum() and total() aggregate functions return the sum of all non-NULL values in the group. **If there are no non-NULL input rows then sum() returns NULL but total() returns 0.0.** 

The result of total() is always a floating point value. The result of sum() is an integer value if all non-NULL inputs are integers. If any input to sum() is neither an integer nor a NULL, then sum() returns a floating point value which is an approximation of the mathematical sum.

Sum() will throw an "integer overflow" exception if all inputs are integers or NULL and an integer overflow occurs at any point during the computation. Total() never throws an integer overflow.
### group by and having
> What if we wanted to group together the values in similar rows and perform the aggregation operations within those groups? We use a GROUP BY clause.
> Just like how we can filter out rows with WHERE, we can also filter out groups with HAVING. Typically, a HAVING clause should use an aggregation function.

Example: `SELECT departure FROM flights GROUP BY departure HAVING COUNT(*) >= 2;`


## string
Use double quote to represent string.
```shell
sqlite> select "aha," || "you";
aha, you
sqlite> CREATE TABLE phrase AS SELECT "hello, world" AS s;
sqlite> select * from phrase;
hello, world
sqlite> SELECT substr(s, 4, 2) || substr(s, instr(s, " ")+1, 1) FROM phrase;
low

```




# References
1. [SQL and databases](https://cs61a.org/lab/lab13/)
2. [SQL JOIN](https://www.w3schools.com/sql/sql_join.asp)

