---
title: 'PostgreSQL-Setup'
date: 2019-06-02
permalink: /posts/2019/PostgreSQL-setup/
tags:
  - PostgreSQL
  - SQL
  - Database
  - Setup
---


# About PostgreSQL

In the world of SQL or RDBMS based databases, PostgreSQL offers great services which can be used by an individual user to large scale enterprises. Similar to most of the SQL based databases, setting it up is fairly simple, and it provides users a great experience and flexibility to meet your goals.<br>

To understand the PostgreSQL and how it suffice your use case, setting it up is an essential step. This post demonstrates how to install PostgreSQL on an Ubuntu 16.04 machine along with basic database administration with a running use case(small app).<br>

## Step 1 - Install PostgreSQL

The most recommended method is to install it via the `apt` packing manager.

``` Ruby
user@foo:~$ sudo apt update
user@foo:~$ sudo apt install postgresql postgresql-contrib

```

After the above installation, automatically a user and a database named as **postgres** have been added to the machine and PostgreSQL service, it is an administration account. Now, you can use this administration user account to access the PostgreSQL related functions and roles. [Roles](http://www.postgresqltutorial.com/postgresql-roles/){:target="_blank"} are nothing but the different types of functions you can perform in the PostgreSQL database.

There are a few ways to use **postgres** account to access PostgreSQL shell.

## Step 2 - Enter the PostgreSQL shell

To switch over to the **postgres** account run the following command:

``` Ruby
user@foo:~$ sudo -i -u postgres
postgres@foo:~$
```
Now you have successfully entered in the **postgres** account, to access the PostgreSQL process shell run the following command:

``` Ruby
postgres@foo:~$ psql
postgres=#

```
### Or you can directly enter in the **postgres** psql shell by:

``` Ruby
user@foo:~$ sudo -i -u postgres psql
postgres=#

```
Now you are free to interact with the database management services.

Exit out of the PostgreSQL shell by:

``` Ruby
postgres=# \q
user@foo:~$

```


## Step 3 - Creating a role

In PostgreSQL, a role/user is required so that it can interact with the PostgreSQL database service via as 3rd party standalone apps, PHP web application, Python scripts, etc.

A very simple way of creating a user is from **postgres** account:

``` Ruby
postgres@foo:~$ createuser -P -s -e demopy
Enter password for new role: 
Enter it again: 
SELECT pg_catalog.set_config('search_path', '', false)
CREATE ROLE demopy PASSWORD 'md516a97ee203992bfc3ab84a77b340de86' SUPERUSER CREATEDB CREATEROLE INHERIT LOGIN;

```

The above script has automatically made the role/user you created with superuser privileges. Select a password and remember, and it will be feed to your application that interacts with the PostgreSQL database on your behalf.

## Step 4 - Creating a Database

Now, very quickly, you can create a database to play around with an application. From your **postgres** account type the following command:

``` Ruby
postgres@foo:~$ createdb demopy

```

## Step 5 - Accessing the database

Access of the newly created PostgreSQL database **demopy** can be done in two ways:

1. Creating a unix user with the same name as role and database(i.e. demopy) so that through terminal prompt you can access the PostgreSQL services the same way user **postgres** does.

``` Ruby
user@foo:~$ sudo adduser demopy

```

Note: the password of the unix user can be different of the password of the role, as during the access of the database through a 3rd party app or plugin the role password will be used not the unix user local account password.

Now to access the database using the following command:

``` Ruby
user@foo:~$ sudo -i -u demopy
demopy@foo:~$ psql
demopy=#

```
`pydemo=#` is the shell through which the database named demopy can be accessed.

2. Any database can be accessed via the default user **postgres** account, without the need of making a separate unix user local account:

Once you enter the PostgreSQL using the **postgres** account, by default it selects the *postgres* database:

``` Ruby
postgres@foo:~$ psql
postgres=#

```

You can switch to any database present inside the PostgreSQL service using the command <br> `\c <name_of_the_database>`
 
``` Ruby
postgres=# \c demopy
You are now connected to database "demopy" as user "postgres".
demopy=#

```

Database admins mostly advise step 1.

## Step 6 - Create and Deleting Tables

In the database, Tables are of a defined structure according to which the data is stored. After selecting a database to work on creating a table:

``` Ruby
demopy=# CREATE TABLE test (
            id_number varchar(50) PRIMARY KEY, 
            name varchar(100) NOT NULL, 
            city varchar(50)
    );


```


After this fill database entries for demonstration purpose
``` Ruby

demopy=# INSERT INTO test (id_number, name, city) VALUES ('1', 'abc', 'JFK');
demopy=# INSERT INTO test (name, id_number) VALUES ('xyz', '2');


```

Run a query against the database to check if the data exists inside the database.

``` Ruby

demopy=# SELECT * FROM test;

 id_number | name | city 
-----------+------+------
 1         | abc  | JFK
 2         | xyz  | 
(2 rows)

```

You can perform many queries/operations over the database, more queries can be found [here](https://www.tutorialspoint.com/postgresql/postgresql_update_query.htm){:target="_blank"}

## Running an Application

We can query the database via 3rd party applications, any web plugin or script, etc. In this example, a simple python script will be used to query the database.

``` Python
#!/usr/bin/python

import pg

conn = pg.DB(host="localhost", user="demopy", passwd="PASSWORD", dbname="demopy")

result = conn.query("SELECT * FROM test")

print result.getresult()

conn.close()


```

Output:
`[('1', 'abc', 'JFK'), ('2', 'xyz', None)]`