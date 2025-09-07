## Database queries

```
select datname from pg_database;
create database database_name;
drop database database_name;
```

## Table queries

```
create table users
(id uuid primary key default uuid_generate_v4(),
name varchar(100) not null,
city varchar(100) not null);

insert into users (name, city)
values
('Shyam Kumar', 'Kolaghat'),
('Ram Chandra', 'Rampur');

select * from users;
select id,name from users;

update orders
set quantity = 4
where customer_name  = 'Sharadindu Das';

delete from orders
where name = 'Vikram Gupta';

```
