/*
SQL - Structure Query Language
SQL is a programming language used to interact with relational databases.

Types of Databases
(a) Relational - Mysql , SQl Server , Oracle , Postgre SQL
(b) Non-Relational - Mongo DB
/*

MYSQL IS NOT CASE-SENSITIVE.

It is used to perform Crud operations.
C - Create
R - Read
U - Update
D - Delete

SQL is formly known as SEQL - Structure English Query Language. Created by IBM.

TYPES OF SQL COMMAND.
DDL (Data Definition Language) : Create , Alter , Rename , Truncate & Drop
DQL (Data Query Language) : Select 
DML (Data Manipulation Language) : Insert, Update, Delete
DCL (Data Control Language) : Grant & Revoke permission to Users
TCL (Transaction Control Language) : Start Transaction, Commit , Rollback

THE MAIN COMMANDS ARE:
START TRANSACTION to begin the process.
COMMIT to save the changes if everything works.
ROLLBACK to cancel all changes if something goes wrong.
/*

-- ---------------------------------------------------------------------------------------------------------------------------------------------------------

/*
WHAT IS PRIMARY KEY 
Characteristics of Primary Key :-
Uniqueness: The primary key ensures that each row in the table is unique. No two rows can have the same primary key value. This uniqueness is 
critical for indexing because MySQL needs to quickly find a specific, unique row.

"Example:
-- because MySQL needs to quickly find a specific, unique row (what is the meaning of this line)
If you're searching for a student with student_ID = 101, MySQL doesn't have to look at all the other students because it knows that student_ID 
is unique. It can go straight to the row with that ID 101.
"
Not Null: A primary key column cannot have NULL values.

Single Per Table: A table can have only one primary key, though it can consist of multiple columns (called a composite primary key).

Indexing in MySQL is a way to make searching for data faster. It works like an index in a book: instead of checking every row in a table, MySQL 
uses the index to quickly find the data you need. 
/*


/*
WHAT IS COMPOSITE PRIMARY KEY.

In SQL, a primary key doesn't have to be a single column. It can be made up of two or more columns, which together ensure the uniqueness of 
each row. This is called a composite primary key.

create table students (
student_ID int primary key,
roll_Number int primary key,
coffee_lover enum ("Yes","No")
);
-- It will give me error, as mysql will think i am trying to identify two primary keys in one table. 

create table students (
student_ID int ,
roll_Number int ,
coffee_lover enum ("Yes","No"),
primary key (student_ID,roll_Number)
);

insert into students (student_id,roll_number,coffee_lover)
values
(1,1,"Yes");

select * from students;

insert into Students (roll_number,coffee_lover)
values
(2,"yes"),
(3,"yes"),
(4,"yes"),
(5,"yes");

How same value in both column is valid :
Combination of the specified columns must be unique.

/* 
DATATYPES : (A) String (B) Number (C) Date

 -- STRING DATATYPES
1.  char(size)  0 - 255
2.  varchar(size) - Can store up to 65,535 bytes
3.  Binary(size) - length binary data, up to 255 bytes
4.  varbinary(size) - length binary data, up to 65,535 bytes,
5.  Tinytext 255 characters
6.  Text (size) - stores up to 65,535 bytes.
7.  Mediumtext - Stores up to 16,777,215 bytes
8.  longtext - Stores up to 4,294,967,295 bytes
9.  TinyBlob - 255 Bytes
10. Blob(size) (Binary Large Object) - up to 65,535 bytes - (use to store images & Videos)
11. LongBlob - 4,294,967,295 bytes
12. Enum (Val 1,Val 2,Val 3...) list upto 65535 values
13. SET (Val 1,Val 2,Val 3...) list upto 64 values

 -- NUMBER DATATYPES
BIT(size) 1 to 64
TinyInt(size) - 128 to 127 (signed) or 0 to 255 (unsigned)
Int/Integer - -2147483648 to 2147483647
SmallInt(Size) - Range is -32,768 to 32,767 (signed) or 0 to 65,535 (unsigned).
MediumInt(Size) -8388608 to 8388607
BigInt(Size) -  -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 (signed). 
Bool - Non-zero values are treated as TRUE
Boolean - same as bool
Float - used to store approximate decimal values
Decimal / Dec(Size,d) it means id i write (5,2) - 999.99 - total values we can put here is 5 and out of 5 last two values will reserved for decimal.

 -- DATE DATATYPES
Date - '1000-01-01' to '1999-12-31'
Datetime(Fsp) yyyy-mm-dd hh:mm:ss -- While inserting values format should be like this - "1991-12-01 12:00:00" 
otherwise you will get  error. 
Timestamp/time - (hh:mm:ss) Only time aayega hh:mm:ss 
Year Four-digit Format :1901 - only year aayega
*/

-- HOW TO CREATE NEW DATABASE.
create database sqlalpha;
-- (Sqlalpha) is database name and (Create Sqlalpha) is command to create database. 

-- if you doubt database with name(Sqlalpha) may already exists.
create database if not exists sqlalpha;

 -- How to drop a datbase whose name is Sqlalpha.
 drop database sqlalpha;

-- If you doubt that database with name (sqlalpha) may already dropped, you may write.
drop database if exists sqlalpha; 

-- How to make any database active. 
Use sqlalpha; -- other way is to double click on the database name. 

-- Let's Create our First Table.
create table users
(id int auto_increment,  -- Only first column in the table can be assigned as auto_increment.  
-- auto_increment means MySQL will automatically assign a unique number to the Id column. It starts from 1 (or the next available number) 
-- and increases by 1.
 Name varchar (100) not null, -- Any value entered in varchar even if it's a number will be treated as text , value can not be empty.
 email_id varchar (100) unique,  -- Unique means two different person cannot share unique email id, 
 mobile_number varchar (15) unique, -- We may use + sign before entering any number, so we use varchar not int.
 password varchar(25), 
 DOB date,  -- date format is YYYY-MM-DD it is enclosed in " "
 age int check (age >= 18) not null, -- you can enclose an integer value in quotes (" " or ' '). 
 address text, -- characteristics of text is same as varchar, only difference is the character limit. 
 gender enum("M","F","o"), -- Here Enum will only accept the values from ("M","F","o")  
 status boolean default 1, -- Boolean is a datatype that can store two possible values: TRUE (1) or FALSE (0).
 -- default 1 means if we don't provide the value in status, it will automatically set value 1 (which represent true.)
 primary key (id) -- now id will be treated as primary key.
);

-- If you forget to mention primary key & Auto_increment in above query go to table edit section and click on these options.

insert into users (id,Name,Emailid,Mobile_number,password,DOB,age,address,Gender,Status)
values
(1,"John","John@gmail.com","6534764529","%$%$%","1994-08-04","20","NYC,NY","M",1),
(2,"Victor","Victor@gmail.com","6542398645","*%$@%^","1994-08-04",27,"Boston,MA","F",1);

insert into users (Name,Emailid,Mobile_number,password,DOB,age,address,Gender)
values
("Victoria","Victoria@gmail.com","7543898625","%&*)%","1991-08-04","24","Plano,TX","F");

insert into users values -- Don't mention all column name if number of entered values in row is equal to number of column.
(4,"Emma","Emma@gmail.com","8735690824","&*#)&^","1990-07-05","26","Piscataway,NJ","F", 2),
(5,"Wilson","Wilson@gmail.com","8643690824","&*&#&^","1993-07-05","26","Miami,FL","M",1);

-- How to enter null value in database.
insert into users values 
(6,"Abbey","Abbey@gmail.com","8643612324","(#&#&^","1991-07-05","29","null","F",1); -- Null should not entered inside " ". 
-- if i can only enter "Null" at string, date, time , enum will give immediate error. 
-- if it entered inside " ", it will be considered as value.

insert into users values 
(7,"Ross","Ross@gmail.com","8233612324","(#&12^","1990-07-05","31",null,"F",1);

select * from users;
select name from users where address is Null; -- Correct 
select name from users where address = "Null"; -- it is not supposed to be a correct query but still could provide result if we entered "null" in varchar.  


select * from users where address is not Null;
Select * from users;
update users set status = 2 where id = 7;  -- In where clause we mention primary key, here id must be a primary key.

-- ---------------------------------------------------------------------------------------------------------------------------------------------------------------

/*
-- DELETE QUERY
delete from students where id = 3;
-- delete from students where id in (4,5,6) 
-- delete from students where age  <= 18; 
*/

-- ---------------------------------------------------------------------------------------------------------------------------------------------------------------


-- (a) ADD COLUMN
-- Alter(To Change Schema) -- ALTER is a command used to modify the structure (schema) of an existing table.
alter table users add column office_address varchar(50) not null; 

alter table users add column office_time time not null;

-- (b) HOW TO DROP A COLUMN
alter table users drop column office_address;

-- (c) How to change column name
alter table users change column office_time have_vehicle enum('Yes','NO') not null;
-- this will give me truncated error, beacause we are just changing the column name name and value inside the office time is null, also can not
-- accept the enum. 

alter table users change column office_time have_vehicle time not null; 

select * from users; 

-- (d) MODIFY COLUMN
Alter table users modify have_vehicle varchar(10);

-- (e) RENAME TABLE
Alter table student_details rename to Consumers;

/*
TRUNCATE & DELETE
Truncate table table_name
Truncate - It will delete all the data inside table.
delete - it will delete the complete table
*/


-- ---------------------------------------------------------------------------------------------------------------------------------------------------------------


/*
COMMIT & ROLLBACK
EDIT - PREFERENCE - SQL EXECUTION - NEW CONNECTIONS - USE AUTO COMMIT MODE - UNCHECK IT  
We use commit command after insert , update , delete. 

commit; 
rollback;
I write 123, commit it, then add value 45 , if i rollback i will get 123. 
*/

-- ---------------------------------------------------------------------------------------------------------------------------------------------------------------

Select * from employee; 

-- select some columns only and apply multiply & change the column name  at same time.
select First_name , Dept , Country, salary*12 as Annual_Salary from employee;  

-- Now i want to see how many different departments are here.
select distinct Dept from employee; 

-- Now i just want to see the employee whose name is steve.  
select * from employee where first_name = "Steve"; 

-- Now i just want to see the employee whose name is not steve.  
select * from employee where first_name != "Steve";
select * from employee where first_name <> "Steve";

-- Find Female employees who belong to canada and gender is female and experience is more than 10.
select * from employee where country = "canada" and gender = "F" and exp > 10 ;

-- we can use OR operator also. Make sure you use brackets.
select * from employee where country = "Canada" and exp >= 5 and (gender = "F" OR gender = "M"); 

-- Retrieve the details of employees who have roles of either "SENIOR DATA SCIENTIST" or "JUNIOR DATA SCIENTIST". 
select * from employee where role in ("SENIOR DATA SCIENTIST","JUNIOR DATA SCIENTIST");

-- Find employees who do not belong to the continents "ASIA" or "EUROPE".
select * from employee where continent not in ("ASIA" , "EUROPE") ; 

-- List all managers from the "FINANCE" and "HEALTHCARE" departments.
select * from employee where role = "manager" and dept in ("FINANCE" , "HEALTHCARE");

-- Find the names of employees with role managers and EMP_ID "E002" or "E428".
select * from employee where role = "Manager" and EMP_ID in ("E002" , "E428"); 

-- Find employees whose salary is not 3000, 4000, or 5000.
select * from employee where salary not in ( 3000, 4000, 5000); 

select * from employee where DEPT not in ("FINANCE" , "AUTOMOTIVE") and CONTINENT in ("ASIA" , "SOUTH AMERICA");

SELECT * FROM employee WHERE (ROLE, COUNTRY) IN ( 
	('SENIOR DATA SCIENTIST', 'INDIA'),
    ('SENIOR DATA SCIENTIST', 'CHINA'),
    ('SENIOR DATA SCIENTIST', 'COLOMBIA')
);

-- 9. Retrieve employees who belong to the "NORTH AMERICA" continent but whose salaries are not in the top 3 highest salaries in their department.
SELECT * FROM sqlalpha.employee;
SELECT * FROM employee e WHERE e.CONTINENT = 'NORTH AMERICA' AND e.SALARY NOT IN (SELECT DISTINCT TOP_SALARY FROM (SELECT DEPT, SALARY AS TOP_SALARY, 
             RANK() OVER (PARTITION BY DEPT ORDER BY SALARY DESC) AS SALARY_RANK FROM employee ) ranked_salaries WHERE SALARY_RANK <= 1);


-- 11. Give me list of all employees whose name starts with (j).
Select * from employee where first_name like "j%";
Select * from employee where first_name like "S_e_%";

Select * from employee where Role like ("lead%");

-- 12. Query the list of first_name starting with vowels (i.e., a, e, i, o, or u) from employee. Your result cannot contain duplicates.
select distinct first_name from employee where left(first_name,1) in ('a', 'e' , 'i' , 'o' , 'u' ); 

-- 13 . uery the list of first_name from employee which have vowels (a, e, i, o, u) from STATION. Your result cannot contain duplicates.
select distinct first_name from employee where right(first_name,1) in ('a', 'e' , 'i' , 'o' , 'u' ); 

-- 14. Query the list of first_name from employee which have vowels (i.e., a, e, i, o, and u) as both their first and last characters. 
-- Your result cannot contain duplicates.
select distinct first_name from employee where left(first_name,1) in ('a', 'e' , 'i' , 'o' , 'u' ) and right(first_name,1) in ('a', 'e' , 'i' , 'o' , 'u' ); 

-- 15. Query the list of first_name from employee which do not start with ('a', 'e' , 'i' , 'o' , 'u' ). Your result cannot contain duplicates.
select distinct first_name from employee where left(first_name,1) not in ('a', 'e' , 'i' , 'o' , 'u' );


-- ---------------------------------------------------------------------------------------------------------------------------------------------------------------
-- BETWEEN 

-- Now i want to see employees whose experience lies in between 8 and 16.
select * from emp_table where exp > 8 and exp <16;
select * from employee where exp between 8 and 16; 
select * from employee where exp not between 8 and 16; 

-- ---------------------------------------------------------------------------------------------------------------------------------------------------------------

-- ORDER BY

-- I want to see the employees from highest salary to lowest salary.
select * from employee order by salary desc;

-- now i want to see highest to lowest salary in each department.
select dept,Salary from employee order by dept , salary desc; -- priority is given to the department.

-- ---------------------------------------------------------------------------------------------------------------------------------------------------------------

-- LIMIT // OFFSET
 
-- now i want to see first 5 employee skiping top 10 employee from the table. 
select emp_id, first_name from employee order by salary desc limit 5 offset 10;  

-- now i want to see top 5 employee only.
Select * from employee order by salary desc limit 5; 

-- ---------------------------------------------------------------------------------------------------------------------------------------------------------------

-- TEXT FUNCTIONS

use northwind;
select * from customers;
-- today we will learn about text functions.

-- I want to see the company name in capital & Lower letter.
select companyname, upper(companyname), Lower(companyname) from customers; 

-- i want to see the first 3 letter and last 4 letter from company name.
select *, companyname, left(companyname,3) , right(companyname,4) from customers; 

select * from employees;
-- i want to see employee full name.
select firstname, lastname, concat(firstname," " ,lastname) as Full_name from employees; 

-- ---------------------------------------------------------------------------------------------------------------------------------------------------------------

-- ROUND FUNCTION

select * from products;
-- in unit price, i don't want to see the decimal. 
select unitprice, round(unitprice,0) from products;
select unitprice, round(unitprice,2) from products;

-- to get the highest integer & Lowest integer value.
select unitprice, ceil(unitprice), floor(unitprice) from products; 

-- ---------------------------------------------------------------------------------------------------------------------------------------------------------------

-- DATE FUNCTION

select curdate();
select Current_date();

-- i want to know the year , Month , monthname , quarter , week , day , dayname of current Date.
select year(curdate()) , quarter(curdate()) , month(curdate()), monthname(curdate()) , week(curdate()) , day(curdate()) , dayname(curdate()); 

-- in which format you want to see the current date.
select date_format (curdate(),"%d-%m-%y"); -- have to mention date_format here

select * from orders;
-- Show me list of all the orders that were placed in the year of 1997 and in month of june.
select * from orders where year(orderdate) = "1997" and monthname(orderdate) = "June";

-- show me the list of orders that were placed in 2nd quarter of 1997.
select * from orders where year(orderdate) = "1997" and quarter(orderdate) = 2 ; 
select * from orders where year(orderdate) = "1997" and monthname(orderdate) in ("April","May","June"); 
select orderdate from orders where orderdate between "1997-04-01" and "1997-06-30" ; 
-- in 1997, june had 30 days in month, if i write between "1997-04-01" and "1997-06-31" , i will get no data.  

-- ---------------------------------------------------------------------------------------------------------------------------------------------------------------

-- AGGREGATE FUNCTIONS: IT WORKS ON GROUP OF DATA AND GIVE ONE OUTPUT.
-- SUM() , AVG() , COUNT() , MAX() , MIN()

Select * from orders;
-- i want to see total number of products in the data.
Select count(*) from orders; 
select count(orderid) from orders;
select count(shipregion) from orders;

-- To know difference between two dates.
select orderid , orderdate , shippeddate, datediff(shippeddate,orderdate) from orders; 

-- List the data where datediff is more than 10.
select orderid , orderdate , shippeddate, datediff(shippeddate,orderdate) from orders where datediff(shippeddate,orderdate) > 10 ; 

-- I want to see the sum of unitsinstock and average unitsinstock of in product.
select * from products;
select sum(unitsinstock) , avg(unitsinstock), min(Unitsinstock) from products;

-- ---------------------------------------------------------------------------------------------------------------------------------------------------------------

-- GROUP BY

-- now i want to see how many times a category is repeated.
select categoryid, count(*)  from products group by categoryid; 

-- Now i wants to know total number of unitsinstock in each categoryID. 
Select categoryID, count(*), sum(Unitsinstock) from products group by (categoryID);
 select categoryID,sum(unitsinstock) from products group by categoryID having sum(unitsinstock) > 500; 

-- Now i only wants to see those categoryID which have minimum 10 products.
Select * from products;
select categoryid, count(*) from products group by (categoryID) having count(*) >= 10 order by count(*) desc;

-- We can add where clause as well in above script.
select categoryid, count(*) from products where categoryid >= 2 group by (categoryID) having count(*) >= 10 order by count(*) desc;


-- Tell me number of customers from each country.
select * from customers;
select country , count(*) from customers group by (country) order by count(*) desc;

-- List number of orders each year for each quarter.
select * from orders; 
select year(orderdate), quarter(orderdate), count(*) from orders group by year(orderdate), quarter(orderdate); 

-- Count of all the orders placed by each country. 
select * from orders;
select shipcountry, count(*) from orders group by (shipcountry) order by count(*) desc;

-- --------------------------------------------------------------------------------------------------------------------------------------------------------------

-- JOINS
-- If i try to add common cloumn i should mention (tablename.columnname) , otherwise i get i get ambiguous error.

use northwind;
-- List all the productname Where categoryname is "confections","Beverages"
select * from categories;
select * from products;
select categoryname , productname 
         from categories c join products p
         on c.categoryid = p.categoryid where categoryname in ("Beverages","Confections"); -- We can also use not in function. 
         
-- How to join three tables.
select * from categories;
select * from products;
select * from suppliers; 

select categoryname, productname,companyname from categories c join products p on c.categoryID = p.categoryID join suppliers s on s.supplierID = p.supplierID; 

-- List total units in stock for each categoryname. 
 select * from categories;
 select * from products; 
 
 select categoryname, sum(Unitsinstock) from categories c join products p on c.categoryID = p.categoryID group by categoryname; 

-- Display number of orders by each customers.
Select * from customers; 
select * from orders;

select contactname, count(orderid) from orders o join customers c on o.customerid = c.customerid group by (contactname) order by count(*); 

-- Display number of orders for each country.
select country, count(*) from orders o join customers c on o.customerid = c.customerid group by (country) order by count(*);

-- ---------------------------------------------------------------------------------------------------------------------------------------------------------------

-- QUERY / SUB-QUERY
use sqlalpha;
select * from employee;

-- Give me the name of employees whose salary is more than Patrick. 
select * from emp_table where first_name = "Patrick"; 
select * from emp_table where salary > 9500; 

-- above code can also be written in simple 
select * from emp_table where salary > (select salary from emp_table where first_name = "Patrick"); 
-- This is (Main-Query)                     -- This is (Sub-Query)

-- List all productname where categories = "Beverages"
Use northwind;
select * from products;
select * from categories;

select * from products where categoryID = (select categoryID from categories where categoryname = "Beverages");     

-- List all the orders made by Maria Anders. 
select * from orders;
select * from customers; 

select * from orders where customerID = (select customerid from customers where contactname  = "Maria Anders");

-- List all the orders taken by steven. 
select * from orders;
select * from employees;

select * from orders where employeeID = (select EmployeeID from employees where firstname = "Steven");   

-- List all the orders placed by germany customers. 
select * from Customers;
Select * from orders; 
select * from orderdetails;
select * from products;

Select * from orders where customerid in (select customerid from customers where country = "Germany");
-- if we use = in above query, we get error (Subquery returns more than 1 row) , as many different customers belong to the country(Germany), we should use In operator.   

-- List all the productname placed by germany customers. 
select * from products;
select * from orderdetails;
Select * from orders; 
select * from Customers;

Select productname from products where productid IN (select ProductId from orderdetails where orderid in (select orderid from orders where customerid in (select 
customerid from customers where country = "Germany")));

-- Give me name of customer who order tea from germany.
select * from customers;
Select * from orders; 
select * from orderdetails;
select * from products;

select * from customers where country = "germany" and customerid in (select customerid from orders where orderid in (select orderid from orderdetails where productid in (select productid from
products where productname = "chai")));    


-- List of all the products made by exotic liquid. 
select * from products;
select * from suppliers;

select * from products where supplierid = (select supplierid from suppliers where companyname = "Exotic Liquids");

select * from products where supplierid > (select supplierid from suppliers where companyname = "Exotic Liquids");
-- it show all the data which have supplier ID greater than 1. 

-- List all the productname purchased by "Maria Anders".
select * from products;
select * from orderdetails;
Select * from orders; 
select * from customers;

select * from products where productID in (select productid from orderdetails where orderid in (select orderid from orders where customerid in (select customerid from
customers where contactname = "maria Anders"))) order by productname;    


-- List of orders placed by each Customers.
select * from customers;
SELECT * FROM orders;
select * from orderdetails; 
select * from products; 

select contactname,count(productname) total_products
   from customers 
   join orders on customers.customerID = orders.customerID
   join orderdetails on orders.orderID = orderdetails.orderID -- you can not write join orders on orders.orderID = orderdetails.orderID.
   join products on orderdetails.productid = products.productid
   group by contactname;


-- List of orders by each company.
select * from orders; 
select * from customers; 

create view ordersbycompany as
select companyname, count(*) as No_of_Orders
from customers join orders on customers.customerid = orders.customerid
group by companyname
order by No_of_Orders desc; 

-- ---------------------------------------------------------------------------------------------------------------------------------------------------------------

-- Co Related SubQuery 
-- List All the employees who earn more than average salary within each department.
use sqlalpha;
select * from employee;
select * from employee e where salary > (select avg(salary) from employee where dept = e.dept);
-- o.dept means it will fetch data from all the departments.

-- To know maximum salary in each department.
Select * from employee e where salary = (select max(salary) from employee where dept = e.dept) order by dept;

use sqlalpha;
select * from employee; 

-- Let's create first table which contains data for employees working in retail department. 

create table emp_retail as select * from employee where dept = "Retail";
create table emp_finance as select * from employee where dept = "Finance";

select * from emp_retail;
select * from emp_finance; 

select * from emp_retail
union
select * from emp_finance;


-- ---------------------------------------------------------------------------------------------------------------------------------------------------------------


-- LET'S LEARN VIEWS
-- View is an alternate way to see the data from one or more tables. also called an virtual table or stored Query. 
-- Advantages of Views (a) Hides the complexity of writing complex Query again and again. (b) protect sensitive Data. 

create view Beverages as  
select productID , Productname, unitprice, unitsinstock, categoryname
   from products p join categories c on p.categoryID = c.categoryID
   where categoryname = "Beverages";

Select * from beverages; 

-- create a view to display total stocks for each category.
select * from categories; 
select * from products; 

create view Total_Sales_per_category as 
select categoryname, sum(unitsinstock) as total_stock
   from products p join categories c 
   on p.categoryID = c.categoryID
   group by CategoryName; 
   
  select * from Total_Sales_per_category ;

-- ---------------------------------------------------------------------------------------------------------------------------------------------------------------

create table demoproducts as select * from products; 
select * from demoproducts; -- now dropdown table demoproducts - dropdown column - you see nothing in indexes.

select * from demoproducts where productid = 55; -- right click on dempproducts - altertable - select productid as primary key.   

-- ---------------------------------------------------------------------------------------------------------------------------------------------------------------

-- WINDOW FUNCTIONS
Select * from employee;
select First_name,Role,Salary, -- beacuse rank is a new column so we give comma
     rank() over(order by salary desc) as RK from employee;
-- if two people have same salary, we are getting, both get same ranking, and upcoming rank number got skipped, this is called tiebraker.

select emp_id,first_name,ROLE,salary, 
dense_rank() over(order by salary desc) as DRK
from employee;

 -- now i want seperate rank for same salary employee.
select emp_id,first_name,ROLE,salary, -- beacuse rank is a new column so we give comma
      row_number() over(order by salary desc) as RN
      from employee;

select emp_id,first_name,ROLE,salary,emp_rating,
      rank() over(order by salary desc) as RK,
      dense_rank() over(order by salary desc) as DRK,
      row_number() over(order by salary desc) as RN
      from employee;

select emp_id,first_name,ROLE,salary,emp_rating, -- This time salary and EMP_rating both will considered before giving rank.
      rank() over(order by salary desc,emp_rating desc) as RK
      from employee;

-- now i wan to give ranking based on department & salary.
select emp_id,first_name,Role,dept,salary,
 rank() over(partition by dept order by salary desc) as star
 from employee;

select * from employee; 
-- select *, sum(salary) from emp_table; -- this will not execute because * give all values and sum give only one value.

select *, sum(salary) over() from employee;	

select *, salary / sum(salary) over() from employee;	

select *, salary / sum(salary) over()*100 from employee;

select emp_id,First_name,salary,exp,ntile(10) over (order by exp) from employee; 
-- If i don't put anything inside over(), it will divide the data based on number of rows.
-- Based on experience ntile will divide the data into 4 parts.

select first_name,salary,lead(salary,1) over() as LD from employee; -- here LD shows the next upcoming values. 

select first_name,salary,lag(salary,1) over() as lg from employee; -- it shows previous value.

-- To know the number of orders each year.

-- create View with name tblsales
select * from tblsales;
-- now use lead and lags in above.
select *, lead(no_orders) over() as LD from tblsales;

-- below is the example, how to use CTE.

-- ---------------------------------------------------------------------------------------------------------------------------------------------------------------

with cte as 
(
select year(orderdate), month(orderdate), count(*) no_orders from orders
     group by year(orderdate), month(orderdate)
     order by year(orderdate),month(orderdate)
) select * from CTE;  -- here we can use lead and lags. 

-- view we can use again and again but CTE (commin table expressions) we can use only immediately after query. 

-- ---------------------------------------------------------------------------------------------------------------------------------------------------------------

-- BELOW ARE 3 DIFFERENT WAYS TO GET SECOND HIGHEST SALARY.
use sqlalpha;
select emp_id, first_name,EXP, salary from emp_table order by salary desc limit 1 offset 1;

select * from emp_table where salary = (
select max(salary) from emp_table where salary <> (select max(salary) from emp_table));

select * from (select *, rank() over(order by salary desc) as Rk from emp_table) as e where rk = 2;

with cte as 
(select *, rank() over(order by salary desc) as Rk from emp_table)
select * from cte where rk = 2 ;

-- ---------------------------------------------------------------------------------------------------------------------------------------------------------------
-- STORED PROCEEDURE - productsbycategory()
select * from categories; 
select * from products; 

call productsbycategory();

-- CREATE PROCEDURE products_by_category(cname varchar(40))

-- made one more stored proceedure with name products_by_category(), this time i have to put categoryname inside bracets in order to get result
call products_by_category("Beverages"); -- i can mention any productname in order to get the result.

-- Let's create new function which depend upon the date.-- orderbydate 
call orderbydate ("1997-01-01","1997-05-06");


update demoproducts set UnitPrice= UnitPrice + UnitPrice * 10/100;
-- giving me truncate error.

DESCRIBE demoproducts;
-- datatype for demoproduct was set to decimal(6,4) , which giving me truncate error , i will change it to int.

ALTER TABLE demoproducts MODIFY UnitPrice int;

update demoproducts set UnitPrice= UnitPrice + UnitPrice * 10/100;
select * from demoproducts; 

-- now i will create stored_proceedure for this.
SELECT * FROM northwind.demoproducts;
call taxeffect(5);

-- ---------------------------------------------------------------------------------------------------------------------------------------------------------------
-- FUNCTIONS / STORED FUNCTIONS - (UDF - USER DEFINE FUNCTION)

-- Here i need to add one function, where if i buy any item, automatically reduce from stock. i will write that later from notepad.
-- Stored Function (User Defined Function - UDF)
-- function name - sqrnum()
select sqrnum(12);

-- Give every employee 50% of Bonus w.r.t their salary. -- CREATE FUNCTION Bonus (emp_id varchar(5)) -- we use sqlalpha for this
select * from employee; 
select *, Bonus(emp_ID) from employee; 

-- create one more function with name bonus by department. 
select *, Bonus_DEPT(emp_ID) from employee; 
-- ---------------------------------------------------------------------------------------------------------------------------------------------------------------

-- NORMALIZATION

/*
-- Normalization

-- Cascading in Foreign key 

-- Data Transaction 

-- data transaction in MySQL is like a "bundle" of actions that must either all happen or not happen at all.

-- Wscube fail to teach me relation in between primary key and foreign key.

 -- Foreign KEY
 -- (a) Foreign key is used to link two tables.
 -- (b) A Foreign key in one table (Child table) is used to point PRIMARY KEY in another table (Parent Table).
 -- unlike primary key, there can be multiple foreign key in an table. 


ERRORS

-- (7,"Ross","Ross@gmail.com","8233612324","(#&12^","1990-07-05","31"," ","F",1); -- This will give data truncated error.

-- We usually get Truncated Error when we entered incorrect data type. or entered data exceed the limit. e.g. varchar(4) , and entered value 5.

-- Union - union is another technique to take data from multiple tables.

-- How To add value into view.

-- INDEXING 
     Types of indexes 
    (a) clustered Index - the data is sorted by key field and search happens.
    (b) non-clustered Index - the data is stored in one place and index info is stored in another place.
    
In SQL, a CROSS JOIN is a type of join that returns the Cartesian product of two tables. This means it combines every row from the first table with every row from the second table, creating all possible combinations of rows from both tables.
Characteristics of a CROSS JOIN:
It does not require any condition to join the tables.
The result is the total number of rows from the first table multiplied by the total number of rows from the second table.



how to use Constraint / ENUM 

auto_increment - there can be only one column identifies as auto_inrement column, and it has to be first column only. 

 */
