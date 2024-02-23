### Introduction ###

 - Taking Ankit's [Namaste Sql course](https://www.namastesql.com/s/courses/6301f405e4b0238f71788354/take) and below are solutions for Day 3 assignment.
 - I used Microsoft SQL server to solve the problems.
 - If you want to replicate the result use [Orders](https://raw.githubusercontent.com/mayankdubey1996/namaste_sql_assignment/main/day_3/orders_table_create_inserts.sql) query to create the table and copy the data. 

 
***Note: please do not use any functions which are not taught in the class. you need to solve the questions only with the concepts that have been discussed so far.***

####Today's Topic####
- NULL keyword (e.g. city=null is not valid, city is null -> valid)
- Aggregation functions: ***Count(), Sum(), Max(), Min(), Avg()***
- Group By, Having Keyword
- Order of execution

#### 1- write a update statement to update city as null for order ids :  CA-2020-161389 , US-2021-156909

**Answer:**

````sql
UPDATE orders
SET    city = NULL
WHERE  order_id = 'CA-2020-161389'
        OR order_id = 'US-2021-156909' 
````

#### 2- write a query to find orders where city is null (2 rows)

**Answer:**

````sql
SELECT *
FROM   orders
WHERE  city IS NULL 
````

#### 3- write a query to get total profit, first order date and latest order date for each category

**Answer:**

````sql
SELECT category,
       Sum(profit)     AS total_profit,
       Min(order_date) AS first_order_date,
       Max(order_date) AS last_order_date
FROM   orders
GROUP  BY category 
````

#### 4- write a query to find sub-categories where average profit is more than the half of the max profit in that sub-category

**Answer:**

````sql
SELECT sub_category,
       Avg(profit)     AS avg_profit,
       Max(profit) / 2 AS half_of_max_profit
FROM   orders
GROUP  BY sub_category
HAVING Avg(profit) > Max(profit) / 2 
````

#### 5- create the exams table with below script;

````sql
create table exams (student_id int, subject varchar(20), marks int);

insert into exams values (1,'Chemistry',91),(1,'Physics',91),(1,'Maths',92)
,(2,'Chemistry',80),(2,'Physics',90)
,(3,'Chemistry',80),(3,'Maths',80)
,(4,'Chemistry',71),(4,'Physics',54)
,(5,'Chemistry',79);
````

#### write a query to find students who have got same marks in Physics and Chemistry.

**Answer:**

````sql
SELECT student_id,
       marks,
       Count(*) AS cnt
FROM   exams
WHERE  subject IN ( 'Chemistry', 'Physics' )
GROUP  BY student_id,
          marks
HAVING Count(*) = 2 
````


#### 6- write a query to find total number of products in each category.

**Answer:**

````sql
SELECT category,
       Count(DISTINCT product_name) AS number_of_product
FROM   orders
GROUP  BY category 
````

#### 7- write a query to find top 5 sub categories in west region by total quantity sold

**Answer:**

````sql
SELECT TOP 5 sub_category,
             Count(sub_category) AS quantity_sold
FROM   orders
WHERE  region = 'West'
GROUP  BY sub_category
ORDER  BY quantity_sold 
````


#### 8- write a query to find total sales for each region and ship mode combination for orders in year 2020

**Answer:**

````sql
SELECT region,
       ship_mode,
       Sum(sales) AS total_sales
FROM   orders
WHERE  order_date BETWEEN '2020-01-01' AND '2020-12-31'
GROUP  BY region,
          ship_mode 
````


