## Database queries

```
select datname from pg_database;
create database database_name;
drop database database_name;
```

## Table queries

```
<!-- CREATING A TABLE -->
create table users(
 id serial primary key,
 name varchar(100),
 email varchar(255),
 password text,
 age int
);

<!-- DELETING A TABLE -->
drop table users;

<!-- ADDING DATA INSIDE TABLE (ROW) -->
insert into users (name, email, password, age)
values ('Sharadindu Das', 'remo@random.com', 'Hello@123', 26);

insert into users (name, email, password, age)
values ('Random User', 'random@gmail.com', 'Random@123', 28);

<!-- SELECTING / GETTING DATA FROM TABLE -->
select * from users;
select name, email from users;
select * from users where age > 27;

<!-- UPDATING DATA INSIDE TABLE -->
update users 
set email = 'sharadindu@gmail.com' 
where id = 1;

<!-- DELETING DATA FROM TABLE -->
delete from users 
where id = 3;

```
