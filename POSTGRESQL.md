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

-   % means it can be anything character length
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
