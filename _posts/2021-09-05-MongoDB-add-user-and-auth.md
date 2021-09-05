---
title: 'MongoDB-add-user-and-auth'
date: 2021-09-05
permalink: /posts/2021/MongoDB-add-user-and-auth/
tags:
  - MongoDB
  - NoSQL
  - Database
  - Setup
  - auth
  - Ubuntu
---


# About MongoDB

MongoDB is a persistent data storage solution where users/applications store data. It falls under NoSQL category i.e. instead of traditional table format used by SQL databases it follows JSON notation to store data. It provides more felxibility than SQL based databases.
So be it user data, images, binaries, one can store almost anything is MongoDB.<br>

Mostly MongoDB is installed on the local system in the form of binaries. There are various sources via which users can install MongoDB on their machines. For Ubuntu [follow the guide](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/).

Databases in general should be accessed using credentials and not the open access that everyone who knows your IP and port number can get access. Best practise is to add a user and start MongoDB with authentication mode on.

# How to add users in local MongoDB installation

This tutorial is a quick guide to add a user so that the MongoDB can be accessed using credentials. 

``` Ruby
# first go inside mongodb
$ mongo

# create a user and password along with a role, e.g. username as "superuser" and password as "password"
# However it is adviced to not only use a stronger password but a complex username as well.
$ db.createUser( { user: "superuser", pwd: "password", roles: ["readWriteAnyDatabase" ] } )

```

Upon successful exectuion of above commands, now makes changes in the MongoDB config files to let only authenticated users use MongoDB. Usually, the config file is present in a standard location in Ubuntu(linux based machines) i.e. 

`/etc/mongodb.conf`

Open this file in editor and find the tag with the name `auth` and set it to `true`:

```Ruby
$ vim /etc/mongodb.conf

```

It should look like the following: 
```Text
  # Turn on/off security.  Off is currently the default
  auth = true
```

Now, restart the MongoDB instance:

```Ruby
$ systemctl restart mongodb.service

```

Also please check if the restart has been successful:

```Ruby
$ systemctl status mongodb.service

```
If it shows `Active: active (running)` in the output then proceed to the final step.

# Authenticate using the credentials:

Now use the following command from the terminal to make sure that the credentials are working:

```Ruby
$ mongo --port 27017 --host 127.0.0.1 -u "superuser" -p "password" --authenticationDatabase "admin"

```

If everything goes perfect then following will be displayed:
```Text
MongoDB shell version v3.6.8
connecting to: mongodb://127.0.0.1:27017/
Implicit session: session { "id" : UUID("e949c438-d914-4067-8762-a28b3bc88d3d") }
MongoDB server version: 3.6.8

```


happy hacking! 