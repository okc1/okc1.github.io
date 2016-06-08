---
layout: post
title: "[CC150v4] 15.2 SQL Types of Join "
comments: true
category: CC150v4

---

### Question

> What are the different types of joins? Please explain how they differ and why certain types are better in certain situations. 

### Implicit and explicit

The "__explicit join notation__" uses the JOIN keyword. The "__implicit join notation__" simply lists the tables for joining, in the FROM clause of the SELECT statement. 

Example of an explicit cross join:

    SELECT *
    FROM employee CROSS JOIN department;

Example of an implicit cross join:

    SELECT *
    FROM employee, department;

### Different Types

1. INNER JOIN: Returns all rows when __there is matching values__ in BOTH tables. 

1. OUTER JOIN: [An outer join](http://en.wikipedia.org/wiki/Join_(SQL)) __does not require each record__ in the two joined tables to have a matching record. 

    1. LEFT JOIN: Return all rows from the left table, and the matched rows from the right table

    1. RIGHT JOIN: Return all rows from the right table, and the matched rows from the left table

    1. FULL JOIN: Return all rows when there is a match in ONE of the tables. If no matching record was found then the corresponding result fields will have a NULL value. 

[source](http://www.w3schools.com/sql/sql_join.asp)
