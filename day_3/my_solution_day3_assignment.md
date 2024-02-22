### Introduction ###

 - Taking Ankit's [Namaste Sql paid course](https://www.namastesql.com/s/courses/6301f405e4b0238f71788354/take) and below are solutions for Day 3 assignment.
 - I used Microsoft SQL server to solve the problems.
 - If you want to replicate the result use [Orders](https://raw.githubusercontent.com/mayankdubey1996/namaste_sql_assignment/main/day_3/orders_table_create_inserts.sql) table to create the table and copy the data.  

***Note: please do not use any functions which are not taught in the class. you need to solve the questions only with the concepts that have been discussed so far.***

#### 1- write a sql to get all the orders where customers name has "a" as second character and "d" as fourth character (58 rows)

**Answer:**

````sql
SELECT *
FROM   orders
WHERE  customer_name LIKE '_a__d%' 
````


#### 2- write a sql to get all the orders placed in the month of dec 2020 (352 rows) 

**Answer:**

````sql
SELECT *
FROM   orders
WHERE  order_date BETWEEN '2020-12-01' AND '2020-12-31' 
````


#### 3- write a query to get all the orders where ship_mode is neither in 'Standard Class' nor in 'First Class' and ship_date is after nov 2020 (944 rows)

**Answer:**

````sql
SELECT *
FROM   orders
WHERE  ship_mode NOT IN ( 'Standard Class', 'First Class' )
       AND ship_date >= '2020-12-01' 
````


#### 4- write a query to get all the orders where customer name neither start with "A" and nor ends with "n" (9815 rows)

**Answer:**

````sql
SELECT *
FROM   orders
WHERE  customer_name NOT LIKE 'A%'
        OR customer_name NOT LIKE '%n' 
````

#### 5- write a query to get all the orders where profit is negative (1871 rows)

**Answer:**

````sql
SELECT *
FROM   orders
WHERE  profit < 0; 
````

#### 6- write a query to get all the orders where either quantity is less than 3 or profit is 0 (3348)

**Answer:**

````sql
SELECT *
FROM   orders
WHERE  quantity < 3
        OR profit = 0; 
````

#### 7- your manager handles the sales for South region and he wants you to create a report of all the orders in his region where some discount is provided to the customers (815 rows)

**Answer:**

````sql
SELECT *
FROM   orders
WHERE  region = 'South'
       AND discount > 0; 
````

#### 8- write a query to find top 5 orders with highest sales in furniture category 

**Answer:**

````sql
SELECT TOP 5 *
FROM   orders
WHERE  category = 'Furniture'
ORDER  BY sales DESC; 
````

#### 9- write a query to find all the records in technology and furniture category for the orders placed in the year 2020 only (1021 rows)

**Answer:**

````sql
SELECT *
FROM   orders
WHERE  category in('Furniture','Technology') 
and order_date between '2020-01-01' and '2020-12-31' 
order by sales desc;
````


#### 10-write a query to find all the orders where order date is in year 2020 but ship date is in 2021 (33 rows)

**Answer:**

````sql
SELECT *
FROM   orders
WHERE  order_date BETWEEN '2020-01-01' AND '2020-12-31'
       AND ship_date BETWEEN '2021-01-01' AND '2021-12-31' 
````
