## Database queries

```
select datname from pg_database;
create database database_name;
drop database database_name;
```

## Table related queries

### Creating a table

```
create table users(
 id serial primary key,
 name varchar(100) not null,
 email varchar(255) unique not null,
 age int check (age >= 0)
);

create table posts(
 id serial primary key,
 title text not null,
 content text,
 user_id int not null
)

```

### Deleting a table

```
drop table users;
```

### Adding new row inside table

```
insert into
users (name, email, age)
values
('Alice', 'alice@gmail.com', 25);
```

```
insert into
users (name, email, age)
values
('Alice', 'alice@gmail.com', 25),
('Bob', 'bob@gmail.com', 30),
('Charlie', 'charlie@gmail.com', 22);
```

### Selecting / Getting data from table

```
select *
from users;

select name, email
from users;

select age
from users;

select *
from users
where age > 25;

select *
from users
where name = 'Bob';

select *
from users
where age > 20 and age < 30;
```

### Updating data inside table

```
update users
set email = 'random@gmail.com'
where id = 2;
```

### Deleting data from table

```
delete
from users
where id = 3;
```

### Filtering, Sorting and Pagination

```
select *
from users
where age > 20 and age < 30;

select *
from users
order by age;

select *
from users
order by age desc
limit 2;
```

### Joins

Combining two table rows into one single row by some common unique identifier inside both tables and if both unique identifier matches then it is shown on table else it is not shown (conditional row showing)

```
create table posts (
id serial primary key,
title text not null,
content text,
user_id int not null
);

insert into posts
(title, content, user_id)
values
('Hello World', 'hello world content', 1),
('SQL Rocks', 'sql rocks content', 1),
('My Post', 'hello this is my post content', 2);

select *
from posts
join users
on posts.user_id = users.id;

select posts.title, posts.content, users.name
from posts
join users
on posts.user_id = users.id;

select p.title, u.name
from posts p
join users u
on p.user_id = u.id;

select p.title, p.content, u.name
from posts p
join users u
on p.user_id = u.id
where u.name = 'Alice';

select p.title, u.email
from posts p
join users u
on p.user_id = u.id;
```

### Left Join

It shows even the null values even if the condition of both table doesn't match it just shows null

```

select p.title, u.email
from posts p
left join users u
on p.user_id = u.id;

```

### Some more clauses

-   Distinct is used to select unique data only

```
select distinct dept
from employees;
```

-   % means it can be any character length
-   \_ means it is used to skip characters

```
select * from employees
where fname like 'A%';

select * from employees
where fname like '%a';

select * from employees
where fname like '%i%';

select * from employees
where dept like '__';

select * from employees
where fname like '_a%';
```

### Aggregate Functions

```
SELECT COUNT(emp_id) FROM employees;

SELECT SUM(salary) FROM employees;

SELECT AVG(salary) FROM employees;

SELECT MIN(salary) FROM employees;

SELECT MAX(salary) FROM employees;

SELECT * FROM employees
WHERE salary = (SELECT MAX(salary) FROM employees);

SELECT COUNT(emp_id) AS total_employees FROM employees;

SELECT dept, COUNT(emp_id) FROM employees
GROUP BY dept;

```

### Group By (Important)

```
SELECT dept, count(emp_id)
FROM employees
GROUP BY dept;
```

### String functions

```
SELECT CONCAT(fname, ' ', lname) AS full_name
FROM employees;

SELECT CONCAT_WS(' ', fname, lname) AS full_name
FROM employees;

SELECT * FROM employees
WHERE LENGTH(fname) = 4;

```

### Find the employee with the highest/lowest salary (Task)

```
SELECT * FROM employees
ORDER BY salary DESC
LIMIT 1;

SELECT * FROM employees
WHERE salary = (SELECT MAX(salary) FROM employees);

SELECT * FROM employees
ORDER BY salary
LIMIT 1;

SELECT * FROM employees
WHERE salary = (SELECT MIN(salary) FROM employees);
```

### Alter Table

```
ALTER TABLE persons
RENAME mob_no TO phone_number;

ALTER TABLE persons
RENAME TO users;

ALTER TABLE users
ADD COLUMN phone_no VARCHAR(15);

ALTER TABLE users
DROP COLUMN city;

```

### Check constraint

```
ALTER TABLE users
ADD COLUMN phone_no VARCHAR(15)
CHECK (LENGTH(phone_no) >= 10);
```

### Relationships

```
CREATE TABLE customers(
	customer_id SERIAL PRIMARY KEY,
	customer_name VARCHAR(100) NOT NULL
);

INSERT INTO customers (customer_name)
VALUES ('Raju'), ('Sham'), ('Paul'), ('Alex');

CREATE TABLE orders(
	order_id SERIAL PRIMARY KEY,
	order_date DATE NOT NULL,
	customer_id INT NOT NULL,
	FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);

INSERT INTO orders (order_date, customer_id)
VALUES ('2024-01-01', 1),
    ('2024-02-01', 2),
    ('2024-03-01', 3),
    ('2024-04-04', 2);
```

### Joins

```
SELECT *
FROM customers
CROSS JOIN orders;

SELECT c.customer_name, o.order_id, o.order_date
FROM customers c
JOIN orders o
ON o.customer_id = c.customer_id;

SELECT c.customer_name , count(o.order_id)
FROM customers c
JOIN orders o
ON o.customer_id = c.customer_id
GROUP BY c.customer_name;

SELECT c.customer_name , o.order_id, o.order_date
FROM customers c
LEFT JOIN orders o
ON o.customer_id = c.customer_id;

```

### Task (Student courses)

```
CREATE TABLE students (
student_id SERIAL PRIMARY KEY,
name VARCHAR(100) NOT null
);

INSERT INTO Students (name) VALUES
('Raju'),
('Sham'),
('Alex');

CREATE TABLE courses(
course_id SERIAL PRIMARY KEY,
course_name VARCHAR(100) NOT NULL,
fees NUMERIC NOT null
);

INSERT INTO courses (course_name, fees)
VALUES
('Mathematics', 500.00),
('Physics', 600.00),
('Chemistry', 700.00);

CREATE TABLE course_enrollments(
enrollment_id SERIAL PRIMARY KEY,
student_id INT NOT NULL,
course_id INT NOT NULL,
enrollment_date DATE NOT NULL,
FOREIGN KEY (student_id) REFERENCES students(student_id),
FOREIGN KEY (course_id) REFERENCES courses(course_id)
);

INSERT INTO course_enrollments (student_id, course_id, enrollment_date)
VALUES (1, 1, '2024-01-01'),
(1, 2, '2024-01-15'),
(2, 1, '2024-02-01'),
(2, 3, '2024-02-15'),
(3, 3, '2024-03-25');

SELECT ce.enrollment_id, s."name", c.course_name, c.fees, ce.enrollment_date
FROM course_enrollments ce
JOIN students s
ON ce.student_id = s.student_id
JOIN courses c
ON ce.course_id = c.course_id;
```

### Task (StoreDB)

```
CREATE TABLE customers(
	customer_id SERIAL PRIMARY KEY,
	customer_name VARCHAR(100) NOT NULL
);

INSERT INTO customers (customer_name)
VALUES ('Raju'), ('Sham'), ('Paul'), ('Alex');

CREATE TABLE orders(
	order_id SERIAL PRIMARY KEY,
	order_date DATE NOT NULL,
	customer_id INT NOT NULL,
	FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);

INSERT INTO orders (order_date, customer_id)
VALUES ('2024-01-01', 1),
    ('2024-02-01', 2),
    ('2024-03-01', 3),
    ('2024-04-04', 2);

CREATE TABLE products (
    product_id SERIAL PRIMARY KEY,
    product_name VARCHAR(100) NOT NULL,
    price NUMERIC NOT NULL
);

INSERT INTO products (product_name, price)
VALUES
    ('Laptop', 55000.00),
    ('Mouse', 500),
    ('Keyboard', 800.00),
    ('Cable', 250.00);

CREATE TABLE order_items (
    item_id SERIAL PRIMARY KEY,
    order_id INTEGER NOT NULL,
    product_id INTEGER NOT NULL,
    quantity INTEGER NOT NULL,
    FOREIGN KEY (order_id) REFERENCES orders(order_id),
    FOREIGN KEY (product_id) REFERENCES products(product_id)
    );

INSERT INTO order_items (order_id, product_id, quantity)
VALUES (1, 1, 1),
    (1, 4, 2),
    (2, 1, 1),
    (3, 2, 1),
    (3, 4, 5),
    (4, 3, 1);

SELECT oi.item_id, c.customer_name, o.order_date , p.product_name,
p.price, oi.quantity, (p.price * oi.quantity) AS total_price
FROM order_items oi
LEFT JOIN products p
ON oi.product_id = p.product_id
LEFT JOIN orders o
ON oi.order_id = o.order_id
LEFT JOIN customers c
ON o.customer_id = c.customer_id;

```
