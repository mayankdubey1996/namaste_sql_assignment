### Introduction ###

 - Taking Ankit's [Namaste Sql course](https://www.namastesql.com/s/courses/6301f405e4b0238f71788354/take) and below are solutions for Day 5 assignment.
 - I used Microsoft SQL server to solve the problems.

Note: please do not use any functions which are not taught in the class. you need to solve the questions only with the concepts that have been discussed so far.

***Note: please do not use any functions which are not taught in the class. you need to solve the questions only with the concepts that have been discussed so far.***

#### Today's Topic - Joins and Aggregate functions ####

[Joins](https://www.youtube.com/watch?v=Yh4CrPHVBdE)
- INNER JOIN
- LEFT JOIN
- RIGHT JOIN
- CROSS JOIN
- FULL OUTER JOIN

1- write a query to get region wise count of return orders

````sql
SELECT o.region,
       Count(DISTINCT r.order_id) AS total_number_of_return_order
FROM   orders o
       RIGHT JOIN returns r
               ON o.order_id = r.order_id
GROUP  BY o.region 
````

2- write a query to get category wise sales of orders that were not returned

````sql
SELECT o.category,
       Sum(sales) AS total_sales
FROM   orders o
       LEFT JOIN returns r
              ON o.order_id = r.order_id
WHERE  r.order_id IS NOT NULL
GROUP  BY o.category 
````

3- write a query to print dep name and average salary of employees in that dep .

****Run below query before jumping to the solution****

````sql
create table employee(
    emp_id int,
    emp_name varchar(20),
    dept_id int,
    salary int,
    manager_id int,
    emp_age int
);


insert into employee values(1,'Ankit',100,10000,4,39);
insert into employee values(2,'Mohit',100,15000,5,48);
insert into employee values(3,'Vikas',100,10000,4,37);
insert into employee values(4,'Rohit',100,5000,2,16);
insert into employee values(5,'Mudit',200,12000,6,55);
insert into employee values(6,'Agam',200,12000,2,14);
insert into employee values(7,'Sanjay',200,9000,2,13);
insert into employee values(8,'Ashish',200,5000,2,12);
insert into employee values(9,'Mukesh',300,6000,6,51);
insert into employee values(10,'Rakesh',500,7000,6,50);
select * from employee;

create table dept(
    dep_id int,
    dep_name varchar(20)
);
insert into dept values(100,'Analytics');
insert into dept values(200,'IT');
insert into dept values(300,'HR');
insert into dept values(400,'Text Analytics');
select * from dept;
````

````sql
SELECT d.dep_name,
       Avg(salary) AS total_salary
FROM   dept d
       INNER JOIN employee e
               ON d.dep_id = e.dept_id
GROUP  BY d.dep_name 
````

4- write a query to print dep names where none of the emplyees have same salary.

````sql
SELECT d.dep_name
FROM   employee e
       INNER JOIN dept d
               ON e.dept_id = d.dep_id
GROUP  BY d.dep_name
HAVING Count(e.emp_id) = Count(DISTINCT e.salary) 
````

5- write a query to print sub categories where we have all 3 kinds of returns (others,bad quality,wrong items)

````sql
SELECT sub_category
FROM   orders o
       INNER JOIN returns r
               ON o.order_id = r.order_id
GROUP  BY sub_category
HAVING Count(DISTINCT return_reason) = 3
ORDER  BY sub_category 
````

6- write a query to find cities where not even a single order was returned.

````sql
SELECT o.city
FROM   orders o
       LEFT JOIN returns r
              ON o.order_id = r.order_id
GROUP  BY city
HAVING Count(DISTINCT r.order_id) = 0 
````

7- write a query to find top 3 subcategories by sales of returned orders in east region

````sql
SELECT TOP 3 o.sub_category,
             Sum(sales) AS sales_of_returned_order
FROM   orders o
       INNER JOIN returns r
               ON o.order_id = r.order_id
WHERE  o.region = 'East'
GROUP  BY o.sub_category
ORDER  BY sales_of_returned_order DESC 
````

8- write a query to print dep name for which there is no employee

````sql
SELECT d.dep_id
FROM   dept d
       LEFT JOIN employee e
              ON d.dep_id = e.dept_id
GROUP  BY d.dep_id
HAVING Count(e.emp_id) = 0 
````

9- write a query to print employees name for dep id is not avaiable in dept table

````sql
SELECT e.emp_name
FROM   employee e
       LEFT JOIN dept d
              ON e.dept_id = d.dep_id
WHERE  d.dep_id IS NULL 
````
